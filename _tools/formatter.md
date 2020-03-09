---
layout: tools
title: Formatter Online
categories: [Json Formatter, Xml Formatter, CSS Formatter, SQL Formatter]
description: Json Formatter, Xml Formatter, CSS Formatter, SQL Formatter, Json parser, Xml parser, CSS parser, SQL parser
keywords: Json Formatter, Xml Formatter, CSS Formatter, SQL Formatter, Json parser, Xml parser, CSS parser, SQL parser
active: true
---

<div style="font-family: monospace;">
	<h3 class="row">
      <a href="javascript:void(0);" id="json" onclick="switchParser('json');">Json Format</a> | 
      <a href="javascript:void(0);" id="xml" onclick="switchParser('xml');">Xml Format</a> | 
      <a href="javascript:void(0);" id="css" onclick="switchParser('css');">CSS Format</a> | 
      <a href="javascript:void(0);" id="sql" onclick="switchParser('sql');">SQL Format</a>
    </h3>
    <textarea class="row" rows="12" id="input" name="input" placeholder="Input" style="white-space: pre; width: 100%;"></textarea>
    <div class="row" style="margin: 5px 0;">
      <button class="btn-outline" onclick="parseData()">Format</button>
      <button class="btn-outline" onclick="compressData()">Minify</button>
      <button class="btn-outline" onclick="copyData('input')" data-toggle="tooltip" title="Copy to clipboard">Copy Input</button>
      <button class="btn-outline" onclick="clearInput()">Clear Input</button>
      <button class="btn-outline" onclick="clearAll()">Clear All</button>
    </div>
	<textarea lang="xml" readonly class="row" rows="12" id="output" name="output" placeholder="Output" style="white-space: pre; width: 100%;"></textarea>
    <div class="row" style="margin: 5px 0;">
      <button class="btn-outline" onclick="copyData('output')" data-toggle="tooltip" title="Copy to clipboard">Copy Output</button>
      <button class="btn-outline" onclick="clearOutput()">Clear Output</button>
    </div>
</div>

<script type="text/javascript" src="{{ site.url }}/assets/js/vkbeautify.min.js"></script>
<script type="text/javascript">
	const TYPES=["json","xml","css","sql"];var current_type="json",switchParser=e=>{document.getElementById(current_type).style.color="#007bff",TYPES.includes(e)&&(current_type=e),document.getElementById(current_type).style.color="#ff5200",window.localStorage.setItem("type",current_type);var t=window.localStorage.getItem(current_type);t?!0===isValidInputData(current_type,t)?document.getElementById("input").value=t:(window.localStorage.removeItem(current_type),clearInput()):clearInput();clearOutput()},validateJson=e=>{try{JSON.parse(e)}catch(e){return e}return!0},validateXml=e=>{const t=(new window.DOMParser).parseFromString(e,"text/xml");return!(t.getElementsByTagName("parsererror").length>0)||t.getElementsByTagName("parsererror")[0].getElementsByTagName("div")[0].innerHTML},isValidInputData=(e,t)=>{let a;switch(e){case"json":a=validateJson(t);break;case"xml":a=validateXml(t);break;case"css":case"sql":a=!0;break;default:a="Invalid type"}return a},initPage=()=>{let e=window.localStorage.getItem("type");e&&TYPES.includes(e)?current_type=e:window.localStorage.setItem("type",current_type),document.getElementById(current_type).style.color="#ff5200";var t=window.localStorage.getItem(current_type);if(t){var a=isValidInputData(current_type,t);!0===a?document.getElementById("input").value=t:(window.localStorage.removeItem(current_type),console.log(a))}};initPage();var parseInputData=(e,t)=>{let a=t;switch(e){case"json":a=vkbeautify.json(t.trim(),4);break;case"xml":a=vkbeautify.xml(t.trim());break;case"css":a=vkbeautify.css(t.trim(),"    ");break;case"sql":a=vkbeautify.sql(t.trim(),"    ");break;default:a="Invalid type"}return a},compressInputData=(e,t)=>{let a=t;switch(e){case"json":a=vkbeautify.jsonmin(t.trim());break;case"xml":a=vkbeautify.xmlmin(t.trim(),!0);break;case"css":a=vkbeautify.cssmin(t.trim());break;case"sql":a=vkbeautify.sqlmin(t.trim());break;default:a="Invalid type"}return a},parseData=()=>{var e=document.getElementById("input").value;if(e){var t=isValidInputData(current_type,e);!0===t?(document.getElementById("output").value=parseInputData(current_type,e),window.localStorage.setItem(current_type,e)):document.getElementById("output").value=t}else document.getElementById("output").value="Input is empty"},compressData=()=>{var e=document.getElementById("input").value;if(e&&""!==e.trim()){var t=isValidInputData(current_type,e);!0===t?(document.getElementById("output").value=compressInputData(current_type,e),window.localStorage.setItem(current_type,e)):document.getElementById("output").value=t}else document.getElementById("output").value="Input value is empty"},copyData=e=>{var t=document.getElementById(e);t.select(),t.setSelectionRange(0,99999),document.execCommand("copy")},clearInput=()=>{document.getElementById("input").value=""},clearOutput=()=>{document.getElementById("output").value=""},clearAll=()=>{clearOutput(),clearInput()};
</script>
