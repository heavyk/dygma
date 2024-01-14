# bazecor
## basic ideas
- each panel can be loaded anywhere, and if it's a popup, it will have an [X] btn, and after changes have been made, a [:rotate-left:] btn to undo the change is added to the left of the [X]; then, upon clicking the [:rotate-left:] undo btn, it will change to [:rotate-right:] redo btn)
	- as an example, the (KE) will be loaded below the (OSK), but can also be loaded in a popup windows
- each btn either pushes/pops a layer on the stack, or modifies the active layer
	- something like a scrollbar is for y-axis: this is z-axis ability to show below layers
	- if there is [redo] {action} states, automatically create a branch
	- since changes automatically save, closing the layer isn't distructive because [undo] (ctrl+z) opens the layer back up where it was.
	- for example, when clicking on a key in the (OSK), it'll popup the (KE), upon which I could select a macro, then press [edit] which brings up the (ME).
- one main experience panel (no sidebar, just (CI)) which, can exist in different places in each experience
	- idea is to make it a full-screen experience, thereby focusing the user
- the main experience panel can only be changed by user action (which ensures everything is saved before anything happens)
- each popup panel has [undo] [redo] [X] to the left.
	- [undo] and [redo] only show up when there's something to undo/redo (if nothing to redo, the space remains there)
	- [X] unconditionally closes the panel. if I reopen the panel, the [undo] [redo] btn is in same state (corresponding to my current {action} position)
- only non-interactive items like text/images get scrollbars.
	- all interactive elements (not inside of a list) should be visible (ie, for long forms, split the form into logical chunks and make it easy to go from one chunk to the next (swipe/arrows left/right))
- all undo/redo actions *highlight* in some way the setting that was changed (sroll to item in list or whatever)
	- highlight probably by putting a color border/background around the setting/part that changed, which fades out in .5-1s or so.
	- just so visually I can easily see what changed
- btns should not move around after an action
	- this is hard for the brain to process what just happened
	- for example, after pressing [undo], it should not move to the left because the [redo] btn was unhidden.
- no greyed out or disabled btns.
	- this is extra work for the brain to process: first it looks like an option, then it doesn't look like an option.
	- instead of disabling, just hide the btn (causing no reflow, leaving the space where it was blank)

## interface walkthrogh
### common experience interface (CEI)
located at the bottom, or some place out of the way inside each main user experience
- select keyboard (only if there is more than one connected)
- [settings](SP)
- battery levels
- [action panel](AP) (perhaps displayed between [undo]/[redo])
- [layout analyzer](LA) (if turned on)

### common layer interface (CLI)
aligned usually to the right/left side of the top/bottom part of popup/layer (depending on win/mac/pref)
- all layers are fullscreen panels
- [X/] [undo/redo/] [redo/undo/] [X/]
- esc closes layer
- (maybe) right-click on non-interactive area closes layer (nav back?)

### common panel interface (CPI)
no resizing or changing at the moment, but *maybe* the option to edit the open panel (maybe w/ a hover border) and the ability to move it around within the layer/popup
- [X/] [undo/redo/] [redo/undo/] [X/]
- positions could be editble:
	- allows for custom dashboards (for stats, etc.)
	- positions as absolute/relative values to another panel/screen edge (ie, `screen.w + 40` or `panels.macro_editor.x - 20`)
- this option requires more thought:
	- quite an interesting idea considering editing stats or adding dashboards.
	- disability options like text size changing or panel reading (cause custom kbds for the disabled is also a potential market)

### initial user experience (IUE)
- if not connected via RF/wire, show alert saying it's necessary, else automatically connect.
- if first time, or no keyboard is found [setup] brings up (NUE) (maybe text like "get setup/started (now)")
- most people will only have one kbd, so no need to show which kbd selector, untill there has been more than one keyboard connected.

### new user experience (NUE)
- first show a welcome screen with an option to set dark/light mode and adjust font settings, with an additional link to "getting started" which will have all of the setup and install directions for the user
- show if the keyboard is connected, and if not, have a btn which will show the install steps from the nue.

### on-screen kbd (OSK)
- show current layout + colors (like how it is already)

### layout editor (LE)
- when clicking on a key, it should pop up a window (KE) that is not fullscreen (like maybe 50-70% wide), and at the top should be an [X] btn which is the same as presssing "diacard changes".
- all changes should automatically be saved, *always* with an option to undo (probably in code, the saving happens with a slight 1-2s delay, or when the window is switched/closed)
- when selecting color mode:
	- when I select a key, it should highlight the pallete color that it's currently set to.
	- it'd be nice to have a "paintbrush" and "erase" tool so I can just swipe all of the keys/underglows that I want with that color
- ability to save/load entire layout
	- all of the layouts submitted to [keyboard layout analyzer](https://patorjk.com/keyboard-layout-analyzer/), can be loaded (for example, I use workman and want to quickly load that configuration).
	- ability to browse others layouts and download/load any {layout} I want to try.
- ability to "move" (by dragging) the key from one location to another, swapping the two keys
- right+click should close the (KE) so that my workflow to reassign a bunch of keys is:
	1. click on key to open (KE)
	2. select new key in (KE)
	3. right-click or esc to close (KE), goto #1

### layout analyzer (LA)
[keyboard layout analyzer](https://patorjk.com/keyboard-layout-analyzer/) [[src](https://github.com/patorjk/keyboard-layout-analyzer)] is a website that allows the user to analyse their layout compared to text. it's got a lot of good ideas on how to consider analyse the keyboard layout for ergonomic reasons. the distances can be percisely calculated based on the kbd model the user is using.
- ability to turn enable/disable the real-time analyser, which essentially logs keystrokes as {action}s
	- perhaps configurale, like for example when I load DOTA or something, or during certain times of day, or maybe *not* in password boxes
	- this feature could potentially lead to a security-related scandal, which is good for publicity
- ability to then generate distance and heatmaps for keys pressed over various periods of history
- ability to suggest improvements to the keys (ie, swap these keys to decrease lateral/vertical movement)
- statistics showing distance traveled over a period of time (by replaying {actions}) key usage, etc. (many things possible)
- show common repeteated actions
- select events and convert into a macro

### key editor (KE)
- when panel pops up, it should have the key/super/macro selected that it already is.
- should show the color of the key
- no need the modifiers panel; simply allow the modifiers on the kbd screen to be toggleable, and if only one one modifier key is toggled, then that is it's "key" (ex. if I press 'k' and then press 'shift', then that's "shift+k" for the "selected value", and then if I now press 'l', then shift stays lit and "selected value" becomes "shift+l")
- below the keyboard layout panel should be the (SE) panel, which by default will have the tap box highlighted (perhaps with a border and different background color). as each mode is selected (1t,1t1h,2t,2t2h,etc), it will change the highlighted keys on the on-screen kbd accordingly (and for macros and other types, show the appropriate screen: for macros a simplified view with an edit btn which loads the (ME) above).

### superkeys editor (SE)
- (maybe) if adding a plain key, the hold should by added by default as well
	- ex. I put dominique's super tab demo, but it made alt+tab inconsistent: I had to put tab on both tap and hold and shift+tab on 2tap and 2tap&hold for alt+tab to work properly again

### macro editor (ME)
- ability to play the macro (test it)
- should look more like a timeline than a list of events
	- in code, it's a sequence of events, but a timeline is more intuitive for 
- easy way to delete an item in the sequence
	- perhaps below the timeline there is a trash area that appears, so I only nned to drag it downward to delete it
- sequyential press+release events should be grouped together so they can be seen as text (ie, ["Dygma"] not [d+shift][y][g][m][a])
	- the interval between keystrokes can be configured (or random within a range)
- double click in empty space should add an event
- pause/wait events can be added
	- it'd be cool to have events that wait to receive an input (and accordingly, take a different branch)
- preview macro
	- play back the sequence visually (each keypress popping up) in accordance with timeline (for games and non-text producing macros)
	- play back the sequence in text editor (for writers/programmers)

### LED editor (LE)
- ability to see the different LED settings
	- these are modifiers to the layer colors, like the rainbow gradient in default 2nd LED effect
	- +add/remove settings and assign to layers/events
	- (needs more thought because I know the layers have key colors already)
- the gradient effects are cool, cause they're like kbd-wide lighting (not individual keys), so it'd be cool to show a shadow of the kbd, w/ point light sources, and a keyframe editor so I can change the position of the point lights and their color
	- tween settings between keyframes so, prolly a simple bezier curve with 2-3 controls to change transition shape
	- also ability to integrate individual key colors with the background effect.
- eventually it'd be cool to have event-driven responces, like play an effect when a key is pressed or a layer is changed, or a js rpc function is called
	- for example the game says the powerup is fully charged, so pulse the bg color
	- or, server is done doing something (or any other *-priority notification), the event can be activated by rpc
	- or when I press a key, I want the key to "splash" out in a radial effect like ripples on a pond (dimming the farther away from the keypress it goes)

### tryout panel (TP)
- textbox or something that captures input
- all events shown in a list so I can see what events the kbd is sending the computer
	- select events and convert into macro

### settings panel (SP)

### actions panel (AP)
this panel is just a list of actions where I can visually see what changes I've made to my layout. I often want the ability
- shows a list of actions (essentially the undo/redo buffer) that have been performed since the program start
	- I often can't remember what I just did, so I want to be able to see and potentially go back to change something
- ability to save a state (like git tag), which which allows me to load that state in the future
	- I can switch easily between states to test out which one I like better
	- I can assign to load that state/tag with the press of a key/button (or js rpc)
- this panel has a lot of potential to it
	- user actions can be seen as a sequence:
		- I can move the state of the keyboard to any position in the sequence
		- undoing back to a previous state, changing a thing, then redoing, creates a new branch
	- which allows for a lot of cool ideas 
	- great parts of this interface can be shared with the (ME)
		- swapping positions of items

### action sequence {actions}
- when action list is saved, actions are stored on disk in chains, something like git.
	- {layout} is the hash of the layout
		- these are just the layout output into some format (JSON encoded?).
		- only the initial state is necessary, as all future states can be calculated by replaying the actions
		- this serves as the base of the branch
	- {action} is a hash of the {layout} + action value + previous {action}
		- {action} value can be the bazecor action
			- one per kbd
			- doubles as the undo/redo buffer
			- replaying action sequence from initial {layout} always calculates to another {layout}
		- {action} value can be the data/keycode sent to the HID
			- replaying action sequence on {layout} preoduces a {macro}
		- {action} value can be anything, really
	- {layout} hashes will be used to label good/backup states for the kbd
	- {layout} and {action} hashes will be used to share with others
	- {macro} is essentially the same as {action} and designed for easy sharing

### buttons/actions
#### [X]
- close the layer (all changes are automatically saved)

#### [undo]
- :rotate-left: icon.
- usually appears next to [X] when [X] is left-most btn.
- usually appears to the right of [redo]
- when pressed, it will show the [redo] btn and highlight what changed

#### [redo]
- :rotate-right: icon
- usually appears next to [X] when [X] is right-most btn.
- usually appears to the left of [undo]
- when pressed, it will hide itself if at top of action sequence
