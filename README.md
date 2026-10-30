# Kickoff UI

Color, typography, spacing, radius and shadow tokens you can drop into any Figma file and start designing straight away. No more spending the first hour of every project setting up the foundation.

Built on Figma variables, with light and dark modes, desktop and mobile type, and colors that pass contrast checks out of the box.

**Figma plugin:** https://www.figma.com/community/plugin/1690011809923056404/kickoff-ui

---

## What's inside

- **306 primitives**: the full Tailwind color palette (22 colors × 11 shades), black and white transparency steps, 11 font families, seven weights (Light to Black), sizes and line heights
- **100 color tokens**: backgrounds, text, icons, borders and shadows, each with a light and a dark value and a short note on when to use it
- **95 typography tokens** with desktop and mobile values
- **95 text styles**: Display, Heading, Title, Body, Label, Caption and Code in every size, each in five weights: Light, Default, Emphasis, Strong and Stronger
- **26 layout tokens**: spacing on a 4px grid and corner radius
- **5 shadow styles** that get stronger in dark mode
- **Built-in documentation pages** in Figma: a getting started guide, every color token in light and dark side by side, a live type specimen, and spacing, radius and shadow examples

Every text color passes WCAG AA contrast (4.5:1) on the surfaces it's meant for, in both modes.

## Get started

**Option 1: Start from the Community file.** Duplicate it, add your own pages, and design right there. Best for new projects.

**Option 2: Use it as a library.** Publish the file as a library and turn it on in your other files from Assets → Libraries. Needs a paid Figma plan. Best for teams.

**Option 3: Run the plugin.** Open any file, press Cmd + P (Ctrl + P on Windows), type "Kickoff UI" and hit Enter. It adds the variables, styles and docs pages without touching your existing layers. Running it again only adds what's missing.

> **Free plan?** Light/dark and desktop/mobile are variable modes, and Figma only allows multiple modes on paid plans. On a free plan you still get every token and style, just in light mode with desktop type.

## How it's built

Three layers, each built on the one before:

1. **Primitives**: raw values with no meaning attached, like `color/blue/600` or `type/size/16`. Hidden from Figma's pickers on purpose.
2. **Semantic tokens**: named by job, like `bg/neutral/primary` or `text/error/strong`. These are what you design with. They point to primitives, and color tokens point to a different primitive in dark mode.
3. **Styles**: text styles and shadow styles built from the tokens. Change a token and every style follows.

### Naming

Every semantic color follows the same pattern: `property / color family / variant`.

| Property | Neutral | Intents (accent, error, success, warning, info) |
| --- | --- | --- |
| `bg` | primary, secondary, tertiary, inverse, placeholder, disabled, plus hover, pressed and overlay states | subtle, muted, solid, plus hover and pressed states |
| `text` / `icon` | primary, secondary, tertiary, placeholder, disabled, inverse, on-solid | primary, strong |
| `border` | primary (strongest) to quaternary (quietest), disabled | subtle, strong, and `border/accent/focus` |
| `shadow` | primary, secondary | |

**Which hover do I use?**

- Solid buttons → `bg/accent/solid-hover` and `solid-pressed`
- White or neutral-filled buttons → `bg/neutral/primary-hover` and `primary-pressed`
- Soft, tinted buttons → `bg/accent/subtle-hover`, with `text/accent/strong` on top
- Ghost buttons, list rows, menu items → `bg/neutral/ghost-hover` and `ghost-pressed`

### Typography

Text styles are named `Role / Size / Weight`, like `Body/Medium/Default` or `Heading/Large/Strong`. Each role has its own five-step weight scale (light, default, emphasis, strong, stronger) in the typography collection. The names are relative to the default, so if you want body text in Medium, point `body/weight/default` to Medium and shift the others to match. Every property (font, weight, size, line height, letter spacing) is linked to a variable.

The default font is **Inter**, with **JetBrains Mono** for code. Also included, ready to swap in: Geist, DM Sans, Manrope, Plus Jakarta Sans, Figtree, IBM Plex Sans, Poppins, Bricolage Grotesque and Geist Mono. All are Google Fonts, so they work in Figma without installing anything.

Weights are stored as names (Light, Regular, Medium, Semi Bold and so on) so they work with any font, including ones installed on your computer. Line heights and letter spacing are in pixels (Figma only supports pixels for these when they're variables), on a 4px grid.

## Make it yours

**Swap fonts:** in the `typography` collection, right-click the value of `family/heading` or `family/body`, choose Create alias, and pick another font from `type/family`.

**Add a font that isn't listed:** add a string variable to `primitives` named `type/family/your-font`, set its value to the font's exact name as Figma shows it, then point `family/heading` or `family/body` to it. The font needs Regular, Medium, Semibold and Bold. Fonts that aren't on Google Fonts must be installed on your computer and used in the Figma desktop app.

**Rebrand the accent:** in the `color` collection, point the accent tokens (`bg/accent`, `text/accent`, `icon/accent`, `border/accent`) to the same steps in another color, like `violet/600` instead of `blue/600`. Then check that text on solid buttons still reads well.

**The golden rule:** use semantic tokens, not primitives. If a layer doesn't change when you switch to dark mode, it's using a primitive or a plain hex value.

## Using the tokens in code

### CSS

```html
<link rel="stylesheet" href="css/kickoff-ui.css">
```

```css
.card {
  background: var(--ko-bg-neutral-secondary);
  color: var(--ko-text-neutral-primary);
  border: 1px solid var(--ko-border-neutral-tertiary);
  border-radius: var(--ko-radius-lg);
  padding: var(--ko-spacing-24);
  box-shadow: var(--ko-shadow-small);
}
```

Text styles are available as classes, like `ko-body-md`, `ko-body-md-emphasis` or `ko-heading-lg-strong`. Dark mode follows the system setting automatically, or you can force it with `data-theme="dark"` (or `"light"`) on any element. Mobile type kicks in below 768px.

You'll need to load the fonts yourself, for example from Google Fonts.

### JSON

The `tokens` folder has every token in the [Design Tokens Community Group](https://www.designtokens.org/) format, ready for tools like Style Dictionary or Tokens Studio:

| File | What's in it |
| --- | --- |
| `primitives.tokens.json` | Colors, font families, weights, sizes, line heights |
| `color.light.tokens.json` / `color.dark.tokens.json` | Semantic colors for each mode |
| `typography.desktop.tokens.json` / `typography.mobile.tokens.json` | Font families, weights, sizes, line heights and letter spacing for each mode |
| `layout.tokens.json` | Spacing and radius |
| `effects.tokens.json` | Shadows |

Semantic tokens reference primitives with aliases like `{color.blue.600}`, so load the primitives file alongside them.

## Repo structure

```
plugin/      The Figma plugin (manifest.json + code.js). code.js holds all token data.
tokens/      Tokens as DTCG JSON (generated)
css/         Tokens as CSS variables and text classes (generated)
scripts/     build.js, which generates tokens/ and css/ from plugin/code.js
```

`plugin/code.js` is the single source of truth. After changing any token there, run:

```
node scripts/build.js
```

to regenerate the JSON and CSS. No dependencies needed, just Node 18 or newer.

### Running the plugin locally

1. Open the Figma desktop app.
2. Go to Plugins → Development → Import plugin from manifest, and pick `plugin/manifest.json`.
3. Run it with Cmd + P (Ctrl + P on Windows) → "Kickoff UI".

## Contributing

Suggestions and fixes are welcome. See [CONTRIBUTING.md](CONTRIBUTING.md).

## Credits

Made by Doris Gabriel.

Color values from [Tailwind CSS](https://tailwindcss.com) (MIT License). Fonts from [Google Fonts](https://fonts.google.com). See [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md).

## License

[MIT](LICENSE). Use it in personal and commercial work, modify it, share it.
