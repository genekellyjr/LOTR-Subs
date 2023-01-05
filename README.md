# LOTR-Subs
*Made whilst wasting on Arwen's wasting pillow*

## How to use
* Choose disc1/disc2 or the combined PGS subs (.sup file).

*If choosing combined PGS subs, make sure your combined is the same as mine since the timings will be off slightly for disc2 stuff if not.*

*You can generate your own PGS subs instead of using the release ones I made by opening the .srt file in Subtitle Edit and then 

* Use MKVToolNix's GUI to replace the original subtitles with the appropriate .sup file for the appropriate movie or movie part.

*You can also embed the .srt file instead of the .sup file. The .sup file is blu-ray PGS subtitles which are pictures and look nice, while the .srt file is just text and it's up to your player to decide how to show them. I haven't done any work on positioning the .srt subtitles, just making sure they're right.*

## Help translate anything missing!

If you notice anything missing a translation, note the movie, time, and disc# or combined and open an issue or find an issue for it already. Hopefully I can find someone translating it (since I am but a laylad) or be graced with someone who can translate it.

## FOTR Extended
**For: 1080p USA blu-ray discs (set w/ embedded Sindarin text occasionally) - combined per following instructions (so times match) or in original disc 1/2 format**
Note that for 4K blu-rays you'd have to remake the subs from the SRT file with `Video res` in Subtitle Edit set to UHD. I don't have the 4k blu-rays so I can't know if the font changed/was adjusted at all/etc. The timings for the subtitles *should* be the same, at least.

### Color Correction & Combine (or just combine w/ howtogeek's timings - make sure you use the qpfile if not color correcting)
This is needed since the colors in FOTR are abs bjorked.
* Follow the guide https://www.howtogeek.com/238725/how-to-fix-the-green-tint-in-the-lord-of-the-rings-fellowship-of-the-ring-extended-edition-blu-ray/ there, use the Web Archive to access any files you can't get.
* *Note that you should use https://github.com/AviSynth/AviSynthPlus instead of the old AviSynth since it's modern (should be faster) but also completely compatible for this.*
* *Note that if you want to encode with H.265 10-bit (small file size, good quality, 10-bit reduces banding): choose x265, set it to Constant Quality 18, Preset Slow, and add these custom options (2nd tab at top of window): `--profile main10 --no-strong-intra-smoothing --no-rect --aq-mode 1 --qpfile "C:\path\to\D1-pause.txt"` (change `D1-pause.txt` to `D2-pause.txt` for disc 2)*
* *Note that if you get a `DirectShowSource` **error** when trying to use the `.avs` file with MeGUI, go download and install LAV Filters from https://forum.doom9.org/showthread.php?t=156191 OR find "MatroskaSplitter" and install it. I guess it's a codec thing?*

### Process to do yourself:
* MKVToolNix's `mkvmerge.exe` & `mkvextract.exe` to extract PGS subtitles from combined blu-ray rip. (I open a CMD window in the MKVToolNix folder and work from there, type `cmd` in Explorer address bar when in the MKVToolNix folder to open a CMD window in said folder)
```
mkvmerge -i "C:\path\to\LORT FOTR_d1.mkv"

>identify subtitle ID #

mkvextract "C:\path\to\LORT FOTR_d1.mkv" tracks #:"C:\path\to\LORT FOTR_d1.sup"

mkvextract "C:\path\to\LORT FOTR_d2.mkv" tracks #:"C:\path\to\LORT FOTR_d2.sup"
```
* Subtitle Edit's Tesseract 5 OCR to convert to SRT with correct timings. Edit each line manually, many I's are |'s, misses most accent marks. Better than bianary.
* Save SRT as original. Save as SRT as translated for edits.
* Load in the movie to Subtitle Edit, use FOTR subs from https://subscene.com/u/1418112 (thx to the user Dietrich!) as a guide for general times Sindarin/Quenya/Black Speech happen (timings aren't quite right due to Disc1+Disc2 combo differing prob idk).
* Add them all in painfully. Pre-embedded subs require Sindarin to be on 1 line only.
* Use http://www.arwen-undomiel.com/elvish/fotr.html & https://www.elvish.org/gwaith/movie_fotr.htm to check translation quality, catch few missing.
* Any text like: `GANDALF: <i>I am a...` needs an extra space to match the original sub spacing like `GANDALF: <i> I am a...`.
* Identify font family and use BDSup2Sub Enhanced 0.0.9 to make sure new subs visually match originals (do not use/save w/ BDSup2Sub, it drops subtitles silently).

```
Font Family: Arial
Font Size: 66
Video res: 1080p
Align: Center, left justify dialog
Bottom margin: 2%
Border style: Normal, width=3
Frame rate: 23.976
Shadow width: 0
Line height: 72
```
Export, use MKVToolNix (`mkvtoolnix-gui.exe`) to merge, remove old subs!


## TTT Extended
**For: Combined TTT Extended Edition ripped from USA blu-ray discs (set w/ embedded Sindarin text occasionally), 3:55:24 runtime combined**
Note that for 4K blu-rays you'd have to remake the subs from the SRT file with `Video res` in Subtitle Edit set to UHD.

### Process:
* MKVToolNix's `mkvmerge.exe` & `mkvextract.exe` to extract PGS subtitles from combined blu-ray rip.
```
mkvmerge -i "The Lord of the Rings 2 The Two Towers - Extended Edition.mkv"

>identify subtitle ID #

mkvextract "The Lord of the Rings 2 The Two Towers - Extended Edition.mkv" tracks #:extracted.sup
```
* Subtitle Edit's Tesseract 5 OCR to convert to SRT with correct timings. Edit each line manually, most I's are |'s, misses most accent marks. Better than bianary.
* Save SRT as original. Save as SRT as translated for edits.
* Load in the movie to Subtitle Edit, use TTT subs from https://subscene.com/u/1418112 (thx to the user Dietrich!) as a guide for general times Sindarin/Rohirric happen (timings aren't quite right).
* Add them all in painfully. Pre-embedded subs require Sindarin to be on 1 line only.
* Use http://www.arwen-undomiel.com/elvish/ttt.html to check translation quality, catch few missing Sindarin lines at the battle for Helm's Deep.
* Any text like: `GANDALF: <i>I am a...` needs an extra space to match the original sub spacing like `GANDALF: <i> I am a...` (but not the very first `GANDALF: <i>You cannot pass!...` for ?reasons?).
* Identify font family and use BDSup2Sub Enhanced 0.0.9 to make sure new subs visually match originals (do not use/save w/ BDSup2Sub, it drops subtitles silently).

```
Font Family: Arial
Font Size: 66
Video res: 1080p
Align: Center, left justify dialog
Bottom margin: 2%
Border style: Normal, width=3
Frame rate: 23.976
Shadow width: 0
Line height: 72
```
Export, use MKVToolNix (`mkvtoolnix-gui.exe`) to merge, remove old subs!
