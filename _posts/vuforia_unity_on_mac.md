# How to install Vuforia 8+ with Unity 2018+ on a Mac
### Sept 1 2019

## How to install Vuforia 8+ with Unity 2018+ on a Mac

I was able to install `Vuforia 8.3.8` to install on `Unity 2018.4.7f1` with Mac (Mid 2014) OS X Mojave (10.14.6).
    
JeanFabre's instructions worked almost perfectly for me; but I had to dive into the .pkg file to figure out what more needed to happen

1. After downloading the file "UnitySetup-Vuforia-AR-Support-for-Editor-2018.4.7f1.pkg".

2. My Unity was installed in the directory "/Applications/Unity/Hub/Editor/2018.4.7f1/"

3. It included the files/directories:
    - PlaybackEngines
    - Unity Bug Reporter.app
    - Unity.app

4. I extracted the UnitySetup-Vuforia-AR-Support-for-Editor-2018.4.7f1.pkg file as 
    `pkgutil --expand ~/Downloads/UnitySetup-Vuforia-AR-Support-for-Editor-2018.4.7f1.pkg ~/Downloads/UnitySetup-Vuforia-AR-Support_Unpackaged`

5. The package included the files/directories:
    - Distribution
    - PlugIns
    - Resources
    - TargetSupport.pkg.tmp

6. I examined every file in that folder for the word "Application" using (i.e. the Unity path):
    `find ./ | grep Applications`

7. This resulted in the following list (as well as some binary file garbage):
    
    ```
    - grep: ./: Is a directory
    - grep: .//Resources: Is a directory
    - grep: .//TargetSupport.pkg.tmp: Is a directory
    - grep: .//TargetSupport.pkg.tmp/Scripts: Is a directory
    - .//TargetSupport.pkg.tmp/Scripts/postinstall:base_dir="/Applications/Unity/PlaybackEngines/PlaybackEngines/VuforiaSupport"
    - .//TargetSupport.pkg.tmp/Scripts/postinstall:    "$base_dir/Documentation/DocCombiner" -autopaths /Applications/Unity
    - .//TargetSupport.pkg.tmp/Scripts/preinstall:PLIST="$DSTVOLUME/Applications/Unity/Unity.app/Contents/Info.plist"
    - .//TargetSupport.pkg.tmp/Scripts/preinstall:if [ -d "$DSTVOLUME/Applications/Unity/PlaybackEngines/VuforiaSupport" ] ; then
    - .//TargetSupport.pkg.tmp/Scripts/preinstall:    rm -rf "$DSTVOLUME/Applications/Unity/PlaybackEngines/VuforiaSupport"
    - .//TargetSupport.pkg.tmp/PackageInfo:{pkg-info overwrite-permissions="true" relocatable="false" identifier="com.unity3d.VuforiaSupport" postinstall-action="none" version="0" format-version="2" generator-version="InstallCmds-502 (14F27)" install-location="/Applications/Unity/PlaybackEngines/VuforiaSupport" auth="root"}
    ```

8. In that list, I see that Vuforia wants Unity's "PlaybackEngines" and the "Unity.app" directories to be located in "/Applications/Unity/"
        
9. So I moved ALL of the files in the "/Applications/Unity/Hub/Editor/2018.4.7f1" to the "/Applications/Unity/" directory

    `mv /Applications/Unity/Hub/Editor/2018.4.7f1/* /Applications/Unity/`


    [THIS is probably where JeanFabre's instructions failed for others]

    I was previously moving the `Contents` folder from the Unity.app directory into the /Applications/Unity/ directory. This was not the correct procedure.

        
10. I finally was able to use the "UnitySetup-Vuforia-AR-Support-for-Editor-2018.4.7f1.pkg" file and install Vuforia correcting (using all default settings). The process proceeded without any questionable behaviour.

    `open ~/Downloads/UnitySetup-Vuforia-AR-Support-for-Editor-2018.4.7f1.pkg`
        
11. I moved all of the content of `/Unity/Application/` back into `/Applications/Unity/Hub/Editor/2018.4.7f1/`
    `mv /Applications/Unity/* /Applications/Unity/Hub/Editor/2018.4.7f1/`

    [This gave a passible error that said "mv: rename Hub to Hub/Hub: Invalid argument"]

12. Open Unity
    - Select Project
    - Select Edit -> Project Settings -> Player -> PC, Mac, & StandAlone Settings
    - Select "Vuforia Augmented Reality Supported"
    - Accept license
    - Delete Main Camera
    - Add Vuforia AR Camera
    - Hit Play
    - See myself on the camera
    - Celebrate!

13. Jump up and down screaming, laughing, and high five-ing my partner!

Copyright 2019 Jonathan David Fraine unless otherwise noted.  
Licensed under [Creative Commons](http://creativecommons.org/licenses/by-nc-sa/3.0/)  
Find me on [Twitter](https://twitter.com/exowanderer)  
[Email](mailto:jdfraine [at] gmail.com)
