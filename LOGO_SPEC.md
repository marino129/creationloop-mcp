# Logo Spec

The Cline marketplace requires a **400x400 PNG** icon for the server listing. This
file specifies that asset. The PNG itself is a **founder-supply item** (see the
flag at the bottom); this repository ships the vector source to export from.

## Required deliverable

- **Format:** PNG.
- **Dimensions:** exactly 400 x 400 pixels (square).
- **File name:** `logo.png`, placed in this folder alongside this spec.
- **Background:** filled, not transparent. Use the Dark Slate ground so the mark
  reads on light and dark listing pages alike.
- **Content:** the CreationLoop loop mark, centered, with comfortable padding
  (roughly 12 to 16 percent of the canvas as margin on each side).

## Brand tokens

| Token        | Value     | Use                                            |
|--------------|-----------|------------------------------------------------|
| System Blue  | `#3B82F6` | Left loop stroke and its node rings            |
| Logic Purple | `#8B5CF6` | Right loop stroke and its node rings           |
| Dark Slate   | `#1A1D24` | Ground / canvas fill and node centers          |
| White        | `#FFFFFF` | Outer mark stroke and the center square        |

- **Wordmark typeface:** Space Grotesk. If the icon includes the wordmark, set it
  in Space Grotesk. For a 400x400 icon the mark alone is usually cleaner; keep the
  wordmark for horizontal or stacked lockups.

## Source assets in this repository / codebase

- **`brand-mark-source.svg`** (in this folder): the loop mark as vector, using the
  exact brand tokens above. Copied from the codebase source below. Export this to a
  400x400 PNG on a Dark Slate square to produce `logo.png`.
- Codebase source of the same mark: `attached_assets/01-mark-color_1781288119645.svg`.
- Codebase stacked lockup (dark ground): `artifacts/landing/public/assets/loop-stacked-dark.png`.
- Codebase horizontal lockup (dark ground): `artifacts/landing/public/assets/loop-horizontal-dark.png`.
- Codebase mark: `artifacts/landing/public/assets/loop-mark.svg`.

## How to export (any one of these)

- Open `brand-mark-source.svg` in a vector editor, place it on a 400x400 Dark
  Slate (`#1A1D24`) square with even padding, and export as PNG.
- Or, with a command-line renderer, for example:
  ```sh
  rsvg-convert -w 400 -h 400 --background-color '#1A1D24' \
    brand-mark-source.svg -o logo.png
  ```
  Confirm the mark is centered with padding; the source viewBox is 2:1
  (horizontal), so you may want to re-center it on the square canvas rather than
  stretch it.

## FOUNDER-SUPPLY ITEM

> The 400x400 `logo.png` is **not** included in this repository yet. No image
> rendering tooling was available in the authoring environment, so the mark could
> not be exported to a square PNG here. Before submitting to the Cline marketplace,
> the founder must export `logo.png` from `brand-mark-source.svg` per this spec and
> add it to this folder.
