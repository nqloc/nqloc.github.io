---
layout: tools
title: JSON Path Online
categories: [JSON Path Online]
description: JSON Path Online
keywords: JSON Path Online
active: true
---

<div style="font-family: monospace;">
    <input class="row" id="syntax" type="text" placeholder="Put JSONPath syntax" style="white-space: pre; width: 100%; margin: 5px 0;">
    
    <textarea class="row" rows="12" id="input" name="input" placeholder="Input" style="white-space: pre; width: 100%;"></textarea>
    <div class="row" style="margin: 5px 0;">
        <button class="btn blue" onclick="find()">Find</button>
        <button class="btn blue" onclick="copyData('input')" data-toggle="tooltip" title="Copy to clipboard">Copy Input</button>
        <button class="btn orange" onclick="addSample()">Sample</button>
        <button class="btn red" onclick="clearInput()">Clear Input</button>
        <button class="btn red" onclick="clearAll()">Clear All</button>
    </div>
    
    <textarea lang="xml" readonly class="row" rows="12" id="output" name="output" placeholder="Output" style="white-space: pre; width: 100%;"></textarea>
    <div class="row" style="margin: 5px 0;">
        <button class="btn-outline" onclick="copyData('output')" data-toggle="tooltip" title="Copy to clipboard">Copy Output</button>
        <button class="btn-outline" onclick="clearOutput()">Clear Output</button>
    </div>
</div>
