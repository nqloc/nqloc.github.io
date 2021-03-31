---
layout: tools
title: JSON Path Online
categories: [JSON Path Online]
description: JSON Path Online
keywords: JSON Path Online
active: true
---

<div style="font-family: monospace;">
    <div class="row" style="margin: 5px 0;">
        <h3>JSONPath Syntax</h3>
        <input id="syntax" type="text" placeholder="Put JSONPath syntax" style="white-space: pre; width: 100%;">
    </div>
    
    <textarea class="row" rows="12" id="input" name="input" placeholder="Input" style="white-space: pre; width: 100%;"></textarea>
    <div class="row" style="margin: 5px 0;">
        <button class="btn-outline" onclick="find()">Find</button>
        <button class="btn-outline" onclick="copyData('input')" data-toggle="tooltip" title="Copy to clipboard">Copy Input</button>
        <button class="btn-outline" onclick="clearInput()">Clear Input</button>
        <button class="btn-outline" onclick="clearAll()">Clear All</button>
        <button class="btn-outline" onclick="addSample()">Sample</button>
    </div>
    
    <textarea lang="xml" readonly class="row" rows="12" id="output" name="output" placeholder="Output" style="white-space: pre; width: 100%;"></textarea>
    <div class="row" style="margin: 5px 0;">
        <button class="btn-outline" onclick="copyData('output')" data-toggle="tooltip" title="Copy to clipboard">Copy Output</button>
        <button class="btn-outline" onclick="clearOutput()">Clear Output</button>
    </div>
</div>
