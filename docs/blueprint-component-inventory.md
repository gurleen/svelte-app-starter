# Blueprint component inventory

Companion to [`blueprint-style-guide.md`](./blueprint-style-guide.md), which records *how*
components are restyled to match Blueprint. This document tracks *which* components have made
the trip, and what's left in Blueprint's own component set.

## Converted (`src/lib/components/ui/`)

| Component | Blueprint counterpart | Style-guide audited? |
|---|---|---|
| `badge` | Tag | No — token colors only, not button-fidelity audited |
| `button` | Button | Yes — full fidelity pass, see style guide |
| `card` | Card | No |
| `checkbox` | Checkbox | No |
| `dialog` | Dialog | No |
| `dropdown-menu` | Menu + Popover | No |
| `input` | InputGroup | No |
| `label` | FormGroup (label portion) | No |
| `select` | HTMLSelect | No |
| `separator` | Divider | No |
| `switch` | Switch | No |
| `table` | HTMLTable | No |
| `tabs` | Tabs | No |
| `tooltip` | Tooltip | No |
| `alert-dialog` | Alert | No |
| `alert` | Callout | No |
| `breadcrumb` | Breadcrumbs | No |
| `collapsible` | Collapse | No |
| `radio-group` | RadioGroup | No |
| `progress` | ProgressBar | No |
| `context-menu` | ContextMenu | No |
| `popover` | Popover | No |
| `textarea` | Textarea | No |
| `icon` | Icon | No |
| `non-ideal-state` | NonIdealState | No |
| `control-group` | ControlGroup | No |
| `sonner` | Toast / OverlayToaster | No |
| `spinner` | Spinner | No |
| `text` | Text | No |

"Style-guide audited" means the component has been checked against Blueprint's own docs
dimension-by-dimension (sizing, spacing, states) the way `button.svelte` was. Everything else
so far only inherits the shared color/spacing/radius/elevation/typography tokens from
`layout.css` — same system, not yet individually verified against Blueprint's spec.

## In Blueprint, not yet in this project

| Blueprint component | shadcn-svelte equivalent | How to add |
|---|---|---|
| Drawer | Sheet | Use existing shadcn component, restyle |
| EditableText | — | Build from scratch (inline-edit text, no shadcn primitive) |
| HTMLTable (data-grid variant) | Table (already converted) | Already covered — `table` handles this |
| Menu / MenuItem (standalone, non-dropdown) | Command / ContextMenu | Combine — `dropdown-menu` primitives already give most of this |
| Navbar | — | Build from scratch (thin layout component, no real shadcn primitive) |
| NumericInput | Input | Combine — `input` plus increment/decrement buttons |
| OverflowList | — | Build from scratch (no shadcn/Radix equivalent; measurement-driven layout) |
| Panel / PanelStack | — | Build from scratch (stacked navigable panel view, no shadcn primitive) |
| Slider / RangeSlider / MultiSlider | Slider | Use existing shadcn component, restyle (MultiSlider needs extension work) |
| Tag / TagInput (input variant) | Badge (Tag done) / InputOTP-style combo | Combine — `input` plus removable `badge` chips for TagInput |
| Tree | — | Build from scratch or additional dependency (no shadcn primitive; consider a headless tree library) |
| **From `@blueprintjs/select`** | | |
| Select (searchable) | Combobox | Use existing shadcn component, restyle |
| MultiSelect | Combobox (multi) | Combine — `combobox` plus `badge` chips, no built-in multi mode in shadcn-svelte |
| Suggest | Combobox | Use existing shadcn component, restyle |
| Omnibar | Command | Use existing shadcn component, restyle (Command already renders as a dialog-hosted palette) |
| **From `@blueprintjs/datetime`** | | |
| DatePicker | Calendar | Use existing shadcn component, restyle |
| DateInput | Calendar + Popover | Combine — shadcn's date-picker pattern already composes these |
| DateRangeInput | Calendar (range mode) | Use existing shadcn component, restyle |
| TimezoneSelect | — | Build from scratch or additional dependency (needs a timezone data source, e.g. `Intl.supportedValuesOf('timeZone')`) |
| **From `@blueprintjs/table`** | | |
| Table (virtualized data grid) | — | Additional dependency (this is a distinct, heavier component from HTMLTable — e.g. TanStack Table for logic + custom virtualized rendering) |

## Notes

- "Use existing shadcn component, restyle" means: run the shadcn-svelte CLI to scaffold it into
  `src/lib/components/ui/`, then apply the same token/spacing/radius/elevation treatment
  documented in `blueprint-style-guide.md` — no new architectural work.
- "Combine" means composing already-converted primitives; once done, add the result as its own
  entry in `src/lib/components/ui/` and move it to the "Converted" table above.
- "Build from scratch" means no shadcn-svelte or Radix/bits-ui primitive exists for it — it's a
  bespoke Svelte component following the structural pattern in the style guide.
- Blueprint's `Overlay2`, `Portal`, `ResizeSensor`, `KeyCombo`/`Hotkeys` are internal/utility
  building blocks rather than end-user UI components and are intentionally omitted here.
