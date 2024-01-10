# Howto export a Logseq page to PDF or epub
- Open the Logseq-Seite in a Text Editor like VS Code by clicking the ...-menu in the top right and selecting 'Open in default application'
- Copy it's content to an new file, e.g. `~/publish-logseq/doc.md`
- Open the containing folder in Terminal with `cd '~/publish-logseq/'`
- Run this script with `pandoc -V lang=de doc.md --filter logseq2md.py --output doc.md`. The language setting is neccesary for correct hyphenation.
- Sadly, this script removes the header (if existing). Copy and paste it from the original file. I use this one:
```
---
geometry: "left=0.5cm,right=1.5cm,top=1cm,bottom=1.5cm"
documentclass: extarticle # needed for fontsize
fontsize: 12pt # or 14pt
mainfont: Source Sans Pro # needs `--pdf-engine xelatex`
---
```
- Sadly, the script wraps Latex Code like `\hyphenation{Fra-ming}` with `. Remove them.
- Run `pandoc --pdf-engine xelatex --lua-filter columns.lua doc.md -o out.pdf`
- I like a two column layout. For that I copied the `columns.lua` file from https://github.com/dialoa/columnsThe in the folder and ran instead `pandoc --pdf-engine xelatex --lua-filter columns.lua doc.md -o out.pdf` and wrapped the part of my text which should me multi-column with `:::`.
- For epub export:
  - in the header add "title: MeinTitel"
  - `pandoc --epub-title-page=false doc.md --output doc.epub`
