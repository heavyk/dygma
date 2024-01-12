# bazecor
## basic ideas
- each panel can be loaded anywhere, and if it's a popup, it will have an [X] btn, and after changes have been made, a [:rotate-left:] btn to undo the change is added to the left of the [X]; then, upon clicking the [:rotate-left:] undo btn, it will change to [:rotate-right:] redo btn)
	- as an example, the (KE) will be loaded below the (OSK), but can also be loaded in a popup windows
- each interface is another layer (popup on popup action), because for example, when clicking on a key in the (OSK), it'll popup the (KE), upon which I could select a macro, then press [edit] which brings up the (ME). changes automatically save, so there's no need to worry how many UI layers high the user gets.
- one main experience panel (no sidebar) which, for example:
	- (IUE) which shows/allows for connectivity
		- if not connected via RF/wire, show alert saying it's necessary, else automatically connect.
		- if first time, or no keyboard is found (NUE) "get setup"
		- once connected, (LE) is shown always
		- [settings] brings up (SP) 
		- [help] brings up (HP)
- the main experience panel can only be changed by user action (which ensures everything is saved before anything happens)
- each popup panel has [undo] [redo] [X] to the left. [undo] and [redo] only show up when there's something to undo/redo (if nothing to redo, there remains the space)
- only non-interactive items like text/images get scrollbars.
	- all interactive elements should be visible (ie, for long forms, split the form into logical chunks and make it easy to go from one chunk to the next (swipe/arrows left/right))
- all undo/redo actions *highlight* in some way the setting that was changed (sroll to item in list)
	- highlight probably by putting a border around the setting/part that changed, which fades out in .5-1s or so.
	- just so visually I can easily see what changed
- buttons should not move around after an action
	- this is hard for the brain to process what just happened
	- for example, after pressing [undo], it should not move to the left because the [redo] btn was unhidden.
- no greyed out or disabled buttons.
	- this is extra work for the brain to process: first it looks like an option, then it doesn't look like an option.
	- just hide the button (leaving the space where it was blank)

## interface walkthrogh
### common interface
located at the bottom, or some place out of the way in the main user experience
- select keyboard (only if there is more than one connected)
- [settings](SP)
- battery levels
- [action panel](AP)
- [layout analyzer](LA) (if turned on)

### initial user experience (IUE)
- if not connected via RF/wire, show alert saying it's necessary, else automatically connect.
- if first time, or no keyboard is found [setup] brings up (NUE) (maybe text like "get setup/started (now)")

### new user experience (NUE)
- first show a welcome screen with an option to set dark/light mode and adjust font settings, with an additional link to "getting started" which will have all of the setup and install directions for the user
- show if the keyboard is connected, and if not, have a btn which will show the install steps from the nue.

### on-screen kbd (OSK)
- show current layout + colors (like how it is already)

### layout editor (LE)
- when clicking on a key, it should pop up a window (KE) that is not fullscreen (like maybe 50-70% wide), and at the top should be an [X] btn which is the same as presssing "diacard changes".
- all changes should automatically be saved, *always* with an option to undo (probably in code, the saving happens with a slight 1-2s delay, or when the window is switched/closed)
- most people will only have one kbd, so no need to show which kbd selector, untill there has been more than one keyboard connected.
- ability to save/load entire layout
	- all of the layouts submitted to [keyboard layout analyzer](https://patorjk.com/keyboard-layout-analyzer/), can be loaded (for example, I use workman and want to quickly load that configuration).
	- ability to browse others layouts and download/load any {layout} I want to try.
- ability to "move" (by dragging) the key from one location to another, swapping the two keys

### layout analyzer (LA)
[keyboard layout analyzer](https://patorjk.com/keyboard-layout-analyzer/) [[src](https://github.com/patorjk/keyboard-layout-analyzer)] is a website that allows the user to analyse their layout compared to text. it's got a lot of good ideas on how to consider analyse the keyboard layout for ergonomic reasons. the distances can be percisely calculated based on the kbd model the user is using.
- ability to turn enable/disable the real-time analyser, which essentially logs keystrokes as {action}s
	- perhaps configurale, like for example when I load DOTA or something, or during certain times of day, or maybe *not* in password boxes
	- this feature could potentially lead to a security-related scandal, which is good for advertising
- ability to then generate distance and heatmaps for keys pressed over various periods of history
- ability to suggest improvements to the keys (ie, swap these keys to decrease lateral/vertical movement)
- statistics showing distance traveled over a period of time (by replaying {actions}) key usage, etc. (many things possible)

### key editor (KE)
- when panel pops up, it should have the key/super/macro selected that it already is.
- no need the modifiers panel; simply allow the modifiers on the kbd screen to be toggleable, and if only one one modifier key is toggled, then that is it's "key" (ex. if I press 'k' and then press 'shift', then that's "shift+k" for the "selected value", and then if I now press 'l', then shift stays lit and "selected value" becomes "shift+l")
- below the keyboard layout panel should be the (SE) panel, which by default will have the tap box highlighted (perhaps with a border and different background color). as each mode is selected (1t,1t1h,2t,2t2h,etc), it will change the highlighted keys on the on-screen kbd accordingly (and for macros and other types, show the appropriate screen: for macros a simplified view with an edit button which loads the (ME) above).

### superkeys editor (SE)

### macro editor (ME)

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
- close button (all changes are automatically saved)

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
