# FS22-heighttypes-increase
## Anleitung zum Erhöhen der heighttypes von 64 auf 128

English version down below!

Gestartet wird mit einer entpackten (**kein zip**) Karte. Es darf sich auch keine gepackte Version im selben Verzeichnis befinden, da der Editor sonst diese lädt!

1) **"maps/data/densityMap_height.gdm"** mit GRLE-Konverter (Download unter https://gdn.giants-software.com/downloads.php) in PNG konvertieren, Original aus dem Map-Ordner löschen. (**Achtung:** Pfad kann abweichen)

2) i3D mit Texteditor bearbeiten, nach **densityMap_height** suchen und die am Anfang der Zeile notierte **fileId** merken

3) sollte die Datei als **densityMap_height.gdm** aufgeführt sein, dann muss dies angepasst werden zu **densityMap_height.png**

4) nach **terrainDetailHeight** suchen, diese muss als Attribut ***densityMapId*** die gleiche Id haben wie die **fileId** aus Schritt 2

Beispiel:
```xml
<DetailLayer name="terrainDetailHeight" densityMapId="339" numDensityMapChannels="12" compressionChannels="6" cellSize="8" objectMask="16711935" decalLayer="2" materialId="135" viewDistance="75" blendOutDistance="5" densityMapShaderNames="blendMap" combinedValuesChannels="0 6 0" heightFirstChannel="6" heightNumChannels="6" maxHeight="4"/>
```

**numDensityMapChannels="12"** und **compressionChannels="6"** bedeutet hier die Karte hat aktuell 64 heighttypes

5) innerhalb dieser Zeile werden nun folgende Einträge angepasst

| Vorher | Nachher |
|--------|---------| 
| numDensityMapChannels="12" | numDensityMapChannels="14" |
| compressionChannels="6" | compressionChannels="7" |
| combinedValuesChannels="0 6 0" | combinedValuesChannels="0 7 0" |
| heightFirstChannel="6" | heightFirstChannel="7" |
| heightNumChannels="6" | heightNumChannels="7" |

```xml
<DetailLayer name="terrainDetailHeight" densityMapId="339" numDensityMapChannels="14" compressionChannels="7" cellSize="8" objectMask="16711935" decalLayer="2" materialId="135" viewDistance="75" blendOutDistance="5" densityMapShaderNames="blendMap" combinedValuesChannels="0 7 0" heightFirstChannel="7" heightNumChannels="7" maxHeight="4"/>
```

6) in der Datei **densityMapHeightTypes.xml** (vorangestellt kann ein map_ oder der Name der Karte sein) folgenden Eintrag suchen

```xml
<densityMapHeightTypes firstChannel="0" numChannels="6">
```

diesen ändern zu 
```xml
<densityMapHeightTypes firstChannel="0" numChannels="7">
```

7) Sollte keine **densityMapHeightTypes.xml** in der Karte existieren, dann muss in der **map.xml** (Name kann abweichen) der Eintrag zu **densityMapHeightTypes.xml** gesucht werden
   Ist dieser auskommentiert oder verweist auf den **§data/...** muss die Datei aus dem Installationsverzeichnis (Pfad kann abgelesen werden) in die map kopiert werden.
   Danach muss der Pfad zur **densityMapHeightTypes.xml** natürlich auf den neuen Speicherort angepasst werden; in der Regel **<densityMapHeightTypes  filename="maps/densityMapHeightTypes.xml" />** (Pfad kann abweichen)

9) Map im Giants Editor laden, Log auf Fehler prüfen. Wenn erfolgreich (keine Fehler) wieder abspeichern. Dann hat man eine neue **densityMap_height.gdm** und die PNG im "maps/data" kann gelöscht werden.

## 2024-04-13

Aktuell kommt es bei Benutzung des Mods FS22_enhancedMixerWagons zu einem Fehler und es erfolgt eine Log-Ausgabe, als habe man das Maximum an heighttypes erreicht (Error: addDensityMapHeightType: maximum number of height types already registered.). Dies wird daurch verursacht, dass in diesem Mod selbst nochmal eine **densityMapHeightTypes.xml** enthalten ist die aktuell leider die Einstellungen auf die Standarwerte zurücksetzt. Bis der Mod gefixt wurde kann man sich selbst mit einem kleinen Fix der Datei behelfen.
Pfad zur Datei: FS22_enhancedMixerWagons\data\fillTypes\densityMapHeightTypes.xml

```xml
<densityMapHeightTypes firstChannel="0" numChannels="6">
```

ändern zu 
```xml
<densityMapHeightTypes>
```


## 2024-05-21

Der Mod FS22_enhancedMixerWagons (1.0.1.0) wurde gefixt und der Fehler oben (2024-04-13) sollte nun nicht mehr auftreten.


# FS22-heighttypes-increase
## Instructions for increasing heighttypes from 64 to 128

You start with an unzipped (**no zip**) card. There must not be a packed version in the same directory, otherwise the editor will load it!

1) Convert **"maps/data/densityMap_height.gdm"** to PNG using the GRLE converter (download at https://gdn.giants-software.com/downloads.php), delete the original from the map folder. (**Attention:** Path may vary)

2) Edit i3D with a text editor, search for **densityMap_height** and note the **fileId** noted at the beginning of the line

3) If the file is listed as **densityMap_height.gdm**, then this must be adjusted to **densityMap_height.png**

4) Look for **terrainDetailHeight**, this must have the same ID as the ***densityMapId*** attribute as the **fileId** from step 2

example:
```xml
<DetailLayer name="terrainDetailHeight" densityMapId="339" numDensityMapChannels="12" compressionChannels="6" cellSize="8" objectMask="16711935" decalLayer="2" materialId="135" viewDistance="75" blendOutDistance="5" densityMapShaderNames="blendMap" combinedValuesChannels="0 6 0" heightFirstChannel="6" heightNumChannels="6" maxHeight="4"/>
```

**numDensityMapChannels="12"** and **compressionChannels="6"** means the map currently has 64 heighttypes

5) innerhalb dieser Zeile werden nun folgende Einträge angepasst

| before | after |
|--------|---------| 
| numDensityMapChannels="12" | numDensityMapChannels="14" |
| compressionChannels="6" | compressionChannels="7" |
| combinedValuesChannels="0 6 0" | combinedValuesChannels="0 7 0" |
| heightFirstChannel="6" | heightFirstChannel="7" |
| heightNumChannels="6" | heightNumChannels="7" |

```xml
<DetailLayer name="terrainDetailHeight" densityMapId="339" numDensityMapChannels="14" compressionChannels="7" cellSize="8" objectMask="16711935" decalLayer="2" materialId="135" viewDistance="75" blendOutDistance="5" densityMapShaderNames="blendMap" combinedValuesChannels="0 7 0" heightFirstChannel="7" heightNumChannels="7" maxHeight="4"/>
```

6) Look for the following entry in the file **densityMapHeightTypes.xml** (preceded by a map_ or the name of the map).

```xml
<densityMapHeightTypes firstChannel="0" numChannels="6">
```

edit to
```xml
<densityMapHeightTypes firstChannel="0" numChannels="7">
```

7) If no **densityMapHeightTypes.xml** exists in the map, then the entry for **densityMapHeightTypes.xml** must be searched for in the **map.xml** (name may differ).
   If this is commented out or refers to **§data/...**, the file must be copied from the installation directory (path can be read) into the map.
   Afterwards, the path to **densityMapHeightTypes.xml** must of course be adjusted to the new storage location; usually **<densityMapHeightTypes filename="maps/densityMapHeightTypes.xml" />** (path may vary)

9) Load map in Giants Editor, check log for errors. If successful (no errors) save again. Then you have a new **densityMap_height.gdm** and the PNG in “maps/data” can be deleted.

## 2024-04-13

Currently, when using the mod FS22_enhancedMixerWagons, an error occurs and a log output is displayed as if the maximum number of heighttypes had been reached (Error: addDensityMapHeightType: maximum number of height types already registered.). This is caused by the fact that this mod itself contains another **densityMapHeightTypes.xml** which unfortunately resets the settings to the default values. Until the mod has been fixed, you can help yourself with a small fix to the file.
Path to the file: FS22_enhancedMixerWagons\data\fillTypes\densityMapHeightTypes.xml

```xml
<densityMapHeightTypes firstChannel="0" numChannels="6">
```

change to
```xml
<densityMapHeightTypes>
```


## 2024-05-21

The mod FS22_enhancedMixerWagons (1.0.1.0) has been fixed and the error above (2024-04-13) should no longer occur.
