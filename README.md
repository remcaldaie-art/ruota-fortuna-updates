# Aggiornamenti Ruota della Fortuna

Repository pubblico per gli aggiornamenti dell'app **Ruota della Fortuna**:

- telefono: `it.remcaldaie.ruota`
- Fire TV: `it.remcaldaie.ruota.tv`

L'app, all'apertura (se c'è internet) e quando si tocca **Controlla aggiornamenti**, legge questo file:

`https://raw.githubusercontent.com/remcaldaie-art/ruota-fortuna-updates/main/version.json`

Se `versionCode` è più alto di quello installato, compare la scritta **Aggiornamento disponibile 1.x – Installa**. L'app scarica l'APK giusto (telefono o Fire TV), controlla lo SHA-256 e apre l'installatore di Android. Senza internet non mostra nulla.

## Contenuto di version.json

```json
{
  "versionCode": 6,
  "versionName": "1.5",
  "notes": "Breve descrizione della versione",
  "telefono": {
    "apkUrl": "https://github.com/remcaldaie-art/ruota-fortuna-updates/releases/download/1.5/RuotaDellaFortuna-telefono.apk",
    "sha256": "…"
  },
  "firetv": {
    "apkUrl": "https://github.com/remcaldaie-art/ruota-fortuna-updates/releases/download/1.5/RuotaDellaFortuna-FireTV.apk",
    "sha256": "…"
  }
}
```

## Come pubblicare una nuova versione

Vedi [HOWTO-PUBLISH.md](HOWTO-PUBLISH.md), oppure dallo spazio di lavoro eseguire `/workspace/ruota/pubblica_aggiornamento.sh` dopo aver costruito gli APK firmati.

Repo: `remcaldaie-art/ruota-fortuna-updates` (pubblico, gratuito). Qui ci sono solo il manifest e le Release con gli APK: niente codice sorgente, niente keystore, niente password.
