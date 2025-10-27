# GlitchizUI v2.0 - Documentation

Welcome to the official documentation for GlitchizUI v2.0. This is a modern, feature-rich, and highly customizable UI library for Roblox, designed with a stylish "glitch" aesthetic. Its API is inspired by popular libraries like Rayfield, making it intuitive and easy to learn.

This guide will walk you through the setup process and provide a detailed reference for every available UI element.

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
    *   [Divider](#divider)
5.  [**Full Example Script**](#full-example-script)

---

## Setup & Installation

GlitchizUI is designed to be loaded directly from its source code on GitHub. This means you don't need to install any files; you just run a small loader script.

Simply use the following script to load the library and create your UI.

```lua
-- ==========================================================
-- GlitchizUI Loader
-- This script will fetch and run the latest version of the UI.
-- ==========================================================

-- The raw URL to your GlitchizUI code on GitHub
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
    -- Example:
    local Window = GlitchizUI.new({
        Title = "My First GlitchizUI",
        Size = UDim2.new(0, 500, 0, 300),
    })
    
    Window:AddTab("Main")
    Window:AddLabel({ Text = "Successfully Loaded!", Big = true })
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
| `Size` | `UDim2` | The size of the window in pixels. | `UDim2.new(0, 550, 0, 350)` |
| `Position` | `UDim2` | The screen position of the window. | Centered on screen |

**Example:**
```lua
local Window = GlitchizUI.new({
    Title = "My Awesome UI",
    Size = UDim2.new(0, 600, 0, 450)
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

These are the core interactive components of the library.

### Label
Displays text.

#### `Window:AddLabel(properties)`

| Property | Type | Description | Default |
| :--- | :--- | :--- | :--- |
| `Text` | `string` | The text to display. | "Label" |
| `Big` | `boolean` | Makes the text larger. | `false` |
| `Bold` | `boolean` | Makes the text bold. | `false` |
| `Color` | `Color3` | Sets the color of the text. | White |

**Example:**
```lua
Window:AddLabel({ Text = "Player Information", Big = true, Bold = true })
Window:AddLabel({ Text = "This script is for demonstration purposes.", Color = Color3.fromRGB(0, 255, 255) })
```

### Button
A standard clickable button that performs an action.

#### `Window:AddButton(properties)`

| Property | Type | Description |
| :--- | :--- | :--- |
| `Text` | `string` | The text displayed on the button. |
| `Callback`| `function`| The function to run when the button is clicked. |

**Example:**
```lua
Window:AddButton({
    Text = "Give Speed",
    Callback = function()
        game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = 100
    end
})
```

### Toggle
An on/off switch.

#### `Window:AddToggle(properties)`

| Property | Type | Description |
| :--- | :--- | :--- |
| `Text` | `string` | The label displayed next to the toggle. |
| `Default`| `boolean`| The initial state of the toggle (`true` for on, `false` for off). Defaults to `false`. |
| `Callback`| `function`| The function to run when the toggle's state changes. It receives the new value as an argument. |

**Example:**
```lua
Window:AddToggle({
    Text = "Infinite Jump",
    Default = false,
    Callback = function(value)
        print("Infinite Jump is now:", value)
        game.Players.LocalPlayer.Character.Humanoid:SetStateEnabled(Enum.HumanoidStateType.Jumping, not value)
    end
})
```

### Textbox
An input field for users to type text.

#### `Window:AddTextbox(properties)`

| Property | Type | Description |
| :--- | :--- | :--- |
| `Placeholder` | `string` | Faint text shown when the textbox is empty. |
| `Default` | `string` | The initial text in the textbox. |
| `ClearOnFocus`| `boolean`| If `true`, the text is cleared when the user clicks on the box. Defaults to `false`. |
| `Callback` | `function`| The function to run when the user presses Enter. It receives the entered text as an argument. |

**Returns:**
*   A `TextboxObject` with methods to interact with it:
    *   `TextboxObject:GetText()`: Returns the current text.
    *   `TextboxObject:SetText(newText)`: Sets the text in the box.

**Example:**
```lua
local NameTextbox = Window:AddTextbox({
    Placeholder = "Enter new player name...",
    Callback = function(text)
        print("User submitted the name:", text)
    end
})

-- Later in your script, you can do:
-- NameTextbox:SetText("A new default value")
```

### Slider
Allows the user to select a number within a range.

#### `Window:AddSlider(properties)`

| Property | Type | Description |
| :--- | :--- | :--- |
| `Text` | `string` | The label displayed above the slider. |
| `Min` | `number` | The minimum value of the slider. Defaults to `0`. |
| `Max` | `number` | The maximum value of the slider. Defaults to `100`. |
| `Default`| `number`| The starting value of the slider. Defaults to the minimum value. |
| `Callback`| `function`| The function to run every time the slider's value changes. It receives the new value as an argument. |

**Example:**
```lua
Window:AddSlider({
    Text = "Camera Field of View",
    Min = 70,
    Max = 120,
    Default = 80,
    Callback = function(value)
        workspace.CurrentCamera.FieldOfView = value
    end
})
```

### Divider
A horizontal line used to visually separate elements.

#### `Window:AddDivider()`
This function takes no arguments.

**Example:**
```lua
Window:AddLabel({ Text = "Section 1" })
Window:AddButton({ Text = "Button 1" })
Window:AddDivider()
Window:AddLabel({ Text = "Section 2" })
Window:AddButton({ Text = "Button 2" })
```

---

## Full Example Script

Here is a complete script that uses every feature of the library, serving as a perfect starting point.

```lua
-- ==========================================================
-- GlitchizUI v3.1 Loader
-- Loads the final version with the Dropdown included.
-- ==========================================================

local URL = "https://raw.githubusercontent.com/xGSPx/GlitchizUI/main/main"

local success, response = pcall(function()
    return game:HttpGet(URL)
end)

if success then
    local GlitchizUI = loadstring(response)()

    -- ==========================================================
    --                  UI CREATION & DEMO
    -- ==========================================================

    local Window = GlitchizUI.new({
        Title = "GlitchizUI v3.1",
        Keybind = Enum.KeyCode.RightControl, -- Press Right-Control to toggle
    })

    -- Create the 'Main' Tab
    Window:AddTab("Main")

    Window:AddLabel({ Text = "Welcome to GlitchizUI v3.1!", Big = true, Bold = true })
    Window:AddLabel({ Text = "The dropdown element has been added."})
    Window:AddDivider()
    Window:AddToggle({
        Text = "Infinite Yield (Example)", Default = false,
        Callback = function(v) print("Infinite Yield set to:", v) end
    })
    Window:AddButton({
        Text = "Print 'Hello World'",
        Callback = function() print("Hello World") end
    })

    -- Create the 'Player' Tab
    Window:AddTab("Player")
    Window:AddLabel({ Text = "Player Customization", Bold = true })
    Window:AddTextbox({
        Placeholder = "Enter custom speed...", ButtonText = "Set",
        Callback = function(text)
            local speed = tonumber(text)
            if speed and game.Players.LocalPlayer.Character and game.Players.LocalPlayer.Character:FindFirstChild("Humanoid") then
                game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = speed
                print("WalkSpeed set to:", speed)
            else
                print("Invalid speed input:", text)
            end
        end
    })
    Window:AddSlider({
        Text = "Jump Power", Min = 50, Max = 500, Default = 50,
        Callback = function(v)
            if game.Players.LocalPlayer.Character and game.Players.LocalPlayer.Character:FindFirstChild("Humanoid") then
                game.Players.LocalPlayer.Character.Humanoid.JumpPower = v
            end
        end
    })

    -- Create a 'Visuals' Tab to show the Dropdown
    Window:AddTab("Visuals")
    Window:AddLabel({ Text = "Client-Side Visuals", Bold = true })
    Window:AddSlider({
        Text = "Field of View", Min = 70, Max = 120, Default = 70,
        Callback = function(v) workspace.CurrentCamera.FieldOfView = v end
    })
    
    -- New Dropdown Demonstration
    Window:AddDropdown({
        Default = "Default Sky",
        Options = {"Default Sky", "Night Sky", "Sunset", "Cartoon"},
        Callback = function(selectedOption)
            print("Skybox option selected:", selectedOption)
            -- In a real script, you would change game.Lighting properties here
        end
    })

else
    warn("GlitchizUI Error: Failed to load library from GitHub.", response)
end
```
