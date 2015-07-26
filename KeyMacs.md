KeyMacs

<b>KeyMacs plugin for CodeBlocks IDE</b>

KeyMacs (or Keyboard Macros) plugin enables Recording, Playback, and editing of keystroke macros.


<b>Contents</b>

  * 1 What is KeyMacs
  * 2 Recording and playback
  * 3 Named Key Symbols
  * 4 Special keys
  * 5 Quirks & restrictions.
  * 6 How do I install it?
  * 7 KeySym definitions
  * 8 Example KeyMacs

<b>What is KeyMacs</b>

KeyMacs is a Code::Blocks plugin providing the user an ability to group sequences of keystokes as a macro (KeyMac). The KeyMac can be executed by either the main Plugin menu, a menu command key, or the context menu.

The KeyMac "{END}{ENTER}//{TAB 2}", for example, will move the cursor to the end of the current line, start a new line, enter the C++ comment sequence and two tabs.

KeyMacs can be created in the KeyMac editor or by way of the "Record Macro" menu. The editor can be accessed via MainMenu => Plugins => KeyMacs => EditMacros.

![http://lh3.ggpht.com/_c-XuBU8YTRg/SddRrmO11-I/AAAAAAAAAHs/A_nPNtR9uuA/keymacs102.png&nonsense=something_that_ends_with.png](http://lh3.ggpht.com/_c-XuBU8YTRg/SddRrmO11-I/AAAAAAAAAHs/A_nPNtR9uuA/keymacs102.png&nonsense=something_that_ends_with.png)
<br />Image:KeyMacs102.PNG

Within the editor, click the New button. A new empty "Untitled" macro is created. Click on "Untitled" and rename it, for example, MyMac. Hit enter to confirm the rename.

> {END}{ENTER}//{TAB 2}

Enter the above keymac into the right hand text window . Click within the "Menued Macro" check box to cause KeyMacs to add MyMac as an entry on the Pugins=>KeyMacs=>submenu and the CodeBlocks editor context menu.

![http://lh5.ggpht.com/_c-XuBU8YTRg/SddRr2eGngI/AAAAAAAAAH0/kDHcPkdgXmM/keymacs103.png&nonsense=something_that_ends_with.png](http://lh5.ggpht.com/_c-XuBU8YTRg/SddRr2eGngI/AAAAAAAAAH0/kDHcPkdgXmM/keymacs103.png&nonsense=something_that_ends_with.png)
<br />Image:KeyMacs103.PNG

Within the Command Key edit box, enter the keystrokes "Ctrl-Alt-M". This is the command (hot) keys that will be placed on the menu entry for MyMac. This key sequence should be unique, not conficting with any other menu command key sequence used in the Code::Blocks menu system.

Click on OK to accept the KeyMac definition.

You will now see a MyMac menu entry at the bottom of the Menu=>Plugins=>KeyMacs menu panel with the command keys Ctrl-Alt-M.

Either clicking on the MyMac menu item, invoking it with the command keys, or choosing it from the KeyMacros context menu should produce "//" followed by two tabs as a new comment line in your edit window.

KeyMacs without command keys can still be "menued", and be invoked by clicking on them from either the main or context menu.

<b>Recording and playback</b>

KeyMac contain a "Record Macro" facility that stores each keystroke for later use by the "Play Macro" menu item.

Once recorded, stopped or played back, the keystrokes are stored in the KeyMacs Editor by the label "Scratch".

The Scratch macro is over written on each record, stop, or playback. If you wish to save it, you must use the KeyMacs editor to rename "Scratch" to some other label.

Recorded keymacs should be edited for accuracy. They may contain misinterpreted or unwanted keystrokes. A '{' brace recorded in a macro, for example, cannot be played back accurately as a character until it's surrounded by escape braces "{{}".

"!", "`^`", `"+", cannot be played back as characters until they too are surrounded by braces; else they play back as the Alt, Ctrl, and Shift prefix modifiers for any key that follows them. Eg., "^c" is not the characters '^' and 'c', but the copy operation Ctrl-C. The character sequence must appear as "{`^`}c".

KeyMacs attempts to determine the intent of the user by surrounding single character occurances of these chars with escape braces, but it's not always correct.

If, during recording, the window focus leaves the editor, KeyMacs cannot see and record user key presses. They can, however, be re-entered into the macro via the KeyMacs editor.

<b>Named Key Symbols</b>

At the bottom of the KeyMacs editor is a list of key symbols (KeySyms) which represent functions performed for the user by KeyMacs. For example, {ENTER} emulates the user depressing then releasing the Enter key.

Other KeySyms, like {ALTDOWN}, depress the keys but do not release them until an opposite KeySym, like {ALTUP}, appears in the key macro stream. These "paired" KeySyms can cause havoc if not entered as matching pairs.

Eg., {CTRLDOWN}{RIGHT}{RIGHT}{CTRLUP} moves two words to the right.

KeySyms which cause movement may contain a numeric parameter. Eg, {RIGHT 4} will move the cursor 4 positions to the right.

> {WAIT 5} will pause for 5 milliseconds.
> {ASC 0191} will enter the char represented by ascii 191 into the editor.
> {ENTER 2} will create two new lines
> {UP}{DOWN}{RIGHT}{LEFT} are others.



<b>Special keys</b>

> !, `^`, +, represent the keystrokes Alt, Ctrl, and Shift respectively. They provide a modifier for the character key that follows it. When KeyMacs sees a "!c", it interprets it as an Alt-c; a "+v" as a Shift-v; a "`^`t" as a Ctrl-t. KeyMacs depresses the modifier key, depresses the char key, releases the char key, then releases the modifier key.

The brace set '{' and '}' are used to delineate special KeySyms. To use them as characters in a macro, they must be surrounded by braces themselves. IE., {{} and {}} correctly represent the left and right brace as characters.


<b>Quirks & restrictions.</b>

Key macros must begin execution from within an editor window. Once invoked from within an editor, macro keys may be injected into other windows, such as the find dialog. The sequence "^fPecan{ENTER}" would invoke the find dialog, insert the chars "Pecan" into the find text control, then execute the find by depressing and releasing the enter key.

Macros not checked as "Menued Macro" in the KeyMacs editor simply remain in the database for future reference. They can, of course, be deleted.

The macro database resides in the users home directory as cbKeyMacs.ini. The first section contains the macro definitions. The second section specifies the menu command keys or blank if "un-menued".

KeyMacs can execute other KeyMacs by referencing their menu command key. Be careful. This can cause an infinte loop if two macros invoke each other. To avoid this, a KeyMac that invokes another KeyMac should itself have no command keys.

A Keymac that is invoked by another KeyMac might execute asynchronously. Invoked KeyMacs do not return to the invoking Keymac The invoking KeyMac cannot wait for the invoked KeyMac. Most likely, the invoked KeyMac is queued up behind the invoking KeyMac, but it might also start its own thread.

The context {MENU} keysym opens on my Windows XP2 system at coordinates (0,0). I've found no way to change this annoying behavior.

KeyMacs injects keys into the focused window keyboard buffer. It attempts to start the KeyMac within the window that invoked the menu. But if you're running a "focus follows mouse" system, the mouse may change the window focus during KeyMac execution causing keys to input into the wrong window. Be careful of the mouse pointer location during invocations of the context menu.

On Linix. I have not yet succeeded in moving the mouse pointer back into the window owning the KeyMac when the mouse ends outside the owning window.

{ASC} is not available for Linix since XWindows does not support it.


<b>How do I install it?</b>

Download: http://code.google.com/p/cbkeymacs/downloads/list to a clean folder.

Compile KeyMacs for MSWindows with KeyMacs.cbp. Then copy KeyMacs.dll to ...\trunk\src\devel\share\CodeBlocks\plugins\KeyMacs.dll. Copy KeyMacs.zip to ...\trunk\src\devel\share\CodeBlocks\KeyMacs.zip

Compile KeyMacs for Linux with KeyMacs(unix).cbp. Then copy KeyMacs.dll to .../trunk/src/devel/share/codeclocks/plugins/KeyMacs.dll. Copy KeyMacs.zip to .../trunk/src/devel/share/codeblocks/KeyMacs.zip

Linux users will need the X11 and Xtst development libraries. These are usually already provided by the distribution. Ubuntu Synaptic provided the following libraries when I searched for xtst:

![http://lh6.ggpht.com/_c-XuBU8YTRg/SddRsE0uf9I/AAAAAAAAAH8/0O9OPjPioZw/s800/keymacs104.png&nonsense=a.png](http://lh6.ggpht.com/_c-XuBU8YTRg/SddRsE0uf9I/AAAAAAAAAH8/0O9OPjPioZw/s800/keymacs104.png&nonsense=a.png)
<br />Image:KeyMacs107.PNG

<b>KeySym definitions</b>

> `^`, !, + are key modifiers representing CTRL, ALT,SHIFT
> {ALT UP|DOWN} - Program menu invocation
> {BACKSPACE} or {BS}
> {DEL}
> {DELETE}
> {DOWN}
> {END}
> {ENTER}
> {ESC} or {ESCAPE}
> {F1} {F2} {F3} {F4} {F5} {F6} {F7} {F8} {F9} {F10} {F11} {F12}
> {HOME}
> {INS} or {INSERT}
> {LEFT} {RIGHT}
> {PGDN} {PGUP}
> {SPACE}
> {TAB}
> {UP}
> {PRINTSCREEN}
> {SCROLLLOCK}
> {NUMLOCK}
> {CTRLBREAK}
> {PAUSE}
> {CAPSLOCK}
> {NUMPAD0}
> {NUMPAD1} {NUMPAD2} {NUMPAD3} {NUMPAD4} {NUMPAD5} {NUMPAD6} {NUMPAD7}
> {NUMPAD8} {NUMPAD9} {NUMPADMULT} {NUMPADADD} {NUMPADSUB} {NUMPADDOT}
> {NUMPADDIV} {NUMPADENTER UP|DOWN}
> {MENU} - context menu
> {LCTRL} {RCTRL}
> {LALT} {RALT}
> {LSHIFT} {RSHIFT}
> {SLEEP}
> {CTRLDOWN} {CTRLUP}
> {ALTDOWN} {ALTUP}
> {SHIFTDOWN} {SHIFTUP}
> {ASC 0nnn}
> {WAIT}


<b>Example KeyMacs</b>

Use cmd key Ctrl-Enter to create a new indented line.

> "{END}{ENTER}"

Use Ctrl-P to enter the C++ pointer sequence (saving alot of mistypes)

> "->"

Use Alt-Ctrl-C to enter the C++ comment sequence

> "{END}{ENTER}//{TAB}"

Use Alt-Ctrl-B to enter a new set of formated braces

> "{END}{ENTER}{{}{ENTER 2}{HOME}{}}{UP}{TAB}"


Pecan 2007/01/15