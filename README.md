# sfaimjank
Janky workaround to allow third to first person aiming in Starfield via AutoHotKey script and Hotkeys mod until somebody updates https://www.nexusmods.com/starfield/mods/1302.

# Hotkeys Mod
Step 1: Install Starfield Hotkeys mod: https://www.nexusmods.com/starfield/mods/1578

Step 2: In Hotkeys.ini file add these keybinds to the [Hotkeys] section:
* NumPad1=cgf "Game.ForceFirstPerson"
* NumPad2=cgf "Game.ForceThirdPerson"

# AutoHotKey
Step 1: Install AutoHotKey and run (or compile to exe) this script (note: this was written for AHK v1.x - AHK v2.x has syntax changes and won't run/compile this)
```
#SingleInstance Force
#Persistent
#UseHook
SetKeyDelay ,, 50
SetTitleMatchMode, 2

enableAimToggle := 1

#IfWinActive ahk_class Starfield

; Change 'q' to whatever keybind you would like to use to toggle this script on/off in-game
*q::
{
	enableAimToggle := !enableAimToggle
	;Tooltip, % enableAimToggle
	Return
}

~*RButton::
{
	if enableAimToggle = 1
	{
		Send {Numpad1}
		KeyWait, RButton
		Send {Numpad2}
	}
	Return
}

#IfWinActive
Return
```

# Usage
Step 1: Press Q to toggle the script on/off in game. Toggle this off when you are driving or piloting to avoid issues with swapping to third/first person while firing weapons.

Step 2: When toggled on, hold right mouse button to ADS - AutoHotKey will send "numpad1" & "numpad2" keys on mouse down/mouse up which will be intercepted by Hotkeys mod and call Game.ForceFirstPerson or Game.ForceThirdPerson accordingly.
