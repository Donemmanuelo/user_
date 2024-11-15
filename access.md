# A BRIEF OVERVIEW OF ACCESSIBILITY
In linux desktop environment have setting and tool to adapt  user interface of people with disabilities. Ordinary human interface devices such as screen, keyboard and mouse/touchpad, can be individually reconfigured to overcome visual impariment or reduced mobility.
Some accessibility feature are provided by desktop environment, like Gnome, KDE, and other are provided by additional program.
## ACCESSIBILITY SETTING
All linus distribution provide about the same accessibility feature, which can be customised with configuration module found in the setting manager that come with the desktop enviroment. The accessibility module is called universal access in Gnome desktop, KDE accessibility is under system settings, Personalization, Accessibility. Other desktop environments, like Xfce, also call it Accessibility in their graphical setting manager. However it offer a reduced functionality compared to the Gnome and KDE. 
### KEYBOARD AND MOUSE ASSIST
##### _keyboard assist_
The default keyboard can be modified to get around specific mobility difficulties. Key combination, key auto repeat rate and unintended key presses can be significant obstacle for user with reduced hand mobility. These typing shotcomings are addressed by three keyboard  related accessibility feature such as sticky, bounce and low key.
####  sticky key
The sticky key feature, found in the _typing assist_ section of Gnome's Universal Access configuration, allows the user to type keyboard shotcuts one key at a time when enabled. The functionility of the sticky key is just like that of caplock.
#### slow key  
The slow key feature tries to inhibit unintended key presses by placing a delay between them, that is, a new key will be accepted only after a specific length of time has passed since the last key press.
#### bounce key 
The bounce key feature ignore fast duplicate keypresses.
##### How the keys above are enabled
- The sticky and slow key can be enabled when the turning on or off the Activation Gesture performed by the keyboard in both Gnome and the KDE desktop environment. However this Activation Gestion on the keyboard is found in Gnome setting under accessibility, typing.  
- After turning the Activation Gesture of the keyboard on, sticky is actvated by pressing shift five consecutives times.
- To enable the slow key the shift key must be press and hold for 8 seconds or if it don't work your can actually go to the Gnome setting, under accessibility and enable them. 
- It is also possible to customise you own keyboard by going to the Gnome setting, under the keyboard and customising the your keyboard shotcut according to your preference. 
###### _mouse assist_
User who find it more comfortable to use keyboard over the mouse or touchpad can resort to keyboard shortcut to get around in the desktop environment. The feature called _mouse key_ when enabled allow user to control the mouse pointer itself with the numerical keypad(8 up, 2 down, 4 left and 6 right), which is present still in the Gnome settings. But however for machine having the keys for number to the right, will simply enable the _Numlock key_, which will allow you to use your keyboard as pointer. 
- The Slow, Sticky, Mouse and Bounce key are accessibility feature that are provided by AccessX, a resource within the X keyboard extension of the X Window System. AccessX can also be modified using the command line, xkbset command. KDE and other desktop environments may not provide the screen keyboard by default, but the onboard package can be manually installed to provide simply on screen keyboard that can be used in the desktop environment. The pointer behaviour can also be modified, if the user is not able to press the mouse quick enough to trigger double click event, the user can go to Gnome settings under accessibility, pointing & clicking and increase the delay time between the first and second click.
##### VISUAL IMPAIRMENTS
Users with reduced eyesight may still be able to use the monitor screen to interact with the computer. Depending on the user's needs, many visual adjustments can be made to improve the otherwise hard to see detail of the standard graphical desktop.
Gnome setting have some option to help people with reduced eyesight:
1. High Contrast
will make windows and buttons easier to see by drawing them in sharper colors.
2. Large Text
will enlarge the standard screen font size.
3. Cursor Size
allows to choose a bigger mouse cursor, making to locate on the screen.

For user for which graphical interface gis not an option or choice, the can use the screen reader. The most popular screen reader is the orca which is usually installed by default in most distributions. Orca generates a synthesized voice to report screen events and to read the text under the mouse cursor. Not all deskop applications are fully adapted for screen readers and not all not all users will find it easy to use them.

