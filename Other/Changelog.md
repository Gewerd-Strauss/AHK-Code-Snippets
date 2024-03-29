# Changelog
v. 07.31.1
- found bug not rendering the first snippet of the first library loaded not being cut correctly → "Examples"- and "Description"-Blocks are not cut for the very first snippet of whatever library is loaded at first
	- [x] regex.Description and Regex.Example does not seem to work uniformly.
		- specifically: any description or example fields in the first-to-be-loaded file will not be found and treated properly. For unknown-to-me reasons, the fields are only correctly found and removed/ingested from file2 onwards) - 
		- #important fixed by force-converting "\`r\`n" to "\`n" immediately after `FileRead()`. I have no clue why these identical files are being read back with different newline formatting, but they are. Might be some include changing formatting behaviour of ahk?? Check up on that idea.
Additions:
- [x] add warning when combining fuzzy and regex search as the fuzzy search is ignored in that case.
- [x] Attach tooltips to various controls



- [x] Small performance increases by small changes - preallocating total row number to LV-Creation and other small tidbids. 
- [x] implement regex-search
- [x] search by snippetID and secID and Instr()/Regex()-searches combined
	- [x] make the search-keys `s:` and `ID:` case-agnostic


Fixes: 
- [x] Fix: Slightly reduced number of loops required by combining two operations in fPopulateLV
- [x] Fix: Clicking the Descriptionbox will copy the currently selected Snippet
- [x] Fix: Single-clicking an item in the LV will not populate the DescriptionBox/RC-Fields, double-clicking was required
- [x] Fix: made snippet search regexes for ID:/s: caseinsensitive
- [x] Fix: Figure out how the fuck the tab3 is supposed to work - because clearly enough it does not work at all.
- [x] Fix: bars here not wrapping properly, as well as the text somehow not wrapping properly ![[Documentation/Pasted image 20220711090346.png]]
- [x] Fix: figure out why the description text of snippet 2 is cut off although there is still space left.
- [x] Fix: figure out why the description text of snippet 2 is cut off although there is still space left.
- [x] at 1080 screen sizing the textfield of the red "xx snippets loaded" will cut over the boundary of the groupbox control
- [x] at 1080 screen sizing the richEdit-fields will cut over the boundary of the tab control
	- Numpad9 acts as a toggle to switch between 1080p-size and the size autoscaled from current monitor's res.
- [x] slightly reduced looping time in fPopulateLV by combining several loops over `Snippets`.

v.16.07.2022-1
- started performance testing to check how viable a rewrite might be for reducing the amount of looping. 
	- created a new branche, speed-Test() for... well speed testing.
	- all library files together  now contain a baseline of 1000 scripts
	- added matlab code for evaluating Code Performance, as well as evaluating code performance under different loading/storage mechanism
v. 14.07.2022-1
- added a bunch of performance changes to most loops
- removed more redundant code.
- combined some loops to reduce overall bootup time
v.13.07.2022-3
- removed some irrelevant code
- added hostring `alib.s` to open GUI- added hostring `alib.s` to open GUI^[previously only possible via Numpad0, which is kinda hard on a mobile 13"-laptop]
- added a few comments on particularly weird stuff, or todo's for later
- renamed `f_IncorporateHash` to `f_IncorporateHashAndFilename`
- moved code out of `f_IncorporateHashAndFileName` into `f_AddHashedFilePath`  - not entirely happy with the current solution either
- added `CodeTimer()` to benchmark the bootup process
- renamed `fCreateIniObj()` to `fCreateSectionNames()` because it has really _nothing to do with an Ini-Object anymore.
- removed unused ini-files

---
v.13.07.2022-2
- removed various instances of clipboard overwriting for testing reasons. Still left in code for possible debug later on, but right now disabled.
- [x] Incorporate Library-Name into Snippet Info during fParseSnippet, then populate the LV field respectively. 
	- added Library-Name to the Listview. Might make it hidable because the information it gives is limited, and only really relevant when you need to figure out where a snippet is located. For that however I could just as well straight out output the snippet-object or just have the file open automatically.
- [x] fixed bug introduced in v.13.07.2022-1 which made a regex-needle unusable.
---
v.13.07.2022-1
- [x] Collect all regex needles in an object at script-start to prevent accidental variation between occurences
- [x] fix the RichCode highlighter not working
---
v.12.07.2022-2
- [ ] tested updater, currently apparently bugged to create unreadable library-files when used to download them.
- [x] fixed needles not removing description/example blocks


- removed old test files

---
v.12.07.2022-1
Additions: 
- [x] search by snippetID and secID and Instr()/Regex()-searches combined

Fixes
- [x] Fix lSearchSnippets searching in the unfixed file string, where snippet ID's are not aligned → must search in Snippets[]-Object Instead
- [x] Fix fLoadFiles to load several source-files together from script.config.libraries into the same GUI

---
v.11.07.2022-3
- fixed GUI not autofocussing on LV when reopening.
- fixed snippets with identical names overwriting each other by creating unique hashes as identifying keys instead of snippet-name
	- [x]		Seems completed, needs to be tested.			 URGENT: Fix the Structure of Snippets[] to not use the snippet name alone as Key → multiple snippets with identical name (but. f.e. different descriptions) will overwrite each other. 
		- Suggestion: make a hash-key out of the library-file 
- removed unnecessary code
- fixed searching by ID working properly, but feeding the wrong ID into the listview when displaying the result




---
v.11.07.2022-2
- build up overview on scope I intend to reach. Stuff might be added or cut from that roadmap as I progress.
---
v.11.07.2022-1
- made gui completely scaleable (have not set lower limits for minimum required sensible size yet)
	- fixed some scaling shenanigans
- [x] Fix this fucking scaling here:![[Documentation/Pasted image 20220711090257.png]]
---
v.10.07.2022-1
- various bugfixes

Additions
- added sorting array in LV based on Section
- added support to load from multiple files simultaneously
	- each file can start indexing at 1 to be usable alone as well. The script aligns snippet indices across all included files when booting up, and uses those as reference
- added mode to continuously number snippets in their respective sections from 1-n. Might disable the legacy mode at some point.
- allows searching by `Index` and `SectionID`: search by key `ID:%Number%` to search by snippet index, and use search "s:Number" to search for a specific section. Currently no combination with other search parameters are possible, but it is intended.SectionID-searching does not allow searching by section `ID:%SectionName%`
- displays number of loaded snippets, as well as number of matches when searching
- index now padded to the length of the number `Snippets.Count()`
- added several library files to test library merging.

Misc
- changelog arbitrarily started now. Versioning arbitrarily started now, following format dd.MM.yyyy-Commit


---

v0.1 - v10.07.2022-3
- basic build. 