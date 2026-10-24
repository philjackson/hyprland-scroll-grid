Defining a `scrollgrid` submap replaces the built-in keyboard navigation in the overview and gives you full control over its keybinds. The submap is activated automatically when the overview opens, and closing the overview restores the default keymap. This makes more advanced interactions possible, such as closing the window under the mouse cursor with a click.

While the submap is active, regular Hyprland keybinds defined outside it are not handled by default. Add `{ submap_universal = true }` to every standard bind that should remain available while the overview is open.

Mouse wheel actions can also be bound inside the submap. If a scroll action is not bound, ScrollGrid continues to use its built-in behavior for that action. Defining a matching scroll bind overrides the built-in action for as long as the submap is active.

```lua
-- hyprland.lua
hl.define_submap("scrollgrid", function()
    hl.bind("left",   hl.plugin.scrollgrid.navigate("left"))
    hl.bind("right",  hl.plugin.scrollgrid.navigate("right"))
    hl.bind("up",     hl.plugin.scrollgrid.navigate("up"))
    hl.bind("down",   hl.plugin.scrollgrid.navigate("down"))
    hl.bind("return", hl.plugin.scrollgrid.overview("select"))
    hl.bind("escape", hl.plugin.scrollgrid.overview("off"))
    hl.bind("mouse:272", function()
        -- Select the clicked window, or just the workspace if no window was clicked, then close the overview. This is the default behaviour if submap is not defined.
        hl.plugin.scrollgrid.overview("select")
        hl.plugin.scrollgrid.window("select")
        hl.plugin.scrollgrid.overview("off")
    end, { mouse = true })
    hl.bind("mouse:274", hl.plugin.scrollgrid.window("close"), { mouse = true })
end)

-- Example Hyprland bind that keeps working inside the submap:
for i = 1, 10 do
    local key = i % 10
    hl.bind("ALT + " .. key, hl.dsp.focus({ workspace = i }), { submap_universal = true })
end
```

For native drag adoption with `cross_monitor_drag = true`, add this optional submap bind:

```lua
hl.bind("SUPER + mouse:272", hl.dsp.window.drag(), { mouse = true })
```

[Back to Configuration](Configuration.md)
