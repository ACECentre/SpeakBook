---
title: SpeakBook Index Page
description: This is a repository to hold a mirror of [Patrick Joyce's SpeakBook project](https://web.archive.org/web/20170325172200/http://www.speakbook.org/) which is sadly no longer accessible on the web. More to follow soon
---
<img src="https://i.imgur.com/FyH8YF2.png" :src="$withBase('/assets/logo.png')" alt="SpeakBook" style="width:100%">

This is a repository to hold the working versions of [Patrick Joyce's SpeakBook project](https://web.archive.org/web/20170325172200/http://www.speakbook.org/). We aim to provide a platform for crowd-sourced version control of future PDF's here. 

To help out with translation into new languages join to [POEditor project here](https://poeditor.com/join/project/wKsMtKRLIj)

[Issues here](https://github.com/acecentre/SpeakBook/issues).  

**Urgent needs**
- German need proofing and more work
- Portuguese has been a Google translation. Certainly isn't right. Needs help. 

[![MIT license](https://img.shields.io/badge/License-MIT-blue.svg)](https://lbesson.mit-license.org/) [![OpenAAC](https://img.shields.io/badge/OpenAAC-💬-red?style=plastic&logoWidth=40&link=https://www.openaac.org)](https://img.shields.io/badge/OpenAAC-💬-red?style=plastic&logoWidth=40&link=https://www.openaac.org)

## Technical Background

This is simply a Vue.js themed template with some scripts to generate a PDF of the document is created. Its designed for chrome as chrome does the PDF generation.  We use a language strings which you can run a PO->Markdown script to convert PO strings to the document. 

### Layout

    .vuepress/
        build-pdf-plugin.js    <-  The pdf build plugin. 
        config.js
        dist/                  <- Where the final build is outputted
        public/                <- Static assets like images sit here and in SpeakBook/
        theme/  
            layouts/
                SpeakBook.vue  <- The main logic for SpeakBook
            styles/
            util/
            fonts/
            components/         

    .scripts/
        common.js
        apply-po-to-md.js     <- Apply a PO Language file to Markdown file. 
        getPOfiles.js         <- NOT WORKING - Grab files from POEditor
        po-from-md.js         <- Make a master PO file from a markdown file.        

    speakbook/
        README.md             <- The English version of SpeakBook

    lang/speakbook/
        README.md             <- Other language versions

### Package scripts

```
# run a local server for development
$ yarn dev
# build it in static html format
$ yarn build
# build pdf format for all pages
$ yarn buildpdf
```

### Language translation scripts

1. Export your PO file from POEditor
2. Convert your language file with the correct strings. e.g. 
```node .scripts/apply-po-to-md.js res/lang/Swedish.po speakbook/README.md > sv/speakbook/README.md```
3. Done!

If you need to make a new POEditor file of terms run
```node .scripts/po-from-md.js speakbook/README.md > res/master.po```


### Script to update all files from POEditor

```
node .scripts/apply-po-to-md.js res/lang/SpeakBook_Spanish.po es/speakbook/README.md > es/speakbook/README2.md && mv es/speakbook/README2.md es/speakbook/README.md 

node .scripts/apply-po-to-md.js res/lang/SpeakBook_French.po fr/speakbook/README.md > fr/speakbook/README2.md && mv fr/speakbook/README2.md fr/speakbook/README.md 

node .scripts/apply-po-to-md.js res/lang/SpeakBook_Portuguese.po po/speakbook/README.md > po/speakbook/README2.md && mv po/speakbook/README2.md po/speakbook/README.md 

node .scripts/apply-po-to-md.js res/lang/SpeakBook_Swedish.po sv/speakbook/README.md > sv/speakbook/README2.md && mv sv/speakbook/README2.md sv/speakbook/README.md 

node .scripts/apply-po-to-md.js res/lang/SpeakBook_German.po de/speakbook/README.md > de/speakbook/README2.md && mv de/speakbook/README2.md de/speakbook/README.md 
```

