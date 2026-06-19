# Hverdagsmagi ✨

A Progressive Web App for everyday household logistics — shared between two people with real-time sync.

## Features

- **Hjem** — daily overview: today's dinner, latest messages, shopping list status
- **Middagsplan** — weekly dinner planner with a meal library; drag meals onto days, then pick ingredients to add to the shopping list
- **Beskjeder** — shared message board, send as yourself or your partner, delete when done
- **Handleliste** — shared shopping list with categories, qty support, drag-and-drop to re-categorize, quick-picks, and long-press to edit

### Shopping list details
- Items grouped by category (Frukt & grønt, Meieri, Kjøtt & fisk, Brød & bakst, Tørrvarer, Frysevarer, Drikke, Annet)
- Adding a duplicate item increments the quantity instead of creating a new entry
- Drag the `⠿` handle to move an item to a different category (also updates the quick-pick if one exists)
- Long-press an item to edit quantity and category
- Quick-picks sorted by frequency; hidden when already in active list; hold to edit qty or delete

### Meal planner details
- Meal library with name and ingredients (each ingredient has a category)
- Drag a meal onto a weekday → confirms the dinner and shows a modal to select which ingredients to add to the shopping cart
- Long-press a meal chip to edit or delete

## Tech stack

- Vanilla HTML/CSS/JS — no build step
- [Firebase Firestore](https://firebase.google.com/docs/firestore) for real-time sync across devices
- Service worker for PWA shell caching

## Project structure

```
Hjemmet/
├── index.html      # Entire app
├── manifest.json   # PWA manifest
├── sw.js           # Service worker
└── README.md
```

## Firebase setup

1. Create a Firebase project at [console.firebase.google.com](https://console.firebase.google.com)
2. Create a Firestore database (Native mode, `europe-west1`)
3. Copy your config into `index.html` under `FIREBASE_CONFIG`
4. Set Firestore rules to allow read/write

## Firestore collections

| Collection   | Description                                                        |
|--------------|--------------------------------------------------------------------|
| `dinners`    | Keyed by date (`YYYY-MM-DD`), fields: `meal`, `mealId`            |
| `meals`      | `name`, `ingredients[]` (`{name, category}`), `count`, `added`    |
| `messages`   | `text`, `author`, `timestamp`                                      |
| `shopping`   | `text`, `qty`, `category`, `done`, `timestamp`                     |
| `quickpicks` | `text`, `category`, `count`, `lastAdded`                           |

## Deployment

Static HTML — deploy to GitHub Pages, Netlify, Vercel, or any web server.
