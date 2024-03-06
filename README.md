# Add a Template Page to a PDF Using Termux and qpdf.
---------------
I love my Boox Tablet, and I love the firmware 3.5 feature to add a page to a PDF, but I wanted to use a Template PDF to add as a page as well.

This is my temporary solution until Boox adds the Functionality Themselves.  

Full Disclosure, it's clunky and slow (Especially for large PDFs) and it might even mess up the writing data on some PDFs (I'm still testing this, it doesn't seem to anymore, but YMMV, and I take NO RESPONSIBILITY for any problems.  If you're concerned, always save as a different filename than the Original.

Please note that all these commands are CASE SENSITIVE (Termux is like Unix that way).  It's best to copy and paste them directly on your Boox device.

## How to Install/Setup
--------------
The code-block below contain commands to enter, please open this page on your Boox device and copy+paste the commands in to make sure you don't mistype them.
1. Install [F-Droid](https://f-droid.org/) (It's an "App Store" for free/open-source software): you can get the APK [Here](https://f-droid.org/F-Droid.apk)
2. Open F-Droid and search for and install Termux from F-Droid. It will ask for permissions to install packages.  Unfortunately F-Droid needs these permissions, if you'd prefer, you can just install the Termux apk from [here](https://f-droid.org/en/packages/com.termux/) (Please use the latest version, you'll also need to update it on your own if you opt not to use F-Droid).
3. Open Termux and you'll need to do a few things:
    1. Enter this Command to Update the Command Line Environment: `apt update && apt upgrade -y`
    2. Install Prerequisite packages: `apt install fzf qpdf curl -y`
    3. Make a directory(Folder) `bin` in your Home Directory(Folder): `mkdir ~/bin`  (If you already had Termux and already did this, obviously you can skip this step).
    4. Grant Termux Storage Permissions: `termux-setup-storage`.  You'll have to accept the Permission change.  If you're not comfortable with this, this program won't work for now (I apologize).
    5. Make a link in your Home directory to your Books directory/folder.  Normally: `[ ! -L ~/Books ] && (ln -s /sdcard/Books ~/Books || echo 'Failed to Create Books Link!')`, but if you have your PDFs somewhere else, `/sdcard/Books` will have to be replaced with the correct location.
    6. Make a link in your Home directory to your Templates directory/folder.  Normally: `[ ! -L ~/Templates ] && (ln -s /sdcard/noteTemplate ~/Templates || echo 'Failed to Create Templates Link!')`, but if you have your Template PDFs somewhere else, `/sdcard/noteTemplate` will have to be replaced with the correct location.
5. Add Templates (In PDF format) to that `noteTemplates` folder (or wherever you linked to on your internal storage) which you want to add as templates (Unfortunately for now, they have to be PDFs and only the first page is added). Here's a good place to look to start: [Free Templates](https://www.inksandpens.com/post/ruled-paper-templates/). Things like MDO I believe use A4 sized sheets, so scroll down for those Templates, otherwise, if you need US Letter sized, those are close to the top of the page.  In general, any PDF should work (It will only use the first page though), and while the Boox Tablets should render them well, sometimes exported PDFs have issues, unless you 'fit to page').
6. Download the script (In Termux): `curl -o ~/bin/pdf-ap -L 'https://raw.githubusercontent.com/jedi453/Add_Template_Page_to_PDF/qpdf/pdf-ap'`
7. Make the script runnable/executable in Termux: `chmod 0700 ~/bin/pdf-ap`

## How to Use
------------
1. Do the Install/Setup above (Please follow all the steps!)
2. Open the Multi-tasking Switcher and close everything (Make sure to save everything first!).  Once everything you have opened is saved, you can hit the trashcan in the multi-tasking menu (It's best if your PDF isn't open in Neoreader or an old instance of it).
3. Open Termux and type `pdf-ap` and hit enter.  
4. The script will prompt you to select a PDF.  Hit Enter to start searching.  This search uses "fuzzy finding" recursively in the directory you linked above to ~/Books (If you followed exactly, it will search the main storage in the 'Books' folder).
5. If setup correctly, this will start showing a lot of PDF filenames and paths.  If you start typing the name of one, it should show up in the list quickly. Once you've selected the proper PDF, (You can use Termux's built-in Up/Down Arrows if needed) hit Enter
6. The script will prompt you to select a Template.  Hit Enter to start searching.
7. Start typing the name of the template. Again this uses a fuzzy finding search, but this time in the ~/Templates link you made (Normally your 'noteTemplate' folder in your main Boox device storage). You don't need to type the whole name usually. Again, you can use the Up/Down Arrows built into Termux (Above the Keyboard) to select an entry when you see what you want.  Hit Enter.
8. Type in the page number you want to insert the Template Page in DIRECTLY AFTER (Not Before!).  So if you want to add a page between page 10 and 11, enter 10, etc. Then hit enter
9. The script will tell you, "This may take a while...".  Just give it some time, especially for large PDFs like Year-long Organizers/Books. (I'm looking into ways to speed this up, but for now it can take a minute or two to add the page... Sorry about that... This all depends on the speed of your device and the sizes of the PDF files used).
10. NOTE: The script will not allow you to over-write the original PDF (For now, while I'm testing it...) If you do want to overwrite (Do so at your own risk!), first use a different name, then copy and paste over the other name with a file explorer.
11. The script will prompt for a new filename.  Enter a new name for the new document (Without the `.pdf` suffix, it'll be added automatically).  It will then write to the same directory/folder the input file was in, but with the new name (If you use an existing name, it will prompt again and again until you enter a new filename or by giving up and quitting out, by typing a capital `Q` and hitting enter).
12. You can open the PDF in NeoReader, but you'll have to "re-embed" the writing data, a pop-up will appear, you should leave the defaults selected and hit "Ok".  This can also take some time, please be patient or you could mess up the writing data.
13. Once the prompt and the status message go away and you see your document, you should be all set! Your new PDF is ready!

## License
----------
This program is just a shell script that uses some open source command-line programs, trying to be a little simpler than using them directly.

The script itself is licensed under [CC0](https://creativecommons.org/public-domain/cc0/) with the understanding that I'm in no way responsible for any problems that arise from using this tool.  The tools used are also open-source `fzf` and `qpdf` (`curl` is only needed to originally download or update the script.), they have different licenses.

## How to update the script
---------
- If you're coming from a version that didn't ask you to make a `~/Templates` link, please follow the setup process again, starting at step 3.
- If you're switching to this version (The qpdf version) from the main version, please run: `apt update && apt install qpdf -y`
- In all cases, run the command: `curl -o ~/bin/pdf-ap -L 'https://raw.githubusercontent.com/jedi453/Add_Template_Page_to_PDF/qpdf/pdf-ap' && chmod 0700 ~/bin/pdf-ap || echo FAILED`

### Hopes for Future Updates
---------------
- Maybe add instructions and modify the script so you can just share the original PDF from the file Manager with Termux, and start the script using that (probably easier) method.
- Get feedback from the community!  Please let me know if this works or doesn't work for you, and if you have any issues!  Please let me know what features you'd like to see!

----------------
Thanks,

Dan
