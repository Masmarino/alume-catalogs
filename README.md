# alume-catalog

Catalog of RSS/podcast feeds for the [Alume](https://github.com/SkollN/Alume) app.

---

## Structure

```
articles/
├── en.json       ← English articles (default fallback)
├── fr.json       ← French articles
└── fr-FR.json    ← French — France specific overrides

podcasts/
├── en.json       ← English podcasts (default fallback)
├── fr.json       ← French podcasts
└── fr-FR.json    ← French — France specific overrides
```

The app fetches both `articles/` and `podcasts/` for the current locale concurrently, then merges categories with the same `id` so that articles and podcasts appear together under the same topic (e.g. all `tech` content in one `tech` category).

## Locale resolution

The app resolves each catalog in this order:

1. `{language}-{REGION}.json` (e.g. `fr-FR.json`)
2. `{language}.json` (e.g. `fr.json`)
3. `en.json` (fallback)

## Category allowlist

The set of valid category IDs is **fixed inside the app**. Remote catalog files may define any categories, but only the following IDs will ever be displayed:

| ID | Description |
|----|-------------|
| `tech` | Technology, software, hardware |
| `science` | Science, research, environment |
| `news` | General news and current affairs |
| `culture` | Arts, music, film, literature |
| `design` | Design, UX, architecture |
| `business` | Economy, finance, entrepreneurship |
| `gaming` | Video games, esport |
| `sports` | Sports and athletics |

Any category with an unknown `id` is silently ignored at runtime. **Do not invent new IDs** — open an issue or PR against the Alume app first so the ID can be added to the allowlist.

## JSON format

```json
{
  "version": 1,
  "categories": [
    {
      "id": "tech",
      "titleKey": "discover_category_tech",
      "icon": "cpu",
      "color": "blue",
      "feeds": [
        {
          "title": "Feed name",
          "description": "Short description",
          "url": "https://example.com/rss.xml",
          "imageURL": "https://www.google.com/s2/favicons?domain=example.com&sz=128",
          "type": "article"
        }
      ]
    }
  ]
}
```

### Field reference

| Field | Type | Description |
|-------|------|-------------|
| `version` | Int | Increment when making breaking changes |
| `id` | String | Unique category identifier — must be in the allowlist above |
| `titleKey` | String | Localization key defined in the app |
| `icon` | String | SF Symbol name |
| `color` | String | One of: `blue`, `green`, `red`, `orange`, `pink`, `indigo`, `cyan`, `mint`, `purple`, `teal`, `yellow` |
| `title` | String | Display name of the feed |
| `description` | String | Short description (max ~100 chars) |
| `url` | String | Valid RSS/Atom feed URL |
| `imageURL` | String? | Feed icon URL (optional, Google Favicons recommended) |
| `type` | String | `article` (in `articles/` files) or `podcast` (in `podcasts/` files) |

> Use `article` as the `type` in `articles/` files and `podcast` as the `type` in `podcasts/` files.

## Contributing

1. Fork this repo
2. Add or modify feeds in the appropriate locale file under `articles/` or `podcasts/`
3. Validate your JSON (e.g. `python3 -m json.tool articles/en.json`)
4. Open a pull request with a short description of the feeds added

### Guidelines

- Feeds must be publicly accessible RSS/Atom feeds (no authentication required)
- Descriptions should be in the language of the catalog file
- Prefer established, regularly-updated sources
- `imageURL` should be a square icon, ideally 128×128px
- Keep `articles/` files to `type: article` only, and `podcasts/` files to `type: podcast` only
- Only use category IDs from the allowlist above — unknown IDs are ignored by the app

---

---

# alume-catalog (français)

Catalogue de flux RSS et podcasts pour l'application [Alume](https://github.com/SkollN/Alume).

---

## Structure

```
articles/
├── en.json       ← Articles en anglais (fallback par défaut)
├── fr.json       ← Articles en français
└── fr-FR.json    ← Articles en français — surcharges spécifiques France

podcasts/
├── en.json       ← Podcasts en anglais (fallback par défaut)
├── fr.json       ← Podcasts en français
└── fr-FR.json    ← Podcasts en français — surcharges spécifiques France
```

L'app récupère simultanément `articles/` et `podcasts/` pour la locale courante, puis fusionne les catégories ayant le même `id`. Articles et podcasts apparaissent ainsi ensemble sous le même thème (ex. tout le contenu `tech` dans une seule catégorie `tech`).

## Résolution de locale

L'app résout chaque catalogue dans cet ordre :

1. `{langue}-{RÉGION}.json` (ex. `fr-FR.json`)
2. `{langue}.json` (ex. `fr.json`)
3. `en.json` (fallback)

## Liste blanche des catégories

L'ensemble des identifiants de catégories valides est **fixé dans l'application**. Les fichiers du catalogue distant peuvent définir n'importe quelles catégories, mais seuls les IDs suivants seront affichés :

| ID | Description |
|----|-------------|
| `tech` | Technologie, logiciels, matériel |
| `science` | Sciences, recherche, environnement |
| `news` | Actualités générales |
| `culture` | Arts, musique, cinéma, littérature |
| `design` | Design, UX, architecture |
| `business` | Économie, finance, entrepreneuriat |
| `gaming` | Jeux vidéo, esport |
| `sports` | Sports et athlétisme |

Toute catégorie avec un `id` inconnu est silencieusement ignorée à l'exécution. **Ne pas inventer de nouveaux IDs** — ouvrez d'abord une issue ou une PR sur le dépôt Alume pour que l'ID soit ajouté à la liste blanche.

## Format JSON

```json
{
  "version": 1,
  "categories": [
    {
      "id": "tech",
      "titleKey": "discover_category_tech",
      "icon": "cpu",
      "color": "blue",
      "feeds": [
        {
          "title": "Nom du flux",
          "description": "Courte description",
          "url": "https://example.com/rss.xml",
          "imageURL": "https://www.google.com/s2/favicons?domain=example.com&sz=128",
          "type": "article"
        }
      ]
    }
  ]
}
```

### Référence des champs

| Champ | Type | Description |
|-------|------|-------------|
| `version` | Int | À incrémenter lors de changements structurels |
| `id` | String | Identifiant unique de catégorie — doit figurer dans la liste blanche |
| `titleKey` | String | Clé de localisation définie dans l'application |
| `icon` | String | Nom de symbole SF Symbol |
| `color` | String | Une valeur parmi : `blue`, `green`, `red`, `orange`, `pink`, `indigo`, `cyan`, `mint`, `purple`, `teal`, `yellow` |
| `title` | String | Nom affiché du flux |
| `description` | String | Courte description (max ~100 caractères) |
| `url` | String | URL RSS/Atom valide et publiquement accessible |
| `imageURL` | String? | URL de l'icône du flux (optionnel, Google Favicons recommandé) |
| `type` | String | `article` (dans les fichiers `articles/`) ou `podcast` (dans les fichiers `podcasts/`) |

> Utiliser `article` comme `type` dans les fichiers `articles/`, et `podcast` dans les fichiers `podcasts/`.

## Contribuer

1. Forker ce dépôt
2. Ajouter ou modifier des flux dans le fichier de locale approprié sous `articles/` ou `podcasts/`
3. Valider le JSON (ex. `python3 -m json.tool articles/fr.json`)
4. Ouvrir une pull request avec une courte description des flux ajoutés

### Règles

- Les flux doivent être des flux RSS/Atom publiquement accessibles (sans authentification)
- Les descriptions doivent être rédigées dans la langue du fichier catalogue
- Privilégier des sources établies et régulièrement mises à jour
- `imageURL` doit être une icône carrée, idéalement 128×128 px
- Garder les fichiers `articles/` en `type: article` uniquement, et les fichiers `podcasts/` en `type: podcast` uniquement
- N'utiliser que les IDs de catégories de la liste blanche — les IDs inconnus sont ignorés par l'application
