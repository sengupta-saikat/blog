---
title: "Automatically Copy Advent-of-Code Sample Data"
author: ["Saikat"]
date: 2022-12-12
draft: false
description: "Tampermonkey Userscript to Automatically Copy Advent-of-Code Sample Data"
tags: ["advent-of-code", "userscript", "tampermonkey"]
categories: ["TIL"]
---

```javascript
// ==UserScript==
// @name         aoc-copy-test-input
// @namespace    http://tampermonkey.net/
// @version      0.1
// @description  Copy the sample test input for AoC puzzles
// @author       You
// @match        https://adventofcode.com/*/day/*
// @icon         https://www.google.com/s2/favicons?sz=64&domain=adventofcode.com
// @grant        none
// ==/UserScript==
(function() {
    'use strict';
    let day = parseInt(window.location.pathname.split('/').pop());
    let url = `https://adventofcode.com/2022/day/${day}/input`;
    async function copyContent () {
        try {
            const response = await fetch(url);
            response.text().then(function (text) {
                navigator.clipboard.writeText(text);
            });
            console.log('Content copied to clipboard');
        } catch (err) {
            console.log('Failed to copy: ', err);
        }
    }
    copyContent();
})();
```
