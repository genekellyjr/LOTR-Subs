# LOTR-Subs
*Made whilst wasting on Arwen's wasting pillow*

## How to use
* Choose disc1/disc2 or the combined PGS subs (.sup file).

*If choosing **combined PGS subs**, make sure your combined is the same as mine since the timings will be off slightly for disc2 stuff if not.*

*You can generate your own PGS subs instead of using the release ones I made by opening the .srt file in Subtitle Edit and then use MKVToolNix's GUI to replace the original subtitles with the appropriate .sup file for the appropriate movie or movie part.*

*You can also embed the .srt file instead of the .sup file. The .sup file is blu-ray PGS subtitles which are pictures and look nice, while the .srt file is just text and it's up to your player to decide how to show them. I haven't done any work on positioning the .srt subtitles, just making sure they're right.*

* Use MKVToolNix to "Add as new source files..." the .SUP (or .SRT) files, set your subtitle options as needed (default, forced for transNonEnglish), optionally delete the original subtitles (trans subs include all original subtitles with added Elvish/other languages), change save name at bottom, and hit the "Start multiplexing" button.

### FOTR Extended Specs
* 1080p USA blu-ray discs (set w/ embedded Sindarin text occasionally). 
* If using combined they must follow the FOTR combining instructions or else things will be off. The combined runtime is 3:48:10.744, 328250 frames, no gap between disc1/2 transition.

*Note that for 4K blu-rays you'd have to remake the subs from the SRT file with `Video res` in Subtitle Edit set to UHD. I don't have the 4k blu-rays so I can't know if the font changed/was adjusted at all/etc. The timings for the subtitles *should* be the same, at least.*

## Help translate anything missing!

If you notice anything missing a translation, note the movie, time, and disc# or combined and open an issue or find an issue for it already. Hopefully I can find someone translating it (since I am but a laylad) or be graced with someone who can translate it.

## FOTR Extended Combine Discs 1 & 2 Instructions

*Also note that it's possible to adjust the time stamps of the combined .srt file's 2nd disc subtitles to align to your combined timing. (hint: put an empty subtitle that ends 24 ms before the time you want to align to, then paste in disc 2 subtitles so they're timed right)*

### Color Correction & Combine
#### Color Correct
This is needed since the colors in FOTR are abs bjorked.

* Follow the guide https://www.howtogeek.com/238725/how-to-fix-the-green-tint-in-the-lord-of-the-rings-fellowship-of-the-ring-extended-edition-blu-ray/ there, use the Web Archive to access any files you can't get.
* *Note that you should use https://github.com/AviSynth/AviSynthPlus instead of the old AviSynth since it's modern (should be faster) but also completely compatible for this.*
* *Note that if you want to encode with H.265 10-bit (small file size, good quality, 10-bit reduces banding): choose x265, set it to Constant Quality 18, Preset Slow, and add these custom options (2nd tab at top of window): for d1 `--profile main10 --no-strong-intra-smoothing --no-rect --aq-mode 1 --qpfile "C:\path\to\D1-pause.txt"` and for d2 `--profile main10 --no-strong-intra-smoothing --no-rect --aq-mode 1 --no-open-gop --qpfile "C:\path\to\D2-pause.txt"` (note they are different!)*
* *Note that for combining following the guide in combo with if you ?keep the commentary tracks? the audio is off by 1 second on the disc 2 stuff. You need to make cut versions of Disc 1 and 2 then append them together, detailed in the Combine section just a bit down. If just the movie audio you are probably OK to do it all in 1 shot per the link above.*

<sup><sub>Shout out to Pascal @ https://gitlab.com/mbunkus/mkvtoolnix/-/issues/2990 for noting the issue was default open GOP (whatver that is). It's no problem for disc 1 b/c it counts from the start of the file, but disc 2 gets cut and references non-existant earlier stuff and goes bad, so --no-open-gop it is for disc 2!</sup></sub>

* *Note that if you get a `DirectShowSource` **error** when trying to use the `.avs` file with MeGUI, go download and install LAV Filters from https://forum.doom9.org/showthread.php?t=156191 OR find "MatroskaSplitter" and install it. I guess it's a codec thing?*

#### Combine

*The multi-step way below will not have any timing issues, but it is more steps than the 1-shot. Esp. use if you're keeping the commentary tracks.*

Per agressiv @ https://forum.makemkv.com/forum/viewtopic.php?p=100657#p100657: *Note their frame #s are off because they missed that MPC-HC counts from 0 as 1st frame while MKVToolNix counts from 1 as 1st frame and that MKVToolNix's ranges are inclusive, so they're off by 2 frames but otherwise right.*

* Rip each extended disk to its own MKV, for example, LOTR1d1.mkv and LOTR1d2.mkv
* Drag Disc 1 into MkvToolNix by itself
* (Add Color Corrected version if using it and disable the H.264 original video)
* Go into the Output tab.
* Change Split mode from Do not split to After frame/field numbers
* Use frame# **151969 for disc 1** and frame# **48 for disc 2**.
* The destination file can be LOTR1d1-clipped.mkv as an example.
* When you click Start multiplexing, it will create two files - LOTR1d1-clipped-001.mkv and LOTR1d1-clipped-002.mkv
* Repeat for Disc 2.
* You'll see that for the first disc, -002 will be just a couple of seconds of black, while for the second disc, -001 will be just a couple of seconds of black.
* Create a new Multiplexer, and drag LOTR1d1-clipped-001.mkv to the list. Right click that video, and do Append files and click LOTR1d2-clipped-002.mkv.
* Make sure the Output section's Split Mode is set to "Do not split", you can rename in the Output sections' File Title
* Click Start multiplexing and verify the output.

*This is the 1-shot way, it will fail if you have commentary tracks since I guess one of them is a bit long so the audio gets offset or something.*

* In MKVToolNix "Add as new source files..." the disc 1 movie, the d1 color corrected mkv (if using it, and disable movie's x264 version), and either the d1 translated subs (can add them later tho via the combined) or directly go for the combined (do not append d2 trans subs to that). Then "Append" (right click thing you want to append to, choose Append) the d2 movie to the d1 movie, the d2 color corrected to the d1 color corrected, and the d2 subs to the d1 subs.

* In MKVToolNix go to the Output tab's Splitting section set the Split Mode to "By parts based on frame/field numbers".

* Put in the box: `-151968,+152138-`

* Click "Start multiplexing"

<sup><sub> *1st number goes up to last movie frame (151968) and splits at 151969 (first black frame which is set as the key frame). 2nd number is based on 152090 total frames in Disc 1 plus 48, so it starts a split at 1st movie frame in d2 (48) and goes from there. Identify frames in MPC-HC via CTRL+G, note it counts from 1st frame 0 while MKVToolNix counts from 1st frame 1, so you need to add 1 to whatever you find.* </sub></sup>
  
## TTT Extended Combine Discs 1 & 2 Instructions
**For: Combined TTT Extended Edition ripped from USA blu-ray discs (set w/ embedded Sindarin text occasionally), 3:55:24 runtime combined**
Note that for 4K blu-rays you'd have to remake the subs from the SRT file with `Video res` in Subtitle Edit set to UHD.

Per agressiv @ https://forum.makemkv.com/forum/viewtopic.php?p=100657#p100657 for TTT
```
Two Towers
Disc 1 - 153307
Disc 2 - 48
```
*Note that I disagreed with 46, which is the last black frame. The ranges are inclusive per https://mkvtoolnix.download/doc/mkvmerge.html so keeping 1 black frame didn't make sense - may change if key frame is at 46 or something*

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

## ROTK Extended Combine Discs 1 & 2 Instructions
Per agressiv @ https://forum.makemkv.com/forum/viewtopic.php?p=100657#p100657 for ROTK
```
Return of the King
Disc 1 - 183542
Disc 2 - 48
```
*Note that I disagreed with 46, which is the last black frame. The ranges are inclusive per https://mkvtoolnix.download/doc/mkvmerge.html so keeping 1 black frame didn't make sense - may change if key frame is at 46 or something*


## Process to translate yourself
* MKVToolNix's `mkvmerge.exe` & `mkvextract.exe` to extract PGS subtitles from combined blu-ray rip. (I open a CMD window in the MKVToolNix folder and work from there, type `cmd` in Explorer address bar when in the MKVToolNix folder to open a CMD window in said folder)
```
mkvmerge -i "C:\path\to\LORT FOTR_d1.mkv"

>identify subtitle ID #

mkvextract "C:\path\to\LORT FOTR_d1.mkv" tracks #:"C:\path\to\LORT FOTR_d1.sup"

mkvextract "C:\path\to\LORT FOTR_d2.mkv" tracks #:"C:\path\to\LORT FOTR_d2.sup"
```
* Subtitle Edit's Tesseract 5 OCR to convert to SRT with correct timings. Edit each line manually, many I's are |'s, misses most accent marks. Better than bianary.
* Save SRT as original. Save as SRT as translated for edits.
* Load in the movie to Subtitle Edit, use FOTR/TTT/ROTK subs from https://subscene.com/u/1418112 as a guide for general times Sindarin/Quenya/Black Speech happen (timings aren't quite right due to Disc1+Disc2 combo differing prob idk).
* Add them all in painfully. Pre-embedded subs require Sindarin to be on 1 line only.
* Use resources (below) to check translation quality, catch few missing translations.
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
Export, use MKVToolNix (`mkvtoolnix-gui.exe`) to merge, remove old subs (or keep and rename/remove default tag)!


## Resources per movie
### FOTR
http://www.arwen-undomiel.com/elvish/fotr.html & https://www.elvish.org/gwaith/movie_fotr.htm

The Lament for Gandalf needs extra crutches:
* Soundtrack from https://youtu.be/5VA0s8kOc1Y?t=442

* Words to the non-extended version of the soundtrack https://www.youtube.com/watch?v=vgN0ydtrnbo

* Sheet music page 1 https://web.archive.org/web/20230107014344/https://www.musicnotes.com/images/productimages/large/mtd/MN0041737.gif

* Sheet music page 2 https://web.archive.org/web/20230107014254/https://cdn.shopify.com/s/files/1/0017/6760/4339/products/84c32bde7d375fec4fd1c5d0df0a1a74_1024x1024.png?v=1618329648

* Official words and translation https://web.archive.org/web/20221209124726/https://www.elvish.org/gwaith/pdf/fotr_annotated_score_2.pdf

* Unofficial words and translation (#10 notes and #11) https://web.archive.org/web/20221126204330/https://www.elvish.org/gwaith/movie_soundtrack_fotr.htm

### TTT
http://www.arwen-undomiel.com/elvish/ttt.html & https://www.elvish.org/gwaith/movie_ttt.htm

### ROTK
http://www.arwen-undomiel.com/elvish/rotk.html & https://www.elvish.org/gwaith/movie_rotk.htm

### Black Speech resources

List of all known words https://web.archive.org/web/20180501031101/http://folk.uib.no/hnohf/o2.htm

Translated Black Speech score (used in at least 1 scene as words) https://www.elvish.org/gwaith/pdf/fotr_annotated_score_2.pdf at "BLACK SPEECH RING-VERSE" on page 17

## Style Guide

### 1st line of Elvish w/ baked-on translations
```
[IN SINDARIN] (Suilad.)
```

```
PERSON [IN SINDARIN]: (Suilad.)
```

### Missing baked-on translations
```
[IN SINDARIN] [Frodo is dying.] (Frodo fîr. Suilad.)
```

### Fully missing translations
```
PERSON [IN SINDARIN]: Hi.
(Suilad.)
```

```
[IN SINDARIN] Hi.
(Suilad.)
```

```
VOICE OF THE RING [WHISPERS IN BLACK SPEECH]: <i> Sauron...
(Zigur...)</i>
```

### Song
```
Words words words

Words words words
```
Punctuation not needed for verses.

```
[SINGING IN SINDARIN] <i> O Queen beyond the Western Seas!
(A Bereth thar Ennui Aeair!)</i>
```

```
STRIDER [HUMS IN SINDARIN]: <i> Tinúviel the elven-fair
(Tinúviel elvanui)</i>
```

### Continued sentences
```
<i>All you have to decide...</i>

...is what to do with the time
that is given to you.
```

### All italicized text needs an extra space after the `<i>` for it to show correctly in the blu-ray PGS .sub output
```
PERSON: <i> Hello.
Hi. </i>
```
(but not the very first `GANDALF: <i>You cannot pass!...` in TTT for ?reasons?)
