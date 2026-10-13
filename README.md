🇬🇧 English | 🇩🇪 [Deutsch](README.de.md)

# Home Assistant Blueprints

A collection of my Home Assistant blueprints. Click the import button of a blueprint to add it to your own Home Assistant instance.

---

## Zone Duration Tracker

Tracks the total time a person spends in a zone (e.g. gym, sports club, office) and adds up the minutes in a number helper.

[![Import blueprint into Home Assistant](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2FEdgarM73%2Fha-blueprints%2Fblob%2Fmain%2Fzone_duration_tracker.yaml)

### How it works

- **On entering the zone**, the current time is stored in a date/time helper. Because it is stored in a helper, a Home Assistant restart during the visit does no harm.
- **On leaving the zone**, the duration of the stay is calculated and added to the total.
- **Plausibility check:** only stays between a minimum and a maximum duration are counted (default 1 to 360 minutes). This filters out GPS glitches, such as briefly driving past, and missed enter events.

### Requirements

Create these two helpers first under *Settings → Devices & services → Helpers*:

| Helper | Settings | Purpose |
| --- | --- | --- |
| Date and/or time | Mode "Date and time" | Stores the time of entering |
| Number | Min 0, max e.g. 1000000, step 1, unit `min`, display mode "Input field" | Stores the total minutes |

You also need a [person](https://www.home-assistant.io/integrations/person/) with location tracking (e.g. the Companion app) and a [zone](https://www.home-assistant.io/integrations/zone/) for the place you want to track.

### Optional: total in hours

Create a template sensor helper (*Helpers → Create helper → Template → Template sensor*) with this state template and unit `h`:

```jinja
{{ (states('input_number.YOUR_HELPER') | float(0) / 60) | round(1) }}
```

---

## License

[MIT](LICENSE) © 2026 Edgar Miller. You may use, modify and share the blueprints, as long as the copyright notice is kept.
