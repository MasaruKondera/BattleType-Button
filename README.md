# HowTo: Install this modification

Warning: This mod is not compatible out of the box with other modifications that edit the service_lib.swf file.
If you want to use this mod with your other mods, either ask your mod creator to create a patch for you, or do it yourself 
via the patch tutorial below. Other mods that also edit the uss_settings.xml file work when you add this modification to this file.

**1. Copy the "res_mods" folder**
You want to copy the res_mods folder from the latest release into the latest version directory from WoWs located in the bin folder.  
It will look similar to this: "C:\World_of_Warships\bin\5045210" 

In case the system asks you to overwrite the uss_settings.xml file, then do not overwrite it and continue with 2.

**2. This step is only needed when your system asked you to overwrite the uss_settings.xml file**
Open up the already existing uss_settings.xml file and add the following lines in the mods block.
```xml
<mods>
    <!--
       Add your modded XML and SWF paths here. Modded content should be put into the unbound/mods folder.
       Example:
       <xmlfile>../unbound/mods/carousel_extended.xml</xmlfile>
       <swffile>../unbound/flash/carousel_extended.swf</swffile>
    -->
    <xmlfile>../unbound/mods/BattleType-Button/BattleButton.xml</xmlfile>
    <swffile>../unbound/mods/BattleType-Button/BattleButton.swf</swffile>
    <!-- already existing mods here-->
</mods>
``` 


---

# HowTo: Patch your own service_lib.swf file

In this tutorial I will try to explain, how to make your modification compatible
with this modification.

## Preparations
&emsp;Install [JPEXS FFdec](https://github.com/jindrapetrik/jpexs-decompiler/releases)  
&emsp;Extract the service_lib.swf file via the [WoWs Unpacker](https://forum.worldofwarships.com/topic/183662-all-wows-unpack-tool-unpack-game-client-resources/) or use an already existing file from another  
&emsp;modification.
## Patching the service_lib.swf
**1. Open the service_lib.swf file with FFdec**  

*When you get a warning, click on **"No to all"***  
![Warning dialog, click no to all](tutorial_images/warning.png)  

It should look like this now  
![JPEXS FFdec window with open service_lib.swf file](tutorial_images/base_window.png)  

**2. Expand _sprites_**  
![Expanded sprites](tutorial_images/sprites.png)

**3. Search for _button_fight_ and expand it**  
![Expanded button_fight](tutorial_images/sprite_button_fight.png)  

**4. Expand frame1 and click on the object with depth: 1**  
![Expanded frame1 with depth1 active](tutorial_images/frame1_depth1.png)

**5. Click on the first element in the Needed Characters list**  
If this is does not bring you to a "DefineBitsLossless2" Object, then go back and try the next element in the list.
![Brufteforce the needed object](tutorial_images/bruteforce_characters.png)

**6. Replace the image with empty.png**  
empty.png is located in the patching folder where you found this tutorial.
![Click replace](tutorial_images/replace.png)

**7. Go back to the button_fight sprite object**  

**8. Right-click in frame1 the Depth: 3 Object and select raw edit**  
![Right click on the depth 3 frame and select raw-edit](tutorial_images/raw_edit.png)

**9. Click on edit below the preview**  
![Click on edit](tutorial_images/edit_depth3.png)

**10. Replace the color value from the GLOWFILTER by clicking on the RGBA Color**  
![Click on the RGBA value from the Glowfilter](tutorial_images/glow_color.png)

**11. Select the following color and press okay**  
![Normal Glow RGB (153,153,153)](tutorial_images/normal_glow.png)

**12. Click on the save button below the edited GLOWFILTER**  
![Save the changes](tutorial_images/save_glowfilter.png)

**13. Select the only element in the "Needed Characters" list and click on edit**
![Edit the font color](tutorial_images/edit_font_color.png)

**14. Edit both color values in line 10 and 17 to #e9e9e9 and save it like before**  
Note: You can ignore the first two 'f' character of the color value in line 10. They are responsible for the 
transparency of the text.  
Line 10: #ffe9e9e9
Line 17: color="#e9e9e9"
![Save the edited font color](tutorial_images/edited_font_color.png)

**15. Go back to the button_fight object by clicking on the "Dependent Characters" element**

**16. Repeat the steps above with the rest of the frames and object mentioned below in the overview table**

##Overview Table

| Frame Nr | Depth Value | To Edit                                                                                                                                                                                                      |
| -------- |-------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1 | 1           | DefineBitsLossless2 Object accessable via Needed Characters, Replace Image with empty.png                                                                                                                    |
| 1 | 3           | Edit the textField glowfilter to the first color [^1], also adjust the textField color by accessing the DefineEditText Object via the Needed Characters List to #ffe9e9e9 for line 10 and #e9e9e9 in line 17 |
| 11 | 3           | DefineBitsLossless2 Object accessable via Needed Characters, Replace Image with hover.png                                                                                                                    |
| 11 | 7           | Edit the textField glowfilter to the second color [^2]                                                                                                                                                       |
| 26 | 1           | DefineBitsLossless2 Object accessable via Needed Characters, Replace Image with clicked.png                                                                                                                  |
| 26 | 7           | Edit the textField glowfilter to the first color [^1], also adjust the textField color by accessing the DefineEditText Object via the Needed Characters List to #ff909090 for line 10 and #909090 in line 17 |
| 36 | 3           | DefineBitsLossless2 Object accessable via Needed Characters, Replace Image with blocked.png                                                                                                                  |

[^1]: ![Normal Glow RGB (153,153,153)](tutorial_images/normal_glow.png)  
[^2]: ![Hover Glow RGB (204,204,204)](tutorial_images/hover_glow.png)