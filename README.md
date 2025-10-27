Of course. A good project needs great documentation.

Here is a comprehensive README.md file. This is the standard format for project documentation on platforms like GitHub. You can copy this entire text and save it as a file named README.md in your GitHub repository, and it will automatically be displayed as the project's homepage.

GlitchizUI v2.0 - Documentation

Welcome to the official documentation for GlitchizUI v2.0. This is a modern, feature-rich, and highly customizable UI library for Roblox, designed with a stylish "glitch" aesthetic. Its API is inspired by popular libraries like Rayfield, making it intuitive and easy to learn.

This guide will walk you through the setup process and provide a detailed reference for every available UI element.

Table of Contents

Setup & Installation

Creating a Window

Adding Tabs

UI Elements (Components)

Label

Button

Toggle

Textbox

Slider

Divider

Full Example Script

Setup & Installation

GlitchizUI is designed to be loaded directly from its source code on GitHub. This means you don't need to install any files; you just run a small loader script.

Simply use the following script to load the library and create your UI.

code
Lua
download
content_copy
expand_less
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
Creating a Window

Everything starts with a Window. This is the main container that holds all of your tabs and UI elements.

GlitchizUI.new(properties)

This function creates and returns a new Window object.

Parameters:

properties (table): A table of properties to customize the window.

Property	Type	Description	Default
Title	string	The text displayed at the top of the window.	"GlitchizUI"
Size	UDim2	The size of the window in pixels.	UDim2.new(0, 550, 0, 350)
Position	UDim2	The screen position of the window.	Centered on screen

Example:

code
Lua
download
content_copy
expand_less
local Window = GlitchizUI.new({
    Title = "My Awesome UI",
    Size = UDim2.new(0, 600, 0, 450)
})
Adding Tabs

Tabs are used to organize your UI elements into different categories. You must add at least one tab before you can add any elements.

Window:AddTab(name)

Adds a new tab to the window and selects it, so any subsequent elements are added to this tab.

Parameters:

name (string): The name of the tab to be displayed.

Example:

code
Lua
download
content_copy
expand_less
Window:AddTab("Main")
-- All elements added now will go into the "Main" tab

Window:AddTab("Settings")
-- All elements added now will go into the "Settings" tab
UI Elements (Components)

These are the core interactive components of the library.

Label

Displays text.

Window:AddLabel(properties)
Property	Type	Description	Default
Text	string	The text to display.	"Label"
Big	boolean	Makes the text larger.	false
Bold	boolean	Makes the text bold.	false
Color	Color3	Sets the color of the text.	White

Example:

code
Lua
download
content_copy
expand_less
Window:AddLabel({ Text = "Player Information", Big = true, Bold = true })
Window:AddLabel({ Text = "This script is for demonstration purposes.", Color = Color3.fromRGB(0, 255, 255) })
Button

A standard clickable button that performs an action.

Window:AddButton(properties)
Property	Type	Description
Text	string	The text displayed on the button.
Callback	function	The function to run when the button is clicked.

Example:

code
Lua
download
content_copy
expand_less
Window:AddButton({
    Text = "Give Speed",
    Callback = function()
        game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = 100
    end
})
Toggle

An on/off switch.

Window:AddToggle(properties)
Property	Type	Description
Text	string	The label displayed next to the toggle.
Default	boolean	The initial state of the toggle (true for on, false for off). Defaults to false.
Callback	function	The function to run when the toggle's state changes. It receives the new value as an argument.

Example:

code
Lua
download
content_copy
expand_less
Window:AddToggle({
    Text = "Infinite Jump",
    Default = false,
    Callback = function(value)
        print("Infinite Jump is now:", value)
        game.Players.LocalPlayer.Character.Humanoid:SetStateEnabled(Enum.HumanoidStateType.Jumping, not value)
    end
})
Textbox

An input field for users to type text.

Window:AddTextbox(properties)
Property	Type	Description
Placeholder	string	Faint text shown when the textbox is empty.
Default	string	The initial text in the textbox.
ClearOnFocus	boolean	If true, the text is cleared when the user clicks on the box. Defaults to false.
Callback	function	The function to run when the user presses Enter. It receives the entered text as an argument.

Returns:

A TextboxObject with methods to interact with it:

TextboxObject:GetText(): Returns the current text.

TextboxObject:SetText(newText): Sets the text in the box.

Example:

code
Lua
download
content_copy
expand_less
local NameTextbox = Window:AddTextbox({
    Placeholder = "Enter new player name...",
    Callback = function(text)
        print("User submitted the name:", text)
    end
})

-- Later in your script, you can do:
-- NameTextbox:SetText("A new default value")
Slider

Allows the user to select a number within a range.

Window:AddSlider(properties)
Property	Type	Description
Text	string	The label displayed above the slider.
Min	number	The minimum value of the slider. Defaults to 0.
Max	number	The maximum value of the slider. Defaults to 100.
Default	number	The starting value of the slider. Defaults to the minimum value.
Callback	function	The function to run every time the slider's value changes. It receives the new value as an argument.

Example:

code
Lua
download
content_copy
expand_less
Window:AddSlider({
    Text = "Camera Field of View",
    Min = 70,
    Max = 120,
    Default = 80,
    Callback = function(value)
        workspace.CurrentCamera.FieldOfView = value
    end
})
Divider

A horizontal line used to visually separate elements.

Window:AddDivider()

This function takes no arguments.

Example:

code
Lua
download
content_copy
expand_less
Window:AddLabel({ Text = "Section 1" })
Window:AddButton({ Text = "Button 1" })
Window:AddDivider()
Window:AddLabel({ Text = "Section 2" })
Window:AddButton({ Text = "Button 2" })
Full Example Script

Here is a complete script that uses every feature of the library, serving as a perfect starting point.

code
Lua
download
content_copy
expand_less
local URL = "https://raw.githubusercontent.com/xGSPx/GlitchizUI/main/main"

local success, response = pcall(function() return game:HttpGet(URL) end)

if success then
    local GlitchizUI = loadstring(response)()

    -- Create the main window
    local Window = GlitchizUI.new({
        Title = "GlitchizUI Full Demo",
        Size = UDim2.new(0, 520, 0, 400),
    })

    -- Create a 'Main' Tab
    Window:AddTab("Player")
    Window:AddLabel({ Text = "Player Modifications", Big = true, Bold = true })
    Window:AddButton({
        Text = "Reset Character",
        Callback = function()
            game.Players.LocalPlayer.Character.Humanoid.Health = 0
        end
    })
    Window:AddDivider()
    Window:AddSlider({
        Text = "WalkSpeed",
        Min = 16, Max = 200, Default = 16,
        Callback = function(v)
            game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = v
        end
    })
    Window:AddToggle({
        Text = "Fly Mode (Placeholder)",
        Default = false,
        Callback = function(v)
            print("Fly mode set to:", v)
        end
    })

    -- Create a 'Settings' Tab
    Window:AddTab("Settings")
    Window:AddLabel({ Text = "UI Settings", Big = true, Bold = true })
    local NameTextbox = Window:AddTextbox({
        Placeholder = "Change UI Title...",
        Callback = function(text)
            -- This is an example of how you might interact with the UI itself.
            -- Note: There is no built-in function to change the title after creation,
            -- this is just for demonstration.
            print("New title requested:", text)
        end
    })
    Window:AddLabel({ Text = "This is a demonstration of all features.", Color = Color3.fromRGB(0, 240, 255) })

else
    warn("GlitchizUI Error:", response)
end
