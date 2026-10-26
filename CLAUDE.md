# Coffee Up V2 – Thème Shopify (base Horizon)

## Contexte
- Refonte e-commerce de Coffee Up (coffee shop, Genève) sur Shopify.
- Base : thème Horizon (architecture "theme blocks" : sections, blocks imbriqués, templates JSON, web components).
- Développement sur une boutique de test (coffeeup-v2-sandbox). Le thème validé sera ensuite poussé sur la boutique client.
- Tout se fait en code : pas d'utilisation de l'éditeur visuel Shopify.

---

## Direction artistique

**Positionnement** : coffee shop genevois premium et chaleureux. Signature : « Sip slowly, time will wait ».
Valeurs à transmettre : lenteur, matière, savoir-faire, chaleur.

**Inspirations web**
- yeezy.com → minimalisme radical du catalogue : grille produits silencieuse, visuels sur fond uniforme, libellés minuscules, aucun bandeau promo, aucun élément décoratif superflu.
- ochi.design → typographie éditoriale XXL, sections à coins arrondis, bandeau de texte défilant, animations d'apparition au scroll, boutons en pilule.

**Synthèse** : un catalogue silencieux (Yeezy) + un storytelling éditorial expressif (Ochi), dans l'univers chaud de Coffee Up (bordeaux, crème, bois, acier brossé).

---

## Design tokens

### Couleurs
| Token | Hex | Usage |
|---|---|---|
| `--color-ink` | `#2E0513` | Texte principal sur fond clair, footer |
| `--color-bordeaux-deep` | `#390517` | Sections sombres, hover des CTA |
| `--color-bordeaux` | `#570B24` | Couleur de marque : CTA, liens actifs, bandeau défilant, sections fortes |
| `--color-sand` | `#E6D9C5` | Texte et logo sur fond bordeaux, bordures, fonds secondaires |
| `--color-cream` | `#FEF6E9` | Fond principal |

Règles :
- Répartition visée : ~60 % crème (fonds), ~30 % ink/bordeaux (texte, sections sombres), ~10 % sable (accents).
- Contrastes calculés : ink sur crème ≈ 17:1, bordeaux sur crème ≈ 13:1, sable sur bordeaux ≈ 10:1 → OK pour du texte.
- Sable sur crème ≈ 1,3:1 → **jamais pour du texte**, uniquement bordures et fonds.
- Pas de noir pur (#000) ni de blanc pur (#FFF).

Schémas de couleurs Horizon à créer :
1. Crème : fond `cream`, texte `ink`, bouton `bordeaux` / texte bouton `cream`
2. Bordeaux : fond `bordeaux`, texte `sand`, bouton `cream` / texte bouton `bordeaux`
3. Sable : fond `sand`, texte `ink`, bouton `bordeaux`
4. Profond : fond `bordeaux-deep`, texte `sand`, bouton `sand` / texte bouton `bordeaux-deep`

### Typographies
| Rôle | Police | Notes |
|---|---|---|
| Display (titres, citations éditoriales) | **EB Garamond** | Libre (Google Fonts). Grandes tailles, interlignage serré, italique pour l'emphase. |
| Texte et UI (navigation, boutons, prix, labels) | **Helvetica Now** | Police commerciale : vérifier que le client possède une licence web. Sinon, utiliser la pile système `"Helvetica Neue", Helvetica, Arial, sans-serif`, ou Inter (libre). |
| Accent (optionnel) | Caslon #3 → **Libre Caslon** | Caslon #3 est commerciale. N'utiliser Libre Caslon que si un accent est vraiment nécessaire ; sinon ne pas la charger. |
| Script | **Amsterdam Four** | Jamais en police web pour du texte. Uniquement pour la citation « Sip slowly, time will wait » et les signatures, exportées en **SVG**. |

Règles de chargement :
- Maximum **2 familles de polices web** (performance) : EB Garamond + la sans-serif.
- Si une police est absente de la bibliothèque Shopify (font_picker), l'auto-héberger en woff2 dans `assets/` avec `@font-face` et `font-display: swap`.
- Précharger uniquement la police display.

Échelle typographique (fluide) :
| Niveau | Taille | Style |
|---|---|---|
| display | `clamp(3rem, 8vw, 8rem)` | EB Garamond, line-height 0.95, letter-spacing -0.02em |
| h1 | `clamp(2.5rem, 5vw, 4.5rem)` | EB Garamond |
| h2 | `clamp(2rem, 3.5vw, 3rem)` | EB Garamond |
| h3 | `1.5rem` | EB Garamond |
| body | `1rem`, line-height 1.6 | Sans-serif |
| label | `0.75rem`, capitales, letter-spacing 0.08em | Sans-serif (nav, prix, boutons, métadonnées) |

### Espacements, grille, formes
- Échelle d'espacement : 4, 8, 16, 24, 32, 48, 64, 96, 128 px.
- Sections : padding vertical 96–128 px en desktop, 64 px en mobile.
- Grille : 12 colonnes en desktop, gouttière 24 px ; marges latérales 16 px en mobile.
- Rayons : blocs éditoriaux et sections 24 px (Ochi) ; boutons en pilule (999 px) ; images produit **sans arrondi** dans la grille (rigueur Yeezy).

---

## Principes de mise en page

**Page d'accueil**
1. Hero éditorial : titre display XXL + visuel d'ambiance (bois, lumière naturelle).
2. Bandeau défilant sur fond bordeaux : « SIP SLOWLY — TIME WILL WAIT — GENÈVE — ».
3. Sélection de produits en grille épurée.
4. Histoire et savoir-faire : sections arrondies alternant crème et bordeaux.
5. Le lieu et les infos pratiques.
6. Footer sur fond ink.

**Catalogue et collections (esprit Yeezy)**
- Grille 2 colonnes en mobile, 4 en desktop.
- Photos sur fond crème uniforme ou détourées.
- Sous chaque photo : uniquement nom + prix, en style label.
- Aucun badge criard, aucun carrousel.

**Page produit**
- Grande image, titre en display, prix en label.
- Variantes en pilules.
- CTA bordeaux, pleine largeur en mobile.
- Description éditoriale courte ; origine, torréfaction et notes de dégustation en liste de caractéristiques.

**Navigation**
- Minimaliste : mini-logo « UP », 3 à 4 liens, panier.
- Menu plein écran en mobile.

**Photographie**
- Lumière naturelle chaude, matières (bois, acier brossé, crème, carton).
- Pas de photos de banque d'images froides.

---

## Motion
- Apparitions au scroll : fondu + translation de 16–24 px, 400–600 ms, ease-out, via IntersectionObserver ou web components.
- Aucune librairie lourde (GSAP, Locomotive Scroll…) sans validation explicite.
- Bandeau défilant en CSS (animation `transform`), en pause au survol.
- Survols : transitions de 200 ms ; boutons en inversion de couleurs.
- `prefers-reduced-motion: reduce` → désactiver toutes les animations.

---

## Où coder les tokens dans Horizon
- **Couleurs et polices** : dans les réglages du thème (`config/settings_data.json` : color schemes, font pickers). Exception autorisée à la règle « ne pas toucher à settings_data » **uniquement pour les tokens de design, après validation du plan**.
- **Autres variables** (échelle typographique, espacements, rayons, motion) : un seul fichier `assets/coffee-tokens.css`, chargé dans `layout/theme.liquid`.
- Jamais de valeurs en dur dans les sections ou les blocks : toujours passer par les variables.

## Assets à demander au client
- Logos « COFFEE UP » et mini-logo « UP » en SVG.
- Citation « Sip slowly, time will wait » en SVG.
- Photos HD (lieu, produits, matières).
- Licence web de Helvetica Now, si elle existe.

---

## Invariants Shopify – ne jamais casser
- `layout/theme.liquid` : garder `{{ content_for_header }}` dans `<head>` et `{{ content_for_layout }}` dans `<body>`.
- Formulaires produit : `<form action="/cart/add">`, champ `name="id"` = variante sélectionnée, bouton `type="submit"`.
- Ne pas renommer les types de sections/blocks ni les IDs de settings existants (les données vivent dans `templates/*.json`).
- Garder les blocs `@app` dans les sections qui en ont.
- Ne jamais toucher au checkout.
- Ne pas modifier `templates/*.json` ni `config/settings_data.json` sans demande explicite (sauf l'exception tokens ci-dessus).

## Méthode de travail
- Toujours lire et proposer un plan avant de modifier quoi que ce soit ; attendre ma validation.
- Une page ou un composant à la fois.
- Après chaque modification : lancer `shopify theme check`, corriger avant de continuer.
- Ne jamais lancer `shopify theme push` ni `publish` : c'est moi qui pousse.
- Préférer étendre ou modifier les sections et blocks existants d'Horizon plutôt que tout réécrire.
- Mobile first, accessibilité (contraste, focus visible, textes alternatifs), performance (images via `image_url` / `image_tag`, lazy loading, JS minimal).