# quarto-revealjs-freestyle

An advanced fork of [quarto-revealjs-editable](https://github.com/EmilHvitfeldt/quarto-revealjs-editable) by Emil Hvitfeldt.

**Freestyle** lets you drag, resize and reposition (almost) anything on your Reveal.js slides — text divs, images, equations, blockquotes, callouts, and even interactive Plotly figures.

## What's new compared to editable

- **Robust initialization** — works reliably on browser reload (fixes blank elements on refresh)
- **Animated glow indicator** — editable elements pulse softly at rest so you always know what's draggable; glow intensifies on hover
- **Floating toolbar** — a non-intrusive bar slides in from the bottom whenever you make a change, with **Copy to clipboard** and **Save edits** buttons and visual feedback
- **Correct initial sizing** — text divs start at 80% slide width with `height: auto`; images respect their natural aspect ratio
- **Correct initial positioning** — elements are anchored at their natural rendered position, not at the slide center
- **UTF-8 support** — accented characters and special symbols are preserved when saving
- **Shortcode support** — `{{< meta ... >}}` and other Quarto shortcodes are now preserved correctly on save (fixes [editable#15](https://github.com/EmilHvitfeldt/quarto-revealjs-editable/issues/15))
- **Backslash support** — backslashes in equations and code are no longer corrupted on save (fixes [editable#16](https://github.com/EmilHvitfeldt/quarto-revealjs-editable/issues/16))

## Installing

```bash
quarto add zinc75/quarto-revealjs-freestyle
```

This will install the extension under the `_extensions` subdirectory.
If you're using version control, you will want to check in this directory.

## Using

Declare the extension in your YAML front matter:

```yaml
revealjs-plugins:
  - editable
filters:
  - editable
```

Mark any element as draggable with the `.editable` class:

```markdown
![](image.png){.editable}
```

```markdown
::: {.editable}
Some text, an equation, a blockquote, a callout...
:::
```

Once you have repositioned and resized your elements, use the floating toolbar at the bottom of the slide to **Copy to clipboard** or **Save edits**. Paste the clipboard content into your `.qmd` (or replace it with the saved file) and re-render — your elements will be locked in place.

> [!NOTE]
> Holding **Shift** while resizing an image preserves its aspect ratio.

> [!NOTE]
> The filter injects the `.qmd` source into the rendered HTML (base64-encoded) so the save/copy feature can rewrite absolute positions. Remove `editable` from `filters` before making your document public if you don't want the source embedded.

> [!WARNING]
> Images with a `width` expressed as a percentage (e.g. `{.editable width=10%}`) are not supported — use `width=Npx` instead or leave width unspecified.

> [!WARNING]
> Images with a `<figcaption>` (Quarto markdown caption syntax) are not fully supported — the caption does not follow the image when dragged. Use images without captions for best results.

> [!TIP]
> If images don't stay the size you dragged them to, add the following to your SCSS theme:
> ```scss
> .reveal img {
>   max-width: unset;
>   max-height: unset;
> }
> ```

## Example

See [example.qmd](example.qmd) for a minimal working example covering text, equations, images, video embeds, and more.

## Credits

Based on [quarto-revealjs-editable](https://github.com/EmilHvitfeldt/quarto-revealjs-editable) by [Emil Hvitfeldt](https://github.com/EmilHvitfeldt). Many thanks to Emil for the original idea and implementation.
