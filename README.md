# Student Schedule Card

[![](https://img.shields.io/badge/Home%20Assistant-Custom%20Card-blue.svg?style=flat-square)](https://www.home-assistant.io/lovelace/)

A flexible and fully UI-configurable student schedule card for [Home Assistant](https://www.home-assistant.io/) Lovelace UI.

Supports subject management, color coding, room display, current time highlighting, responsive layout, and more.

![Preview 1](https://github.com/DomCim/student-schedule-card/blob/main/images/columnWidth1.png)
![Preview 2](https://github.com/DomCim/student-schedule-card/blob/main/images/ColumnWidth2.png)

---

## ✨ Features

- 📅 Custom days, times, breaks & layout
- 🎨 Color-coded subjects (incl. "free" slots)
- 🧑 Displays avatar & name from `person` entity
- 🏫 Optional room display per subject
- 📱 Responsive layout with shortened labels
- ⏰ Highlights current day and lesson
- 🔧 Full visual configuration (no YAML required)
- 🛠️ Still editable in YAML if preferred

---

## 🔥 Also available inside Hearth

If you use [Hearth](https://github.com/DomCim/Homeassistant-hearth), the same timetable is now one
of its cards (`custom:hearth-timetable-card`), configured in the integration instead of in the card:

- **Lesson times** are entered once for the whole household, one `HH:MM-HH:MM` per line.
- **Breaks are not configured at all** — every gap of five minutes or more between two periods is
  drawn as one.
- **A week is one field per weekday**, one lesson per line: `Kunst | 1.OG 5` for a room, `-` for a
  free period, `6. Sport` for a day that starts late.
- **Subject colours come from the subject names**, so the same subject is the same colour on every
  child's card. The colour picker is only there to correct them.
- **Days, names and avatars come from the family members** already configured in Hearth, so the
  card itself usually needs no options at all.

This card stays as it is: it is standalone, needs no integration, and remains the right choice if
you do not run Hearth. Migrating is mostly mechanical — `times:` becomes the lesson-times field,
and each day of `subjects:` becomes that weekday's field.

---
## 📦 HACS Installation

This card is available as a **custom repository** in [HACS](https://hacs.xyz):

1. In HACS, go to **Frontend > ⋮ > Custom repositories**
2. Add the repository URL:  `https://github.com/DomCim/student-schedule-card/`
3. Set category to **Lovelace**
4. Install `student-schedule-card`
5. Add the resource automatically or manually (see below)

## 🚀 Installation

### Manual Installation

1. Download the latest `student-schedule-card.js` file.
2. Place it into your `config/www/` directory.
3. Add the resource to your Lovelace config:

```yaml
resources:
  - url: /local/student-schedule-card.js?v=1.0.0
    type: module
```

4. Restart Home Assistant or reload Lovelace resources.

---

## 🧪 Example Configuration

```yaml
type: custom:student-schedule-card
name: Jan
description: Week A
person_entity: person.jan
default_placeholder: "--"
show_breaks: true
break_label: Break
show_rooms: true
shorten_room_names: true
show_highlight: true
days:
  - Monday
  - Tuesday
  - Wednesday
  - Thursday
  - Friday
  - Saturday
  - Sunday
times:
  - 8:00 - 8:45
  - 8:45 - 9:30
  - 9:50 - 10:35
  - 10:35 - 11:20
  - 11:30 - 12:15
  - 12:15 - 13:00
  - 13:15 - 14:00
  - 16:30 - 17:30
  - 17:30 - 18:30
breaks:
  - 9:30 - 9:50
  - 11:20 - 11:30
  - 13:00 - 13:15
colors:
  Deutsch: "#4caf50"
  Mathe: "#b13e3e"
  Kunst: "#961599"
  HSU: "#2774b0"
  Religion: "#330505"
  Musik: "#009688"
  Englisch: "#bd42a2"
  WG: "#ffc107"
  Chor: "#476d80"
  Sport: "#ff9800"
  Handball: "#888888"
  Fußball: "#999999"
  FREE: "#ae4242"
subjects:
  "1":
    - subject: Deutsch
    - subject: Mathe
    - subject: Kunst
      free: false
      room: 1.OG 5
    - subject: HSU
    - subject: Deutsch
    - subject: HSU
      free: true
    - free: true
    - free: true
    - free: true
  "2":
    - subject: Deutsch
    - subject: Religion
    - subject: WG
    - subject: WG
    - free: true
    - subject: Chor
    - subject: Handball
    - free: true
    - free: true
```

---

## ⚙️ Options

### General

| Name                  | Type     | Default | Description                                                  |
|-----------------------|----------|---------|--------------------------------------------------------------|
| `type`                | string   | —       | Required. Must be `custom:student-schedule-card`             |
| `name`                | string   | —       | Card title (if no `person_entity` is set)                    |
| `description`         | string   | —       | Subtitle below the name/avatar                               |
| `icon`                | string   | —       | Icon to show if no `person_entity` is used                   |
| `person_entity`       | string   | —       | A person entity (e.g. `person.jan`)                          |
| `default_placeholder` | string   | `--`    | Placeholder text for empty subjects                          |

### Layout

| Name                  | Type    | Default | Description                                                  |
|-----------------------|---------|---------|--------------------------------------------------------------|
| `show_breaks`         | bool    | true    | Show break rows                                              |
| `break_label`         | string  | "Pause" | Label for breaks                                             |
| `show_rooms`          | bool    | true    | Show room info below subject name                            |
| `shorten_room_names`  | bool    | true    | Shorten room names if layout is narrow                       |
| `show_highlight`      | bool    | true    | Highlight current day and ongoing lesson                     |

### Data

| Name       | Type     | Description                                                  |
|------------|----------|--------------------------------------------------------------|
| `days`     | string[] | List of day labels                                           |
| `times`    | string[] | Time slot definitions (format: `HH:mm - HH:mm`)             |
| `breaks`   | string[] | Optional break time slots                                   |
| `colors`   | object   | Map subject → hex color                                      |
| `subjects` | object   | Map of day (1–7) → array of subject objects or strings       |

---

## 🐞 Troubleshooting

If the card doesn't show up:

- Check Dev Tools → Console for errors
- Clear your browser cache
- Confirm that the `type` is set correctly
- Make sure the resource path and version match

```yaml
type: custom:student-schedule-card
```
## 🐞 Bug Reports & Feature Requests

Please open an issue here:
👉 https://github.com/DomCim/student-schedule-card/issues

---

## 📄 License

MIT © 2025

---

_Developed with ❤️ for Home Assistant_
