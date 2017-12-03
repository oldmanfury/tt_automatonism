# tt_automatonism
Subpatches to run Automatonism on the terminal tedium

Automatonism https://www.automatonism.com/the-software/ is a set of pure data patches that function much in the way modules do in a modular sysnthesizer.  It is intuitive, powerful, graphical, and makes getting started in PD much easier.  The organelle has its own set of sub patches, which made it very easy to write some for the tt.  While simple, it took some care to put these together - all data is converted to signal waveforms in Automatonism, probably so that you can easily patch audio signals into CV and vice-versa.  I think they're all working, although I may have messed up the order of some inputs and outputs.  Really wish PD labeled them with something other than inlet~ inlet~ inlet~ ...

Install the full package from above on your PC and on the tt.  Put all the files in this archive in the main AUTOMATONISM_2.1 directory.  Edit main.pd and create a patch.  Insert the controls you need by hitting ctrl-1 and typing in the name of the control, like tt-knbs~.pd.  Wire it up and test the controls on your PC.  Click the save button.

Here is an oddity you need to be aware of - whatever sliders the tt is wired to need to be zeroed when you save it, otherwise you don't get the full range of the control with the knob.

Once your patch is working (start with something simple like the example AutoExample.png I put in the archive.) and it is saved, you need to copy the patch to the tt.  This is a bit difficult, since there are thousands of files related to the patch.  Copying them all over to the tt takes too long.  I put an example windows batch file in the repository that I ginned up to copy just the files that the patch needs.  I copy main.pd and the other .pd subpatches from the main directory, and then individually copy the text files the patch requires.  I found these by looking at the most recent date stamps of files in the patch_editor_abs directory.  Then I manually inserted them into the batch file.  Running it to copy to the tt is easy.  But once you add a widget, you will need to include another file in the script.  Painful - maybe someone can figure out a better way with robocopy or something.

To execute you put a line like this in your pdpd file


sudo /home/pi/pd-0.46-7/bin/pd -nogui -rt -midiindev 0,1 /home/pi/pdpatch/AUTOMATONISM_2.1/main.pd |& python /home/pi/pdpatch/AUTOMATONISM_2.1/tt-OLED.py


tt-OLED.pd has a signal input for an audio-stream on the left.  This gets displayed in an oscilloscope mode.  The inlet on the right is used to toggle the display.  Make sure you check-that box, when you do you'll see the data-stream written to the command-line in pure-data.




