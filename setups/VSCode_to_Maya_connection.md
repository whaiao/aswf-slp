### Updated: 5/15/23  
### Date: 5/10/23  
### Authors: Ninette Tan and Benjamin Beilharz
---

# Setup VSCode to Maya Connection:
1. Install VSCode extensions: MayaCode and MayaPy
	- MayaCode will be the one sending the file to Maya
	- MayaPy will automatically set up the paths for autocompletion (might need some time to scan the registry)

2. Go to you Maya Documents Folder, see this [link](https://help.autodesk.com/view/MAYAUL/2023/ENU/?guid=GUID-228CCA33-4AFE-4380-8C3D-18D23F7EAC72). 
3. Create a new file called `userSetup.py` in the scripts folder, with the following content:
	```python
	import maya.cmds
   	cmds.commandPort(name="localhost:7001", sourceType="mel")
	```
4. Open Maya and create a new scene in the launcher.
5. Check the connection by opening VSCode and create a new Python file (ends with `.py`).
	```python
	import maya.cmds as cmds
	cmds.polySphere()
	```
6. Open the command palette in VSCode with Shift+Ctrl/Cmd+P and type `Maya: Send Python Code to Maya`, switch over to Maya to see if there is now a sphere in the viewport called `pSphere1/polySphere1`. If it appears, you are done setting up VSCode with Maya. If not, please conduct the following in the troubleshooting area.
7. For autocompletion it might take a while for VSCode to analyse the underlying structure. Please check when you type `cmds.poly`, you see an option for `polySphere` as an autocompletion suggestion



# Troubleshooting:
1. Check `settings.json` in VSCode by hitting Shift + Ctrl/Cmd + P and selecting `Preferences: Open User Settings (JSON)`
2. Search for `python.analysis.extraPath` in your user settings and remove any extra paths that connect directly to dev kit, i.e.:
	```json
	"python.analysis.extraPaths": [
        "C:/Program Files/Autodesk/Maya2022/devkit/other/Python27/pymel/extras/completion/py/maya/api"
	],
	```
3. Reinstall `MayaPy` so it can set the path to your Maya installation again

4. Save and close in your directory `C:\Users\{user}\Documents\maya\{version_number}\scripts (for Windows)`
5. Restart Maya and VSCode, retry if you are now able to send `Python` code to Maya with step **5** from above.
