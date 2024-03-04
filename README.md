# Add a Template Page to a PDF Using Termux and pdftk.
---------------
I love my Boox Tablet, and I love the firmware 3.5 feature to add a page to a PDF, but I wanted to use a Template PDF to add as a page as well.

This is my temporary solution until Boox adds the Functionality Themselves.  

Full Disclosure, it's clunky and slow (Especially for large PDFs) and it might even mess up the writing data on some PDFs (I'm still testing this, it doesn't seem to anymore, but YMMV, and I take NO RESPONSIBILITY for any problems.  If you're concerned, always save as a different filename than the Original.

## How to Install/Setup
--------------
1. Install F-Droid (It's an "App Store" for free/open-source software): you can get the APK [Here](https://f-droid.org/F-Droid.apk)
2. Open F-Droid and search for and install Termux.
3. Open Termux and you'll need to do a few things:
    1. Update Termux: `apt update && apt upgrade -y`
    2. Install Prerequisite packages: `apt install fzf pdftk curl -y`
    3. Make a directory(Folder) `bin` in your Home Directory(Folder): `mkdir ~/bin`
    4. Termux Storage Permissions: `termux-setup-storage`.  You'll have to accept the Permission change.  If you're not comfortable with this, this program won't work for now.
    5. Make a link in your Home directory to your Books directory/folder.  Normally: `ln -s /sdcard/Books ~/Books`, but if you have your PDFs somewhere else, `/sdcard/Books` will have to be replaced with the correct location.
4. Make a Templates Folder. For now, they'll have to be in a sub-directory/folder named `Templates` within your Books folder you linked to so Normally Make a Folder Templates in your Books directory from the file explorer.
5. Add Templates to that new Templates Folder/Directory (PDFs which you want to add the first page from to any PDF), Here's a good place to look to start: [Free Templates](https://www.inksandpens.com/post/ruled-paper-templates/). Things like MDO I believe use A4 sized sheets, so scroll down for those Templates, otherwise, if you need US Letter sized, those are close to the top of the page.
6. Download the script (In Termux): `curl -O ~/bin/pdf-ap -L 'https://raw.githubusercontent.com/jedi453/Add_Template_Page_to_PDF/main/pdf-ap'`
7. Make the script runnable/executable in Termux: `chmod 0700 ~/bin/pdf-ap`

## How to Use
------------
1. Do the Install/Setup above (Please follow all the steps!)
2. Open the Multi-tasking Switcher and close everything (Make sure to save everything first!).  Once everything you have opened is saved, you can hit the trashcan in this menu.
3. Open Termux and type `pdf-ap` and hit enter.  
4. The script will prompt you to select a PDF.  Hit Enter to start searching.
5. If setup correctly, this will start showing a lot of PDF filenames and paths.  If you start typing the name of one, it should show up in the list quickly. Once you've selected the proper PDF, (You can use Termux's built-in Up/Down Arrows if needed) hit Enter
6. The script will prompt you to select a Template.  Hit Enter to start searching.
7. Start typing the name of the template. You don't need to type the whole name usually. Again, you can use the Up/Down Arrows built into Termux (Above the Keyboard) to select an entry when you see what you want.  Hit Enter.
8. Type in the page number you want to insert the Template Page in DIRECTLY AFTER.  So if you want to add a page between page 10 and 11, enter 10, etc. Then hit enter
9. The script will tell you, "This may take a while...".  Just give it some time, especially for large PDFs like Year-long Organizers/Books. (I'm looking into ways to speed this up, but for now it can take several minutes to add the page... Sorry about that... XD)
10. The script will prompt you if you want to over-write the original PDF. The default is "No", which I recommend for now while I sort out some possible issues. If you do want to overwrite (Do so at your own risk!) type a `y` and hit enter.
    1. If you chose to overwrite the output PDF, the script should finish.
    2. If you chose not to overwrite the output PDF, the script will prompt for a new filename.  Enter a new name for the new document (Without the `.pdf` suffix, it'll be added automatically).  It will then write to the same directory/folder the input file was in, but with the new name (Make sure you don't use an existing name!).
11. You can open the PDF in NeoReader, but you'll have to "re-sync" the writing data, a pop-up will appear, you should leave the defaults selected and hit "Ok".
12. You should be all set! Your new PDF is ready!

## License
----------
This program is just a shell script that uses some open source command-line programs, trying to be a little simpler than using them directly.

The script itself is licensed under [CC0](https://creativecommons.org/public-domain/cc0/) with the understanding that I'm in no way responsible for any problems that arise from using this tool.

## How to update the script
---------
Open Termux and run the command: `curl -O ~/bin/pdf-ap -L 'https://raw.githubusercontent.com/jedi453/Add_Template_Page_to_PDF/main/pdf-ap && chmod 0700 ~/bin/pdf-ap || echo FAILED'`

### Hopes for Future Updates
---------------
- Maybe switch from using pdftk, which is great, but seems slower than molasses to insert the page (Especially in Large PDFs), to maybe use qpdf, after making sure it won't mess with the hand-writing data (It seems to throw a lot of errors on my marked-up PDFs).
- Maybe add instructions and modify the script so you can just share the original PDF from the file Manager with Termux, and start the script using that (probably easier) method.
- Get feedback from the community!  Please let me know if this works or doesn't work for you, and if you have any issues!  Please let me know what features you'd like to see!

----------------
Thanks,

Dan
