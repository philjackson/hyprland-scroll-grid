# ScrollGrid

A Hyprland overview plugin that lays your workspaces out in a grid.

ScrollGrid is based on [hyprland-scroll-overview](https://github.com/yayuuu/hyprland-scroll-overview) by
[yayuuu](https://github.com/yayuuu), a niri-style overview for Hyprland. It keeps all of that plugin's features (live
previews, drag and drop, scrolling-layout support, gestures, submap keybinds) and adds a `grid` layout:

- workspaces are arranged in rows and columns instead of a single strip, centred on the monitor
- the grid stays put while it's open; it zooms out of your current workspace and into the one you pick
- left/right move along a row, up/down jump a whole row
- each workspace card shrinks its contents until every window fits, so off-screen columns of a scrolling workspace are
  always visible without panning

The plugin is registered as `scrollgrid`, so it can be installed alongside `scrolloverview`. Don't open both overviews at
the same time.

## Installation

```bash
hyprpm add https://github.com/philjackson/hyprland-scroll-grid
hyprpm enable scrollgrid
hyprpm reload
```

To load it on login, run `hyprpm reload` from your `hyprland.start` handler. Building from source and loading the `.so`
directly is covered in the [installation guide](docs/wiki/Installation.md).

ScrollGrid is developed against Hyprland v0.56.2.

## Configuration

```lua
-- .config/hypr/hyprland.lua
hl.config({
    plugin = {
        scrollgrid = {
            layout = "grid", -- grid (default), vertical, horizontal, or auto
            columns = 0, -- grid columns; 0 picks a near-square grid for your workspace count
            scale = 0.3, -- size of each workspace card (strip layouts; the grid sizes itself to fit the monitor)
            workspace_gap = 30,
        },
    },
})

hl.bind("SUPER + g", function()
    hl.plugin.scrollgrid.overview("toggle all")
end)
```

To navigate with your own keys (for example Vim-style `h`/`j`/`k`/`l`), define a `scrollgrid` submap; see
[Keybind submap](docs/wiki/Keybind-submap.md).

## Documentation

The [docs](docs/wiki/Home.md) are adapted from hyprland-scroll-overview's wiki and cover every option, dispatcher,
gesture and submap. Everything there applies to ScrollGrid; only the plugin name differs.

## Credits

All of the overview itself is yayuuu's work in
[hyprland-scroll-overview](https://github.com/yayuuu/hyprland-scroll-overview), which credits Vaxry / Hypr Development
as co-authors. ScrollGrid only adds the grid layout. BSD 3-Clause, see [LICENSE](LICENSE).
