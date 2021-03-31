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
        <button class="tool_btn tool_blue" onclick="find()">Find</button>
        <button class="tool_btn tool_green" onclick="copyData('input')" data-toggle="tooltip" title="Copy to clipboard">Copy Input</button>
        <button class="tool_btn tool_orange" onclick="addSample()">Sample</button>
        <button class="tool_btn tool_red" onclick="clearInput()">Clear Input</button>
        <button class="tool_btn tool_red" onclick="clearAll()">Clear All</button>
    </div>
    
    <textarea lang="xml" readonly class="row" rows="12" id="output" name="output" placeholder="Output" style="white-space: pre; width: 100%;"></textarea>
    <div class="row" style="margin: 5px 0;">
        <button class="tool_btn tool_green" onclick="copyData('output')" data-toggle="tooltip" title="Copy to clipboard">Copy Output</button>
        <button class="tool_btn tool_red" onclick="clearOutput()">Clear Output</button>
    </div>
</div>

<script type="text/javascript" src="{{ site.url }}/assets/js/jsonpath.js"></script>

<script type = "text/javascript" >
    var input = document.getElementById("input").value;
    var syntax = document.getElementById("syntax").value;
    if (input && "" !== input.trim()) {
        var result = JSONPath.JSONPath({path: syntax, json: input});
        document.getElementById("output").innerHTML = JSON.stringify(result, null, 2);
    } else {
        document.getElementById("output").value = "Input value is empty"
    }
</script>
