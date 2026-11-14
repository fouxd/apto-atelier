# CSS/Apto Atelier Build test

This experimental Creator build retains the Jyxy tools. Its GUI choices live in
`config/apto-atelier-test/ui/layout.json`, and theme snapshots in
`config/apto-atelier-test/themes`. It does not update the main branch.

Open Edit → CSS. **Export CSS** saves the current appearance. Edit that file in
VS Code or any text editor, then **Import CSS / theme**. Preview before Apply.
**Link CSS file** watches saves and referenced local assets. Reload forces a read;
Unlink stops live updates. Invalid edits keep the last valid preview. Apply saves
a local snapshot, and Cancel leaves your source files untouched. Re-export retains
the imported stylesheet and comments. Native settings without CSS equivalents are
preserved in the generated `--apto-base` declaration; leave that declaration intact.

## Apto CSS v1

This is a native CSS subset, not a browser stylesheet. Use `:root` for shared text,
variables and Apto options. Available component classes: `.panel`, `.module`,
`.search`, `.button`, `.settings`, `.slider`, `.toggle`, `.sidebar`, `.category`,
`.editor`, `.gui`. Prefix a component with `.menu` or `.dropdown` to scope it.
Supported states are `:hover`, `:focus`, `:active`, `:checked` on applicable controls.
Comma-separated selectors, source order, specificity and `var(--name)` work.
Unknown selectors/properties, imports and `!important` produce diagnostics.

```css
:root {
  --accent: #A5D8FF;
  color: var(--accent);
  font-family: geist;
  font-size: 110%;
  transition-duration: 220ms;
}
.module { background-color: #182535; border-radius: 12px; gap: 14px; }
.module:hover { border-color: var(--accent); border-width: 1px; }
.panel { background-image: url(assets/background.png); }
```

Use six-digit hex colours. Font size is 75–150%, corner radius 0–24px,
spacing 0–48px, border width 0–8px, opacity .15–1 and transition duration
80–1000ms. Text size is global for measured layout. Use built-in font IDs or
`font-family: url(assets/font.ttf)` for a packaged font; weight supports normal/bold.
Padding and gaps cannot remove the safety spacing required by decorations.

Apto properties select the existing native effects:

| Property | Values |
| --- | --- |
| `--apto-background` | colour, glass, rainbow, gradient, contours, galaxy, glitch |
| `--apto-gradient-start`, `--apto-gradient-end`, `--apto-tint` | #RRGGBB |
| `--apto-blur`, `--apto-transparency` | 0–20, 0–100 |
| `--apto-animated` | true, false |
| `--apto-border` | none, solid, glass, rainbow, gradient, minecrafty |
| `--apto-decoration` | existing design IDs, e.g. sakura, botanical, art_deco |
| `--apto-decoration-size`, `--apto-placement` | 50–200%; inside, edge, outside |
| `--apto-shape`, `--apto-module-size` | rounded, square, cut; 75–150% |
| `--apto-icons` | existing icon-set enum IDs |
| `--apto-opening`, `--apto-closing`, `--apto-hover`, `--apto-tabs`, `--apto-settings`, `--apto-toggles`, `--apto-search` | supported native animation IDs for that target |

CSS takes precedence over matching normal settings. Disable the CSS theme to
return to the underlying appearance. CSS changes appearance only; module actions
and navigation stay controlled by Apto. The editor preview uses mock module state.

## Packages and approval

A theme folder has `manifest.json`, `theme.css` and optional local assets. See
`atelier/themes` for three original CC0 examples. PNG/JPEG and TTF/OTF are supported.
No JavaScript, shaders, remote asset URLs or CSS imports. Limits: 25 MB compressed,
64 MB unpacked, 128 files, 256 KB CSS, four fonts, 16 megapixels of decoded images.

Run `gradlew atelierValidate -PthemePath=path/to/theme` or
`gradlew atelierPack -PthemePath=path/to/theme -PthemeOutput=theme.apto-theme`.
Submit the archive, screenshots, asset licences and supported layouts using the
catalogue repository's submission template. Every version is reviewed; updates
never silently replace an installed theme. All test themes are free.

Profile → Apto Atelier opens the curated gallery. Downloaded packages are checked
against the catalogue SHA-256, validated, then previewed. Apply is a separate step.
Catalogue failures leave local CSS and saved themes usable. Future paid themes and
the creator upload portal are not part of this test build.
