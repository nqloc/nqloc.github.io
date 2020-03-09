---
layout: tools
title: Json Tree
categories: [Json Tree, Json Pretty]
description: Json Tree, Json Pretty
keywords: Json Tree, Json Pretty
active: true
---

<style type="text/css">
  /* common */
  .mark-water{
      color:#bbb;
  }
  /* eof common */

  /* node */
  .node-content-wrapper{
      font-family: 'Quicksand', sans-serif;
      background-color:#fff;
  }
  .node-content-wrapper ul{
      border-left:1px dotted #ccc;
      list-style:none;
      padding-left:25px;
      margin:0px;
  }
  .node-content-wrapper ul li{
      list-style:none;
      border-bottom:0; 
      padding-bottom:0
  }
  .node-hgl-path{
      background-color:#fefbdf;
  }
  .node-bracket{
      font-weight:bold;
      display:inline-block;
      cursor:pointer;
  }
  .node-bracket:hover{
      color:#999;
  }
  /* eof node */

  /* leaf */
  .leaft-container{
      width:100%;
      max-width:300px;
      height:100%;
  }

  .title{ color:#ccc;}
  .string{ color:#080;}
  .number{ color:#ccaa00;}
  .boolean{ color:#1979d3;}
  .date{ color:#aa6655;}
  .null{ color:#ff5050;}
  /* eof leaf */
</style>

<div style="font-family: monospace;">
	<h3 class="row">
      <a href="javascript:void(0);" id="json" onclick="switchParser('json');">Json Tree</a>
    </h3>
    <textarea class="row" rows="12" id="input" name="input" placeholder="Input" style="white-space: pre; width: 100%;"></textarea>
    <div class="row" style="margin: 5px 0;">
      <button class="btn-outline" onclick="parseData()">Pretty</button>
      <button class="btn-outline" onclick="collapseAll()">Collapse</button>
      <button class="btn-outline" onclick="expandAll()">Expand</button>
      <button class="btn-outline" onclick="clearData()">Clear</button>
      <button class="btn-outline" id="showbtn" onclick="showHideInput(true)">Show Input</button>
      <button class="btn-outline" id="hidebtn" onclick="showHideInput(false)">Hide Input</button>
    </div>
    <div class="row">
      <span id="output"></span>
    </div>
</div>

<script type="text/javascript" src="{{ site.url }}/assets/js/underscore-min.js"></script>
<script type="text/javascript" src="{{ site.url }}/assets/js/backbone-min.js"></script>
<script type="text/javascript" src="{{ site.url }}/assets/js/pretty-json-min.js"></script>
<script type="text/javascript">
  const TYPES = [ 'json'];
  var current_type = 'json';
  var tool_type = 'json_pretty';
  var node = null;

  var switchParser = (type) => {

      // remove scurrent menu color
      document.getElementById(current_type).style.color = "#007bff";
      
      // need to check exists enum
      if (TYPES.includes(type)) {
          current_type = type;
      }

      // update to new menu color
      document.getElementById(current_type).style.color = "#ff5200";

      window.localStorage.setItem(tool_type, current_type);

      var input = window.localStorage.getItem(current_type);
      if (input) {
          var validate = isValidInputData(current_type, input);
          if (validate === true) {
              document.getElementById("input").value = input;
          } else {
              window.localStorage.removeItem(current_type);
              clearInput();
          }
      } else {
          clearInput();
      }
      clearOutput();
  }

  // For JSON
  var validateJson = (txt) => {
      try {
          JSON.parse(txt);
      } catch (e) {
          return e;
      }
      return true;
  }

  var isValidInputData = (type, txt) => {
      let result;
      switch(type) {
        case "json":
          result = validateJson(txt);
          break;
        default:
          result = "Invalid type";
      }
      return result;
  }

  // Init page
  var initPage = () => {
      $("#showbtn").hide(0);

      let type =  window.localStorage.getItem(tool_type);

      if (!type || !TYPES.includes(type)) {
          window.localStorage.setItem(tool_type, current_type);
      } else {
          current_type = type;
      }
      // update menu color
      document.getElementById(current_type).style.color = "#ff5200";

      // Load history data by type
      var input = window.localStorage.getItem(current_type);
      if (input) {
          var validate = isValidInputData(current_type, input);
          if (validate === true) {
              document.getElementById("input").value = input;
          } else {
              window.localStorage.removeItem(current_type);
              console.log(validate);
          }
      }
  }

  initPage();

  var jsonParser = (txt) => {
      let data = JSON.parse(txt);
      let result_el = document.getElementById('output');

      node = new PrettyJSON.view.Node({ 
          el:result_el,
          data: data,
          dateFormat:"DD/MM/YYYY - HH24:MI:SS"
      });

      console.log(node);
      return node;
  }

  var parseInputData = (type, input) => {
      let result = input;

      switch(type) {
        case "json":
          result = jsonParser(input);
          break;
        default:
          result = "Invalid type";
      }
      return result;
  }

  var parseData = () => {

      var input = document.getElementById("input").value;

      if (!input) {
          alert("Input is empty");
          return;
      }

      var validate = isValidInputData(current_type, input);

      if (validate !== true) {
          alert("Invalid json: " + validate);
          return;
      }

      document.getElementById("output").value = parseInputData(current_type, input);
      window.localStorage.setItem(current_type, input)
  }

  var showHideInput = (flag) => {
      if (flag === true) {
          $("#input").show(1000);
          $("#showbtn").hide(0);
          $("#hidebtn").show(1000);
      } else {
          $("#input").hide(1000);
          $("#hidebtn").hide(0);
          $("#showbtn").show(1000);
      }
  }

  var removeOutputClass = () => {
     $("span").remove(".node-container"); 
  }

  var expandAll = () => {
      if (node == null) {
          removeOutputClass();
          document.getElementById("output").value = 'Missing input';
      } else {
          node.expandAll();
      }
  }

  var collapseAll = () => {
      if (node == null) {
          removeOutputClass();
          document.getElementById("output").value = 'Missing input';
      } else {
          node.collapseAll();
      }
  }

  var clearData = () => {
      node = null;
      document.getElementById("input").value = '';
      removeOutputClass();
      showHideInput(true);
  }
</script>