# LOTR-Subs
*Made whilst wasting on Arwen's wasting pillow*

## FOTR Extended
### Color Correction
This is needed since the colors in FOTR are abs bjorked.
* Follow the guide https://www.howtogeek.com/238725/how-to-fix-the-green-tint-in-the-lord-of-the-rings-fellowship-of-the-ring-extended-edition-blu-ray/ there, use the Web Archive to access any files you can't get.
* *Note that if you want to encode with H.265 10-bit (small file size, good quality, 10-bit reduces banding), choose x265 and add these custom options: `--profile main10 --no-strong-intra-smoothing --no-rect --aq-mode 1 --qpfile D1-pause.txt` (change `D1-pause.txt` to `D2-pause.txt` for disc 2)*
* *Note that if you get a `DirectShowSource` **error** when trying to use the `.avs` file with MeGUI, go download and install LAV Filters from https://forum.doom9.org/showthread.php?t=156191 OR find "MatroskaSplitter" and install it. I guess it's a codec thing?*

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
