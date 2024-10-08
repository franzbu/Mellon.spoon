# Mellon

Mellon has been developed because the window managers I have tried on macOS left me wanting. Mellon has been inspired by Aerospace, Moom, BetterTouchTool, and others. Mellon has helped me to simplify my workflow and save time along the way; may it do the same for you.

As has been hinted at, Mellon helps you managing your windows and spaces. Due to limitations of Apple's Spaces, Mellon has its own implementation of Spaces; they will be referred to as mSpaces.

mSpaces are fast and flexible: moving a window to and switching between mSpaces is instantaneous, as it is a matter of pressing a keyboard shortcut or flicking your pointing device. Additional features such as 'sticky windows' provide additional options. 'Sticky windows' means that windows can be present on more than one mSpace at the same time; each one is a full-featured reference, i.e., references can have different sizes and positions on different mSpaces. More about this feature later.

Windows and mSpaces can be handled using your keyboard only; however, similar to other workflows, at times it is simpler and faster to use keyboard and pointing device together, and Mellon allows that whereever it has proved beneficial. 

Mellon is easiest understood on the go, so let us get started with its installation.


## Installation

Mellon requires [Hammerspoon](https://www.hammerspoon.org/), so just go ahead with its installation.

To install Mellon, after downloading and unzipping it, move the folder to ~/.hammerspoon/Spoons and make sure the name of the folder is 'Mellon.spoon'. 

Alternatively, run the following command in a terminal window:

```terminal

mkdir -p ~/.hammerspoon/Spoons && git clone https://github.com/franzbu/Mellon.spoon.git ~/.hammerspoon/Spoons/Mellon.spoon

```

## Usage

Once you've installed Mellon, add the following lines to your `~/.hammerspoon/init.lua` file:

```lua
local Mellon = hs.loadSpoon('Mellon')

Mellon:new({

  -- mSpaces:
  mSpaces = { '1', '2', '3', 'E', 'T' }, -- default { '1', '2', '3' }
  startmSpace = 'E', -- default 2

  modifier1 = { 'alt' }, -- default: { 'alt' }
  modifier2 = { 'ctrl' }, -- default: { 'ctrl' }

})

```

Restart Hammerspoon and you are ready to go. You might additionally be interested in adjusting the amount and names of your 'mSpaces' and the default mSpace, see above. 


## mSpaces

The default setup uses 'modifier1' and the keys 'a', 's', 'd', 'f', 'q', and 'w' to switch to the mSpace on the left/right ('a', 's'), move window to the mSpace on the left/right ('d', 'f'), move window to the mSpace on the left/right and switch there ('q', 'w'). 

Now, by pressing 'modifier1' and 'q', for instance, you move the active window from your current mSpace to the adjacent mSpace on the left and switch there. For moving the window without switching or switching without moving any window use the other keyboard shortcuts.

In case you would like to use another modifier key for dealing with mSpaces while keeping the original 'modifier1' key (which is used for various other tasks, as you will see in a minute) and/or change additional keys, add the following lines with the desired adjustments to your 'init.lua'; the example below shows my setup with CapsLock set up as hyper key with [Karabiner Elements]([https://www.hammerspoon.org/](https://karabiner-elements.pqrs.org/)):


```lua
  ...
  modifierSwitchMS = { 'shift', 'ctrl', 'alt', 'cmd' }, -- hyper key
  -- 1, 2: switch to mSpace left/right ('a', 's')
  -- 3, 4: move window to mSpace left/right ('d', 'f')
  -- 5, 6: move window to mSpace left/right and switch there ('q', 'w')
  modifierSwitchMSKeys = {'a', 's', 'd', 'f', 'q', 'w'}, 
  ...
```

### Move Windows Directly to Any mSpace 

So far you have been shown how to move windows to the adjacent mSpace. In case you would like to have a keyboard shortcut for directly moving windows to any mSpace, add the following line to your 'init.lua' and change it to represent your desired modifier key(s):

```lua
  ...
  modifierMoveWinMSpace = { 'alt', 'shift' }, -- default: nil
  ...
```

## mSpaces Have Further Potential

However, this has just been the beginning. See each mSpace represents your windows rather than just some general space where the windows are placed, for instance, you can have two mSpaces with the same windows in different sizes and positions. Or you can have the same Notes, Calendar, Finder or Safari window on two, more, or even all your mSpaces.
  
To create such representations of windows, press your 'ctrl' and 'shift' keys simultaneously and additionally press the key corresponding to the mSpace you would like to create a reference of the currently active window on, for instance, '3'. In case you would like to adjust the modifier keys, add the following line to your 'init.lua':

```lua
  ...
  modifierReference = { 'ctrl', 'shift' }, -- default: { 'ctrl', 'shift' }
  ...
```
To delete a reference, press 'modifierReference' and '0'. In case you are 'de-referencing' the last window on your mSpaces, the window gets minimized.


## Switching Between Windows

You can use macOS's integrated window switcher (cmd-tab) or any third party switcher such as [AltTab]([[https://www.hammerspoon.org/](https://karabiner-elements.pqrs.org/](https://alt-tab-macos.netlify.app/))) for switching between all your windows. Also for switching between the different windows of one application you can use Apple's integrated switcher or third party alternatives.

However, since mSpaces provide additional features, further possibilities for switching are available, namely switching between the windows on the current mSpace and switching between references of windows ('sticky windows').

### Switching between the Windows on an mSpace

For switching between all windows on your current mSpace, press 'modifier1' and 'tab', and for switching in reverse order accordingly press 'shift'. Add the following lines to 'init.lua' in case you prefer different keyboard shortcuts:


```lua
  ...
  -- keyboard shortcuts for switching between windows on one mSpace...
  -- ... and between references of one and the same window on different mSpaces
  modifierSwitchWin = { 'alt' }, -- default: modifier1
  modifierSwitchWinKeys = { 'tab', 'escape' }, -- default: { 'tab', 'escape' }
  ...
```

### Switching between References of Windows

For switching between the references of a window ('sticky windows'), press 'modifier1' and 'escape'. In case you would like to change that, change the second element in the table 'modifierSwitchWinKeys' (see directly above).


## Moving and Resizing of Windows:

With Mellon you can automatically resize and position the windows on your mSpaces on a dynamically changing grid size. Let us get started with manual moving and resizing, though:


### Manual Moving and Positioning

To move a window, hold your 'modifier1' or 'modifier2' key(s) down, position your cursor in any area within the window, click the left mouse button, and drag the window. If a window is dragged up to 10 percent of its width (left and right borders of screen) or its height (bottom border) outside the screen borders, it will automatically snap back within the borders of the screen. If the window is dragged beyond the 10-percent-margin, things are getting interesting because then window management with automatic resizing and positioning comes into play.

### Automatic Resizing and Positioning - Mouse and/or Trackpad

For automatic resizing and positioning of a window, you simply move between 10 and 80 percent of the window beyond the left, right, or bottom borders of your screen using your left mouse button. 

As long as windows are resized - or moved within the borders of the screen -, it makes no difference whether you use your 'modifier1' or 'modifier2' keys. However, once a window is moved beyond the screen borders, different positioning and resizing scenarios are called into action; they are as follows:

* modifier1: 
  * If windows are moved beyond the left (right) borders of the screen: imagine your screen border divided into three equally long sections: if the cursor crosses the screen border in the middle third of the border, the window snaps into the left (right) half of the screen. Crossing the screen border in the upper and lower thirds, the window snaps into the respective quarters of the screen.
  * If windows are moved beyond the bottom border of the screen: imagine your bottom screen border divided into three equally long sections: if the cursor crosses the screen border in the middle third of the bottom border, the window snaps into full screen. Crossing the screen border in the left or right thirds, the window snaps into the respective halfs of the screen.

* modifier2: 
  * The difference to 'modifier1' is that your screen has a 3x3 grid. This means that windows snap into the left third of the 3x3 grid when dragged beyond the left screen border and into the right third when dragged beyond the right screen border. If 'modifier2' is released before the left mouse button, the window will snap into the middle.
 
* The moment dragging of a window starts, indicators will guide you.

All this is been implemented with the goal of being as intuitive as possible; therefore, you will be able to train your muscle memory in no time. Promise.


### Automatic Resizing and Positioning - Keyboard

#### 2x2 Grid

To resize and move the active window into a 2x2 grid position, use your 'modifier1' and number keys 4-9. In case you would like to use a different modifier key, add the following line to your 'init.lua':


```lua
  ...
  modifierSnap2 = { 'ctrl' }, -- default: modifier2
  modifierSnap2Keys = {'4', '5', '6', '7', '8', '9', '0'},
  ...
```

Adjust the keys to your liking; in the order of the entries in 'modifierSnap2Keys', windows are positioned as follows:
- 1: left half of screen (4)
- 2: right half of screen (5)
- 3: top left quarter of screen (6)
- 4: bottom left quarter of screen (7)
- 5: top right quarter of screen (8)
- 6: bottom right quarter of screen (9)
- 0: whole screen (0)

#### 3x3 Grid

Add the following lines to your 'init.lua' (in case this has not become clear yet: if you do not add these lines to your 'init.lua', the default options automatically take over):

```lua
  ...
  modifierSnap3 = { 'alt' }, -- default: modifier2
  modifierSnap3Keys = {'1', '2', '3', '4', '5', '6', '7', '8', '9', '0', 'o', 'p'},
  ...
```

Windows are positioned as follows:
- 1: left third of screen (1)
- 2: middle third of screen (2)
- 3: right third of screen (3)
- 4: top left ninth of screen (4)
- 5: middle left night of screen (5)
- 6: bottom left ninth of screen (6)
- ...

##### 3x3 Grid - Double (and Quadruple) Sizes

With the following keyboard shortcuts, you can create windows that take up more cells on the 3x3 grid, which contains 9 cells altogether:

```lua
  ...
  modifierSnap3_2 = { 'ctrl', 'alt', 'shift' }, -- default: modifier1 + modifier2
  modifierSnap3_2Keys = {'1', '2', '3', '4', '5', '6', '7', '8', '9', '0', 'o', 'p'},
  ...
```

Windows are positioned as follows (descriptions might prove tricky; in that case simply try it out):
- 1: left two thirds of screen: 3 cells (1)
- 2: right two thirds of screen: 3 cells (2)
- 3: left third, upper two cells (3)
- 4: left third, lower two cells (4)
- 5: middle third, upper two cells (5)
- 6: middle third, lower two cells (6)
- 7: right third, upper two cells (7)
- 8: right third, lower two cells (8)
- 9: top left and middle thirds: 4 cells (9)
- 10: bottom left and middle thirds: 4 cells (0)
- 11: top middle and right thirds: 4 cells (o)
- 12: bottom middle and right thirds: 4 cells (p)


## Additional Information

### Change Size, Color, and Opacity of Grid Indicators

In case you would like to change the size, color and/or opacity of the grid indicators, add the following line to your 'init.lua'. The values, in this order, stand for: width, red, green, blue, opacity. Apart from the width, values between 0 and 1 are possible:

```lua
  ...
  -- change grid indicators:
    gridIndicator = { 20, 1, 0, 0, 0.5 }, -- default: { 20, 1, 0, 0, 0.5 }, 

  ...
```

### After Restart

- If you restart Mellon, the windows on the mSpace as the were before the restart will remain unchanged, while the windows that were placed on other mSpaces before the restart will also be present on the current mSpace. In other words, if you plan to stop using Mellon, either move all windows to one mSpace first, or restart Mellon one last time.

- A backup feature restoring windows too their original mSpaces are on the todo list.


## Experimental Features

### Manual Resizing

Similar to manual moving, manual resizing of windows can be initiated by positioning the cursor in virtually any area of the window. Be aware, though, that windows of certain applications, such as LosslessCut or Kdenlive, can behave in a stuttering and sluggish way when being resized. That being said, resizing works well with the usual suspects such as Safari, Google Chrome, Finder, and so on.

In order to enable manual resizing, add the following option to your 'init.lua':

```lua
  ...
  -- enable resizing:
  resize = true, -- default: false
  ...
```

To manually resize a window, hold your 'modifier1' or 'modifier2' key(s) down, then click the right mouse button in any part of the window and drag the window.

To have the additional possibility of precisely resizing windows horizontally-only and vertically-only, 30 percent of the window (15 precent left and right of the middle of each border) is reserved for horizontal-only and vertical-only resizing. The size of this area can be adjusted; for more information see below.

<img src="https://github.com/franzbu/WinHammer.spoon/blob/main/doc/demo1.gif" />

At the center of the window there is an erea (M) where you can also move the window by pressing the right mouse button. 

<img src="https://github.com/franzbu/WinHammer.spoon/blob/main/doc/resizing.png" width="200">


#### Manual Resizing of Windows - Margin

You can change the size of the area of the window where the vertical-only and horizontal-only resizing applies by adjusting the option 'margin'. The standard value is 0.3, which corresponds to 30 percent. Changing it to 0 results in deactivating this options, changing it to 1 results in deactivating resizing.

```lua
  ...
  -- adjust the size of the area with vertical-only and horizontal-only resizing:
  margin = 0.2, -- default: 0.3
  ...
})
```



