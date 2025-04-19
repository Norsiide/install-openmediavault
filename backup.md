<p align="center"><img src="https://wiki.debian.org/FrontPage?action=AttachFile&do=get&target=11-bullseye-wiki-banner-04.png" width="400" alt="norsiide"></p>

Parfait ! Voici le **script de sauvegarde complet**, 100% prêt à l’emploi :  
- 🔁 Sauvegarde multiple dossiers
- 📂 Exclut certains dossiers
- 🧹 Supprime les backups anciens
- 🧨 Envoie une **notification Discord**
  - ✅ Message vert si tout s’est bien passé
  - ❌ Message rouge avec `@here` et **logs d’erreur** en cas de souci

---

## 🖥️ Script complet `backup.sh`

```bash
#!/bin/bash

# === CONFIGURATION ===
SRC_DIRS=(
    "/home/user/Documents"
    "/etc"
    "/var/www"
)
DEST="/mnt/backup"
RETENTION_DAYS=7
LOG="/var/log/rsync_backup.log"
DATE=$(date "+%Y-%m-%d")
BACKUP_ROOT="$DEST/backup-$DATE"
START_TIME=$(date +%s)
ERROR_OCCURRED=0
ERROR_LOG=""

WEBHOOK_URL="https://discord.com/api/webhooks/TON_ID/TON_TOKEN"
HOSTNAME=$(hostname)

# === EXCLUSIONS ===
EXCLUDES=(
    "node_modules/"
    ".cache/"
    "Downloads/"
    "tmp/"
)
EXCLUDE_PARAMS=()
for excl in "${EXCLUDES[@]}"; do
    EXCLUDE_PARAMS+=(--exclude="$excl")
done

# === DÉBUT DU LOG ===
echo "[$DATE] ➤ Début des sauvegardes..." >> "$LOG"
mkdir -p "$BACKUP_ROOT"

# === SAUVEGARDE DE CHAQUE DOSSIER ===
for SRC in "${SRC_DIRS[@]}"; do
    BASENAME=$(basename "$SRC")
    DEST_DIR="$BACKUP_ROOT/$BASENAME"
    
    echo "[$DATE] ➤ Sauvegarde de $SRC..." >> "$LOG"
    mkdir -p "$DEST_DIR"
    
    RSYNC_OUTPUT=$(rsync -avh --info=progress2 --no-links --delete "${EXCLUDE_PARAMS[@]}" "$SRC/" "$DEST_DIR" 2>&1)
    RSYNC_EXIT_CODE=$?
    echo "$RSYNC_OUTPUT" | tee -a "$LOG"
    
    if [ $RSYNC_EXIT_CODE -ne 0 ]; then
        echo "[$DATE] ❌ Erreur lors de la sauvegarde de $SRC" >> "$LOG"
        ERROR_OCCURRED=1
        ERROR_LOG+="🗂️ $SRC :\n$(echo "$RSYNC_OUTPUT" | tail -n 10)\n\n"
    fi
done

# === SUPPRESSION DES BACKUPS ANCIENS ===
echo "[$DATE] ➤ Suppression des anciens backups (> $RETENTION_DAYS jours)" >> "$LOG"
find "$DEST" -maxdepth 1 -type d -name "backup-*" -mtime +$RETENTION_DAYS -exec rm -rf {} \;
echo "[$DATE] ➤ Nettoyage terminé." >> "$LOG"

# === CALCUL TEMPS ET TAILLE ===
END_TIME=$(date +%s)
DURATION=$((END_TIME - START_TIME))
DURATION_FORMATTED=$(printf '%02dh:%02dm:%02ds' $((DURATION/3600)) $((DURATION%3600/60)) $((DURATION%60)))
BACKUP_SIZE=$(du -sh "$BACKUP_ROOT" 2>/dev/null | cut -f1)

# === ENVOI DU MESSAGE DISCORD ===
if [ "$ERROR_OCCURRED" -eq 0 ]; then
  JSON=$(jq -n \
    --arg title "✅ Sauvegarde terminée" \
    --arg description "📦 Sauvegarde complétée sans erreur." \
    --arg machine "$HOSTNAME" \
    --arg date "$DATE" \
    --arg folder "$BACKUP_ROOT" \
    --arg size "$BACKUP_SIZE" \
    --arg duration "$DURATION_FORMATTED" \
    '{
      embeds: [{
        title: $title,
        description: $description,
        color: 65280,
        fields: [
          { name: "🖥️ Machine", value: $machine, inline: true },
          { name: "📅 Date", value: $date, inline: true },
          { name: "📁 Dossier", value: $folder, inline: false },
          { name: "💾 Taille", value: $size, inline: true },
          { name: "⏱️ Durée", value: $duration, inline: true }
        ],
        footer: { text: "Backup Automatique - rsync" },
        timestamp: now | todate
      }]
    }')
else
  JSON=$(jq -n \
    --arg title "❌ Erreur de sauvegarde" \
    --arg description "⚠️ Une ou plusieurs erreurs sont survenues lors du backup." \
    --arg machine "$HOSTNAME" \
    --arg date "$DATE" \
    --arg errors "$ERROR_LOG" \
    --arg mention "@here" \
    '{
      content: $mention,
      allowed_mentions: { parse: ["everyone"] },
      embeds: [{
        title: $title,
        description: $description,
        color: 16711680,
        fields: [
          { name: "🖥️ Machine", value: $machine, inline: true },
          { name: "📅 Date", value: $date, inline: true },
          { name: "🧨 Logs d\'erreur", value: ($errors | if . == "" then "Aucun détail." else . end), inline: false }
        ],
        footer: { text: "Backup Automatique - ERREUR" },
        timestamp: now | todate
      }]
    }')
fi

curl -H "Content-Type: application/json" \
     -X POST \
     -d "$JSON" \
     "$WEBHOOK_URL"
```

---

## 📌 Instructions :

1. **Remplace** :
   - `TON_ID` et `TON_TOKEN` dans `WEBHOOK_URL`
2. **Ajoute à la crontab** :
   ```bash
   crontab -e
   ```
   ```cron
   0 2 * * * /usr/local/bin/backup.sh >> /var/log/rsync_backup.log 2>&1
   ```

3. Donne les bons droits :
   ```bash
   chmod +x /usr/local/bin/backup.sh
   ```

---