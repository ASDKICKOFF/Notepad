# Notepad
Affected Version
1.80.19

Bug Behavior
When i launch the game with pre-launch commands my game launched and turns off and then the launcher pop out.
I'll include the pre-launch commands below.

Expected Behavior
Collapse should launch the game after executing the pre-launch commands.

Steps to reproduce
download 3dmigoto and Collapse (both are in additional information, below), and install. 3dmigoto files should be in desktop\3dmigoto if you don't want to change step 5 directory
Open Collapse
set game to [genshin impact], change region to [Global] (game was downloaded from hoyoplay)
go to [game settings] (from collapse)
in advance settings (enable) enable pre-launch commands, and input the command [start cmd.exe @cmd /k "cd C:\Users%USERPROFILE%\Desktop\3dmigoto && "3DMigotoLoader.exe" && exit"] without the []
Apply settings (delay doesn't affect the process for me, that's why i didn't mention it)
go to [Launcher]
Start game
i heard beep beep-boop beep-boop and then launcher pops out.
Related Issues
#580

Screenshot(s)
No response

Additional Information
DxDiag.txt
Collapse
3dmigoto
I have tried repairing the game it does not fix this bug; bug only work with pre-launch commands enabled if disabled then game works just fine.

@ASDKICKOFF ASDKICKOFF added the Needs Triaging label 13 hours ago
@studiobutter
studiobutter commented 11 hours ago • 
I don't mod Genshin, but the problem is 3dmigoto is executing from a directory that doesn't have the necessary dlls.

Try creating a batch file with the following

@echo off
cd [Directory where 3dmigoto executable is]
"3DMigoto Loader.exe"
Save as [name].bat
(Example: 3dlaunch.bat)

In the pre-launch commands

[Path to Batch]
Example:

C:\CLI\3dlaunch.bat
Put quotes if the folders or executable have space

If you need to see what 3dmigoto console, enable Collapse Console in the Launcher settings

@studiobutter
This comment has been minimized.
Show comment
@studiobutter
studiobutter commented 11 hours ago
I forgot to mention that if you currently have any 3dmigoto instance running, kill it with this command

taskkill /f /im "3DMigoto Loader.exe"
Admin is required.
(Windows 11 24H2 can use sudo to run any admin commands)
im on the latest update for windows, this did not work

ChatGPT said:
ChatGPT
Memory updated
The issue you're facing seems to be linked to how the pre-launch commands for 3DMigoto are being executed. From the steps and suggestions provided, it appears that the game launcher is not handling the pre-launch process correctly, causing the game to close and return to the launcher.

Here’s an alternative approach that might help:

Creating and Using a Batch File for 3DMigoto
Create a Batch File:

Open Notepad.
Paste the following into Notepad:
bash
Copy code
@echo off
cd C:\Users%USERPROFILE%\Desktop\3dmigoto
"3DMigotoLoader.exe"
exit
Save the file as 3dlaunch.bat on your desktop or another folder you prefer.
Update the Pre-Launch Command:

In the pre-launch commands inside Collapse, replace the current command with:
swift
Copy code
"C:\path\to\3dlaunch.bat"
Ensure that the path to your batch file is correct and surrounded by quotes if there are any spaces in the folder names.
Taskkill any Running Instances (optional but recommended): If a previous instance of 3DMigoto is running, you may want to kill it before starting the game:

Add this at the start of your batch file:
bash
Copy code
taskkill /f /im "3DMigotoLoader.exe"
Run as Administrator: Since some commands require admin privileges, make sure to run the game or batch file as an administrator. You can either:

Right-click on 3dlaunch.bat and select Run as Administrator, or
Modify the pre-launch commands to invoke admin privileges using sudo if needed for your version of Windows (Windows 11 24H2 supports it).
Verifying Console Output
To get more feedback, enable Collapse Console in the Launcher settings to see if there are any errors when executing the batch file or launching 3DMigoto.

Give these steps a try and let me know if the issue persists.






You said:
no im on 23h2 , don't repeat the above output if there is no need for any changes
ChatGPT said:
ChatGPT
Memory updated
Thanks for the clarification. Since you're on Windows 11 23H2, there is no need to adjust the above solution for the Windows version. Follow the steps for creating the batch file and updating the pre-launch commands, and you should be able to resolve the issue. Let me know if anything else comes up!






You said:
Add this at the start of your batch file

so taskkill /f /im "3DMigotoLoader.exe"
@echo off
cd C:\Users%USERPROFILE%\Desktop\3dmigoto
"3DMigotoLoader.exe"
exitis correct?
ChatGPT said:
ChatGPT
Your batch file should look like this:

batch
Copy code
taskkill /f /im "3DMigotoLoader.exe"
@echo off
cd C:\Users%USERPROFILE%\Desktop\3dmigoto
"3DMigotoLoader.exe"
exit
This format is correct. The taskkill command ensures any existing instances of 3DMigotoLoader.exe are closed, and the exit at the end ensures the batch file closes properly after running the loader.

Let me know how it goes!






You said:
didn't work, this worked before start cmd.exe @cmd /k "cd C:\Users\ahada\Desktop\3dmigoto && "3DMigotoLoader.exe" && exit"
ChatGPT said:
ChatGPT
Since the command start cmd.exe @cmd /k "cd C:\Users\ahada\Desktop\3dmigoto && "3DMigotoLoader.exe" && exit" worked for you before, let's adjust the batch file based on this.

Here’s how you can modify the batch file to match that approach:

batch
Copy code
taskkill /f /im "3DMigotoLoader.exe"
start cmd.exe /k "cd C:\Users\ahada\Desktop\3dmigoto && 3DMigotoLoader.exe && exit"
This command will:

Kill any running instances of 3DMigotoLoader.exe.
Start a new cmd.exe session, navigate to the 3DMigoto folder, and run 3DMigotoLoader.exe.
This should replicate what worked for you before, but with the addition of killing any previous instances first.

Let me know if this version works!






You said:
`start cmd.exe @cmd /k "cd C:\Users\ahada\Desktop\3dmigoto && "3DMigotoLoader.exe" && exit"`

i mean for the pre-launch commands. do not repeat the above if changes needed
ChatGPT said:
ChatGPT
For your pre-launch commands, use the following (based on what worked before):

batch
Copy code
start cmd.exe @cmd /k "cd C:\Users\ahada\Desktop\3dmigoto && 3DMigotoLoader.exe && exit"
No need for changes if this setup worked previously. It should function the same in your current configuration.






You said:
i changing the .exe to the 3dlaunch batch file above, it says something incorrect
ChatGPT said:
ChatGPT
If you're changing the .exe reference to the 3dlaunch.bat file in your pre-launch commands, the syntax needs to reflect the batch file execution correctly. Here's how you should structure it:

For pre-launch commands, change it to:

batch
Copy code
start cmd.exe @cmd /k "C:\path\to\3dlaunch.bat && exit"
Make sure to replace C:\path\to\3dlaunch.bat with the actual path where you saved the batch file. If there are spaces in any folder names, ensure the entire path is surrounded by quotes, like this:

batch
Copy code
start cmd.exe @cmd /k "C:\Users\ahada\Desktop\3dlaunch.bat && exit"
This should work if you're invoking the batch file instead of the .exe.






You said:
'C:\Users\ahada\Desktop\3dlaunch.bat' is not recognized as an internal or external command,
operable program or batch file.

C:\Program Files\Collapse Launcher\app-1.80.19>
ChatGPT said:
ChatGPT
It seems like the batch file isn’t being recognized as a valid command. The issue might be that cmd.exe doesn't recognize the batch file unless it’s explicitly executed as such. Here's how to modify the pre-launch command to fix that:

Use this for your pre-launch commands:

batch
Copy code
start cmd.exe /k "call C:\Users\ahada\Desktop\3dlaunch.bat && exit"
The call command is necessary when executing batch files in scripts or from another command line.

This should ensure the 3dlaunch.bat file is properly recognized and executed. Let me know if this resolves the issue!






You said:
got the same message as before, can i do this command with the cmd.exe?
ChatGPT said:
ChatGPT
Yes, you can directly execute the batch file using cmd.exe in your pre-launch command. Here's the correct syntax for that:

batch
Copy code
start cmd.exe /c "C:\Users\ahada\Desktop\3dlaunch.bat"
This command does the following:

start cmd.exe opens a new command prompt.
/c tells cmd.exe to execute the specified command (your batch file) and then terminate.
"C:\Users\ahada\Desktop\3dlaunch.bat" is the path to your batch file.
This should resolve the issue and execute your batch file properly from the pre-launch commands. Let me know how it works!






You said:
change the batch file to launch 3DMigotoLoader.exe
ChatGPT said:
ChatGPT
To modify the batch file so that it properly launches 3DMigotoLoader.exe, here's the final version of the batch file:

batch
Copy code
@echo off
cd C:\Users\ahada\Desktop\3dmigoto
start "" "3DMigotoLoader.exe"
exit
Explanation:
@echo off: Hides command output to keep things clean.
cd C:\Users\ahada\Desktop\3dmigoto: Changes the directory to where 3DMigotoLoader.exe is located.
start "" "3DMigotoLoader.exe": Uses the start command to launch 3DMigotoLoader.exe. The "" is just an empty title for the new window.
exit: Closes the batch file after running.
Make sure the path is correct, and save the file as 3dlaunch.bat. You can then use the pre-launch command:

batch
Copy code
start cmd.exe /c "C:\Users\ahada\Desktop\3dlaunch.bat"
This should now properly launch 3DMigotoLoader.exe via the batch file.






You said:

did not work, can this help?
ChatGPT said:
ChatGPT
Based on the screenshot, the pre-launch command seems correctly formatted. However, since it didn’t work, here are a few possible adjustments to troubleshoot:

1. Ensure Batch File is Working
Double-check that the 3dlaunch.bat file runs correctly when you manually double-click it. If it does not execute properly outside of Collapse, there may be an issue with the batch file itself.

2. Administrator Privileges
Since the pre-launch commands will run as Administrator, it's essential that both cmd.exe and the batch file have proper permissions. Try running Collapse Launcher as Administrator by:

Right-clicking the Collapse Launcher shortcut.
Selecting Run as Administrator.
3. Adjust the Command
Sometimes extra quotes or slight syntax differences can affect command execution. Try simplifying the command as follows:

batch
Copy code
cmd /c "C:\Users\ahada\Desktop\3dlaunch.bat"
This eliminates the start command and should directly execute the batch file.

4. Test Without Batch File
To narrow down the problem, you could also test the original pre-launch command (the one that worked before with the direct path to 3DMigotoLoader.exe):

batch
Copy code
start cmd.exe @cmd /k "cd C:\Users\ahada\Desktop\3dmigoto && 3DMigotoLoader.exe && exit"
If this works, the issue might be with how Collapse handles the batch file.

Let me know if any of these adjustments help!






You said:
start cmd.exe @cmd /k "cd C:\\Users\\ahada\\Desktop\\3dmigoto && 3DMigotoLoader.exe && exit"

the first command did not work, when launched from collapse (collapse runs on admin by default, and executes the commands as admin by default). this whole thing stems from the fact that this command works, but the game does not launch with this command when executed from Collapse (3rd party launcher). yes the .exe works when i do it manually but i downloaded collapse to not do that. the problems stems from collapse or how the pre-launch commands work, by using any command besides this the game launches immediately but no command, if i use this command game does not launch.
ChatGPT said:
ChatGPT
Memory updated
Given the context that the command works manually but not when executed from Collapse, the issue likely lies in how Collapse handles the execution environment or timing of commands.

Here are a few potential solutions to try:
Use a Timeout: Adding a delay before launching the loader can sometimes help with timing issues. Modify your batch file to include a timeout command:

batch
Copy code
@echo off
timeout /t 2 /nobreak > nul
cd C:\Users\ahada\Desktop\3dmigoto
start "" "3DMigotoLoader.exe"
exit
This introduces a 2-second delay before launching 3DMigotoLoader.exe.

Change to cmd /c: Try using cmd /c instead of cmd /k in your pre-launch command:

batch
Copy code
cmd /c "cd C:\Users\ahada\Desktop\3dmigoto && 3DMigotoLoader.exe"
This runs the command and then exits, which might help in properly executing the loader.

Debugging Output: Modify your batch file to output messages to a log file to help identify where it might be failing:

batch
Copy code
@echo off
echo Launching 3DMigotoLoader.exe > C:\Users\ahada\Desktop\launch_log.txt
cd C:\Users\ahada\Desktop\3dmigoto >> C:\Users\ahada\Desktop\launch_log.txt
start "" "3DMigotoLoader.exe" >> C:\Users\ahada\Desktop\launch_log.txt 2>&1
exit
This will create a launch_log.txt file on your Desktop with any output and errors.

Check for Environment Variables: Ensure there are no environment variables set that could be affecting the execution. This includes path settings or user permissions.

Testing with Direct Execution: If all else fails, you could bypass the batch file entirely and call 3DMigotoLoader.exe directly in your pre-launch commands:

batch
Copy code
start cmd.exe /c "C:\Users\ahada\Desktop\3dmigoto\3DMigotoLoader.exe"
Additional Notes
If none of these work, the issue might be inherent to the Collapse Launcher itself, and it may be worth checking their documentation or community for any known limitations with running batch files or certain commands.

Let me know how it goes or if you need further assistance!






You said:
first 3 commands did not work not even a launch_log.txt file was found in my desktop, last one said : Waiting for program ...
Found

Traceback (most recent call last):
File "3DMigotoLoader.py", line 20, in <module>
File "3DMigotoLoader.py", line 13, in main
File "pyinjector\api.py", line 92, in inject
pyinjector. api. LibraryNotFoundException: Could not find library: b'd3d11.dll'
[PYI-25200: ERROR] Failed to execute script '3DMigotoLoader' due to unhandled exception!

GenshinImpact.exe 28212
ChatGPT said:
ChatGPT
The error message you're encountering indicates that 3DMigotoLoader is having trouble finding the d3d11.dll library. This suggests that the 3DMigotoLoader is not being executed in the correct context or environment where the necessary files are available.

Here are some steps to address the issue:
Ensure Files are in the Correct Directory: Verify that the d3d11.dll file is located in the same directory as 3DMigotoLoader.exe. If it's missing, you'll need to ensure that all necessary files are present.

Modify Batch File for Full Path: You might need to explicitly set the working directory within your batch file. Update your 3dlaunch.bat to ensure it runs in the correct context:

batch
Copy code
@echo off
setlocal
pushd C:\Users\ahada\Desktop\3dmigoto
start "" "3DMigotoLoader.exe"
popd
exit
The pushd and popd commands change the current directory to 3dmigoto and then revert back after the command runs.

Check Dependencies: Make sure that 3DMigotoLoader.exe and any other required DLLs (like d3d11.dll) are present and compatible with your version of Genshin Impact. If d3d11.dll is missing, it can usually be found in other applications that utilize DirectX.

Run Directly from Collapse: If you want to try again running directly from Collapse, use the following pre-launch command (without a batch file):

batch
Copy code
start cmd.exe /c "cd C:\Users\ahada\Desktop\3dmigoto && 3DMigotoLoader.exe"
Ensure the command is pointing directly to the 3DMigotoLoader.exe and the directory it resides in.

Check for Compatibility Issues: Sometimes compatibility issues arise with different versions of software. Ensure that Collapse Launcher, 3DMigoto, and Genshin Impact are all up-to-date and compatible with each other.

Use Dependency Walker: You can use a tool like Dependency Walker to check if 3DMigotoLoader.exe is missing any dependencies, including d3d11.dll.

Conclusion
Once you've verified the files and made these changes, try launching through Collapse again. If the problem persists, you might consider reaching out to the support community for 3DMigoto or Collapse for more tailored assistance. Let me know how it goes!






You said:
did not work, im not missing any dependancies all i got is beep beep-boop beep-boop
ChatGPT said:
ChatGPT
The "beep beep-boop beep-boop" sound indicates that the command is being processed, but the game fails to launch correctly. This suggests that the issue may be related to how Collapse handles launching 3DMigotoLoader.exe rather than missing dependencies.

Here are additional troubleshooting steps to try:
Check for Running Instances: Before launching the game, ensure no previous instances of 3DMigotoLoader.exe are running. You can include a command to kill any running instances in your batch file or pre-launch command:

batch
Copy code
taskkill /f /im "3DMigotoLoader.exe"
Add this line at the beginning of your batch file:

batch
Copy code
@echo off
taskkill /f /im "3DMigotoLoader.exe"
cd C:\Users\ahada\Desktop\3dmigoto
start "" "3DMigotoLoader.exe"
exit
Modify Pre-Launch Command: Use a simple pre-launch command to run the batch file, without trying to open a new command window. Try this command:

batch
Copy code
"C:\Users\ahada\Desktop\3dlaunch.bat"
Add Logging to Batch File: If logging did not work previously, try adding logging directly in the command window by redirecting both standard output and error output to a log file:

batch
Copy code
@echo off
echo Starting 3DMigotoLoader at %date% %time% >> C:\Users\ahada\Desktop\launch_log.txt
taskkill /f /im "3DMigotoLoader.exe" >> C:\Users\ahada\Desktop\launch_log.txt 2>&1
cd C:\Users\ahada\Desktop\3dmigoto >> C:\Users\ahada\Desktop\launch_log.txt 2>&1
start "" "3DMigotoLoader.exe" >> C:\Users\ahada\Desktop\launch_log.txt 2>&1
exit
Try Different Execution Methods: If the game runs fine without any commands, consider running 3DMigotoLoader.exe directly without Collapse to see if there’s a fundamental issue with the loader itself when run in this context.

Check for Anti-virus/Anti-cheat Issues: Sometimes anti-virus or anti-cheat systems (especially with games like Genshin Impact) might interfere with third-party loaders. Ensure that 3DMigoto and Collapse are whitelisted in your anti-virus or security software.

Reach Out for Community Support: Since this seems to be an issue with the interaction between Collapse and 3DMigotoLoader.exe, consider reaching out on forums or communities related to either software. Other users may have faced similar issues and could have solutions.

Last Resort
If these methods do not resolve the issue, you might need to explore alternative launchers or methods to achieve the same result without running into these conflicts. Let me know if you need further assistance or want to try any specific approach!






You said:
game started without the command, as i mentioned previously the game works just fine without collapse launcher (with the commands). 5. i added both through my firewall. 6. i did. did not work and the developers closed my request 3dmigoto is violating genshin's terms of service
ChatGPT said:
ChatGPT
Memory updated
Given that Genshin Impact is actively enforcing its terms of service, using 3DMigoto could lead to account issues, including potential bans. Since the game runs fine without Collapse or the pre-launch commands, here are some alternative approaches you could consider:

Alternative Launchers: Look for other third-party launchers or mods that are more compliant with the game's terms of service. They may offer similar functionalities without the risks associated with 3DMigoto.

Manual Modifications: If you want to enhance your gaming experience, consider manual modifications that don't require third-party tools. Sometimes, in-game settings or graphics tweaks can improve performance.

Community Recommendations: Engage with communities focused on Genshin Impact for legitimate mods or optimizations that are approved or don't violate the terms of service.

Official Support: If you face any issues with the game itself or suspect that it might be related to using tools, reaching out to official support could provide clarity on what is allowed.

Check for Updates: Keep an eye on updates from both Genshin Impact and 3DMigoto. Sometimes, developers will release updates that may alter how mods can interact with the game.

If you have any specific needs or preferences for your gaming setup that you want to explore within the guidelines of the game's terms, let me know!
