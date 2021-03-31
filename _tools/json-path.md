---
layout: tools
title: JSON Path Online
categories: [JSON Path Online]
description: JSON Path Online
keywords: JSON Path Online
active: true
---

<div style="font-family: monospace;">
    <input class="row" id="syntax" type="text" placeholder="Put JSONPath syntax" onchange="find();" onkeyup="this.onchange();" onpaste="this.onchange();" oninput="this.onchange();" style="white-space: pre; width: 100%; margin: 5px 0;">
    
    <textarea class="row" rows="18" id="input" name="input" placeholder="Input" style="white-space: pre; width: 100%;"></textarea>
    <div class="row" style="margin: 5px 0;">
        <button class="tool_btn tool_blue" onclick="find()">Find</button>
        <button class="tool_btn tool_green" onclick="copyData('input')" data-toggle="tooltip" title="Copy to clipboard">Copy Input</button>
        <button class="tool_btn tool_orange" onclick="loadSample()">Load Sample</button>
        <button class="tool_btn tool_red" onclick="clearInput()">Clear Input</button>
        <button class="tool_btn tool_red" onclick="clearAll()">Clear All</button>
    </div>
    
    <textarea lang="xml" readonly class="row" rows="6" id="output" name="output" placeholder="Output" style="white-space: pre; width: 100%;"></textarea>
    <div class="row" style="margin: 5px 0;">
        <button class="tool_btn tool_green" onclick="copyData('output')" data-toggle="tooltip" title="Copy to clipboard">Copy Output</button>
        <button class="tool_btn tool_red" onclick="clearOutput()">Clear Output</button>
    </div>
</div>

<script type="text/javascript" src="{{ site.url }}/assets/js/jsonpath.js"></script>

<script type = "text/javascript">
    function find() {
        var input = document.getElementById("input").value;
        var syntax = document.getElementById("syntax").value;
        if (input && "" !== input.trim()) {
            var result = JSONPath.JSONPath({path: syntax, json: JSON.parse(input)});
            document.getElementById("output").innerHTML = JSON.stringify(result, null, 4);
        } else {
            document.getElementById("output").value = "Input value is empty"
        }
    }
    
    var loadSample = () => {
        document.getElementById("syntax").value = '$.phoneNumbers[?(@.type)].type'
        var json = '{"firstName":"John","lastName":"doe","age":26,"address":{"streetAddress":"naist street","city":"Nara","postalCode":"630-0192"},"phoneNumbers":[{"type":"iPhone","number":"0123-4567-8888"},{"type":"home","number":"0123-4567-8910"}]}';
        document.getElementById("input").value = JSON.stringify(JSON.parse(json), null, 4);
        find();
    }
    
    var copyData = e => {
        var t = document.getElementById(e);
        t.select(), t.setSelectionRange(0, 99999), document.execCommand("copy")
    }
    
    var clearInput = () => {
        document.getElementById("syntax").value = ""
        document.getElementById("input").value = ""
    }
    
    var clearOutput = () => {
        document.getElementById("output").value = ""
    }
    
    var clearAll = () => {
        clearOutput(), clearInput()
    }
</script>
