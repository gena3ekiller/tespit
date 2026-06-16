# Tespit – App Store Connect / Datenschutz-Check nach Codeprüfung

Stand: 16. Juni 2026  
Kontakt: Esat Arslan <e.arslan2025@gmail.com>

## 1. Geprüfte technische Punkte aus dem Projekt

Gefunden:
- iOS-App: `ch.esat.tespit`, iOS 17.0
- App-Kategorie im Projekt: Navigation
- Berechtigungen: Standort „Beim Verwenden“, Bluetooth, Bluetooth-Central-Background-Mode, Live Activities
- Lokale Speicherung: UserDefaults für App-Einstellungen, Fahrzeug-VIN, Fahrzeugname, Kopplungsstatus, Promo-Freischaltung
- Sichere lokale Speicherung: iOS-Keychain für privaten Fahrzeugschlüssel
- Apple-Dienste: StoreKit, MapKit/MKDirections, iTunes Search für Coverbilder, Apple-Diagnosen nur falls vom Nutzer freigegeben
- Optional vorbereitet: Google Maps SDK/API-Key, aktuell ohne API-Key
- Kein eigenes Backend gefunden
- Kein Firebase gefunden
- Kein Werbe-SDK gefunden
- Kein AppTrackingTransparency/AdSupport gefunden
- Kein eigenes Analytics-Backend gefunden
- Kein CloudKit gefunden

## 2. Datenschutz-URLs für App Store Connect

### Deutsch
Support:
https://esat-o-arslan.github.io/tespit/de/support.html

Datenschutz:
https://esat-o-arslan.github.io/tespit/de/privacy.html

### English
Support:
https://esat-o-arslan.github.io/tespit/en/support.html

Privacy Policy:
https://esat-o-arslan.github.io/tespit/en/privacy.html

### Türkçe
Destek:
https://esat-o-arslan.github.io/tespit/tr/support.html

Gizlilik Politikası:
https://esat-o-arslan.github.io/tespit/tr/privacy.html

## 3. Wichtiger Zusatz für App Store Connect – Datenerfassung

Nach Codeprüfung würde ich es so formulieren:

Tracking:
Nein

Datenverkauf:
Nein

Werbung:
Nein

Eigenes Entwickler-Backend:
Nein

Ich als Entwickler sehe keine Rohdaten aus der App. Ich sehe keine Fahrzeugdaten, keine VIN, keine Standortdaten, keine privaten Fahrzeugschlüssel und keine lokalen App-Einstellungen. Diese Daten bleiben lokal auf dem iPhone oder werden, soweit erforderlich, über Apple-Dienste verarbeitet.

Über Apple können verarbeitet werden:
- In-App-Käufe und Abos über StoreKit
- Karten, Standort- und Routenfunktionen über MapKit/MKDirections
- Medien-Cover-Suche über iTunes Search
- Crash-/Diagnosedaten nur, wenn Nutzer das Teilen mit Entwicklern erlaubt haben
- Zusammengefasste App-Store-Connect-Auswertungen wie Downloads, Verkäufe und Umsätze

## 4. App Store Connect Datenschutz-Fragen – empfohlene Richtung

Wichtig: Apple unterscheidet zwischen „lokal verarbeitet“ und „gesammelt“. Daten, die nur auf dem Gerät verarbeitet und nicht an einen Server gesendet werden, müssen laut Apple grundsätzlich nicht als gesammelt angegeben werden. Trotzdem müssen Daten angegeben werden, wenn du oder Drittanbieter sie sammeln oder länger als für die Echtzeit-Anfrage nötig zugänglich machen.

Empfehlung:
- Tracking: Nein
- Standort: Nur angeben, wenn App Store Connect wegen MapKit/Routen/Google Maps danach fragt oder wenn du Daten selbst/über Drittanbieter sammelst. In deiner eigenen App kein eigenes Backend.
- Käufe: Apple/StoreKit verarbeitet Käufe. Du siehst nur App-Store-Connect-Auswertungen.
- Diagnose: Wenn Apple Crash-/Diagnosedaten bereitstellt und Nutzer zugestimmt haben.
- Supportdaten: Nur wenn Nutzer freiwillig per E-Mail Supportanfragen senden.

## 5. Wichtiger technischer Punkt: PrivacyInfo.xcprivacy

Im Projekt habe ich keine PrivacyInfo.xcprivacy gefunden. Da dein Code UserDefaults nutzt, solltest du eine Privacy Manifest Datei in das App-Target aufnehmen.

Ich habe dir eine Vorlage erstellt:
ios/PrivacyInfo.xcprivacy

Diese enthält:
- Tracking: false
- Tracking-Domains: leer
- Collected Data Types: leer
- Required Reason API: UserDefaults mit Reason CA92.1

## 6. README-Widerspruch

In deiner README steht noch:
„Werbung und Premiumkäufe sind nicht Bestandteil dieses privaten Projekts.“

Im Code sind aber StoreKit-Produkte enthalten:
- ch.esat.tespit.premium.monthly
- ch.esat.tespit.premium.quarterly
- ch.esat.tespit.premium.yearly
- ch.esat.tespit.premium.lifetime

Vor dem App-Store-Upload solltest du README oder App-Funktion angleichen.

## 7. Optionaler Google-Maps-Hinweis

Google Maps ist im Code nur optional vorbereitet. Aktuell ist der API-Key leer. Falls du Google Maps später wirklich aktivierst, musst du Datenschutz, Privacy Manifest/SDK-Angaben und App-Store-Connect-Datenerfassung erneut prüfen.


## 8. Ergänzung Apple und Tesla

Neu ergänzt:
- Apple kann als eigener Dienstanbieter Daten verarbeiten, z. B. Apple-ID, Käufe, Abos, App Store Connect, Diagnosen, Karten-/Routendienste und iTunes Search.
- Tesla kann als eigener Dienstanbieter Daten verarbeiten, z. B. Tesla-Konto, Tesla-App, Fahrzeugdaten, Diagnosedaten, Standort-/Routeninformationen, Software-/Servicedaten oder Fahrzeug-Systemdaten.
- Der Entwickler von Tespit sieht diese Daten nicht.
- Tespit hat dafür kein eigenes Backend, keine eigene Cloud-Datenbank und kein Dashboard, über das diese Daten eingesehen werden könnten.
