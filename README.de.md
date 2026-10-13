🇬🇧 [English](README.md) | 🇩🇪 Deutsch

# Home Assistant Blueprints

Eine Sammlung meiner Blueprints für Home Assistant. Mit dem Import-Button eines Blueprints fügst du ihn direkt deiner eigenen Home-Assistant-Instanz hinzu.

---

## Aufenthaltsdauer in einer Zone aufsummieren

Zählt, wie lange eine Person insgesamt in einer Zone verbringt (z. B. Fitnessstudio, Sportverein, Büro), und summiert die Minuten in einem Zahlen-Helfer auf.

[![Blueprint in Home Assistant importieren](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2FEdgarM73%2Fha-blueprints%2Fblob%2Fmain%2Fzonen_aufenthaltsdauer.yaml)

### So funktioniert es

- **Beim Betreten der Zone** wird die aktuelle Uhrzeit in einem Datum/Zeit-Helfer gespeichert. Weil sie in einem Helfer liegt, schadet ein Neustart von Home Assistant während des Besuchs nicht.
- **Beim Verlassen der Zone** wird die Aufenthaltsdauer berechnet und auf die Gesamtsumme addiert.
- **Plausibilitätsprüfung:** Gezählt werden nur Aufenthalte zwischen einer Mindest- und einer Höchstdauer (Standard 1 bis 360 Minuten). So fallen GPS-Ausreißer wie kurzes Vorbeifahren und verpasste Betreten-Ereignisse heraus.

### Voraussetzungen

Lege vorher unter *Einstellungen → Geräte & Dienste → Helfer* diese zwei Helfer an:

| Helfer | Einstellungen | Zweck |
| --- | --- | --- |
| Datum und/oder Uhrzeit | Modus „Datum und Uhrzeit“ | Speichert den Zeitpunkt des Betretens |
| Zahl | Min 0, Max z. B. 1000000, Schrittweite 1, Einheit `min`, Anzeige „Eingabefeld“ | Speichert die Gesamtminuten |

Außerdem brauchst du eine [Person](https://www.home-assistant.io/integrations/person/) mit Standortverfolgung (z. B. über die Companion-App) und eine [Zone](https://www.home-assistant.io/integrations/zone/) für den Ort, den du erfassen möchtest.

### Optional: Gesamtzeit in Stunden

Lege einen Template-Sensor-Helfer an (*Helfer → Helfer erstellen → Template → Template-Sensor*) mit dieser Zustandsvorlage und der Einheit `h`:

```jinja
{{ (states('input_number.DEIN_HELFER') | float(0) / 60) | round(1) }}
```

---

## Lizenz

[MIT](LICENSE) © 2026 Edgar Miller. Du darfst die Blueprints nutzen, verändern und weitergeben, solange der Copyright-Vermerk erhalten bleibt.
