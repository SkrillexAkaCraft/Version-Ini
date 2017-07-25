Sponge Installer is able to instal all stable sponge versions there are!

Please leave feedback






code:

version = 0.1
product := "Sponge Installer"

VanillaVersions := "1.8|1.8.9|1.9|1.9.4|1.10.2|1.11|1.11.2"
ForgeVersions := "1.10.2|1.11|1.11.2"
APIVersions := "3|4|5|6"
VanillaLinks := []
VanillaLinks["1.8"] := "https://repo.spongepowered.org/maven/org/spongepowered/spongevanilla/1.8-3.1.0-BETA-171/spongevanilla-1.8-3.1.0-BETA-171.jar"
VanillaLinks["1.8.9"] := "https://repo.spongepowered.org/maven/org/spongepowered/spongevanilla/1.8.9-4.2.0-BETA-352/spongevanilla-1.8.9-4.2.0-BETA-352.jar"
VanillaLinks["1.9"] := "NONE"
VanillaLinks["1.9.4"] := "NONE"
VanillaLinks["1.10.2"] := "https://repo.spongepowered.org/maven/org/spongepowered/spongevanilla/1.10.2-5.2.0-BETA-391/spongevanilla-1.10.2-5.2.0-BETA-391.jar"
VanillaLinks["1.11"] := "NONE"
VanillaLinks["1.11.2"] := "https://repo.spongepowered.org/maven/org/spongepowered/spongevanilla/1.11.2-6.1.0-BETA-16/spongevanilla-1.11.2-6.1.0-BETA-16.jar"

ForgeLinks := []
ForgeLinks["1.10.2"] := "https://repo.spongepowered.org/maven/org/spongepowered/spongeforge/1.10.2-2281-5.2.0-BETA-2464/spongeforge-1.10.2-2281-5.2.0-BETA-2464.jar"
ForgeLinks["1.11"] := "NONE"
ForgeLinks["1.11.2"] := "https://repo.spongepowered.org/maven/org/spongepowered/spongeforge/1.11.2-2393-6.1.0-BETA-2471/spongeforge-1.11.2-2393-6.1.0-BETA-2471.jar"

APILinks := []
APILinks[3] := "https://repo.spongepowered.org/maven/org/spongepowered/spongeapi/3.1.0/spongeapi-3.1.0-shaded.jar"
APILinks[4] := "https://repo.spongepowered.org/maven/org/spongepowered/spongeapi/4.1.0/spongeapi-4.1.0-shaded.jar"
APILinks[5] := "https://repo.spongepowered.org/maven/org/spongepowered/spongeapi/5.1.0/spongeapi-5.1.0-shaded.jar"
APILinks[6] := "https://repo.spongepowered.org/maven/org/spongepowered/spongeapi/6.0.0/spongeapi-6.0.0-shaded.jar"

UrlDownloadToFile, https://raw.githubusercontent.com/SkrillexAkaCraft/Version-Ini/master/new_version.ini, new_version.ini
      INIRead, newVersion,% "new_version.ini", version, new_version
    if (newVersion > version){
        Gui, Update:Add, Text,    x10   y10   wp400 h25     ,% "A new version of " product "has arrived!`n`n"
        Gui, Update:Add, Text,    xp    y40   wp-40 hp      ,% "Current version:`t" Version "`n"
        Gui, Update:Add, Text,    xp    y55   wp    hp      ,% "New version:`t" newVersion "`n"
        Gui, Update:Add, Text,    xp    y85   wp    hp      ,% "Would you like to update?"
        Gui, Update:Add, Button,  xp+170yp-6  w30   hp gYes ,% "Yes"
        Gui, Update:Add, Button,  xp+50 yp    wp    hp gHome ,% "No" 
        Gui, Update:Show,                     w290  h130    ,% "Update?"
        return
        } Else {
			gosub Home
	}
return

UpdateGuiClose:
ExitApp	

Home: 
Gui, Update:Destroy
Gui, Home:Add, Text, x10 y10 w315 h60, Welcome to Sponge installer, This is made by Skrill_Craft to make it possible to download Sponge Forge and Sponge Vanilla whitout going to the site,
Gui, Home:Add, Text, x20 y85 w300 h25, Please select either you want Sponge Vanilla or Sponge Forge
Gui, Home:Add, DropDownList, x20 y115 w120 h100 vSponge Choose1 AltSubmit, Sponge Vanilla|Sponge Forge|Sponge API
Gui, Home:Add, Button, x245 y245 w43 h23 gGuiHomeSubmit, Next
Gui, Home:Add, Button, x290 y245 w43 h23 gHomeGuiClose, Close

Gui, SpongeInstall:Hide
Gui, Home:Show, w336 h271, Sponge Installer
return

SpongeInstallGuiClose:
HomeGuiClose:
ExitApp

GuiHomeSubmit:
Gui, Home:Submit
SpongeInstall: 
Gui, SpongeInstall:New
Gui, SpongeInstall:Add, Text, x15 y15 w295 h20, % "Please select the version of Sponge " . (Sponge = 1 ? "Vanilla" : Sponge = 2 ? "Forge" : "API") .  " you want to install"
Gui, SpongeInstall:Add, DropDownList, x15 y40 w120 vSpongeVersion Choose1, % (Sponge = 1 ? VanillaVersions : Sponge = 2 ? ForgeVersions : APIVersions)
Gui, SpongeInstall:Add, Edit, x15 y175 w245 h25 vLocation ReadOnly,
Gui, SpongeInstall:Add, Text, x15 y150 w255 h25, Please select the location you want it to be installed
Gui, SpongeInstall:Add, Button, x260 y175 w30 h25 gChooseLocation, ....
Gui, SpongeInstall:Add, Button, x290 y245 w43 h23 gSpongeInstallGuiClose , Close
Gui, SpongeInstall:Add, Button, x245 y245 w43 h23 gOpenDownloadSite, Next
Gui, SpongeInstall:Add, Button, x200 y245 w43 h23 gHome, Back
Gui, SpongeInstall:Show, w336 h271, % "Sponge " . (Sponge = 1 ? "Vanilla" : Sponge = 2 ? "Forge" : "API") . " Installer"
return


ChooseLocation:
FileSelectFolder, Location,,3,Please select the location you want it to be installed
GUIControl,,Location, %Location%
Return

OpenDownloadSite:
Gui, SpongeInstall:Submit, NoHide
IF (Location) {
	URL := (Sponge = 1 ? VanillaLinks : Sponge = 2 ? ForgeLinks : APILinks)[SpongeVersion]
	IF (URL != "NONE") {
		useFileName := RegExReplace(URL, ".*/")
		URLDownloadtoFile, %URL%, % Location . "\" . useFileName
		}
	ELSE
		MsgBox,,, Stable Version doesn't exist
}
ELSE
	MsgBox, A location is needed before i can install!
Return

Yes:
;UrlDownloadToFile, https://github.com/SkrillexAkaCraft/FiestaOnline/raw/master/price_checker.exe, %A_Workingdir%\Fiesta Online Price Checker.exe 
gosub Run
return


Run:
Run, %A_Workingdir%\%product%.exe
ExitApp
