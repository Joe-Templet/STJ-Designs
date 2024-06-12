---
aliases: 
tags: 
template: "[[(Folder Note) Template]]"
type: "[[0_Meta/Folder Notes|Folder Notes]]"
title: 2402-64px_Chips
description: 
icon: 💡
---
# 2402-64px_Chips

## Project

[[../23-History-AlSTJv2/AlSTJv2_Stephan_231018.pptx|AlSTJv2_Stephan_231018.pptx]]
[[../23-History-AlSTJv2/AlSTJv2_Stephan_2310247.pptx|AlSTJv2_Stephan_2310247]]
- 64 pixels require 128 pads
	- 128/4 = 32 pads per side
	- 32 * 250 / 1000 = 8 mm sides
	- **or 200?**
		- 32 * 200 / 1000 = 6.4 mm of pad.

## Current Contents
%% These are all the files in the current folder. Copy and Paste this table into Replicates, then run Search and Replace to remove `app://obsidian.md/`  
This makes the table permanent.  
Be sure to update Replicates with new rows as new files are created. %%

```dataview
table file.type as "Type"
where file.folder = this.file.folder
where file.path != this.file.path
```

---

```dataviewjs
const thisfolder = dv.current().file.folder
// File Objects (basneame, path, parent object, vault object, stat times)
let files = dv.array(
	app.vault.getFiles().filter(
		f=>f.path.includes(thisfolder)
	).filter(f=>f.path != dv.current().file.path)
)
// Page Objects
let pages = dv.pages().filter(f=>f.file.path.includes(thisfolder)).filter(f=>f.path != dv.current().file.path)
// Get subdirectory (relative to this Folder Note).

function bounds(stats, bound) {
	let late = stats.mtime
	let early = stats.ctime
	let lkey = 'mtime'
	let ekey = 'ctime'
	let all = {}
	let tzFormat = new Intl.DateTimeFormat('en-US',
			{timeZoneName: "short"})
	let timeFormat = new Intl.DateTimeFormat('en-US', 
			{hour:'2-digit', minute:'2-digit', second:'2-digit', hour12: true}
		)
	let toOutput = (f=>[
				f.toDateString(),(
					timeFormat.format(f)
					+" ("
					+tzFormat.formatToParts(f).find(p=>p.type === 'timeZoneName').value
					+")"
				)
			])
	for (const key of Object.keys(stats)) {
		if (key.endsWith('time')) {
			[late, lkey] = stats[key] > late ? [stats[key], key] : [late, lkey]
			[early, ekey] = stats[key] < early ? [stats[key], key] : [early, ekey]
			let date = new Date(stats[key])
			all[key] = toOutput(date)
		}
	}
	let eDate = new Date(early)
	let earlyOut = toOutput(eDate)
	let lDate = new Date(late)
	let lateOut = toOutput(lDate)
	switch (bound) {
		case "e":
			return {[ekey]: earlyOut}
		case "l":
			return {[lkey]: lateOut}
		case "b":
			return {["(Earliest )"+ekey]: earlyOut, ["(Latest) "+lkey]: lateOut}
		case "a":
			return all
		default:
			console.log("(e), (l), or (b) supported.")
			}
}

function tableList(obj) {
	let text = ""
	let iKey = 0
	for (const [key, vals] of Object.entries(obj)) {
		if (iKey>0) {
			text+="<br>"
		}
		text += "**"+key+"**:"
		for (const val of vals) {
			text += "<br>- "+val
		}
		iKey+=1
	}
	return text
}

files = files.map(
	g=>{return {...g,
		subdir: (g.path.replace(thisfolder,"")
				.replace(g.name, "")),
		bounds: tableList(bounds(g.stat, 'a')),
		early: tableList(bounds(g.stat, 'e')),
		late: tableList(bounds(g.stat, 'l'))
		};}
)

for (const group of files.groupBy(g=>g.subdir)) {
	let ob = {}
	dv.span("### Path: `"+group.key+"`\n"+dv.markdownTable(
			['File','Replicate', 'Version', 'Stat: Earliest', 'Stat: Latest'],
			group.rows.map(f=>[
				"["+f.basename+"]("+f.path.replaceAll(" ","%20")+")",
				"["+f.basename+"]("+f.path.replaceAll(" ","%20")+(
	 					f.extension == "md" ? ")" : ".md)"
				),
				f.version,
				f.early,
				f.late,
			])
		)+"\n---"
	)
}
```

## Replicates
%% These are the echoes of files that have moved from one folder to another.

Replicates help track active files as they find their purpose.

After finding their purpose, or dying, replicates should be retired.  
This is typically accomplished by starting a new project. %%

| File | Replicate |
| ---- | --------- |
|      |           |