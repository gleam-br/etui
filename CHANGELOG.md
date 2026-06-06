# Changelog

All notable changes to étui are listed here.

## 1.0.1 - 2026-06-06

### Fixed

- **Keyboard I/O dropped keys (#2, #4):** replaced spawn/kill polling loop in
  `etui_terminal_ffi.erl` with persistent `etui_kbd_reader` actor. Reader
  blocks on `io:get_chars` and forwards `{etui_input, Bin}` to owner.
  Eliminates dropped keys and TTY lock contention in 60FPS loops.
  Thanks [@salespaulo](https://github.com/salespaulo).
- **Input widget horizontal scroll (#3, #5):** removed hardcoded `- 2`
  column margin in `widgets/input` truncation and cursor tracking. Uses
  full `area.size.width` via `int.max(1, area.size.width)`. Cursor no
  longer jumps prematurely; widget fills assigned cells.
  Thanks [@salespaulo](https://github.com/salespaulo).

## 1.0.0 - 2026-05-27

First public release.

### Added

- Buffer-diff rendering with cell-accurate Unicode (UAX #29 grapheme clusters).
- Layout primitives: `Length`, `Min`, `Max`, `Percentage`, `Ratio`, `Fill`,
  plus `split_with_spacing`, `split_flex`, `split_responsive`.
- 32 widgets: block, paragraph, list, table, tabs, gauge, line_gauge, hbar,
  chart, sparkline, canvas, input, textarea, tree, scrollbar, popup, statusbar,
  spinner, marquee, dialog, form, notification, scene, progress, gradient_bar,
  line, clear, scroll_view, paginator, help, fieldset, multi_select.
- Bubbletea-inspired additions (port of ratatui-cheese ideas):
  - Spinner gains 10 presets (MiniDot, Jump, Pulse, Points, Globe, Moon,
    Monkey, Meter, Hamburger, Ellipsis) on top of Dots, Line, Circle, Bounce.
  - Tree supports a right-aligned count per node via `leaf_with_count`,
    `node_with_count` and `with_count`.
  - Input gains `with_prompt`, `with_password`, `with_mask` for prompt
    prefixes and masked password fields.
  - Paginator: dot or arabic page indicator, with `slice/2` helper.
  - Help: short single-line and full multi-column key bindings view.
  - Fieldset: horizontal rule with inline title (left/center/right).
  - MultiSelect: toggle list with optional `max` cap and cursor scrolling.
- 10 built-in themes: dracula, nord, catppuccin_mocha, catppuccin_latte,
  monokai, solarized_dark, gruvbox_dark, tokyo_night, dark, light.
- App loops with crash-restore on Erlang `try/after`: `run`, `run_buffered`,
  `run_animated`, `run_buffered_cursor`.
- Backends for Erlang/BEAM, Node.js and the browser. `etui/backend/default`
  picks one at compile time.
- Typed keyboard input via `keys.match`, command tables via `keymap`,
  multi-slot focus via `focus`, integer-math easing via `anim`.
- Composition helpers in `etui/widget`: `layer`, `at`, `compose`, `stack`,
  `StatefulWidget`, `AnimatedWidget`.
- Test mock backend for app-loop coverage (`test/app_loop_test`).
