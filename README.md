# chm_from_lidar

The CHM from LIDAR plugin creates a Canopy Height Model (CHM) starting from LIDAR data (DTM and DSM First Pulse)


The file *tile_dsm_dtm.gpkg* contains by default data of Regione Veneto (Italy) which has founded this work. Each user can modify the data included in this file with data of their LIDAR survey campaigns.

This plugin is founded by 

![](img/4ISTITUZIONALI.png)

https://psrveneto.it/

Notes for translation:
<b>LINUX</b>
<ul>
<li> add the list of abbreviations of the languages to locales variable in the <b>Makefile</b>, e.g. LOCALES = en it nl de
<li> add all the paths to the files that contains the string to be translated in the <b>Makefile</b>:

SOURCES = \\<br>
........__init__.py \\<br>
........plugin.py plugin_dialog.py

UI_FILES = plugin_base.ui

<li> to translate strings in a .py file this strings have to be within the self.tr() method e.g. self.tr("this is a string"). If the string contains the .format(), only the string has to be managed with the self.tr() method while the .format() part has to be left outside e.g. self.tr("this is a string {}").format("bla")
<li> run from a terminal <b>make transup</b> (linux) in order to create the .ts file (this command will create a .ts file for each abbreviation of the languages added to the LOCALES variable)
<li> open the .ts file (e.g. it.ts) with Qt Linguist
<li> translate all the elements of the GUI and all the strings from the .py file (pay attention to new line symbols, if the original string contains a new line symbol it has to be added also to the translated string). In case of strings with {} due to .format(), the {} have to be added also to the translated string.
<li> save the .ts file
<li> always from Qt Linguist File --> Release to create the .qm file (NB. the .qm file is called by the plugin_name.py file in the init method, pay attention to the declared name of the .qm file)
<li> instead of creating the .qm file from Qt Linguist, it is possible to create it running <b>make transcompile</b> in terminal (linux)
</ul>
Whenever you add/change something in the files/UI you have to run make transup again, translate and recompile the .qm file

<b>NB:</b> We have modified the update-strings.sh file in the scripts folder of the plugin directory. This file initially called the pylupdate4 (line 51) tool but we have to change it with pylupdate5 because of the installed version of Qt.

<b>WINDOWS</b>
<ul>
<li> create a .pro file (Qt project) with the following lines:

SOURCES = __init__.py \\<br>
..........chm_from_lidar_dialog.py \\<br>
..........chm_from_lidar.py

FORMS = chm_from_lidar_dialog_base.ui

TRANSLATIONS = i18n/ChmFromLidar_it.ts\\<br>
...............i18n/ChmFromLidar_de.ts\\<br>
...............i18n/ChmFromLidar_es.ts\\<br>
...............ecc.

the SOURCES variable includes all the .py file which contain strings to be translated, the FORMS variable includes all the .ui file to be translated while the TRANSLATIONS variable includes all the desired languages

<b>NB</b> the .pro file must be saved in the plugin folder

<li> create a .bat file with the following lines:

@echo off<br>
call "C:\OSGeo4W64\bin\o4w_env.bat"<br>
call "C:\OSGeo4W64\bin\qt5_env.bat"<br>
call "C:\OSGeo4W64\bin\py3_env.bat"<br>

@echo on<br>
pylupdate5 ChmFromLidar.pro

the pylupdate5 tool loads the .pro file and creates the .ts file (one for each language added to the .pro file).

Running the .bat file all the specified .ts file will be created in the i18n folder within the plugin directory.

<b>NB</b> the .bat file must be saved in the plugin folder

<li> open the .ts file (e.g. ChmFromLidar_it.ts) with Qt Linguist
<li> translate all the elements of the GUI and all the strings from the .py file (pay attention to new line symbols, if the original string contains a new line symbol it has to be added also to the translated string). In case of strings with {} due to .format(), the {} have to be added also to the translated string.
<li> save the .ts file
<li> always from Qt Linguist File --> Release to create the .qm file (NB. the .qm file is called by the plugin_name.py file in the init method, pay attention to the declared name of the .qm file)