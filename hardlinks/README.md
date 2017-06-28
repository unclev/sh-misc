# hardlinks


## Purpose

The script finds hardlinks to regular files within specified filesystem subtrees
by finding files with link count more than 1 and groupping them by inode.

## Usage

``` bash
harlinks [path [path ...]]
```

### Output format
```
<inode1><10 space chars><relative path to filename>
<inode1><10 space chars><relative path to filename>

<inode2><10 space chars><relative path to filename>
 ...
```
### Caution

I would like to warn you against using the script on large file systems.
If hard links are used extensively the script may read lots of files, then sorts them, makes the selection and grouping of the operating system in memory, which may cause very intensive use of system resources.
I would advise you specifying multiple non-overlapping sub-directories at a time instead of an entire partition.

## Known issues

Linux _find_ command is used to retrieve files with hardlinks. The script accepts path arguments and passes them to find.
As well as paths, expressions may be passed to the script, but in this case _find_ would very likely exclude some files with the same inode,
therefore missing some hardlinks. Please be careful when passing options to the script.

## Example
```bash
hardlinks torrents/kinozal.tv/Видео/Фильмы XBMC\ Storage/Video/Desktop\ PC/Фильмы/3D\ *
```

results in

```
52953564          torrents/kinozal.tv/Видео/Фильмы/Зарубежные/Черная бабочка (2017)/Black.Butterfly.2017.P.WEB-DLRip.14OOMB_KOSHARA.avi
52953564          torrents/kinozal.tv/Видео/Фильмы/Зарубежные/Black.Butterfly.2017.P.WEB-DLRip.14OOMB_KOSHARA.avi

52958323          torrents/kinozal.tv/Видео/Фильмы/Зарубежные/Metallica. Сквозь невозможное [Metallica. Through the Never] (2013) 3D (HOU)/Metallica.Through.The.Never.3D.2013.1080p.BluRay.Half-OU.DTS.x264-PublicHD.mkv
52958323          XBMC Storage/Video/Desktop PC/Фильмы/3D (HOU)/Metallica. Сквозь невозможное [Metallica. Through the Never] (2013).3D.TAB.mkv

...

71435239          torrents/kinozal.tv/Видео/Фильмы/Зарубежные/Люди Икс/TheWolverine(2013)3D-halfOU(Ash61)Theatrical.MVOx2/TheWolverine(2013)3D-halfOU(Ash61)Theatrical.MVOx2.mkv
71435239          XBMC Storage/Video/Desktop PC/Фильмы/3D (HOU)/Росомаха. Бессмертный [The Wolverine] (2013).3D.TAB.halfOU(Ash61)Theatrical.MVOx2.mkv

```
