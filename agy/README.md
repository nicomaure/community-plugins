# Antigravity AGY

Quick bar launcher for the Antigravity Agent CLI (`agy`) with optional floating terminal support in Niri.

## Plugin

| Field | Value |
| --- | --- |
| ID | `nicomaure/agy` |
| Entries | Bar widget: `bar` |

## Requirements

- `alacritty` available on `PATH`.
- `agy` (Antigravity CLI) available on `PATH`.

If either is missing, the widget shows an error notification instead of launching.

For optional floating-window behavior on Niri, add this window rule manually to `~/.config/niri/cfg/rules.kdl`:

```kdl
// BEGIN AGY_NIRI_NOCTALIA
window-rule {
    match app-id="^agy-terminal$"
    open-floating true
    geometry-corner-radius 16
    clip-to-geometry true
    default-column-width { fixed 1100; }
    default-window-height { fixed 720; }
}
// END AGY_NIRI_NOCTALIA
```

The plugin does not modify compositor configuration.

## Usage

Add the **Antigravity AGY** widget to your Noctalia Bar under **Settings** (Mod+Shift+S) -> **Bar** -> **Widgets**.

- **Left click:** Launches `agy` in the configured project directory. If that directory does not exist, the plugin falls back to `~/Proyectos/agy` when available, and then to `$HOME`.
- **Right click:** Launches `agy` in your home directory (`$HOME`).

## Settings

| Setting | Type | Default | Description |
| --- | --- | --- | --- |
| `show_label` | `bool` | `true` | Show the AGY text label next to the icon in the bar. |
| `project_dir` | `string` | `~/Proyectos/agy` | Default workspace directory opened on left click. |

## Notes

- **Process Lifecycle:** The widget remains idle until the user clicks it. It launches Alacritty and `agy` only after interaction.
- **Spawned Processes:** On click it launches `alacritty` with arguments to run `agy`. It does not invoke a shell.
- **Filesystem and Network:** The plugin does not write files or make network calls. It checks whether configured commands and directories exist before launching.
- **Compositor Support:** Tested on Niri. The widget may also work on other Wayland compositors, but the floating-window rule in this README is specific to Niri.
- **Privacy & Security:** The plugin runs locally and does not download or execute remote code.
