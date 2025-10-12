# PoGoSDex – Contribution Guide

This repository hosts the public-facing catalogue for PoGoSDex.  
The sections below explain how to extend the catalogue with new devices and how to localise the UI.

---

## Adding devices

Device records are stored in [`data/devices.json`](data/devices.json). To create or update entries you can use the JSON file directly or our Builder on the Website.

### 1. Collect required fields

Each device object must contain:

| Field        | Type     | Description                                                           |
| ------------ | -------- | --------------------------------------------------------------------- |
| `id`         | string   | Unique identifier (e.g. `pixel-8-pro`). Prefer lower-case kebab case. |
| `brand`      | string   | Manufacturer name (e.g. `Google`).                                    |
| `model`      | string   | Marketing model (e.g. `Pixel 8 Pro`).                                 |
| `os`         | string   | Operating system / version (e.g. `Android 14`).                       |
| `type`       | string   | Device category (phone, tablet, etc.).                                |
| `compatible` | boolean  | `true` if PoGo works out of the box, otherwise `false`.               |
| `notes`      | string[] | Optional bullet notes; omit or use an empty array if not needed.      |
| `rootLinks`  | string[] | Optional URLs for rooting/custom guides.                              |

### 2. Add or edit entries

**Editing the JSON file manually**

1. Open [`data/devices.json`](data/devices.json).
2. Insert a new object following the schema above. Example:

   ```jsonc
   {
     "id": "pixel-8-pro",
     "brand": "Google",
     "model": "Pixel 8 Pro",
     "os": "Android 14",
     "type": "phone",
     "compatible": true,
     "notes": [
       "Excellent AR performance",
       "Battery lasts 2+ hours with AR scanning"
     ],
     "rootLinks": ["https://example.com/root-guide"]
   }
   ```

3. Ensure the JSON stays valid (no trailing commas, unique `id` values).
4. Commit the change along with any translation updates (see below).

---

## Adding or updating translations

Language resources live in [`lang/*.json`](lang/en.json).

### 1. Update existing languages

When adding device-specific labels or UI strings:

1. Choose a reference file, usually [`lang/en.json`](lang/en.json).
2. Add the new key/value pair.
3. Mirror the key across all other language files (`de.json`, `es.json`, …).  
   If a translation is pending, duplicate the English text and append `TODO`.

### 2. Add a new language

1. Copy [`lang/en.json`](lang/en.json) to `lang/<code>.json` (ISO 639-1 code preferred).
2. Translate every value.
3. Register the new language code in the language selector (`LANG_OPTIONS`) inside [`public/main.js`](public/main.js).

---

## Validation checklist

- `npm test` (or equivalent) passes.
- JSON files remain valid (`npm run lint:json` if available).
- All language files include the new keys.
- Committed changes include updated documentation if behaviour changed.

Thank you for helping expand PoGoSDex!
