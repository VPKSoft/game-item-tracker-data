# Game Item Tracker – Templates

Community item templates for [Game Item Tracker](https://github.com/VPKSoft/game-item-tracker).
A template (`*.gitemplate.json`) describes the items of a game: categories, items, images,
attributes, tags and counters.

## Using the templates

You don't need GitHub to use these templates. In the app, open **Library → Online templates…**,
pick a template and click **Install**. When a template here gets a newer version, the same list
shows **Update to vX**. Your saves then offer the upgrade.

The templates are also listed with download links at
<https://vpksoft.github.io/game-item-tracker-data/>. A downloaded file can be imported with
**Library → Import file…**.

## Repository layout

Templates are grouped by the first letter of the game's name, then by game:

```
A/ … Z/
P/
  Palia/
    palia-bugs.gitemplate.json
    palia-bundles.gitemplate.json
    palia-elderwoods-artifacts-bundle.gitemplate.json
    palia-fish.gitemplate.json
    palia-floors.gitemplate.json
    palia-food-recipe-items.gitemplate.json
    palia-food-recipes.gitemplate.json
    palia-guild-store-exclusives.gitemplate.json
    palia-maji-market.gitemplate.json
    palia-plushies.gitemplate.json
    palia-potato-pods.gitemplate.json
    palia-roofing.gitemplate.json
    palia-royal-highlands-artifacts-bundle.gitemplate.json
    palia-stickers.gitemplate.json
    palia-tints.gitemplate.json
    palia-wallpapers.gitemplate.json
    palia-zekis-prize-wheel.gitemplate.json
    palia-zekis-wondrous-machine.gitemplate.json
```

- The letter folder is the first letter of the game's name in upper case (`Palia` → `P/`).
  A name that starts with a digit goes under the first letter of the number written out in
  English (`7 Days to Die` → `S/`).
- The game folder uses the game's name exactly as it is written in the template's `game` field.
- Template file names are lower case with dashes: `<game>-<collection>.gitemplate.json`.

## Adding or updating a template

Before you export, fill in the template's *Source / attribution* field (**Details** tab) with where
the data came from. When you update an existing template, start from the online version (install it
from **Online templates…**), make your changes and raise its version on the **Details** tab, so that
existing saves can be upgraded.

### The easy way: submission form (no git needed)

1. Export the template in the app: **Library → Templates → Export**.
2. Open the [**Submit a template**](https://github.com/VPKSoft/game-item-tracker-data/issues/new?template=submit-template.yml)
   form (you need a free GitHub account), fill it in and attach the `.gitemplate.json` file.
3. A maintainer checks the template and adds it to the repository with a pull request. The issue is
   closed when the template is online.

### With a pull request

1. Fork the repository and create a branch, for example `template/palia-bugs`.
2. Export the template from the app (**Library → Templates → Export**) and put it in the right
   `<Letter>/<Game>/` folder.
3. When you update an existing template, raise its `version` (for example `1.0.0` → `1.1.0`) and keep
   its `templateId`, so existing saves can be upgraded to the new version.
4. Open a pull request and fill in the checklist.

Every template, submitted either way, is added by a pull request. A pull request is merged only when:

- the automatic check passes (see below): the template imports into the app without validation
  errors and is in the right folder,
- the template's `source` field (*Source / attribution* on the template's **Details** tab) names
  where the data came from, with a URL.

### Tags

Use `Name: value` for tags that name a property, with a capitalized name, a colon and one space,
for example `Location: Kilima Lake` or `Source: Fishing`. Plain tags without a name are fine too.

## How publishing works

The workflow in [`.github/workflows/publish.yml`](.github/workflows/publish.yml) runs on every pull
request and every push to `main`:

1. It checks every template with the app's own validation (the same checks as an import), checks the
   folder layout above and rejects a `templateId` used by two files. A pull request with a failing
   check is not merged.
2. On `main`, it builds `index.json`, the catalog the app reads, and publishes the templates to
   GitHub Pages. The app sees the change within a few minutes.

The check uses the catalog builder of the app repository (`npm run build-catalog`, from its
`develop` branch). To run it locally, with the app repository next to this one:

```bash
cd ../game-item-tracker
npm ci
npm run build-catalog -- --data ../game-item-tracker-data
```

One-time setup in this GitHub repository: **Settings → Pages → Build and deployment → Source:
GitHub Actions**.
