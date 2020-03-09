---
layout: tools
title: XML to JSON, JSON to XML converter
categories: [JSON to XML converter, XML to JSON converter]
description: XML to JSON, JSON to XML converter
keywords: XML to JSON, JSON to XML, XML to JSON converter, JSON to XML converter, xml2json, json2xml, jsonToXml, xmlToJson
active: true
---

<div style="font-family: monospace;">
	<h3 class="row">
      <a href="javascript:void(0);" id="json2xml" onclick="switchParser('json2xml');">JSON 2 XML</a> | 
      <a href="javascript:void(0);" id="xml2json" onclick="switchParser('xml2json');">XML 2 JSON</a>
    </h3>
    <textarea class="row" rows="12" id="input" name="input" placeholder="Input" style="white-space: pre; width: 100%;"></textarea>
    <div class="row" style="margin: 5px 0;">
      <button class="btn-outline" onclick="parseData()">Convert</button>
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
<script type="text/javascript" src="{{ site.url }}/assets/js/xml2json.min.js"></script>
<script type="text/javascript">
	const TYPES=["json2xml","xml2json"];var current_type="json2xml",x2js=new X2JS,switchParser=e=>{document.getElementById(current_type).style.color="#007bff",TYPES.includes(e)&&(current_type=e),document.getElementById(current_type).style.color="#ff5200",window.localStorage.setItem("converter_type",current_type);var t=window.localStorage.getItem(current_type);t?!0===isValidInputData(current_type,t)?document.getElementById("input").value=t:(window.localStorage.removeItem(current_type),clearInput()):clearInput();clearOutput()},validateJson=e=>{try{JSON.parse(e)}catch(e){return e}return!0},validateXml=e=>{const t=(new window.DOMParser).parseFromString(e,"text/xml");return!(t.getElementsByTagName("parsererror").length>0)||t.getElementsByTagName("parsererror")[0].getElementsByTagName("div")[0].innerHTML},isValidInputData=(e,t)=>{let r;switch(e){case"json2xml":r=validateJson(t);break;case"xml2json":r=validateXml(t);break;default:r="Invalid type"}return r},initPage=()=>{let e=window.localStorage.getItem("converter_type");e&&TYPES.includes(e)?current_type=e:window.localStorage.setItem("converter_type",current_type),document.getElementById(current_type).style.color="#ff5200";var t=window.localStorage.getItem(current_type);if(t){var r=isValidInputData(current_type,t);!0===r?document.getElementById("input").value=t:(window.localStorage.removeItem(current_type),console.log(r))}};initPage();var parseXml=e=>{return(new window.DOMParser).parseFromString(e,"text/xml")},parseInputData=(e,t)=>{let r=t;switch(e){case"json2xml":r=vkbeautify.xml(x2js.json2xml_str(JSON.parse(t.trim())));break;case"xml2json":r=vkbeautify.json(x2js.xml_str2json(t.trim()),4);break;default:r="Invalid type"}return r},parseData=()=>{var e=document.getElementById("input").value;if(e){var t=isValidInputData(current_type,e);!0===t?(document.getElementById("output").value=parseInputData(current_type,e),window.localStorage.setItem(current_type,e)):document.getElementById("output").value=current_type.toUpperCase()+" validation: "+t}else document.getElementById("output").value="Input is empty"},compressInputData=(e,t)=>{let r=t;switch(e){case"json2xml":r=vkbeautify.xmlmin(x2js.json2xml_str(JSON.parse(t.trim())),!0);break;case"xml2json":r=vkbeautify.jsonmin(JSON.stringify(x2js.xml_str2json(t.trim())));break;default:r="Invalid type"}return r},compressData=()=>{var e=document.getElementById("input").value;if(e&&""!==e.trim()){var t=isValidInputData(current_type,e);!0===t?(document.getElementById("output").value=compressInputData(current_type,e),window.localStorage.setItem(current_type,e)):document.getElementById("output").value=current_type.toUpperCase()+" validation: "+t}else document.getElementById("output").value="Input value is empty"},copyData=e=>{var t=document.getElementById(e);t.select(),t.setSelectionRange(0,99999),document.execCommand("copy")},clearInput=()=>{document.getElementById("input").value=""},clearOutput=()=>{document.getElementById("output").value=""},clearAll=()=>{clearOutput(),clearInput()};
</script>