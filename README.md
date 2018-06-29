# Welcome Center
![Welcome Center screenshot](https://raw.githubusercontent.com/knuxfanwin8/welcome-center-info/master/WelcomeCenterScreenshot.png)

Welcome Center is a program that showcases several programs if it finds them on your computer.
The majority of software in Welcome Center is either obsolete or no longer updated. If you don't have any of the software specified in the program's language files (I'll talk about this in a minute!) it will display an error message saying "No content".
Adding your own software to Welcome Center is suprisingly easy: you just have to modify the language files in the Welcome Center folder. They are named in a scheme of language.ini, for example "en.ini"

Welcome Center is available for download from [here](https://mega.nz/#!yC4jiYSA!ekG2NPBiAopkU3RGRVVQ7sPXC8EspxceuCcH_Rv1EDo). 

**NOTE: Welcome Center is provided under fair use for research purposes.**

## Here's what you have to do to add your own app:
1. Open your language file (for example ``en.ini``). To learn more about language files, read the Languages section below.

2. You will see the following line:

```
PreferedSection=Item20,Item21,Item25...
```

Pick a random number and add ``Item<the number you picked>`` to the end of the line after a coma, for example:

```
PreferedSection=Item20,Item21
```
turns into:
```
PreferedSection=Item20,Item21,Item70
```

Remember to make sure an item with that name does not exist yet.

3. Scroll down to the bottom of the file and copy the following template:

```
[item<the number you picked>]
BannerDetail=
CmdText=
It_Title=
It_Text=
Tooltip=
Target=C:\Windows\explorer.exe
TargetX64=C:\Windows\explorer.exe
SetupTarget=C:\Windows\explorer.exe
SetupTargetX64=C:\Windows\explorer.exe
BtnType=Gray
BrandImg=%brand%\logo.png
Banner=
PreviewPicture=
BannerTitle=
IconPicture=
ColorTextBanner=
```

Remember to replace ``<the number you picked>`` with the number you picked earlier.

4. Fill in the template as follows:

```
CmdText= ;This is the text that appears on the grey button on the bottom right.
It_Title= ;This is the title of the app in the application picker on the bottom.
It_Text= ;This is the description of the app in the application picker on the bottom.
Tooltip= ;This is what appears when you hover on the button of the app in the application picker on the bottom.
Target=C:\Windows\explorer.exe ;This is the file that is ran when you press the grey button (the same one as in CmdText)
TargetX64=C:\Windows\explorer.exe ;Same as above.
BrandImg=%brand%\logo.png ;This is the logo that appears on the top right.
Banner= ;This is the background of the app description part of the window.
PreviewPicture= ;This is the program's icon in the app description part of the window.
BannerTitle= ;This is the title on the banner. 
BannerDetail= ;This is the description on the banner.
IconPicture= ;This is the icon that appears on the app button on the bottom part of the window.
ColorTextBanner= ;This is the font color on the banner in hex. For example, 000000 is black and ffffff is white.
```
Optional lines:
```
BtnType=Gray ;Button type. Button types are explained in the Button types section. This defaults to Gray.
SetupTarget=C:\Windows\explorer.exe ;Same thing as Target.
SetupTargetX64=C:\Windows\explorer.exe ;Same as TargetX64.
```
Example:

```
[item70]
CmdText=Try today!
It_Title=Cool App
It_Text=It's a very cool app!
Tooltip=Tooltip
Target=C:\Windows\explorer.exe
TargetX64=C:\Windows\explorer.exe
BtnType=Gray
BrandImg=%brand%\logo.png
Banner=%brand%\WelcomeCenterBanner.png
PreviewPicture=content\item180\PeMachines Accessory Store.png
BannerTitle=Cool App for Free!
BannerDetail=Yep, try it today!\nIt's soooo cool!
IconPicture=content\item180\eMachines Accessory Store.ico
ColorTextBanner=ffffff
```

This should look like this:
![Welcome Center screenshot](https://raw.githubusercontent.com/knuxfanwin8/welcome-center-info/master/CoolApp.png)

### Additional research
If any of the text values (e.g. ``It_Text``, ``BannerTitle`` and simmilar) do not exist, they just appear empty.

If ``Tooltip`` doesn't exist, the tooltip will simply not appear. If ``BtnType`` doesn't exist, it will just be Gray. If ``Banner`` is not specified, it will just turn into the normal Welcome Center banner (Banner=%brand%\WelcomeCenterBanner.png).

You might have noticed the ``Target``, ``TargetX64``, ``SetupTarget`` and ``SetupTargetX64`` values. 

``SetupTarget`` is executed if ``Target`` doesn't exist, and the same thing goes for the X64 values. 

If ``SetupTargetX64`` is not specified/is empty or the file to which the value points 

If the file specified in ``DoubleCondition`` is found, the entry is shown. If it doesn't, it's not. If ``DoubleCondition`` is not specified/is empty, it is ignored and the entry is shown anyways (if the ``Target``/``SetupTarget`` are found of course).

If the file specified in ``Target-NOT`` is found, the entry is not shown. Same thing with its X64 counterpart (``TargetX64-NOT``).

**TODO: I just found those two values: ``Argument`` and ``ArgumentX64``. These are most likely for running executables with certain arguments. Still, I'll have to find an app that is good for testing and see how exactly that works. Example of value usage:**
```
Argument=/src welcomecenteroem
ArgumentX64=/src welcomecenteroem
```
**Do they work on ``Target``, ``SetupTarget`` or both?**


## Buttons
Every button's graphics are stored in separate folders placed in the ``\IMG\_Btn`` directory. The name of the button's folder represents the button style name, which can then be used by setting the ``BtnType`` value to it, for example ``BtnType=Blue`` or ``BtnType=eMachines``.

Every button folder contains images named ``l.png`` (which is the left part of the button), ``m.png`` (which is the middle) and ``r.png`` (which is the right part). The only exception to this rule is the style in the ``Generic`` button folder - this one contains the background for the bottom picker buttons.

The following button types are available:
- Gray (Default)
- Blue 
- Green 
- Black 

There are also copies of those buttons, this time with brand names:
- Acer (copy of Green)
- eMachines (copy of Blue)
- Gateway (copy of Black)
- Packard Bell (copy of Gray)

There's also a folder for Generic, but it stores the images for the buttons on the bottom picker and cannot be used as a normal button.

## Languages
Welcome Center loads a language file matching the operating system's language. For example, if you're running a Polish copy of Windows, it will load the ``pl.ini`` file, and if you have an English copy, it will load content from ``en.ini``. Every language file is separate, which means that for example if you edit the ``en.ini`` file and launch it on a Polish system, you will not see your changes - you'll have to modify ``pl.ini``.

There are several language files in the folder. The unnamed file only seems to contain a few lines, possibly for any case in which the system language was not found. There is also a file called OEMWelcomeCenter.ini (the same as the executable) which contains lines that are displayed whenever there is no content to display (when none of the files specified in the chosen language file are found)

## Brands
This version of Welcome Center is Acer branded. I still didn't figure out how it checks for that though.

## App list (in ``en.ini``)
Norton Internet Security (2011, 60 day trial), McAfee Internet Security, iGoogle, Brand Game Console, Brand GameZone, eBay, Mercado (SIDENOTE 1), Norton Online Backup, Microsoft Office 2007, Netflix, Skype, NetZero (SIDENOTE 2), EarthLink (SIDENOTE 3), Microsoft Works (90-85 and SE 9), MyWinLocker, Nero 9, Adobe Photoshop Elements 7/8, Brand Accessory Store, eSobi, Barnes & Noble Desktop Reader (SIDENOTE 4), Times Reader 2.0

Sidenotes:

Brand is the currently chosen brand.

1. Oddly enough, this one was entirely in Mexican, despite this being an English config file.
2. This seems to be an ad for some ISP.
3. Another ad for an ISP.
4. Some kind of e-book reader.
