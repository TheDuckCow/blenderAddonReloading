# blenderAddonReloading
This is an in-blender addon reloading addon. Super meta. 

## Goals
- To be able to one-click reload (ie zip, load into UI, and refresh) addons as the code is beign developed
- Really most intended for addons with .zip folder structures, but could be extended to single-py file adodns (but honestly, little advantage since you can just run/refresh those through the UI).

## Structure/method
- Have a UI list of addon sources folders that are used/in development for quick reloading. 
- Each addon should have a "make.py" file, or optionally a "reload.py" file (explanation TBD)
  - make.py: Maybe turn into a real make file, but essentially should just list the files and folders to be included with the zip. In this case, the addon defines where and how to create the zip folder.
  - reload.py: A more customized script that gets run via popen subprocess using e.g. system built-in python. In this case, the reload.py creates the zip file and this reloading addon just needs to know where the .zip will be located. This is currently what I have been doing before working on this utility addon.
- The above file, ehicever accoridnly, will create a .zip file either in a subfolder called make or compiled, or one directly level up. Could just be a user prefernce option or allow for custom rules eventually
- Then, the script loads in the addon.
  - This is close but not quite the same as the way you would install by user interface; instead of using the install button operator, the files are overwritten file-per-file.
  - Default blender behavior is to not overwrite (ie update) non-py files if in an addon folder. Sometimes this is desirable, sometimes not. This addon re-loader should allow if desired automatic "clean installing" which is equivalent to removing the folder and unzipping the zip file there and then refreshing the loaded addon. 
  - Otherwise, to emulate default blender behavior, the existing addon folder under scripts/addons/ will remain, and only the files contained in the zip folder will overwrite py files only; any other files e.g. json or txt will remain unaltered. (should orphan folders/files be removed??)

## Other features/wishlist
- Verison 1. I've wanted to make this forever just haven't prioritized it.
- (Mac/Linux) Open terminal instance with blender button; ideally can set location according to addon
- Be able to check/uncheck ie enable or disable these in-development addons from this UI List of projects, which si presumedly somewhere convinient ie not user preferences (but also there just in case).
- Have a quick addons-folder opening button (either overall or per-addon). So useful... 
- Be able to quick open github or bitbucket webpage (grab from .git folder if present.. should be auto-check/automatic)

I've been wanting/needing this thing since forever, it's such a pain to always reload. Other convineince features to eventually add.. opening a terminal? provide quick-access to opening the scripts folder?

Note to self, look at that other addon reloader from once upon a time. I recall it didn't do exactly what I wanted but worth the look.
