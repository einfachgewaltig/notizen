cd /usr/local/www/apache24/noexec/cloud.raphael-christopher.de

sudo -u web php occ maintenance:mode --off

---

---

---

sudo -u #1001 ./occ usage-report:

## Datenansicht aktualisieren im Web

sudo -u web php /usr/local/www/apache24/noexec/cloud.raphael-christopher.de/console.php files:scan --all

## Update

sudo -u web php updater.phar