# Come pubblicare una nuova versione della Ruota della Fortuna

Passi da ripetere per ogni aggiornamento. Tutto è gratuito (repository pubblico e Release su GitHub, senza carta).

L'app controlla questo indirizzo:

`https://raw.githubusercontent.com/remcaldaie-art/ruota-fortuna-updates/main/version.json`

Se `versionCode` è più alto di quello installato, l'utente può scaricare e installare l'APK (telefono o Fire TV).

Il modo più semplice, dopo aver costruito e firmato gli APK con `ruota.keystore` (la stessa firma di sempre):

```bash
# Gli APK devono chiamarsi così, in /workspace/ruota:
#   RuotaDellaFortuna-telefono.apk
#   RuotaDellaFortuna-FireTV.apk
/workspace/ruota/pubblica_aggiornamento.sh "Breve descrizione della versione"
```

Lo script aggiorna `version.json`, lo carica sul ramo `main` e crea la Release con entrambi gli APK e il manifest.

## Passi manuali (se serve)

### 1. Costruire gli APK

- Alzare `versionCode` e `versionName` (es. 7 / 1.6) in `android/app/build.gradle`.
- Firmare con `ruota.keystore` (la stessa di sempre; una firma diversa non si installa sopra).
- File di uscita: `/workspace/ruota/RuotaDellaFortuna-telefono.apk` e `/workspace/ruota/RuotaDellaFortuna-FireTV.apk`.

### 2. Aggiornare version.json

Nel file `version.json` del ramo `main`, con gli SHA-256 dei due APK e gli URL della Release (tag uguale a `versionName`).

### 3. Caricare version.json sul ramo main e creare la Release

```bash
gh release create 1.6 \
  /workspace/ruota/RuotaDellaFortuna-telefono.apk \
  /workspace/ruota/RuotaDellaFortuna-FireTV.apk \
  version.json \
  --repo remcaldaie-art/ruota-fortuna-updates \
  --title "1.6" \
  --notes "Breve descrizione della versione"
```

### 4. Verificare

```bash
curl -fsSL https://raw.githubusercontent.com/remcaldaie-art/ruota-fortuna-updates/main/version.json
```

Controllare che `versionCode` sia quello nuovo e che gli SHA-256 coincidano con gli APK firmati.

## Note

- Non mettere gli APK nel repository git: vanno solo come allegati della Release.
- Non usare funzioni a pagamento di GitHub.
- Non caricare il keystore, le password o il codice sorgente in questo repository.
- Le carte aggiunte sul telefono restano dopo l'aggiornamento.
