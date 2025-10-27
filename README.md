# GlitchizUI v3.1 - Documentation

Welcome to the official documentation for GlitchizUI v3.1. This is a modern, feature-rich, and highly customizable UI library for Roblox, designed with a stylish "glitch" aesthetic. Its API is inspired by popular libraries like Rayfield, making it intuitive and easy to learn.

## Key Features in v3.1
*   **Full Mobile Support**: The UI automatically reshapes itself for a native feel on vertical screens.
*   **Keybind Toggling**: Set a keyboard key (like RightControl) to quickly hide and show the UI.
*   **Fully Animated**: Smooth, tweened animations for tab transitions, sliders, dropdowns, and interactive feedback on all elements.
*   **Complete UI Suite**: Includes all essential components: buttons, toggles, sliders, textboxes with submit buttons, and dropdowns.

## Table of Contents
1.  [**Setup & Installation**](#setup--installation)
2.  [**Creating a Window**](#creating-a-window)
3.  [**Adding Tabs**](#adding-tabs)
4.  [**UI Elements (Components)**](#ui-elements-components)
    *   [Label](#label)
    *   [Button](#button)
    *   [Toggle](#toggle)
    *   [Textbox](#textbox)
    *   [Slider](#slider)
    *   [Dropdown](#dropdown)
    *   [Divider](#divider)
5.  [**Full Example Script**](#full-example-script)

---

## Setup & Installation

GlitchizUI is designed to be loaded directly from its source code on GitHub. This means you don't need to install any files; you just run a small loader script.

```lua
-- ==========================================================
-- GlitchizUI v3.1 Loader
-- This script will fetch and run the latest version of the UI.
-- ==========================================================

local URL = "https://raw.githubusercontent.com/xGSPx/GlitchizUI/main/main"

-- Safely download the library code
local success, response = pcall(function()
    return game:HttpGet(URL)
end)

if success then
    -- Compile and run the downloaded code to get the library table
    local GlitchizUI = loadstring(response)()

    -- ==========================================================
    -- YOUR UI CODE GOES HERE
    -- ==========================================================
    
else
    warn("GlitchizUI Error: Failed to load library from GitHub.", response)
end
```

---

## Creating a Window

Everything starts with a Window. This is the main container that holds all of your tabs and UI elements.

### `GlitchizUI.new(properties)`

This function creates and returns a new Window object.

**Parameters:**
*   `properties` (table): A table of properties to customize the window.

| Property | Type | Description | Default |
| :--- | :--- | :--- | :--- |
| `Title` | `string` | The text displayed at the top of the window. | "GlitchizUI" |
| `Size` | `UDim2` | The size of the window (only applies to PC). | `UDim2.new(0, 550, 0, 350)` |
| `Keybind`| `Enum.KeyCode`| The keyboard key to toggle the UI's visibility. | `Enum.KeyCode.RightControl`|

**Example:**
```lua
local Window = GlitchizUI.new({
    Title = "My Awesome UI",
    Keybind = Enum.KeyCode.RightShift -- Use Right-Shift to open/close
})
```

---

## Adding Tabs

Tabs are used to organize your UI elements into different categories. You must add at least one tab before you can add any elements.

### `Window:AddTab(name)`

Adds a new tab to the window and selects it, so any subsequent elements are added to this tab.

**Parameters:**
*   `name` (string): The name of the tab to be displayed.

**Example:**
```lua
Window:AddTab("Main")
-- All elements added now will go into the "Main" tab

Window:AddTab("Settings")
-- All elements added now will go into the "Settings" tab
```

---

## UI Elements (Components)

### Label
Displays text.

#### `Window:AddLabel(properties)`

| Property | Type | Description | Default |
| :--- | :--- | :--- | :--- |
| `Text` | `string` | The text to display. | "Label" |
| `Big` | `boolean` | Makes the text larger. | `false` |
| `Bold` | `boolean` | Makes the text bold. | `false` |
| `Color` | `Color3` | Sets the color of the text. | White |

### Button
A standard clickable button that performs an action.

#### `Window:AddButton(properties)`

| Property | Type | Description |
| :--- | :--- | :--- |
| `Text` | `string` | The text displayed on the button. |
| `Callback`| `function`| The function to run when the button is clicked. |

### Toggle
An on/off switch.

#### `Window:AddToggle(properties)`

| Property | Type | Description |
| :--- | :--- | :--- |
| `Text` | `string` | The label displayed next to the toggle. |
| `Default`| `boolean`| The initial state of the toggle (`true` for on). Defaults to `false`. |
| `Callback`| `function`| Runs when the state changes. It receives the new boolean value as an argument. |

### Textbox
An input field for users to type text, with a submit button.

#### `Window:AddTextbox(properties)`

| Property | Type | Description |
| :--- | :--- | :--- |
| `Placeholder` | `string` | Faint text shown when the textbox is empty. |
| `ButtonText`| `string` | The text on the submit button. Defaults to "Submit". |
| `Callback` | `function`| Runs when the user presses Enter or clicks Submit. It receives the entered text as an argument. |

### Slider
Allows the user to select a number within a range.

#### `Window:AddSlider(properties)`

| Property | Type | Description |
| :--- | :--- | :--- |
| `Text` | `string` | The label displayed above the slider. |
| `Min` | `number` | The minimum value of the slider. Defaults to `0`. |
| `Max` | `number` | The maximum value of the slider. Defaults to `100`. |
| `Default`| `number`| The starting value of the slider. |
| `Callback`| `function`| Runs every time the value changes. It receives the new number value as an argument. |

### Dropdown
A button that reveals a list of selectable options.

#### `Window:AddDropdown(properties)`

| Property | Type | Description |
| :--- | :--- | :--- |
| `Default`| `string` | The text shown before an option is selected. |
| `Options`| `table` | An array of strings representing the choices in the dropdown. |
| `Callback`| `function`| Runs when an option is selected. It receives the selected option string as an argument. |

**Example:**
```lua
Window:AddDropdown({
    Default = "Select a Tool",
    Options = {"Sword", "Gravity Coil", "Speed Coil"},
    Callback = function(selectedOption)
        print(selectedOption .. " was chosen!")
        -- Add logic here to give the player the tool
    end
})
```

### Divider
A horizontal line used to visually separate elements.

#### `Window:AddDivider()`
This function takes no arguments.

---

## Full Example Script

Here is a complete script that uses every feature of the library, serving as a perfect starting point.

```lua
local URL = "https://raw.githubusercontent.com/xGSPx/GlitchizUI/main/main"

local success, response = pcall(function() return game:HttpGet(URL) end)

if success then
    local GlitchizUI = loadstring(response)()

    -- Create the main window
    local Window = GlitchizUI.new({
        Title = "GlitchizUI Full Demo",
        Keybind = Enum.KeyCode.RightControl,
    })

    -- Create a 'Main' Tab
    Window:AddTab("Main")
    Window:AddLabel({ Text = "Main Features", Big = true, Bold = true })
    Window:AddButton({
        Text = "Reset Character",
        Callback = function() game.Players.LocalPlayer.Character.Humanoid.Health = 0 end
    })
    Window:AddToggle({
        Text = "Fly Mode (Placeholder)", Default = false,
        Callback = function(v) print("Fly mode set to:", v) end
    })

    -- Create a 'Player' Tab
    Window:AddTab("Player")
    Window:AddLabel({ Text = "Player Customization", Bold = true })
    Window:AddTextbox({
        Placeholder = "Enter custom speed...", ButtonText = "Set",
        Callback = function(text)
            local speed = tonumber(text)
            if speed then game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = speed end
        end
    })
    Window:AddSlider({
        Text = "WalkSpeed", Min = 16, Max = 200, Default = 16,
        Callback = function(v) game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = v end
    })
    
    -- Create a 'Visuals' Tab
    Window:AddTab("Visuals")
    Window:AddLabel({ Text = "Client-Side Visuals", Bold = true })
    Window:AddSlider({
        Text = "Field of View", Min = 70, Max = 120, Default = 70,
        Callback = function(v) workspace.CurrentCamera.FieldOfView = v end
    })
    Window:AddDropdown({
        Default = "Select Skybox",
        Options = {"Day", "Night", "Sunset"},
        Callback = function(option)
            print("Skybox changed to:", option)
            -- Add logic to change lighting here
        end
    })

else
    warn("GlitchizUI Error:", response)
end
```
