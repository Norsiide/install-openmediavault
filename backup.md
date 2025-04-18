<p align="center"><img src="https://wiki.debian.org/FrontPage?action=AttachFile&do=get&target=11-bullseye-wiki-banner-04.png" width="400" alt="norsiide"></p>

**script de sauvegarde quotidien avec `rsync`** qui crée une copie incrémentielle chaque jour, tout en supprimant les anciens backups pour éviter de saturer ton espace disque.

---

### 🎯 Objectif du script

- Sauvegarde incrémentielle avec `rsync` chaque jour
- Conserve uniquement les **X derniers backups** (suppression des anciens)
- Crée un dossier de **backup avec la date** (ex: `backup-2025-04-18`)
- Supprime les **anciens backups** en fonction du nombre de jours conservés

---

### 🧠 Script `rsync` quotidien avec suppression des anciens backups

```bash
#!/bin/bash

# === CONFIG ===
SRC="/chemin/vers/source/"          # Répertoire source à sauvegarder
DEST="/chemin/vers/backup/"         # Répertoire où stocker les backups
RETENTION_DAYS=7                    # Nombre de jours de backups à conserver
LOG="/var/log/rsync_backup.log"     # Fichier log
DATE=$(date "+%Y-%m-%d")            # Date du jour pour le backup

# === NOM DU BACKUP ===
BACKUP_DIR="$DEST/backup-$DATE"     # Dossier pour la sauvegarde du jour

# === CRÉER LE BACKUP ===
echo "[$DATE] Démarrage de la sauvegarde rsync" >> "$LOG"
mkdir -p "$BACKUP_DIR"

rsync -avh --delete --progress "$SRC" "$BACKUP_DIR" >> "$LOG" 2>&1

echo "[$DATE] Sauvegarde terminée dans $BACKUP_DIR" >> "$LOG"

# === SUPPRESSION DES BACKUPS ANCIENS ===
echo "[$DATE] Suppression des backups plus anciens que $RETENTION_DAYS jours" >> "$LOG"

# On supprime les sauvegardes de plus de $RETENTION_DAYS jours
find "$DEST" -maxdepth 1 -type d -name "backup-*" -mtime +$RETENTION_DAYS -exec rm -rf {} \;

echo "[$DATE] Anciennes sauvegardes supprimées." >> "$LOG"

```

---

### 🧾 Explication des options :

- **Création de la sauvegarde :**
  - `rsync -avh --delete --progress` : Sauvegarde incrémentielle avec suppression des fichiers supprimés à la source.
  - Chaque backup est stocké dans un dossier portant la date du jour (`backup-YYYY-MM-DD`).
  
- **Suppression des anciens backups :**
  - `find "$DEST" -maxdepth 1 -type d -name "backup-*" -mtime +$RETENTION_DAYS -exec rm -rf {} \;`
    - Cela recherche tous les dossiers de type `backup-*` dans le dossier de destination.
    - Puis supprime ceux qui ont plus de `X` jours (définis par `RETENTION_DAYS`).

- **Journalisation :**
  - Le script consigne chaque étape dans un fichier `rsync_backup.log`.

---

### ⏲️ Pour automatiser : Cron

Tu peux exécuter ce script automatiquement tous les jours en utilisant `cron`.

1. Ouvre la crontab :

```bash
crontab -e
```

2. Ajoute cette ligne pour exécuter le script tous les jours à 3h du matin :

```bash
0 3 * * * /chemin/vers/script/rsync_backup.sh
```

3. Assure-toi que ton script est exécutable :

```bash
chmod +x /chemin/vers/script/rsync_backup.sh
```

---

### 📆 Exemple de structure de répertoires après 7 jours :

```
/chemin/vers/backup/
    backup-2025-04-18/
    backup-2025-04-19/
    backup-2025-04-20/
    ...
    backup-2025-04-24/
```

Chaque jour, un nouveau dossier `backup-YYYY-MM-DD` est créé, et les anciens dossiers sont supprimés après `RETENTION_DAYS` jours.

---