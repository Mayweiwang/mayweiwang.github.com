---
layout: post
title: "A tutorial on how to design a simple prediction model"
description: ""
category: "Python"
tags: []
---
{% include JB/setup %}



 
<head>

<meta charset="utf-8" />
<title>SimplePredictionModel</title>

<script src="https://cdnjs.cloudflare.com/ajax/libs/require.js/2.1.10/require.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/2.0.3/jquery.min.js"></script>

<style type="text/css">
    .clearfix{*zoom:1}.clearfix:before,.clearfix:after{display:table;content:"";line-height:0}
.clearfix:after{clear:both}
.hide-text{font:0/0 a;color:transparent;text-shadow:none;background-color:transparent;border:0}
.input-block-level{display:block;width:100%;min-height:30px;-webkit-box-sizing:border-box;-moz-box-sizing:border-box;box-sizing:border-box}
article,aside,details,figcaption,figure,footer,header,hgroup,nav,section{display:block}
audio,canvas,video{display:inline-block;*display:inline;*zoom:1}
audio:not([controls]){display:none}
html{font-size:100%;-webkit-text-size-adjust:100%;-ms-text-size-adjust:100%}
a:focus{outline:thin dotted #333;outline:5px auto -webkit-focus-ring-color;outline-offset:-2px}
a:hover,a:active{outline:0}
sub,sup{position:relative;font-size:75%;line-height:0;vertical-align:baseline}
sup{top:-0.5em}
sub{bottom:-0.25em}
img{max-width:100%;width:auto\9;height:auto;vertical-align:middle;border:0;-ms-interpolation-mode:bicubic}
#map_canvas img,.google-maps img{max-width:none}
button,input,select,textarea{margin:0;font-size:100%;vertical-align:middle}
button,input{*overflow:visible;line-height:normal}
button::-moz-focus-inner,input::-moz-focus-inner{padding:0;border:0}
button,html input[type="button"],input[type="reset"],input[type="submit"]{-webkit-appearance:button;cursor:pointer}
label,select,button,input[type="button"],input[type="reset"],input[type="submit"],input[type="radio"],input[type="checkbox"]{cursor:pointer}
input[type="search"]{-webkit-box-sizing:content-box;-moz-box-sizing:content-box;box-sizing:content-box;-webkit-appearance:textfield}
input[type="search"]::-webkit-search-decoration,input[type="search"]::-webkit-search-cancel-button{-webkit-appearance:none}
textarea{overflow:auto;vertical-align:top}
@media print{*{text-shadow:none !important;color:#000 !important;background:transparent !important;box-shadow:none !important} a,a:visited{text-decoration:underline} a[href]:after{content:" (" attr(href) ")"} abbr[title]:after{content:" (" attr(title) ")"} .ir a:after,a[href^="javascript:"]:after,a[href^="#"]:after{content:""} pre,blockquote{border:1px solid #999;page-break-inside:avoid} thead{display:table-header-group} tr,img{page-break-inside:avoid} img{max-width:100% !important} @page {margin:.5cm}p,h2,h3{orphans:3;widows:3} h2,h3{page-break-after:avoid}}body{margin:0;font-family:"Helvetica Neue",Helvetica,Arial,sans-serif;font-size:13px;line-height:20px;color:#000;background-color:#fff}
a{color:#08c;text-decoration:none}
a:hover,a:focus{color:#005580;text-decoration:underline}
.img-rounded{border-radius:6px;-webkit-border-radius:6px;-moz-border-radius:6px;border-radius:6px}
.img-polaroid{padding:4px;background-color:#fff;border:1px solid #ccc;border:1px solid rgba(0,0,0,0.2);-webkit-box-shadow:0 1px 3px rgba(0,0,0,0.1);-moz-box-shadow:0 1px 3px rgba(0,0,0,0.1);box-shadow:0 1px 3px rgba(0,0,0,0.1)}
.img-circle{border-radius:500px;-webkit-border-radius:500px;-moz-border-radius:500px;border-radius:500px}
.row{margin-left:-20px;*zoom:1}.row:before,.row:after{display:table;content:"";line-height:0}
.row:after{clear:both}
[class*="span"]{float:left;min-height:1px;margin-left:20px}
.container,.navbar-static-top .container,.navbar-fixed-top .container,.navbar-fixed-bottom .container{width:940px}
.span12{width:940px}
.span11{width:860px}
.span10{width:780px}
.span9{width:700px}
.span8{width:620px}
.span7{width:540px}
.span6{width:460px}
.span5{width:380px}
.span4{width:300px}
.span3{width:220px}
.span2{width:140px}
.span1{width:60px}
.offset12{margin-left:980px}
.offset11{margin-left:900px}
.offset10{margin-left:820px}
.offset9{margin-left:740px}
.offset8{margin-left:660px}
.offset7{margin-left:580px}
.offset6{margin-left:500px}
.offset5{margin-left:420px}
.offset4{margin-left:340px}
.offset3{margin-left:260px}
.offset2{margin-left:180px}
.offset1{margin-left:100px}
.row-fluid{width:100%;*zoom:1}.row-fluid:before,.row-fluid:after{display:table;content:"";line-height:0}
.row-fluid:after{clear:both}
.row-fluid [class*="span"]{display:block;width:100%;min-height:30px;-webkit-box-sizing:border-box;-moz-box-sizing:border-box;box-sizing:border-box;float:left;margin-left:2.127659574468085%;*margin-left:2.074468085106383%}
.row-fluid [class*="span"]:first-child{margin-left:0}
.row-fluid .controls-row [class*="span"]+[class*="span"]{margin-left:2.127659574468085%}
.row-fluid .span12{width:100%;*width:99.94680851063829%}
.row-fluid .span11{width:91.48936170212765%;*width:91.43617021276594%}
.row-fluid .span10{width:82.97872340425532%;*width:82.92553191489361%}
.row-fluid .span9{width:74.46808510638297%;*width:74.41489361702126%}
.row-fluid .span8{width:65.95744680851064%;*width:65.90425531914893%}
.row-fluid .span7{width:57.44680851063829%;*width:57.39361702127659%}
.row-fluid .span6{width:48.93617021276595%;*width:48.88297872340425%}
.row-fluid .span5{width:40.42553191489362%;*width:40.37234042553192%}
.row-fluid .span4{width:31.914893617021278%;*width:31.861702127659576%}
.row-fluid .span3{width:23.404255319148934%;*width:23.351063829787233%}
.row-fluid .span2{width:14.893617021276595%;*width:14.840425531914894%}
.row-fluid .span1{width:6.382978723404255%;*width:6.329787234042553%}
.row-fluid .offset12{margin-left:104.25531914893617%;*margin-left:104.14893617021275%}
.row-fluid .offset12:first-child{margin-left:102.12765957446808%;*margin-left:102.02127659574467%}
.row-fluid .offset11{margin-left:95.74468085106382%;*margin-left:95.6382978723404%}
.row-fluid .offset11:first-child{margin-left:93.61702127659574%;*margin-left:93.51063829787232%}
.row-fluid .offset10{margin-left:87.23404255319149%;*margin-left:87.12765957446807%}
.row-fluid .offset10:first-child{margin-left:85.1063829787234%;*margin-left:84.99999999999999%}
.row-fluid .offset9{margin-left:78.72340425531914%;*margin-left:78.61702127659572%}
.row-fluid .offset9:first-child{margin-left:76.59574468085106%;*margin-left:76.48936170212764%}
.row-fluid .offset8{margin-left:70.2127659574468%;*margin-left:70.10638297872339%}
.row-fluid .offset8:first-child{margin-left:68.08510638297872%;*margin-left:67.9787234042553%}
.row-fluid .offset7{margin-left:61.70212765957446%;*margin-left:61.59574468085106%}
.row-fluid .offset7:first-child{margin-left:59.574468085106375%;*margin-left:59.46808510638297%}
.row-fluid .offset6{margin-left:53.191489361702125%;*margin-left:53.085106382978715%}
.row-fluid .offset6:first-child{margin-left:51.063829787234035%;*margin-left:50.95744680851063%}
.row-fluid .offset5{margin-left:44.68085106382979%;*margin-left:44.57446808510638%}
.row-fluid .offset5:first-child{margin-left:42.5531914893617%;*margin-left:42.4468085106383%}
.row-fluid .offset4{margin-left:36.170212765957444%;*margin-left:36.06382978723405%}
.row-fluid .offset4:first-child{margin-left:34.04255319148936%;*margin-left:33.93617021276596%}
.row-fluid .offset3{margin-left:27.659574468085104%;*margin-left:27.5531914893617%}
.row-fluid .offset3:first-child{margin-left:25.53191489361702%;*margin-left:25.425531914893618%}
.row-fluid .offset2{margin-left:19.148936170212764%;*margin-left:19.04255319148936%}
.row-fluid .offset2:first-child{margin-left:17.02127659574468%;*margin-left:16.914893617021278%}
.row-fluid .offset1{margin-left:10.638297872340425%;*margin-left:10.53191489361702%}
.row-fluid .offset1:first-child{margin-left:8.51063829787234%;*margin-left:8.404255319148938%}
[class*="span"].hide,.row-fluid [class*="span"].hide{display:none}
[class*="span"].pull-right,.row-fluid [class*="span"].pull-right{float:right}
.container{margin-right:auto;margin-left:auto;*zoom:1}.container:before,.container:after{display:table;content:"";line-height:0}
.container:after{clear:both}
.container-fluid{padding-right:20px;padding-left:20px;*zoom:1}.container-fluid:before,.container-fluid:after{display:table;content:"";line-height:0}
.container-fluid:after{clear:both}
p{margin:0 0 10px}
.lead{margin-bottom:20px;font-size:19.5px;font-weight:200;line-height:30px}
small{font-size:85%}
strong{font-weight:bold}
em{font-style:italic}
cite{font-style:normal}
.muted{color:#999}
a.muted:hover,a.muted:focus{color:#808080}
.text-warning{color:#c09853}
a.text-warning:hover,a.text-warning:focus{color:#a47e3c}
.text-error{color:#b94a48}
a.text-error:hover,a.text-error:focus{color:#953b39}
.text-info{color:#3a87ad}
a.text-info:hover,a.text-info:focus{color:#2d6987}
.text-success{color:#468847}
a.text-success:hover,a.text-success:focus{color:#356635}
.text-left{text-align:left}
.text-right{text-align:right}
.text-center{text-align:center}
h1,h2,h3,h4,h5,h6{margin:10px 0;font-family:inherit;font-weight:bold;line-height:20px;color:inherit;text-rendering:optimizelegibility}h1 small,h2 small,h3 small,h4 small,h5 small,h6 small{font-weight:normal;line-height:1;color:#999}
h1,h2,h3{line-height:40px}
h1{font-size:35.75px}
h2{font-size:29.25px}
h3{font-size:22.75px}
h4{font-size:16.25px}
h5{font-size:13px}
h6{font-size:11.049999999999999px}
h1 small{font-size:22.75px}
h2 small{font-size:16.25px}
h3 small{font-size:13px}
h4 small{font-size:13px}
.page-header{padding-bottom:9px;margin:20px 0 30px;border-bottom:1px solid #eee}
ul,ol{padding:0;margin:0 0 10px 25px}
ul ul,ul ol,ol ol,ol ul{margin-bottom:0}
li{line-height:20px}
ul.unstyled,ol.unstyled{margin-left:0;list-style:none}
ul.inline,ol.inline{margin-left:0;list-style:none}ul.inline>li,ol.inline>li{display:inline-block;*display:inline;*zoom:1;padding-left:5px;padding-right:5px}
dl{margin-bottom:20px}
dt,dd{line-height:20px}
dt{font-weight:bold}
dd{margin-left:10px}
.dl-horizontal{*zoom:1}.dl-horizontal:before,.dl-horizontal:after{display:table;content:"";line-height:0}
.dl-horizontal:after{clear:both}
.dl-horizontal dt{float:left;width:160px;clear:left;text-align:right;overflow:hidden;text-overflow:ellipsis;white-space:nowrap}
.dl-horizontal dd{margin-left:180px}
hr{margin:20px 0;border:0;border-top:1px solid #eee;border-bottom:1px solid #fff}
abbr[title],abbr[data-original-title]{cursor:help;border-bottom:1px dotted #999}
abbr.initialism{font-size:90%;text-transform:uppercase}
blockquote{padding:0 0 0 15px;margin:0 0 20px;border-left:5px solid #eee}blockquote p{margin-bottom:0;font-size:16.25px;font-weight:300;line-height:1.25}
blockquote small{display:block;line-height:20px;color:#999}blockquote small:before{content:'\2014 \00A0'}
blockquote.pull-right{float:right;padding-right:15px;padding-left:0;border-right:5px solid #eee;border-left:0}blockquote.pull-right p,blockquote.pull-right small{text-align:right}
blockquote.pull-right small:before{content:''}
blockquote.pull-right small:after{content:'\00A0 \2014'}
q:before,q:after,blockquote:before,blockquote:after{content:""}
address{display:block;margin-bottom:20px;font-style:normal;line-height:20px}
code,pre{padding:0 3px 2px;font-family:monospace;font-size:11px;color:#333;border-radius:3px;-webkit-border-radius:3px;-moz-border-radius:3px;border-radius:3px}
code{padding:2px 4px;color:#d14;background-color:#f7f7f9;border:1px solid #e1e1e8;white-space:nowrap}
pre{display:block;padding:9.5px;margin:0 0 10px;font-size:12px;line-height:20px;word-break:break-all;word-wrap:break-word;white-space:pre;white-space:pre-wrap;background-color:#f5f5f5;border:1px solid #ccc;border:1px solid rgba(0,0,0,0.15);border-radius:4px;-webkit-border-radius:4px;-moz-border-radius:4px;border-radius:4px}pre.prettyprint{margin-bottom:20px}
pre code{padding:0;color:inherit;white-space:pre;white-space:pre-wrap;background-color:transparent;border:0}
.pre-scrollable{max-height:340px;overflow-y:scroll}
form{margin:0 0 20px}
fieldset{padding:0;margin:0;border:0}
legend{display:block;width:100%;padding:0;margin-bottom:20px;font-size:19.5px;line-height:40px;color:#333;border:0;border-bottom:1px solid #e5e5e5}legend small{font-size:15px;color:#999}
label,input,button,select,textarea{font-size:13px;font-weight:normal;line-height:20px}
input,button,select,textarea{font-family:"Helvetica Neue",Helvetica,Arial,sans-serif}
label{display:block;margin-bottom:5px}
select,textarea,input[type="text"],input[type="password"],input[type="datetime"],input[type="datetime-local"],input[type="date"],input[type="month"],input[type="time"],input[type="week"],input[type="number"],input[type="email"],input[type="url"],input[type="search"],input[type="tel"],input[type="color"],.uneditable-input{display:inline-block;height:20px;padding:4px 6px;margin-bottom:10px;font-size:13px;line-height:20px;color:#555;-webkit-border-radius:4px;-moz-border-radius:4px;border-radius:4px;vertical-align:middle}
input,textarea,.uneditable-input{width:206px}
textarea{height:auto}
textarea,input[type="text"],input[type="password"],input[type="datetime"],input[type="datetime-local"],input[type="date"],input[type="month"],input[type="time"],input[type="week"],input[type="number"],input[type="email"],input[type="url"],input[type="search"],input[type="tel"],input[type="color"],.uneditable-input{background-color:#fff;border:1px solid #ccc;-webkit-box-shadow:inset 0 1px 1px rgba(0,0,0,0.075);-moz-box-shadow:inset 0 1px 1px rgba(0,0,0,0.075);box-shadow:inset 0 1px 1px rgba(0,0,0,0.075);-webkit-transition:border linear .2s, box-shadow linear .2s;-moz-transition:border linear .2s, box-shadow linear .2s;-o-transition:border linear .2s, box-shadow linear .2s;transition:border linear .2s, box-shadow linear .2s}textarea:focus,input[type="text"]:focus,input[type="password"]:focus,input[type="datetime"]:focus,input[type="datetime-local"]:focus,input[type="date"]:focus,input[type="month"]:focus,input[type="time"]:focus,input[type="week"]:focus,input[type="number"]:focus,input[type="email"]:focus,input[type="url"]:focus,input[type="search"]:focus,input[type="tel"]:focus,input[type="color"]:focus,.uneditable-input:focus{border-color:rgba(82,168,236,0.8);outline:0;outline:thin dotted \9;-webkit-box-shadow:inset 0 1px 1px rgba(0,0,0,.075), 0 0 8px rgba(82,168,236,.6);-moz-box-shadow:inset 0 1px 1px rgba(0,0,0,.075), 0 0 8px rgba(82,168,236,.6);box-shadow:inset 0 1px 1px rgba(0,0,0,.075), 0 0 8px rgba(82,168,236,.6)}
input[type="radio"],input[type="checkbox"]{margin:4px 0 0;*margin-top:0;margin-top:1px \9;line-height:normal}
input[type="file"],input[type="image"],input[type="submit"],input[type="reset"],input[type="button"],input[type="radio"],input[type="checkbox"]{width:auto}
select,input[type="file"]{height:30px;*margin-top:4px;line-height:30px}
select{width:220px;border:1px solid #ccc;background-color:#fff}
select[multiple],select[size]{height:auto}
select:focus,input[type="file"]:focus,input[type="radio"]:focus,input[type="checkbox"]:focus{outline:thin dotted #333;outline:5px auto -webkit-focus-ring-color;outline-offset:-2px}
.uneditable-input,.uneditable-textarea{color:#999;background-color:#fcfcfc;border-color:#ccc;-webkit-box-shadow:inset 0 1px 2px rgba(0,0,0,0.025);-moz-box-shadow:inset 0 1px 2px rgba(0,0,0,0.025);box-shadow:inset 0 1px 2px rgba(0,0,0,0.025);cursor:not-allowed}
.uneditable-input{overflow:hidden;white-space:nowrap}
.uneditable-textarea{width:auto;height:auto}
input:-moz-placeholder,textarea:-moz-placeholder{color:#999}
input:-ms-input-placeholder,textarea:-ms-input-placeholder{color:#999}
input::-webkit-input-placeholder,textarea::-webkit-input-placeholder{color:#999}
.radio,.checkbox{min-height:20px;padding-left:20px}
.radio input[type="radio"],.checkbox input[type="checkbox"]{float:left;margin-left:-20px}
.controls>.radio:first-child,.controls>.checkbox:first-child{padding-top:5px}
.radio.inline,.checkbox.inline{display:inline-block;padding-top:5px;margin-bottom:0;vertical-align:middle}
.radio.inline+.radio.inline,.checkbox.inline+.checkbox.inline{margin-left:10px}
.input-mini{width:60px}
.input-small{width:90px}
.input-medium{width:150px}
.input-large{width:210px}
.input-xlarge{width:270px}
.input-xxlarge{width:530px}
input[class*="span"],select[class*="span"],textarea[class*="span"],.uneditable-input[class*="span"],.row-fluid input[class*="span"],.row-fluid select[class*="span"],.row-fluid textarea[class*="span"],.row-fluid .uneditable-input[class*="span"]{float:none;margin-left:0}
.input-append input[class*="span"],.input-append .uneditable-input[class*="span"],.input-prepend input[class*="span"],.input-prepend .uneditable-input[class*="span"],.row-fluid input[class*="span"],.row-fluid select[class*="span"],.row-fluid textarea[class*="span"],.row-fluid .uneditable-input[class*="span"],.row-fluid .input-prepend [class*="span"],.row-fluid .input-append [class*="span"]{display:inline-block}
input,textarea,.uneditable-input{margin-left:0}
.controls-row [class*="span"]+[class*="span"]{margin-left:20px}
input.span12,textarea.span12,.uneditable-input.span12{width:926px}
input.span11,textarea.span11,.uneditable-input.span11{width:846px}
input.span10,textarea.span10,.uneditable-input.span10{width:766px}
input.span9,textarea.span9,.uneditable-input.span9{width:686px}
input.span8,textarea.span8,.uneditable-input.span8{width:606px}
input.span7,textarea.span7,.uneditable-input.span7{width:526px}
input.span6,textarea.span6,.uneditable-input.span6{width:446px}
input.span5,textarea.span5,.uneditable-input.span5{width:366px}
input.span4,textarea.span4,.uneditable-input.span4{width:286px}
input.span3,textarea.span3,.uneditable-input.span3{width:206px}
input.span2,textarea.span2,.uneditable-input.span2{width:126px}
input.span1,textarea.span1,.uneditable-input.span1{width:46px}
.controls-row{*zoom:1}.controls-row:before,.controls-row:after{display:table;content:"";line-height:0}
.controls-row:after{clear:both}
.controls-row [class*="span"],.row-fluid .controls-row [class*="span"]{float:left}
.controls-row .checkbox[class*="span"],.controls-row .radio[class*="span"]{padding-top:5px}
input[disabled],select[disabled],textarea[disabled],input[readonly],select[readonly],textarea[readonly]{cursor:not-allowed;background-color:#eee}
input[type="radio"][disabled],input[type="checkbox"][disabled],input[type="radio"][readonly],input[type="checkbox"][readonly]{background-color:transparent}
.control-group.warning .control-label,.control-group.warning .help-block,.control-group.warning .help-inline{color:#c09853}
.control-group.warning .checkbox,.control-group.warning .radio,.control-group.warning input,.control-group.warning select,.control-group.warning textarea{color:#c09853}
.control-group.warning input,.control-group.warning select,.control-group.warning textarea{border-color:#c09853;-webkit-box-shadow:inset 0 1px 1px rgba(0,0,0,0.075);-moz-box-shadow:inset 0 1px 1px rgba(0,0,0,0.075);box-shadow:inset 0 1px 1px rgba(0,0,0,0.075)}.control-group.warning input:focus,.control-group.warning select:focus,.control-group.warning textarea:focus{border-color:#a47e3c;-webkit-box-shadow:inset 0 1px 1px rgba(0,0,0,0.075),0 0 6px #dbc59e;-moz-box-shadow:inset 0 1px 1px rgba(0,0,0,0.075),0 0 6px #dbc59e;box-shadow:inset 0 1px 1px rgba(0,0,0,0.075),0 0 6px #dbc59e}
.control-group.warning .input-prepend .add-on,.control-group.warning .input-append .add-on{color:#c09853;background-color:#fcf8e3;border-color:#c09853}
.control-group.error .control-label,.control-group.error .help-block,.control-group.error .help-inline{color:#b94a48}
.control-group.error .checkbox,.control-group.error .radio,.control-group.error input,.control-group.error select,.control-group.error textarea{color:#b94a48}
.control-group.error input,.control-group.error select,.control-group.error textarea{border-color:#b94a48;-webkit-box-shadow:inset 0 1px 1px rgba(0,0,0,0.075);-moz-box-shadow:inset 0 1px 1px rgba(0,0,0,0.075);box-shadow:inset 0 1px 1px rgba(0,0,0,0.075)}.control-group.error input:focus,.control-group.error select:focus,.control-group.error textarea:focus{border-color:#953b39;-webkit-box-shadow:inset 0 1px 1px rgba(0,0,0,0.075),0 0 6px #d59392;-moz-box-shadow:inset 0 1px 1px rgba(0,0,0,0.075),0 0 6px #d59392;box-shadow:inset 0 1px 1px rgba(0,0,0,0.075),0 0 6px #d59392}
.control-group.error .input-prepend .add-on,.control-group.error .input-append .add-on{color:#b94a48;background-color:#f2dede;border-color:#b94a48}
.control-group.success .control-label,.control-group.success .help-block,.control-group.success .help-inline{color:#468847}
.control-group.success .checkbox,.control-group.success .radio,.control-group.success input,.control-group.success select,.control-group.success textarea{color:#468847}
.control-group.success input,.control-group.success select,.control-group.success textarea{border-color:#468847;-webkit-box-shadow:inset 0 1px 1px rgba(0,0,0,0.075);-moz-box-shadow:inset 0 1px 1px rgba(0,0,0,0.075);box-shadow:inset 0 1px 1px rgba(0,0,0,0.075)}.control-group.success input:focus,.control-group.success select:focus,.control-group.success textarea:focus{border-color:#356635;-webkit-box-shadow:inset 0 1px 1px rgba(0,0,0,0.075),0 0 6px #7aba7b;-moz-box-shadow:inset 0 1px 1px rgba(0,0,0,0.075),0 0 6px #7aba7b;box-shadow:inset 0 1px 1px rgba(0,0,0,0.075),0 0 6px #7aba7b}
.control-group.success .input-prepend .add-on,.control-group.success .input-append .add-on{color:#468847;background-color:#dff0d8;border-color:#468847}
.control-group.info .control-label,.control-group.info .help-block,.control-group.info .help-inline{color:#3a87ad}
.control-group.info .checkbox,.control-group.info .radio,.control-group.info input,.control-group.info select,.control-group.info textarea{color:#3a87ad}
.control-group.info input,.control-group.info select,.control-group.info textarea{border-color:#3a87ad;-webkit-box-shadow:inset 0 1px 1px rgba(0,0,0,0.075);-moz-box-shadow:inset 0 1px 1px rgba(0,0,0,0.075);box-shadow:inset 0 1px 1px rgba(0,0,0,0.075)}.control-group.info input:focus,.control-group.info select:focus,.control-group.info textarea:focus{border-color:#2d6987;-webkit-box-shadow:inset 0 1px 1px rgba(0,0,0,0.075),0 0 6px #7ab5d3;-moz-box-shadow:inset 0 1px 1px rgba(0,0,0,0.075),0 0 6px #7ab5d3;box-shadow:inset 0 1px 1px rgba(0,0,0,0.075),0 0 6px #7ab5d3}
.control-group.info .input-prepend .add-on,.control-group.info .input-append .add-on{color:#3a87ad;background-color:#d9edf7;border-color:#3a87ad}
input:focus:invalid,textarea:focus:invalid,select:focus:invalid{color:#b94a48;border-color:#ee5f5b}input:focus:invalid:focus,textarea:focus:invalid:focus,select:focus:invalid:focus{border-color:#e9322d;-webkit-box-shadow:0 0 6px #f8b9b7;-moz-box-shadow:0 0 6px #f8b9b7;box-shadow:0 0 6px #f8b9b7}
.form-actions{padding:19px 20px 20px;margin-top:20px;margin-bottom:20px;background-color:#f5f5f5;border-top:1px solid #e5e5e5;*zoom:1}.form-actions:before,.form-actions:after{display:table;content:"";line-height:0}
.form-actions:after{clear:both}
.help-block,.help-inline{color:#262626}
.help-block{display:block;margin-bottom:10px}
.help-inline{display:inline-block;*display:inline;*zoom:1;vertical-align:middle;padding-left:5px}
.input-append,.input-prepend{display:inline-block;margin-bottom:10px;vertical-align:middle;font-size:0;white-space:nowrap}.input-append input,.input-prepend input,.input-append select,.input-prepend select,.input-append .uneditable-input,.input-prepend .uneditable-input,.input-append .dropdown-menu,.input-prepend .dropdown-menu,.input-append .popover,.input-prepend .popover{font-size:13px}
.input-append input,.input-prepend input,.input-append select,.input-prepend select,.input-append .uneditable-input,.input-prepend .uneditable-input{position:relative;margin-bottom:0;*margin-left:0;vertical-align:top;border-radius:0 4px 4px 0;-webkit-border-radius:0 4px 4px 0;-moz-border-radius:0 4px 4px 0;border-radius:0 4px 4px 0}.input-append input:focus,.input-prepend input:focus,.input-append select:focus,.input-prepend select:focus,.input-append .uneditable-input:focus,.input-prepend .uneditable-input:focus{z-index:2}
.input-append .add-on,.input-prepend .add-on{display:inline-block;width:auto;height:20px;min-width:16px;padding:4px 5px;font-size:13px;font-weight:normal;line-height:20px;text-align:center;text-shadow:0 1px 0 #fff;background-color:#eee;border:1px solid #ccc}
.input-append .add-on,.input-prepend .add-on,.input-append .btn,.input-prepend .btn,.input-append .btn-group>.dropdown-toggle,.input-prepend .btn-group>.dropdown-toggle{vertical-align:top;border-radius:0;-webkit-border-radius:0;-moz-border-radius:0;border-radius:0}
.input-append .active,.input-prepend .active{background-color:#a9dba9;border-color:#46a546}
.input-prepend .add-on,.input-prepend .btn{margin-right:-1px}
.input-prepend .add-on:first-child,.input-prepend .btn:first-child{border-radius:4px 0 0 4px;-webkit-border-radius:4px 0 0 4px;-moz-border-radius:4px 0 0 4px;border-radius:4px 0 0 4px}
.input-append input,.input-append select,.input-append .uneditable-input{border-radius:4px 0 0 4px;-webkit-border-radius:4px 0 0 4px;-moz-border-radius:4px 0 0 4px;border-radius:4px 0 0 4px}.input-append input+.btn-group .btn:last-child,.input-append select+.btn-group .btn:last-child,.input-append .uneditable-input+.btn-group .btn:last-child{border-radius:0 4px 4px 0;-webkit-border-radius:0 4px 4px 0;-moz-border-radius:0 4px 4px 0;border-radius:0 4px 4px 0}
.input-append .add-on,.input-append .btn,.input-append .btn-group{margin-left:-1px}
.input-append .add-on:last-child,.input-append .btn:last-child,.input-append .btn-group:last-child>.dropdown-toggle{border-radius:0 4px 4px 0;-webkit-border-radius:0 4px 4px 0;-moz-border-radius:0 4px 4px 0;border-radius:0 4px 4px 0}
.input-prepend.input-append input,.input-prepend.input-append select,.input-prepend.input-append .uneditable-input{border-radius:0;-webkit-border-radius:0;-moz-border-radius:0;border-radius:0}.input-prepend.input-append input+.btn-group .btn,.input-prepend.input-append select+.btn-group .btn,.input-prepend.input-append .uneditable-input+.btn-group .btn{border-radius:0 4px 4px 0;-webkit-border-radius:0 4px 4px 0;-moz-border-radius:0 4px 4px 0;border-radius:0 4px 4px 0}
.input-prepend.input-append .add-on:first-child,.input-prepend.input-append .btn:first-child{margin-right:-1px;border-radius:4px 0 0 4px;-webkit-border-radius:4px 0 0 4px;-moz-border-radius:4px 0 0 4px;border-radius:4px 0 0 4px}
.input-prepend.input-append .add-on:last-child,.input-prepend.input-append .btn:last-child{margin-left:-1px;border-radius:0 4px 4px 0;-webkit-border-radius:0 4px 4px 0;-moz-border-radius:0 4px 4px 0;border-radius:0 4px 4px 0}
.input-prepend.input-append .btn-group:first-child{margin-left:0}
input.search-query{padding-right:14px;padding-right:4px \9;padding-left:14px;padding-left:4px \9;margin-bottom:0;border-radius:15px;-webkit-border-radius:15px;-moz-border-radius:15px;border-radius:15px}
.form-search .input-append .search-query,.form-search .input-prepend .search-query{border-radius:0;-webkit-border-radius:0;-moz-border-radius:0;border-radius:0}
.form-search .input-append .search-query{border-radius:14px 0 0 14px;-webkit-border-radius:14px 0 0 14px;-moz-border-radius:14px 0 0 14px;border-radius:14px 0 0 14px}
.form-search .input-append .btn{border-radius:0 14px 14px 0;-webkit-border-radius:0 14px 14px 0;-moz-border-radius:0 14px 14px 0;border-radius:0 14px 14px 0}
.form-search .input-prepend .search-query{border-radius:0 14px 14px 0;-webkit-border-radius:0 14px 14px 0;-moz-border-radius:0 14px 14px 0;border-radius:0 14px 14px 0}
.form-search .input-prepend .btn{border-radius:14px 0 0 14px;-webkit-border-radius:14px 0 0 14px;-moz-border-radius:14px 0 0 14px;border-radius:14px 0 0 14px}
.form-search input,.form-inline input,.form-horizontal input,.form-search textarea,.form-inline textarea,.form-horizontal textarea,.form-search select,.form-inline select,.form-horizontal select,.form-search .help-inline,.form-inline .help-inline,.form-horizontal .help-inline,.form-search .uneditable-input,.form-inline .uneditable-input,.form-horizontal .uneditable-input,.form-search .input-prepend,.form-inline .input-prepend,.form-horizontal .input-prepend,.form-search .input-append,.form-inline .input-append,.form-horizontal .input-append{display:inline-block;*display:inline;*zoom:1;margin-bottom:0;vertical-align:middle}
.form-search .hide,.form-inline .hide,.form-horizontal .hide{display:none}
.form-search label,.form-inline label,.form-search .btn-group,.form-inline .btn-group{display:inline-block}
.form-search .input-append,.form-inline .input-append,.form-search .input-prepend,.form-inline .input-prepend{margin-bottom:0}
.form-search .radio,.form-search .checkbox,.form-inline .radio,.form-inline .checkbox{padding-left:0;margin-bottom:0;vertical-align:middle}
.form-search .radio input[type="radio"],.form-search .checkbox input[type="checkbox"],.form-inline .radio input[type="radio"],.form-inline .checkbox input[type="checkbox"]{float:left;margin-right:3px;margin-left:0}
.control-group{margin-bottom:10px}
legend+.control-group{margin-top:20px;-webkit-margin-top-collapse:separate}
.form-horizontal .control-group{margin-bottom:20px;*zoom:1}.form-horizontal .control-group:before,.form-horizontal .control-group:after{display:table;content:"";line-height:0}
.form-horizontal .control-group:after{clear:both}
.form-horizontal .control-label{float:left;width:160px;padding-top:5px;text-align:right}
.form-horizontal .controls{*display:inline-block;*padding-left:20px;margin-left:180px;*margin-left:0}.form-horizontal .controls:first-child{*padding-left:180px}
.form-horizontal .help-block{margin-bottom:0}
.form-horizontal input+.help-block,.form-horizontal select+.help-block,.form-horizontal textarea+.help-block,.form-horizontal .uneditable-input+.help-block,.form-horizontal .input-prepend+.help-block,.form-horizontal .input-append+.help-block{margin-top:10px}
.form-horizontal .form-actions{padding-left:180px}
table{max-width:100%;background-color:transparent;border-collapse:collapse;border-spacing:0}
.table{width:100%;margin-bottom:20px}.table th,.table td{padding:8px;line-height:20px;text-align:left;vertical-align:top;border-top:1px solid #ddd}
.table th{font-weight:bold}
.table thead th{vertical-align:bottom}
.table caption+thead tr:first-child th,.table caption+thead tr:first-child td,.table colgroup+thead tr:first-child th,.table colgroup+thead tr:first-child td,.table thead:first-child tr:first-child th,.table thead:first-child tr:first-child td{border-top:0}
.table tbody+tbody{border-top:2px solid #ddd}
.table .table{background-color:#fff}
.table-condensed th,.table-condensed td{padding:4px 5px}
.table-bordered{border:1px solid #ddd;border-collapse:separate;*border-collapse:collapse;border-left:0;border-radius:4px;-webkit-border-radius:4px;-moz-border-radius:4px;border-radius:4px}.table-bordered th,.table-bordered td{border-left:1px solid #ddd}
.table-bordered caption+thead tr:first-child th,.table-bordered caption+tbody tr:first-child th,.table-bordered caption+tbody tr:first-child td,.table-bordered colgroup+thead tr:first-child th,.table-bordered colgroup+tbody tr:first-child th,.table-bordered colgroup+tbody tr:first-child td,.table-bordered thead:first-child tr:first-child th,.table-bordered tbody:first-child tr:first-child th,.table-bordered tbody:first-child tr:first-child td{border-top:0}
.table-bordered thead:first-child tr:first-child>th:first-child,.table-bordered tbody:first-child tr:first-child>td:first-child,.table-bordered tbody:first-child tr:first-child>th:first-child{-webkit-border-top-left-radius:4px;-moz-border-radius-topleft:4px;border-top-left-radius:4px}
.table-bordered thead:first-child tr:first-child>th:last-child,.table-bordered tbody:first-child tr:first-child>td:last-child,.table-bordered tbody:first-child tr:first-child>th:last-child{-webkit-border-top-right-radius:4px;-moz-border-radius-topright:4px;border-top-right-radius:4px}
.table-bordered thead:last-child tr:last-child>th:first-child,.table-bordered tbody:last-child tr:last-child>td:first-child,.table-bordered tbody:last-child tr:last-child>th:first-child,.table-bordered tfoot:last-child tr:last-child>td:first-child,.table-bordered tfoot:last-child tr:last-child>th:first-child{-webkit-border-bottom-left-radius:4px;-moz-border-radius-bottomleft:4px;border-bottom-left-radius:4px}
.table-bordered thead:last-child tr:last-child>th:last-child,.table-bordered tbody:last-child tr:last-child>td:last-child,.table-bordered tbody:last-child tr:last-child>th:last-child,.table-bordered tfoot:last-child tr:last-child>td:last-child,.table-bordered tfoot:last-child tr:last-child>th:last-child{-webkit-border-bottom-right-radius:4px;-moz-border-radius-bottomright:4px;border-bottom-right-radius:4px}
.table-bordered tfoot+tbody:last-child tr:last-child td:first-child{-webkit-border-bottom-left-radius:0;-moz-border-radius-bottomleft:0;border-bottom-left-radius:0}
.table-bordered tfoot+tbody:last-child tr:last-child td:last-child{-webkit-border-bottom-right-radius:0;-moz-border-radius-bottomright:0;border-bottom-right-radius:0}
.table-bordered caption+thead tr:first-child th:first-child,.table-bordered caption+tbody tr:first-child td:first-child,.table-bordered colgroup+thead tr:first-child th:first-child,.table-bordered colgroup+tbody tr:first-child td:first-child{-webkit-border-top-left-radius:4px;-moz-border-radius-topleft:4px;border-top-left-radius:4px}
.table-bordered caption+thead tr:first-child th:last-child,.table-bordered caption+tbody tr:first-child td:last-child,.table-bordered colgroup+thead tr:first-child th:last-child,.table-bordered colgroup+tbody tr:first-child td:last-child{-webkit-border-top-right-radius:4px;-moz-border-radius-topright:4px;border-top-right-radius:4px}
.table-striped tbody>tr:nth-child(odd)>td,.table-striped tbody>tr:nth-child(odd)>th{background-color:#f9f9f9}
.table-hover tbody tr:hover>td,.table-hover tbody tr:hover>th{background-color:#f5f5f5}
table td[class*="span"],table th[class*="span"],.row-fluid table td[class*="span"],.row-fluid table th[class*="span"]{display:table-cell;float:none;margin-left:0}
.table td.span1,.table th.span1{float:none;width:44px;margin-left:0}
.table td.span2,.table th.span2{float:none;width:124px;margin-left:0}
.table td.span3,.table th.span3{float:none;width:204px;margin-left:0}
.table td.span4,.table th.span4{float:none;width:284px;margin-left:0}
.table td.span5,.table th.span5{float:none;width:364px;margin-left:0}
.table td.span6,.table th.span6{float:none;width:444px;margin-left:0}
.table td.span7,.table th.span7{float:none;width:524px;margin-left:0}
.table td.span8,.table th.span8{float:none;width:604px;margin-left:0}
.table td.span9,.table th.span9{float:none;width:684px;margin-left:0}
.table td.span10,.table th.span10{float:none;width:764px;margin-left:0}
.table td.span11,.table th.span11{float:none;width:844px;margin-left:0}
.table td.span12,.table th.span12{float:none;width:924px;margin-left:0}
.table tbody tr.success>td{background-color:#dff0d8}
.table tbody tr.error>td{background-color:#f2dede}
.table tbody tr.warning>td{background-color:#fcf8e3}
.table tbody tr.info>td{background-color:#d9edf7}
.table-hover tbody tr.success:hover>td{background-color:#d0e9c6}
.table-hover tbody tr.error:hover>td{background-color:#ebcccc}
.table-hover tbody tr.warning:hover>td{background-color:#faf2cc}
.table-hover tbody tr.info:hover>td{background-color:#c4e3f3}
[class^="icon-"],[class*=" icon-"]{display:inline-block;width:14px;height:14px;*margin-right:.3em;line-height:14px;vertical-align:text-top;background-image:url("../img/glyphicons-halflings.png");background-position:14px 14px;background-repeat:no-repeat;margin-top:1px}
.icon-white,.nav-pills>.active>a>[class^="icon-"],.nav-pills>.active>a>[class*=" icon-"],.nav-list>.active>a>[class^="icon-"],.nav-list>.active>a>[class*=" icon-"],.navbar-inverse .nav>.active>a>[class^="icon-"],.navbar-inverse .nav>.active>a>[class*=" icon-"],.dropdown-menu>li>a:hover>[class^="icon-"],.dropdown-menu>li>a:focus>[class^="icon-"],.dropdown-menu>li>a:hover>[class*=" icon-"],.dropdown-menu>li>a:focus>[class*=" icon-"],.dropdown-menu>.active>a>[class^="icon-"],.dropdown-menu>.active>a>[class*=" icon-"],.dropdown-submenu:hover>a>[class^="icon-"],.dropdown-submenu:focus>a>[class^="icon-"],.dropdown-submenu:hover>a>[class*=" icon-"],.dropdown-submenu:focus>a>[class*=" icon-"]{background-image:url("../img/glyphicons-halflings-white.png")}
.icon-glass{background-position:0 0}
.icon-music{background-position:-24px 0}
.icon-search{background-position:-48px 0}
.icon-envelope{background-position:-72px 0}
.icon-heart{background-position:-96px 0}
.icon-star{background-position:-120px 0}
.icon-star-empty{background-position:-144px 0}
.icon-user{background-position:-168px 0}
.icon-film{background-position:-192px 0}
.icon-th-large{background-position:-216px 0}
.icon-th{background-position:-240px 0}
.icon-th-list{background-position:-264px 0}
.icon-ok{background-position:-288px 0}
.icon-remove{background-position:-312px 0}
.icon-zoom-in{background-position:-336px 0}
.icon-zoom-out{background-position:-360px 0}
.icon-off{background-position:-384px 0}
.icon-signal{background-position:-408px 0}
.icon-cog{background-position:-432px 0}
.icon-trash{background-position:-456px 0}
.icon-home{background-position:0 -24px}
.icon-file{background-position:-24px -24px}
.icon-time{background-position:-48px -24px}
.icon-road{background-position:-72px -24px}
.icon-download-alt{background-position:-96px -24px}
.icon-download{background-position:-120px -24px}
.icon-upload{background-position:-144px -24px}
.icon-inbox{background-position:-168px -24px}
.icon-play-circle{background-position:-192px -24px}
.icon-repeat{background-position:-216px -24px}
.icon-refresh{background-position:-240px -24px}
.icon-list-alt{background-position:-264px -24px}
.icon-lock{background-position:-287px -24px}
.icon-flag{background-position:-312px -24px}
.icon-headphones{background-position:-336px -24px}
.icon-volume-off{background-position:-360px -24px}
.icon-volume-down{background-position:-384px -24px}
.icon-volume-up{background-position:-408px -24px}
.icon-qrcode{background-position:-432px -24px}
.icon-barcode{background-position:-456px -24px}
.icon-tag{background-position:0 -48px}
.icon-tags{background-position:-25px -48px}
.icon-book{background-position:-48px -48px}
.icon-bookmark{background-position:-72px -48px}
.icon-print{background-position:-96px -48px}
.icon-camera{background-position:-120px -48px}
.icon-font{background-position:-144px -48px}
.icon-bold{background-position:-167px -48px}
.icon-italic{background-position:-192px -48px}
.icon-text-height{background-position:-216px -48px}
.icon-text-width{background-position:-240px -48px}
.icon-align-left{background-position:-264px -48px}
.icon-align-center{background-position:-288px -48px}
.icon-align-right{background-position:-312px -48px}
.icon-align-justify{background-position:-336px -48px}
.icon-list{background-position:-360px -48px}
.icon-indent-left{background-position:-384px -48px}
.icon-indent-right{background-position:-408px -48px}
.icon-facetime-video{background-position:-432px -48px}
.icon-picture{background-position:-456px -48px}
.icon-pencil{background-position:0 -72px}
.icon-map-marker{background-position:-24px -72px}
.icon-adjust{background-position:-48px -72px}
.icon-tint{background-position:-72px -72px}
.icon-edit{background-position:-96px -72px}
.icon-share{background-position:-120px -72px}
.icon-check{background-position:-144px -72px}
.icon-move{background-position:-168px -72px}
.icon-step-backward{background-position:-192px -72px}
.icon-fast-backward{background-position:-216px -72px}
.icon-backward{background-position:-240px -72px}
.icon-play{background-position:-264px -72px}
.icon-pause{background-position:-288px -72px}
.icon-stop{background-position:-312px -72px}
.icon-forward{background-position:-336px -72px}
.icon-fast-forward{background-position:-360px -72px}
.icon-step-forward{background-position:-384px -72px}
.icon-eject{background-position:-408px -72px}
.icon-chevron-left{background-position:-432px -72px}
.icon-chevron-right{background-position:-456px -72px}
.icon-plus-sign{background-position:0 -96px}
.icon-minus-sign{background-position:-24px -96px}
.icon-remove-sign{background-position:-48px -96px}
.icon-ok-sign{background-position:-72px -96px}
.icon-question-sign{background-position:-96px -96px}
.icon-info-sign{background-position:-120px -96px}
.icon-screenshot{background-position:-144px -96px}
.icon-remove-circle{background-position:-168px -96px}
.icon-ok-circle{background-position:-192px -96px}
.icon-ban-circle{background-position:-216px -96px}
.icon-arrow-left{background-position:-240px -96px}
.icon-arrow-right{background-position:-264px -96px}
.icon-arrow-up{background-position:-289px -96px}
.icon-arrow-down{background-position:-312px -96px}
.icon-share-alt{background-position:-336px -96px}
.icon-resize-full{background-position:-360px -96px}
.icon-resize-small{background-position:-384px -96px}
.icon-plus{background-position:-408px -96px}
.icon-minus{background-position:-433px -96px}
.icon-asterisk{background-position:-456px -96px}
.icon-exclamation-sign{background-position:0 -120px}
.icon-gift{background-position:-24px -120px}
.icon-leaf{background-position:-48px -120px}
.icon-fire{background-position:-72px -120px}
.icon-eye-open{background-position:-96px -120px}
.icon-eye-close{background-position:-120px -120px}
.icon-warning-sign{background-position:-144px -120px}
.icon-plane{background-position:-168px -120px}
.icon-calendar{background-position:-192px -120px}
.icon-random{background-position:-216px -120px;width:16px}
.icon-comment{background-position:-240px -120px}
.icon-magnet{background-position:-264px -120px}
.icon-chevron-up{background-position:-288px -120px}
.icon-chevron-down{background-position:-313px -119px}
.icon-retweet{background-position:-336px -120px}
.icon-shopping-cart{background-position:-360px -120px}
.icon-folder-close{background-position:-384px -120px;width:16px}
.icon-folder-open{background-position:-408px -120px;width:16px}
.icon-resize-vertical{background-position:-432px -119px}
.icon-resize-horizontal{background-position:-456px -118px}
.icon-hdd{background-position:0 -144px}
.icon-bullhorn{background-position:-24px -144px}
.icon-bell{background-position:-48px -144px}
.icon-certificate{background-position:-72px -144px}
.icon-thumbs-up{background-position:-96px -144px}
.icon-thumbs-down{background-position:-120px -144px}
.icon-hand-right{background-position:-144px -144px}
.icon-hand-left{background-position:-168px -144px}
.icon-hand-up{background-position:-192px -144px}
.icon-hand-down{background-position:-216px -144px}
.icon-circle-arrow-right{background-position:-240px -144px}
.icon-circle-arrow-left{background-position:-264px -144px}
.icon-circle-arrow-up{background-position:-288px -144px}
.icon-circle-arrow-down{background-position:-312px -144px}
.icon-globe{background-position:-336px -144px}
.icon-wrench{background-position:-360px -144px}
.icon-tasks{background-position:-384px -144px}
.icon-filter{background-position:-408px -144px}
.icon-briefcase{background-position:-432px -144px}
.icon-fullscreen{background-position:-456px -144px}
.dropup,.dropdown{position:relative}
.dropdown-toggle{*margin-bottom:-3px}
.dropdown-toggle:active,.open .dropdown-toggle{outline:0}
.caret{display:inline-block;width:0;height:0;vertical-align:top;border-top:4px solid #000;border-right:4px solid transparent;border-left:4px solid transparent;content:""}
.dropdown .caret{margin-top:8px;margin-left:2px}
.dropdown-menu{position:absolute;top:100%;left:0;z-index:1000;display:none;float:left;min-width:160px;padding:5px 0;margin:2px 0 0;list-style:none;background-color:#fff;border:1px solid #ccc;border:1px solid rgba(0,0,0,0.2);*border-right-width:2px;*border-bottom-width:2px;-webkit-border-radius:6px;-moz-border-radius:6px;border-radius:6px;-webkit-box-shadow:0 5px 10px rgba(0,0,0,0.2);-moz-box-shadow:0 5px 10px rgba(0,0,0,0.2);box-shadow:0 5px 10px rgba(0,0,0,0.2);-webkit-background-clip:padding-box;-moz-background-clip:padding;background-clip:padding-box}.dropdown-menu.pull-right{right:0;left:auto}
.dropdown-menu .divider{*width:100%;height:1px;margin:9px 1px;*margin:-5px 0 5px;overflow:hidden;background-color:#e5e5e5;border-bottom:1px solid #fff}
.dropdown-menu>li>a{display:block;padding:3px 20px;clear:both;font-weight:normal;line-height:20px;color:#333;white-space:nowrap}
.dropdown-menu>li>a:hover,.dropdown-menu>li>a:focus,.dropdown-submenu:hover>a,.dropdown-submenu:focus>a{text-decoration:none;color:#fff;background-color:#0081c2;background-image:-moz-linear-gradient(top, #08c, #0077b3);background-image:-webkit-gradient(linear, 0 0, 0 100%, from(#08c), to(#0077b3));background-image:-webkit-linear-gradient(top, #08c, #0077b3);background-image:-o-linear-gradient(top, #08c, #0077b3);background-image:linear-gradient(to bottom, #08c, #0077b3);background-repeat:repeat-x;filter:progid:DXImageTransform.Microsoft.gradient(startColorstr='#ff0088cc', endColorstr='#ff0077b3', GradientType=0)}
.dropdown-menu>.active>a,.dropdown-menu>.active>a:hover,.dropdown-menu>.active>a:focus{color:#fff;text-decoration:none;outline:0;background-color:#0081c2;background-image:-moz-linear-gradient(top, #08c, #0077b3);background-image:-webkit-gradient(linear, 0 0, 0 100%, from(#08c), to(#0077b3));background-image:-webkit-linear-gradient(top, #08c, #0077b3);background-image:-o-linear-gradient(top, #08c, #0077b3);background-image:linear-gradient(to bottom, #08c, #0077b3);background-repeat:repeat-x;filter:progid:DXImageTransform.Microsoft.gradient(startColorstr='#ff0088cc', endColorstr='#ff0077b3', GradientType=0)}
.dropdown-menu>.disabled>a,.dropdown-menu>.disabled>a:hover,.dropdown-menu>.disabled>a:focus{color:#999}
.dropdown-menu>.disabled>a:hover,.dropdown-menu>.disabled>a:focus{text-decoration:none;background-color:transparent;background-image:none;filter:progid:DXImageTransform.Microsoft.gradient(enabled = false);cursor:default}
.open{*z-index:1000}.open>.dropdown-menu{display:block}
.dropdown-backdrop{position:fixed;left:0;right:0;bottom:0;top:0;z-index:990}
.pull-right>.dropdown-menu{right:0;left:auto}
.dropup .caret,.navbar-fixed-bottom .dropdown .caret{border-top:0;border-bottom:4px solid #000;content:""}
.dropup .dropdown-menu,.navbar-fixed-bottom .dropdown .dropdown-menu{top:auto;bottom:100%;margin-bottom:1px}
.dropdown-submenu{position:relative}
.dropdown-submenu>.dropdown-menu{top:0;left:100%;margin-top:-6px;margin-left:-1px;border-radius:0 6px 6px 6px;-webkit-border-radius:0 6px 6px 6px;-moz-border-radius:0 6px 6px 6px;border-radius:0 6px 6px 6px}
.dropdown-submenu:hover>.dropdown-menu{display:block}
.dropup .dropdown-submenu>.dropdown-menu{top:auto;bottom:0;margin-top:0;margin-bottom:-2px;border-radius:5px 5px 5px 0;-webkit-border-radius:5px 5px 5px 0;-moz-border-radius:5px 5px 5px 0;border-radius:5px 5px 5px 0}
.dropdown-submenu>a:after{display:block;content:" ";float:right;width:0;height:0;border-color:transparent;border-style:solid;border-width:5px 0 5px 5px;border-left-color:#ccc;margin-top:5px;margin-right:-10px}
.dropdown-submenu:hover>a:after{border-left-color:#fff}
.dropdown-submenu.pull-left{float:none}.dropdown-submenu.pull-left>.dropdown-menu{left:-100%;margin-left:10px;border-radius:6px 0 6px 6px;-webkit-border-radius:6px 0 6px 6px;-moz-border-radius:6px 0 6px 6px;border-radius:6px 0 6px 6px}
.dropdown .dropdown-menu .nav-header{padding-left:20px;padding-right:20px}
.typeahead{z-index:1051;margin-top:2px;border-radius:4px;-webkit-border-radius:4px;-moz-border-radius:4px;border-radius:4px}
.well{min-height:20px;padding:19px;margin-bottom:20px;background-color:#f5f5f5;border:1px solid #e3e3e3;-webkit-border-radius:4px;-moz-border-radius:4px;border-radius:4px;-webkit-box-shadow:inset 0 1px 1px rgba(0,0,0,0.05);-moz-box-shadow:inset 0 1px 1px rgba(0,0,0,0.05);box-shadow:inset 0 1px 1px rgba(0,0,0,0.05)}.well blockquote{border-color:#ddd;border-color:rgba(0,0,0,0.15)}
.well-large{padding:24px;border-radius:6px;-webkit-border-radius:6px;-moz-border-radius:6px;border-radius:6px}
.well-small{padding:9px;border-radius:3px;-webkit-border-radius:3px;-moz-border-radius:3px;border-radius:3px}
.fade{opacity:0;-webkit-transition:opacity .15s linear;-moz-transition:opacity .15s linear;-o-transition:opacity .15s linear;transition:opacity .15s linear}.fade.in{opacity:1}
.collapse{position:relative;height:0;overflow:hidden;-webkit-transition:height .35s ease;-moz-transition:height .35s ease;-o-transition:height .35s ease;transition:height .35s ease}.collapse.in{height:auto}
.close{float:right;font-size:20px;font-weight:bold;line-height:20px;color:#000;text-shadow:0 1px 0 #fff;opacity:.2;filter:alpha(opacity=20)}.close:hover,.close:focus{color:#000;text-decoration:none;cursor:pointer;opacity:.4;filter:alpha(opacity=40)}
button.close{padding:0;cursor:pointer;background:transparent;border:0;-webkit-appearance:none}
.btn{display:inline-block;*display:inline;*zoom:1;padding:4px 12px;margin-bottom:0;font-size:13px;line-height:20px;text-align:center;vertical-align:middle;cursor:pointer;color:#333;text-shadow:0 1px 1px rgba(255,255,255,0.75);background-color:#f5f5f5;background-image:-moz-linear-gradient(top, #fff, #e6e6e6);background-image:-webkit-gradient(linear, 0 0, 0 100%, from(#fff), to(#e6e6e6));background-image:-webkit-linear-gradient(top, #fff, #e6e6e6);background-image:-o-linear-gradient(top, #fff, #e6e6e6);background-image:linear-gradient(to bottom, #fff, #e6e6e6);background-repeat:repeat-x;filter:progid:DXImageTransform.Microsoft.gradient(startColorstr='#ffffffff', endColorstr='#ffe6e6e6', GradientType=0);border-color:#e6e6e6 #e6e6e6 #bfbfbf;border-color:rgba(0,0,0,0.1) rgba(0,0,0,0.1) rgba(0,0,0,0.25);*background-color:#e6e6e6;filter:progid:DXImageTransform.Microsoft.gradient(enabled = false);border:1px solid #ccc;*border:0;border-bottom-color:#b3b3b3;-webkit-border-radius:4px;-moz-border-radius:4px;border-radius:4px;*margin-left:.3em;-webkit-box-shadow:inset 0 1px 0 rgba(255,255,255,.2), 0 1px 2px rgba(0,0,0,.05);-moz-box-shadow:inset 0 1px 0 rgba(255,255,255,.2), 0 1px 2px rgba(0,0,0,.05);box-shadow:inset 0 1px 0 rgba(255,255,255,.2), 0 1px 2px rgba(0,0,0,.05)}.btn:hover,.btn:focus,.btn:active,.btn.active,.btn.disabled,.btn[disabled]{color:#333;background-color:#e6e6e6;*background-color:#d9d9d9}
.btn:active,.btn.active{background-color:#ccc \9}
.btn:first-child{*margin-left:0}
.btn:hover,.btn:focus{color:#333;text-decoration:none;background-position:0 -15px;-webkit-transition:background-position .1s linear;-moz-transition:background-position .1s linear;-o-transition:background-position .1s linear;transition:background-position .1s linear}
.btn:focus{outline:thin dotted #333;outline:5px auto -webkit-focus-ring-color;outline-offset:-2px}
.btn.active,.btn:active{background-image:none;outline:0;-webkit-box-shadow:inset 0 2px 4px rgba(0,0,0,.15), 0 1px 2px rgba(0,0,0,.05);-moz-box-shadow:inset 0 2px 4px rgba(0,0,0,.15), 0 1px 2px rgba(0,0,0,.05);box-shadow:inset 0 2px 4px rgba(0,0,0,.15), 0 1px 2px rgba(0,0,0,.05)}
.btn.disabled,.btn[disabled]{cursor:default;background-image:none;opacity:.65;filter:alpha(opacity=65);-webkit-box-shadow:none;-moz-box-shadow:none;box-shadow:none}
.btn-large{padding:11px 19px;font-size:16.25px;border-radius:6px;-webkit-border-radius:6px;-moz-border-radius:6px;border-radius:6px}
.btn-large [class^="icon-"],.btn-large [class*=" icon-"]{margin-top:4px}
.btn-small{padding:2px 10px;font-size:11.049999999999999px;border-radius:3px;-webkit-border-radius:3px;-moz-border-radius:3px;border-radius:3px}
.btn-small [class^="icon-"],.btn-small [class*=" icon-"]{margin-top:0}
.btn-mini [class^="icon-"],.btn-mini [class*=" icon-"]{margin-top:-1px}
.btn-mini{padding:0 6px;font-size:9.75px;border-radius:3px;-webkit-border-radius:3px;-moz-border-radius:3px;border-radius:3px}
.btn-block{display:block;width:100%;padding-left:0;padding-right:0;-webkit-box-sizing:border-box;-moz-box-sizing:border-box;box-sizing:border-box}
.btn-block+.btn-block{margin-top:5px}
input[type="submit"].btn-block,input[type="reset"].btn-block,input[type="button"].btn-block{width:100%}
.btn-primary.active,.btn-warning.active,.btn-danger.active,.btn-success.active,.btn-info.active,.btn-inverse.active{color:rgba(255,255,255,0.75)}
.btn-primary{color:#fff;text-shadow:0 -1px 0 rgba(0,0,0,0.25);background-color:#006dcc;background-image:-moz-linear-gradient(top, #08c, #04c);background-image:-webkit-gradient(linear, 0 0, 0 100%, from(#08c), to(#04c));background-image:-webkit-linear-gradient(top, #08c, #04c);background-image:-o-linear-gradient(top, #08c, #04c);background-image:linear-gradient(to bottom, #08c, #04c);background-repeat:repeat-x;filter:progid:DXImageTransform.Microsoft.gradient(startColorstr='#ff0088cc', endColorstr='#ff0044cc', GradientType=0);border-color:#04c #04c #002a80;border-color:rgba(0,0,0,0.1) rgba(0,0,0,0.1) rgba(0,0,0,0.25);*background-color:#04c;filter:progid:DXImageTransform.Microsoft.gradient(enabled = false)}.btn-primary:hover,.btn-primary:focus,.btn-primary:active,.btn-primary.active,.btn-primary.disabled,.btn-primary[disabled]{color:#fff;background-color:#04c;*background-color:#003bb3}
.btn-primary:active,.btn-primary.active{background-color:#039 \9}
.btn-warning{color:#fff;text-shadow:0 -1px 0 rgba(0,0,0,0.25);background-color:#faa732;background-image:-moz-linear-gradient(top, #fbb450, #f89406);background-image:-webkit-gradient(linear, 0 0, 0 100%, from(#fbb450), to(#f89406));background-image:-webkit-linear-gradient(top, #fbb450, #f89406);background-image:-o-linear-gradient(top, #fbb450, #f89406);background-image:linear-gradient(to bottom, #fbb450, #f89406);background-repeat:repeat-x;filter:progid:DXImageTransform.Microsoft.gradient(startColorstr='#fffbb450', endColorstr='#fff89406', GradientType=0);border-color:#f89406 #f89406 #ad6704;border-color:rgba(0,0,0,0.1) rgba(0,0,0,0.1) rgba(0,0,0,0.25);*background-color:#f89406;filter:progid:DXImageTransform.Microsoft.gradient(enabled = false)}.btn-warning:hover,.btn-warning:focus,.btn-warning:active,.btn-warning.active,.btn-warning.disabled,.btn-warning[disabled]{color:#fff;background-color:#f89406;*background-color:#df8505}
.btn-warning:active,.btn-warning.active{background-color:#c67605 \9}
.btn-danger{color:#fff;text-shadow:0 -1px 0 rgba(0,0,0,0.25);background-color:#da4f49;background-image:-moz-linear-gradient(top, #ee5f5b, #bd362f);background-image:-webkit-gradient(linear, 0 0, 0 100%, from(#ee5f5b), to(#bd362f));background-image:-webkit-linear-gradient(top, #ee5f5b, #bd362f);background-image:-o-linear-gradient(top, #ee5f5b, #bd362f);background-image:linear-gradient(to bottom, #ee5f5b, #bd362f);background-repeat:repeat-x;filter:progid:DXImageTransform.Microsoft.gradient(startColorstr='#ffee5f5b', endColorstr='#ffbd362f', GradientType=0);border-color:#bd362f #bd362f #802420;border-color:rgba(0,0,0,0.1) rgba(0,0,0,0.1) rgba(0,0,0,0.25);*background-color:#bd362f;filter:progid:DXImageTransform.Microsoft.gradient(enabled = false)}.btn-danger:hover,.btn-danger:focus,.btn-danger:active,.btn-danger.active,.btn-danger.disabled,.btn-danger[disabled]{color:#fff;background-color:#bd362f;*background-color:#a9302a}
.btn-danger:active,.btn-danger.active{background-color:#942a25 \9}
.btn-success{color:#fff;text-shadow:0 -1px 0 rgba(0,0,0,0.25);background-color:#5bb75b;background-image:-moz-linear-gradient(top, #62c462, #51a351);background-image:-webkit-gradient(linear, 0 0, 0 100%, from(#62c462), to(#51a351));background-image:-webkit-linear-gradient(top, #62c462, #51a351);background-image:-o-linear-gradient(top, #62c462, #51a351);background-image:linear-gradient(to bottom, #62c462, #51a351);background-repeat:repeat-x;filter:progid:DXImageTransform.Microsoft.gradient(startColorstr='#ff62c462', endColorstr='#ff51a351', GradientType=0);border-color:#51a351 #51a351 #387038;border-color:rgba(0,0,0,0.1) rgba(0,0,0,0.1) rgba(0,0,0,0.25);*background-color:#51a351;filter:progid:DXImageTransform.Microsoft.gradient(enabled = false)}.btn-success:hover,.btn-success:focus,.btn-success:active,.btn-success.active,.btn-success.disabled,.btn-success[disabled]{color:#fff;background-color:#51a351;*background-color:#499249}
.btn-success:active,.btn-success.active{background-color:#408140 \9}
.btn-info{color:#fff;text-shadow:0 -1px 0 rgba(0,0,0,0.25);background-color:#49afcd;background-image:-moz-linear-gradient(top, #5bc0de, #2f96b4);background-image:-webkit-gradient(linear, 0 0, 0 100%, from(#5bc0de), to(#2f96b4));background-image:-webkit-linear-gradient(top, #5bc0de, #2f96b4);background-image:-o-linear-gradient(top, #5bc0de, #2f96b4);background-image:linear-gradient(to bottom, #5bc0de, #2f96b4);background-repeat:repeat-x;filter:progid:DXImageTransform.Microsoft.gradient(startColorstr='#ff5bc0de', endColorstr='#ff2f96b4', GradientType=0);border-color:#2f96b4 #2f96b4 #1f6377;border-color:rgba(0,0,0,0.1) rgba(0,0,0,0.1) rgba(0,0,0,0.25);*background-color:#2f96b4;filter:progid:DXImageTransform.Microsoft.gradient(enabled = false)}.btn-info:hover,.btn-info:focus,.btn-info:active,.btn-info.active,.btn-info.disabled,.btn-info[disabled]{color:#fff;background-color:#2f96b4;*background-color:#2a85a0}
.btn-info:active,.btn-info.active{background-color:#24748c \9}
.btn-inverse{color:#fff;text-shadow:0 -1px 0 rgba(0,0,0,0.25);background-color:#363636;background-image:-moz-linear-gradient(top, #444, #222);background-image:-webkit-gradient(linear, 0 0, 0 100%, from(#444), to(#222));background-image:-webkit-linear-gradient(top, #444, #222);background-image:-o-linear-gradient(top, #444, #222);background-image:linear-gradient(to bottom, #444, #222);background-repeat:repeat-x;filter:progid:DXImageTransform.Microsoft.gradient(startColorstr='#ff444444', endColorstr='#ff222222', GradientType=0);border-color:#222 #222 #000;border-color:rgba(0,0,0,0.1) rgba(0,0,0,0.1) rgba(0,0,0,0.25);*background-color:#222;filter:progid:DXImageTransform.Microsoft.gradient(enabled = false)}.btn-inverse:hover,.btn-inverse:focus,.btn-inverse:active,.btn-inverse.active,.btn-inverse.disabled,.btn-inverse[disabled]{color:#fff;background-color:#222;*background-color:#151515}
.btn-inverse:active,.btn-inverse.active{background-color:#080808 \9}
button.btn,input[type="submit"].btn{*padding-top:3px;*padding-bottom:3px}button.btn::-moz-focus-inner,input[type="submit"].btn::-moz-focus-inner{padding:0;border:0}
button.btn.btn-large,input[type="submit"].btn.btn-large{*padding-top:7px;*padding-bottom:7px}
button.btn.btn-small,input[type="submit"].btn.btn-small{*padding-top:3px;*padding-bottom:3px}
button.btn.btn-mini,input[type="submit"].btn.btn-mini{*padding-top:1px;*padding-bottom:1px}
.btn-link,.btn-link:active,.btn-link[disabled]{background-color:transparent;background-image:none;-webkit-box-shadow:none;-moz-box-shadow:none;box-shadow:none}
.btn-link{border-color:transparent;cursor:pointer;color:#08c;border-radius:0;-webkit-border-radius:0;-moz-border-radius:0;border-radius:0}
.btn-link:hover,.btn-link:focus{color:#005580;text-decoration:underline;background-color:transparent}
.btn-link[disabled]:hover,.btn-link[disabled]:focus{color:#333;text-decoration:none}
.btn-group{position:relative;display:inline-block;*display:inline;*zoom:1;font-size:0;vertical-align:middle;white-space:nowrap;*margin-left:.3em}.btn-group:first-child{*margin-left:0}
.btn-group+.btn-group{margin-left:5px}
.btn-toolbar{font-size:0;margin-top:10px;margin-bottom:10px}.btn-toolbar>.btn+.btn,.btn-toolbar>.btn-group+.btn,.btn-toolbar>.btn+.btn-group{margin-left:5px}
.btn-group>.btn{position:relative;border-radius:0;-webkit-border-radius:0;-moz-border-radius:0;border-radius:0}
.btn-group>.btn+.btn{margin-left:-1px}
.btn-group>.btn,.btn-group>.dropdown-menu,.btn-group>.popover{font-size:13px}
.btn-group>.btn-mini{font-size:9.75px}
.btn-group>.btn-small{font-size:11.049999999999999px}
.btn-group>.btn-large{font-size:16.25px}
.btn-group>.btn:first-child{margin-left:0;-webkit-border-top-left-radius:4px;-moz-border-radius-topleft:4px;border-top-left-radius:4px;-webkit-border-bottom-left-radius:4px;-moz-border-radius-bottomleft:4px;border-bottom-left-radius:4px}
.btn-group>.btn:last-child,.btn-group>.dropdown-toggle{-webkit-border-top-right-radius:4px;-moz-border-radius-topright:4px;border-top-right-radius:4px;-webkit-border-bottom-right-radius:4px;-moz-border-radius-bottomright:4px;border-bottom-right-radius:4px}
.btn-group>.btn.large:first-child{margin-left:0;-webkit-border-top-left-radius:6px;-moz-border-radius-topleft:6px;border-top-left-radius:6px;-webkit-border-bottom-left-radius:6px;-moz-border-radius-bottomleft:6px;border-bottom-left-radius:6px}
.btn-group>.btn.large:last-child,.btn-group>.large.dropdown-toggle{-webkit-border-top-right-radius:6px;-moz-border-radius-topright:6px;border-top-right-radius:6px;-webkit-border-bottom-right-radius:6px;-moz-border-radius-bottomright:6px;border-bottom-right-radius:6px}
.btn-group>.btn:hover,.btn-group>.btn:focus,.btn-group>.btn:active,.btn-group>.btn.active{z-index:2}
.btn-group .dropdown-toggle:active,.btn-group.open .dropdown-toggle{outline:0}
.btn-group>.btn+.dropdown-toggle{padding-left:8px;padding-right:8px;-webkit-box-shadow:inset 1px 0 0 rgba(255,255,255,.125), inset 0 1px 0 rgba(255,255,255,.2), 0 1px 2px rgba(0,0,0,.05);-moz-box-shadow:inset 1px 0 0 rgba(255,255,255,.125), inset 0 1px 0 rgba(255,255,255,.2), 0 1px 2px rgba(0,0,0,.05);box-shadow:inset 1px 0 0 rgba(255,255,255,.125), inset 0 1px 0 rgba(255,255,255,.2), 0 1px 2px rgba(0,0,0,.05);*padding-top:5px;*padding-bottom:5px}
.btn-group>.btn-mini+.dropdown-toggle{padding-left:5px;padding-right:5px;*padding-top:2px;*padding-bottom:2px}
.btn-group>.btn-small+.dropdown-toggle{*padding-top:5px;*padding-bottom:4px}
.btn-group>.btn-large+.dropdown-toggle{padding-left:12px;padding-right:12px;*padding-top:7px;*padding-bottom:7px}
.btn-group.open .dropdown-toggle{background-image:none;-webkit-box-shadow:inset 0 2px 4px rgba(0,0,0,.15), 0 1px 2px rgba(0,0,0,.05);-moz-box-shadow:inset 0 2px 4px rgba(0,0,0,.15), 0 1px 2px rgba(0,0,0,.05);box-shadow:inset 0 2px 4px rgba(0,0,0,.15), 0 1px 2px rgba(0,0,0,.05)}
.btn-group.open .btn.dropdown-toggle{background-color:#e6e6e6}
.btn-group.open .btn-primary.dropdown-toggle{background-color:#04c}
.btn-group.open .btn-warning.dropdown-toggle{background-color:#f89406}
.btn-group.open .btn-danger.dropdown-toggle{background-color:#bd362f}
.btn-group.open .btn-success.dropdown-toggle{background-color:#51a351}
.btn-group.open .btn-info.dropdown-toggle{background-color:#2f96b4}
.btn-group.open .btn-inverse.dropdown-toggle{background-color:#222}
.btn .caret{margin-top:8px;margin-left:0}
.btn-large .caret{margin-top:6px}
.btn-large .caret{border-left-width:5px;border-right-width:5px;border-top-width:5px}
.btn-mini .caret,.btn-small .caret{margin-top:8px}
.dropup .btn-large .caret{border-bottom-width:5px}
.btn-primary .caret,.btn-warning .caret,.btn-danger .caret,.btn-info .caret,.btn-success .caret,.btn-inverse .caret{border-top-color:#fff;border-bottom-color:#fff}
.btn-group-vertical{display:inline-block;*display:inline;*zoom:1}
.btn-group-vertical>.btn{display:block;float:none;max-width:100%;border-radius:0;-webkit-border-radius:0;-moz-border-radius:0;border-radius:0}
.btn-group-vertical>.btn+.btn{margin-left:0;margin-top:-1px}
.btn-group-vertical>.btn:first-child{border-radius:4px 4px 0 0;-webkit-border-radius:4px 4px 0 0;-moz-border-radius:4px 4px 0 0;border-radius:4px 4px 0 0}
.btn-group-vertical>.btn:last-child{border-radius:0 0 4px 4px;-webkit-border-radius:0 0 4px 4px;-moz-border-radius:0 0 4px 4px;border-radius:0 0 4px 4px}
.btn-group-vertical>.btn-large:first-child{border-radius:6px 6px 0 0;-webkit-border-radius:6px 6px 0 0;-moz-border-radius:6px 6px 0 0;border-radius:6px 6px 0 0}
.btn-group-vertical>.btn-large:last-child{border-radius:0 0 6px 6px;-webkit-border-radius:0 0 6px 6px;-moz-border-radius:0 0 6px 6px;border-radius:0 0 6px 6px}
.alert{padding:8px 35px 8px 14px;margin-bottom:20px;text-shadow:0 1px 0 rgba(255,255,255,0.5);background-color:#fcf8e3;border:1px solid #fbeed5;border-radius:4px;-webkit-border-radius:4px;-moz-border-radius:4px;border-radius:4px}
.alert,.alert h4{color:#c09853}
.alert h4{margin:0}
.alert .close{position:relative;top:-2px;right:-21px;line-height:20px}
.alert-success{background-color:#dff0d8;border-color:#d6e9c6;color:#468847}
.alert-success h4{color:#468847}
.alert-danger,.alert-error{background-color:#f2dede;border-color:#eed3d7;color:#b94a48}
.alert-danger h4,.alert-error h4{color:#b94a48}
.alert-info{background-color:#d9edf7;border-color:#bce8f1;color:#3a87ad}
.alert-info h4{color:#3a87ad}
.alert-block{padding-top:14px;padding-bottom:14px}
.alert-block>p,.alert-block>ul{margin-bottom:0}
.alert-block p+p{margin-top:5px}
.nav{margin-left:0;margin-bottom:20px;list-style:none}
.nav>li>a{display:block}
.nav>li>a:hover,.nav>li>a:focus{text-decoration:none;background-color:#eee}
.nav>li>a>img{max-width:none}
.nav>.pull-right{float:right}
.nav-header{display:block;padding:3px 15px;font-size:11px;font-weight:bold;line-height:20px;color:#999;text-shadow:0 1px 0 rgba(255,255,255,0.5);text-transform:uppercase}
.nav li+.nav-header{margin-top:9px}
.nav-list{padding-left:15px;padding-right:15px;margin-bottom:0}
.nav-list>li>a,.nav-list .nav-header{margin-left:-15px;margin-right:-15px;text-shadow:0 1px 0 rgba(255,255,255,0.5)}
.nav-list>li>a{padding:3px 15px}
.nav-list>.active>a,.nav-list>.active>a:hover,.nav-list>.active>a:focus{color:#fff;text-shadow:0 -1px 0 rgba(0,0,0,0.2);background-color:#08c}
.nav-list [class^="icon-"],.nav-list [class*=" icon-"]{margin-right:2px}
.nav-list .divider{*width:100%;height:1px;margin:9px 1px;*margin:-5px 0 5px;overflow:hidden;background-color:#e5e5e5;border-bottom:1px solid #fff}
.nav-tabs,.nav-pills{*zoom:1}.nav-tabs:before,.nav-pills:before,.nav-tabs:after,.nav-pills:after{display:table;content:"";line-height:0}
.nav-tabs:after,.nav-pills:after{clear:both}
.nav-tabs>li,.nav-pills>li{float:left}
.nav-tabs>li>a,.nav-pills>li>a{padding-right:12px;padding-left:12px;margin-right:2px;line-height:14px}
.nav-tabs{border-bottom:1px solid #ddd}
.nav-tabs>li{margin-bottom:-1px}
.nav-tabs>li>a{padding-top:8px;padding-bottom:8px;line-height:20px;border:1px solid transparent;border-radius:4px 4px 0 0;-webkit-border-radius:4px 4px 0 0;-moz-border-radius:4px 4px 0 0;border-radius:4px 4px 0 0}.nav-tabs>li>a:hover,.nav-tabs>li>a:focus{border-color:#eee #eee #ddd}
.nav-tabs>.active>a,.nav-tabs>.active>a:hover,.nav-tabs>.active>a:focus{color:#555;background-color:#fff;border:1px solid #ddd;border-bottom-color:transparent;cursor:default}
.nav-pills>li>a{padding-top:8px;padding-bottom:8px;margin-top:2px;margin-bottom:2px;border-radius:5px;-webkit-border-radius:5px;-moz-border-radius:5px;border-radius:5px}
.nav-pills>.active>a,.nav-pills>.active>a:hover,.nav-pills>.active>a:focus{color:#fff;background-color:#08c}
.nav-stacked>li{float:none}
.nav-stacked>li>a{margin-right:0}
.nav-tabs.nav-stacked{border-bottom:0}
.nav-tabs.nav-stacked>li>a{border:1px solid #ddd;border-radius:0;-webkit-border-radius:0;-moz-border-radius:0;border-radius:0}
.nav-tabs.nav-stacked>li:first-child>a{-webkit-border-top-right-radius:4px;-moz-border-radius-topright:4px;border-top-right-radius:4px;-webkit-border-top-left-radius:4px;-moz-border-radius-topleft:4px;border-top-left-radius:4px}
.nav-tabs.nav-stacked>li:last-child>a{-webkit-border-bottom-right-radius:4px;-moz-border-radius-bottomright:4px;border-bottom-right-radius:4px;-webkit-border-bottom-left-radius:4px;-moz-border-radius-bottomleft:4px;border-bottom-left-radius:4px}
.nav-tabs.nav-stacked>li>a:hover,.nav-tabs.nav-stacked>li>a:focus{border-color:#ddd;z-index:2}
.nav-pills.nav-stacked>li>a{margin-bottom:3px}
.nav-pills.nav-stacked>li:last-child>a{margin-bottom:1px}
.nav-tabs .dropdown-menu{border-radius:0 0 6px 6px;-webkit-border-radius:0 0 6px 6px;-moz-border-radius:0 0 6px 6px;border-radius:0 0 6px 6px}
.nav-pills .dropdown-menu{border-radius:6px;-webkit-border-radius:6px;-moz-border-radius:6px;border-radius:6px}
.nav .dropdown-toggle .caret{border-top-color:#08c;border-bottom-color:#08c;margin-top:6px}
.nav .dropdown-toggle:hover .caret,.nav .dropdown-toggle:focus .caret{border-top-color:#005580;border-bottom-color:#005580}
.nav-tabs .dropdown-toggle .caret{margin-top:8px}
.nav .active .dropdown-toggle .caret{border-top-color:#fff;border-bottom-color:#fff}
.nav-tabs .active .dropdown-toggle .caret{border-top-color:#555;border-bottom-color:#555}
.nav>.dropdown.active>a:hover,.nav>.dropdown.active>a:focus{cursor:pointer}
.nav-tabs .open .dropdown-toggle,.nav-pills .open .dropdown-toggle,.nav>li.dropdown.open.active>a:hover,.nav>li.dropdown.open.active>a:focus{color:#fff;background-color:#999;border-color:#999}
.nav li.dropdown.open .caret,.nav li.dropdown.open.active .caret,.nav li.dropdown.open a:hover .caret,.nav li.dropdown.open a:focus .caret{border-top-color:#fff;border-bottom-color:#fff;opacity:1;filter:alpha(opacity=100)}
.tabs-stacked .open>a:hover,.tabs-stacked .open>a:focus{border-color:#999}
.tabbable{*zoom:1}.tabbable:before,.tabbable:after{display:table;content:"";line-height:0}
.tabbable:after{clear:both}
.tab-content{overflow:auto}
.tabs-below>.nav-tabs,.tabs-right>.nav-tabs,.tabs-left>.nav-tabs{border-bottom:0}
.tab-content>.tab-pane,.pill-content>.pill-pane{display:none}
.tab-content>.active,.pill-content>.active{display:block}
.tabs-below>.nav-tabs{border-top:1px solid #ddd}
.tabs-below>.nav-tabs>li{margin-top:-1px;margin-bottom:0}
.tabs-below>.nav-tabs>li>a{border-radius:0 0 4px 4px;-webkit-border-radius:0 0 4px 4px;-moz-border-radius:0 0 4px 4px;border-radius:0 0 4px 4px}.tabs-below>.nav-tabs>li>a:hover,.tabs-below>.nav-tabs>li>a:focus{border-bottom-color:transparent;border-top-color:#ddd}
.tabs-below>.nav-tabs>.active>a,.tabs-below>.nav-tabs>.active>a:hover,.tabs-below>.nav-tabs>.active>a:focus{border-color:transparent #ddd #ddd #ddd}
.tabs-left>.nav-tabs>li,.tabs-right>.nav-tabs>li{float:none}
.tabs-left>.nav-tabs>li>a,.tabs-right>.nav-tabs>li>a{min-width:74px;margin-right:0;margin-bottom:3px}
.tabs-left>.nav-tabs{float:left;margin-right:19px;border-right:1px solid #ddd}
.tabs-left>.nav-tabs>li>a{margin-right:-1px;border-radius:4px 0 0 4px;-webkit-border-radius:4px 0 0 4px;-moz-border-radius:4px 0 0 4px;border-radius:4px 0 0 4px}
.tabs-left>.nav-tabs>li>a:hover,.tabs-left>.nav-tabs>li>a:focus{border-color:#eee #ddd #eee #eee}
.tabs-left>.nav-tabs .active>a,.tabs-left>.nav-tabs .active>a:hover,.tabs-left>.nav-tabs .active>a:focus{border-color:#ddd transparent #ddd #ddd;*border-right-color:#fff}
.tabs-right>.nav-tabs{float:right;margin-left:19px;border-left:1px solid #ddd}
.tabs-right>.nav-tabs>li>a{margin-left:-1px;border-radius:0 4px 4px 0;-webkit-border-radius:0 4px 4px 0;-moz-border-radius:0 4px 4px 0;border-radius:0 4px 4px 0}
.tabs-right>.nav-tabs>li>a:hover,.tabs-right>.nav-tabs>li>a:focus{border-color:#eee #eee #eee #ddd}
.tabs-right>.nav-tabs .active>a,.tabs-right>.nav-tabs .active>a:hover,.tabs-right>.nav-tabs .active>a:focus{border-color:#ddd #ddd #ddd transparent;*border-left-color:#fff}
.nav>.disabled>a{color:#999}
.nav>.disabled>a:hover,.nav>.disabled>a:focus{text-decoration:none;background-color:transparent;cursor:default}
.navbar{overflow:visible;margin-bottom:20px;*position:relative;*z-index:2}
.navbar-inner{min-height:36px;padding-left:20px;padding-right:20px;background-color:#fafafa;background-image:-moz-linear-gradient(top, #fff, #f2f2f2);background-image:-webkit-gradient(linear, 0 0, 0 100%, from(#fff), to(#f2f2f2));background-image:-webkit-linear-gradient(top, #fff, #f2f2f2);background-image:-o-linear-gradient(top, #fff, #f2f2f2);background-image:linear-gradient(to bottom, #fff, #f2f2f2);background-repeat:repeat-x;filter:progid:DXImageTransform.Microsoft.gradient(startColorstr='#ffffffff', endColorstr='#fff2f2f2', GradientType=0);border:1px solid #d4d4d4;-webkit-border-radius:4px;-moz-border-radius:4px;border-radius:4px;-webkit-box-shadow:0 1px 4px rgba(0,0,0,0.065);-moz-box-shadow:0 1px 4px rgba(0,0,0,0.065);box-shadow:0 1px 4px rgba(0,0,0,0.065);*zoom:1}.navbar-inner:before,.navbar-inner:after{display:table;content:"";line-height:0}
.navbar-inner:after{clear:both}
.navbar .container{width:auto}
.nav-collapse.collapse{height:auto;overflow:visible}
.navbar .brand{float:left;display:block;padding:8px 20px 8px;margin-left:-20px;font-size:20px;font-weight:200;color:#777;text-shadow:0 1px 0 #fff}.navbar .brand:hover,.navbar .brand:focus{text-decoration:none}
.navbar-text{margin-bottom:0;line-height:36px;color:#777}
.navbar-link{color:#777}.navbar-link:hover,.navbar-link:focus{color:#333}
.navbar .divider-vertical{height:36px;margin:0 9px;border-left:1px solid #f2f2f2;border-right:1px solid #fff}
.navbar .btn,.navbar .btn-group{margin-top:3px}
.navbar .btn-group .btn,.navbar .input-prepend .btn,.navbar .input-append .btn,.navbar .input-prepend .btn-group,.navbar .input-append .btn-group{margin-top:0}
.navbar-form{margin-bottom:0;*zoom:1}.navbar-form:before,.navbar-form:after{display:table;content:"";line-height:0}
.navbar-form:after{clear:both}
.navbar-form input,.navbar-form select,.navbar-form .radio,.navbar-form .checkbox{margin-top:3px}
.navbar-form input,.navbar-form select,.navbar-form .btn{display:inline-block;margin-bottom:0}
.navbar-form input[type="image"],.navbar-form input[type="checkbox"],.navbar-form input[type="radio"]{margin-top:3px}
.navbar-form .input-append,.navbar-form .input-prepend{margin-top:5px;white-space:nowrap}.navbar-form .input-append input,.navbar-form .input-prepend input{margin-top:0}
.navbar-search{position:relative;float:left;margin-top:3px;margin-bottom:0}.navbar-search .search-query{margin-bottom:0;padding:4px 14px;font-family:"Helvetica Neue",Helvetica,Arial,sans-serif;font-size:13px;font-weight:normal;line-height:1;border-radius:15px;-webkit-border-radius:15px;-moz-border-radius:15px;border-radius:15px}
.navbar-static-top{position:static;margin-bottom:0}.navbar-static-top .navbar-inner{border-radius:0;-webkit-border-radius:0;-moz-border-radius:0;border-radius:0}
.navbar-fixed-top,.navbar-fixed-bottom{position:fixed;right:0;left:0;z-index:1030;margin-bottom:0}
.navbar-fixed-top .navbar-inner,.navbar-static-top .navbar-inner{border-width:0 0 1px}
.navbar-fixed-bottom .navbar-inner{border-width:1px 0 0}
.navbar-fixed-top .navbar-inner,.navbar-fixed-bottom .navbar-inner{padding-left:0;padding-right:0;border-radius:0;-webkit-border-radius:0;-moz-border-radius:0;border-radius:0}
.navbar-static-top .container,.navbar-fixed-top .container,.navbar-fixed-bottom .container{width:940px}
.navbar-fixed-top{top:0}
.navbar-fixed-top .navbar-inner,.navbar-static-top .navbar-inner{-webkit-box-shadow:0 1px 10px rgba(0,0,0,.1);-moz-box-shadow:0 1px 10px rgba(0,0,0,.1);box-shadow:0 1px 10px rgba(0,0,0,.1)}
.navbar-fixed-bottom{bottom:0}.navbar-fixed-bottom .navbar-inner{-webkit-box-shadow:0 -1px 10px rgba(0,0,0,.1);-moz-box-shadow:0 -1px 10px rgba(0,0,0,.1);box-shadow:0 -1px 10px rgba(0,0,0,.1)}
.navbar .nav{position:relative;left:0;display:block;float:left;margin:0 10px 0 0}
.navbar .nav.pull-right{float:right;margin-right:0}
.navbar .nav>li{float:left}
.navbar .nav>li>a{float:none;padding:8px 15px 8px;color:#777;text-decoration:none;text-shadow:0 1px 0 #fff}
.navbar .nav .dropdown-toggle .caret{margin-top:8px}
.navbar .nav>li>a:focus,.navbar .nav>li>a:hover{background-color:transparent;color:#333;text-decoration:none}
.navbar .nav>.active>a,.navbar .nav>.active>a:hover,.navbar .nav>.active>a:focus{color:#555;text-decoration:none;background-color:#e5e5e5;-webkit-box-shadow:inset 0 3px 8px rgba(0,0,0,0.125);-moz-box-shadow:inset 0 3px 8px rgba(0,0,0,0.125);box-shadow:inset 0 3px 8px rgba(0,0,0,0.125)}
.navbar .btn-navbar{display:none;float:right;padding:7px 10px;margin-left:5px;margin-right:5px;color:#fff;text-shadow:0 -1px 0 rgba(0,0,0,0.25);background-color:#ededed;background-image:-moz-linear-gradient(top, #f2f2f2, #e5e5e5);background-image:-webkit-gradient(linear, 0 0, 0 100%, from(#f2f2f2), to(#e5e5e5));background-image:-webkit-linear-gradient(top, #f2f2f2, #e5e5e5);background-image:-o-linear-gradient(top, #f2f2f2, #e5e5e5);background-image:linear-gradient(to bottom, #f2f2f2, #e5e5e5);background-repeat:repeat-x;filter:progid:DXImageTransform.Microsoft.gradient(startColorstr='#fff2f2f2', endColorstr='#ffe5e5e5', GradientType=0);border-color:#e5e5e5 #e5e5e5 #bfbfbf;border-color:rgba(0,0,0,0.1) rgba(0,0,0,0.1) rgba(0,0,0,0.25);*background-color:#e5e5e5;filter:progid:DXImageTransform.Microsoft.gradient(enabled = false);-webkit-box-shadow:inset 0 1px 0 rgba(255,255,255,.1), 0 1px 0 rgba(255,255,255,.075);-moz-box-shadow:inset 0 1px 0 rgba(255,255,255,.1), 0 1px 0 rgba(255,255,255,.075);box-shadow:inset 0 1px 0 rgba(255,255,255,.1), 0 1px 0 rgba(255,255,255,.075)}.navbar .btn-navbar:hover,.navbar .btn-navbar:focus,.navbar .btn-navbar:active,.navbar .btn-navbar.active,.navbar .btn-navbar.disabled,.navbar .btn-navbar[disabled]{color:#fff;background-color:#e5e5e5;*background-color:#d9d9d9}
.navbar .btn-navbar:active,.navbar .btn-navbar.active{background-color:#ccc \9}
.navbar .btn-navbar .icon-bar{display:block;width:18px;height:2px;background-color:#f5f5f5;-webkit-border-radius:1px;-moz-border-radius:1px;border-radius:1px;-webkit-box-shadow:0 1px 0 rgba(0,0,0,0.25);-moz-box-shadow:0 1px 0 rgba(0,0,0,0.25);box-shadow:0 1px 0 rgba(0,0,0,0.25)}
.btn-navbar .icon-bar+.icon-bar{margin-top:3px}
.navbar .nav>li>.dropdown-menu:before{content:'';display:inline-block;border-left:7px solid transparent;border-right:7px solid transparent;border-bottom:7px solid #ccc;border-bottom-color:rgba(0,0,0,0.2);position:absolute;top:-7px;left:9px}
.navbar .nav>li>.dropdown-menu:after{content:'';display:inline-block;border-left:6px solid transparent;border-right:6px solid transparent;border-bottom:6px solid #fff;position:absolute;top:-6px;left:10px}
.navbar-fixed-bottom .nav>li>.dropdown-menu:before{border-top:7px solid #ccc;border-top-color:rgba(0,0,0,0.2);border-bottom:0;bottom:-7px;top:auto}
.navbar-fixed-bottom .nav>li>.dropdown-menu:after{border-top:6px solid #fff;border-bottom:0;bottom:-6px;top:auto}
.navbar .nav li.dropdown>a:hover .caret,.navbar .nav li.dropdown>a:focus .caret{border-top-color:#333;border-bottom-color:#333}
.navbar .nav li.dropdown.open>.dropdown-toggle,.navbar .nav li.dropdown.active>.dropdown-toggle,.navbar .nav li.dropdown.open.active>.dropdown-toggle{background-color:#e5e5e5;color:#555}
.navbar .nav li.dropdown>.dropdown-toggle .caret{border-top-color:#777;border-bottom-color:#777}
.navbar .nav li.dropdown.open>.dropdown-toggle .caret,.navbar .nav li.dropdown.active>.dropdown-toggle .caret,.navbar .nav li.dropdown.open.active>.dropdown-toggle .caret{border-top-color:#555;border-bottom-color:#555}
.navbar .pull-right>li>.dropdown-menu,.navbar .nav>li>.dropdown-menu.pull-right{left:auto;right:0}.navbar .pull-right>li>.dropdown-menu:before,.navbar .nav>li>.dropdown-menu.pull-right:before{left:auto;right:12px}
.navbar .pull-right>li>.dropdown-menu:after,.navbar .nav>li>.dropdown-menu.pull-right:after{left:auto;right:13px}
.navbar .pull-right>li>.dropdown-menu .dropdown-menu,.navbar .nav>li>.dropdown-menu.pull-right .dropdown-menu{left:auto;right:100%;margin-left:0;margin-right:-1px;border-radius:6px 0 6px 6px;-webkit-border-radius:6px 0 6px 6px;-moz-border-radius:6px 0 6px 6px;border-radius:6px 0 6px 6px}
.navbar-inverse .navbar-inner{background-color:#1b1b1b;background-image:-moz-linear-gradient(top, #222, #111);background-image:-webkit-gradient(linear, 0 0, 0 100%, from(#222), to(#111));background-image:-webkit-linear-gradient(top, #222, #111);background-image:-o-linear-gradient(top, #222, #111);background-image:linear-gradient(to bottom, #222, #111);background-repeat:repeat-x;filter:progid:DXImageTransform.Microsoft.gradient(startColorstr='#ff222222', endColorstr='#ff111111', GradientType=0);border-color:#252525}
.navbar-inverse .brand,.navbar-inverse .nav>li>a{color:#999;text-shadow:0 -1px 0 rgba(0,0,0,0.25)}.navbar-inverse .brand:hover,.navbar-inverse .nav>li>a:hover,.navbar-inverse .brand:focus,.navbar-inverse .nav>li>a:focus{color:#fff}
.navbar-inverse .brand{color:#999}
.navbar-inverse .navbar-text{color:#999}
.navbar-inverse .nav>li>a:focus,.navbar-inverse .nav>li>a:hover{background-color:transparent;color:#fff}
.navbar-inverse .nav .active>a,.navbar-inverse .nav .active>a:hover,.navbar-inverse .nav .active>a:focus{color:#fff;background-color:#111}
.navbar-inverse .navbar-link{color:#999}.navbar-inverse .navbar-link:hover,.navbar-inverse .navbar-link:focus{color:#fff}
.navbar-inverse .divider-vertical{border-left-color:#111;border-right-color:#222}
.navbar-inverse .nav li.dropdown.open>.dropdown-toggle,.navbar-inverse .nav li.dropdown.active>.dropdown-toggle,.navbar-inverse .nav li.dropdown.open.active>.dropdown-toggle{background-color:#111;color:#fff}
.navbar-inverse .nav li.dropdown>a:hover .caret,.navbar-inverse .nav li.dropdown>a:focus .caret{border-top-color:#fff;border-bottom-color:#fff}
.navbar-inverse .nav li.dropdown>.dropdown-toggle .caret{border-top-color:#999;border-bottom-color:#999}
.navbar-inverse .nav li.dropdown.open>.dropdown-toggle .caret,.navbar-inverse .nav li.dropdown.active>.dropdown-toggle .caret,.navbar-inverse .nav li.dropdown.open.active>.dropdown-toggle .caret{border-top-color:#fff;border-bottom-color:#fff}
.navbar-inverse .navbar-search .search-query{color:#fff;background-color:#515151;border-color:#111;-webkit-box-shadow:inset 0 1px 2px rgba(0,0,0,.1), 0 1px 0 rgba(255,255,255,.15);-moz-box-shadow:inset 0 1px 2px rgba(0,0,0,.1), 0 1px 0 rgba(255,255,255,.15);box-shadow:inset 0 1px 2px rgba(0,0,0,.1), 0 1px 0 rgba(255,255,255,.15);-webkit-transition:none;-moz-transition:none;-o-transition:none;transition:none}.navbar-inverse .navbar-search .search-query:-moz-placeholder{color:#ccc}
.navbar-inverse .navbar-search .search-query:-ms-input-placeholder{color:#ccc}
.navbar-inverse .navbar-search .search-query::-webkit-input-placeholder{color:#ccc}
.navbar-inverse .navbar-search .search-query:focus,.navbar-inverse .navbar-search .search-query.focused{padding:5px 15px;color:#333;text-shadow:0 1px 0 #fff;background-color:#fff;border:0;-webkit-box-shadow:0 0 3px rgba(0,0,0,0.15);-moz-box-shadow:0 0 3px rgba(0,0,0,0.15);box-shadow:0 0 3px rgba(0,0,0,0.15);outline:0}
.navbar-inverse .btn-navbar{color:#fff;text-shadow:0 -1px 0 rgba(0,0,0,0.25);background-color:#0e0e0e;background-image:-moz-linear-gradient(top, #151515, #040404);background-image:-webkit-gradient(linear, 0 0, 0 100%, from(#151515), to(#040404));background-image:-webkit-linear-gradient(top, #151515, #040404);background-image:-o-linear-gradient(top, #151515, #040404);background-image:linear-gradient(to bottom, #151515, #040404);background-repeat:repeat-x;filter:progid:DXImageTransform.Microsoft.gradient(startColorstr='#ff151515', endColorstr='#ff040404', GradientType=0);border-color:#040404 #040404 #000;border-color:rgba(0,0,0,0.1) rgba(0,0,0,0.1) rgba(0,0,0,0.25);*background-color:#040404;filter:progid:DXImageTransform.Microsoft.gradient(enabled = false)}.navbar-inverse .btn-navbar:hover,.navbar-inverse .btn-navbar:focus,.navbar-inverse .btn-navbar:active,.navbar-inverse .btn-navbar.active,.navbar-inverse .btn-navbar.disabled,.navbar-inverse .btn-navbar[disabled]{color:#fff;background-color:#040404;*background-color:#000}
.navbar-inverse .btn-navbar:active,.navbar-inverse .btn-navbar.active{background-color:#000 \9}
.breadcrumb{padding:8px 15px;margin:0 0 20px;list-style:none;background-color:#f5f5f5;border-radius:4px;-webkit-border-radius:4px;-moz-border-radius:4px;border-radius:4px}.breadcrumb>li{display:inline-block;*display:inline;*zoom:1;text-shadow:0 1px 0 #fff}.breadcrumb>li>.divider{padding:0 5px;color:#ccc}
.breadcrumb>.active{color:#999}
.pagination{margin:20px 0}
.pagination ul{display:inline-block;*display:inline;*zoom:1;margin-left:0;margin-bottom:0;-webkit-border-radius:4px;-moz-border-radius:4px;border-radius:4px;-webkit-box-shadow:0 1px 2px rgba(0,0,0,0.05);-moz-box-shadow:0 1px 2px rgba(0,0,0,0.05);box-shadow:0 1px 2px rgba(0,0,0,0.05)}
.pagination ul>li{display:inline}
.pagination ul>li>a,.pagination ul>li>span{float:left;padding:4px 12px;line-height:20px;text-decoration:none;background-color:#fff;border:1px solid #ddd;border-left-width:0}
.pagination ul>li>a:hover,.pagination ul>li>a:focus,.pagination ul>.active>a,.pagination ul>.active>span{background-color:#f5f5f5}
.pagination ul>.active>a,.pagination ul>.active>span{color:#999;cursor:default}
.pagination ul>.disabled>span,.pagination ul>.disabled>a,.pagination ul>.disabled>a:hover,.pagination ul>.disabled>a:focus{color:#999;background-color:transparent;cursor:default}
.pagination ul>li:first-child>a,.pagination ul>li:first-child>span{border-left-width:1px;-webkit-border-top-left-radius:4px;-moz-border-radius-topleft:4px;border-top-left-radius:4px;-webkit-border-bottom-left-radius:4px;-moz-border-radius-bottomleft:4px;border-bottom-left-radius:4px}
.pagination ul>li:last-child>a,.pagination ul>li:last-child>span{-webkit-border-top-right-radius:4px;-moz-border-radius-topright:4px;border-top-right-radius:4px;-webkit-border-bottom-right-radius:4px;-moz-border-radius-bottomright:4px;border-bottom-right-radius:4px}
.pagination-centered{text-align:center}
.pagination-right{text-align:right}
.pagination-large ul>li>a,.pagination-large ul>li>span{padding:11px 19px;font-size:16.25px}
.pagination-large ul>li:first-child>a,.pagination-large ul>li:first-child>span{-webkit-border-top-left-radius:6px;-moz-border-radius-topleft:6px;border-top-left-radius:6px;-webkit-border-bottom-left-radius:6px;-moz-border-radius-bottomleft:6px;border-bottom-left-radius:6px}
.pagination-large ul>li:last-child>a,.pagination-large ul>li:last-child>span{-webkit-border-top-right-radius:6px;-moz-border-radius-topright:6px;border-top-right-radius:6px;-webkit-border-bottom-right-radius:6px;-moz-border-radius-bottomright:6px;border-bottom-right-radius:6px}
.pagination-mini ul>li:first-child>a,.pagination-small ul>li:first-child>a,.pagination-mini ul>li:first-child>span,.pagination-small ul>li:first-child>span{-webkit-border-top-left-radius:3px;-moz-border-radius-topleft:3px;border-top-left-radius:3px;-webkit-border-bottom-left-radius:3px;-moz-border-radius-bottomleft:3px;border-bottom-left-radius:3px}
.pagination-mini ul>li:last-child>a,.pagination-small ul>li:last-child>a,.pagination-mini ul>li:last-child>span,.pagination-small ul>li:last-child>span{-webkit-border-top-right-radius:3px;-moz-border-radius-topright:3px;border-top-right-radius:3px;-webkit-border-bottom-right-radius:3px;-moz-border-radius-bottomright:3px;border-bottom-right-radius:3px}
.pagination-small ul>li>a,.pagination-small ul>li>span{padding:2px 10px;font-size:11.049999999999999px}
.pagination-mini ul>li>a,.pagination-mini ul>li>span{padding:0 6px;font-size:9.75px}
.pager{margin:20px 0;list-style:none;text-align:center;*zoom:1}.pager:before,.pager:after{display:table;content:"";line-height:0}
.pager:after{clear:both}
.pager li{display:inline}
.pager li>a,.pager li>span{display:inline-block;padding:5px 14px;background-color:#fff;border:1px solid #ddd;border-radius:15px;-webkit-border-radius:15px;-moz-border-radius:15px;border-radius:15px}
.pager li>a:hover,.pager li>a:focus{text-decoration:none;background-color:#f5f5f5}
.pager .next>a,.pager .next>span{float:right}
.pager .previous>a,.pager .previous>span{float:left}
.pager .disabled>a,.pager .disabled>a:hover,.pager .disabled>a:focus,.pager .disabled>span{color:#999;background-color:#fff;cursor:default}
.modal-backdrop{position:fixed;top:0;right:0;bottom:0;left:0;z-index:1040;background-color:#000}.modal-backdrop.fade{opacity:0}
.modal-backdrop,.modal-backdrop.fade.in{opacity:.8;filter:alpha(opacity=80)}
.modal{position:fixed;top:10%;left:50%;z-index:1050;width:560px;margin-left:-280px;background-color:#fff;border:1px solid #999;border:1px solid rgba(0,0,0,0.3);*border:1px solid #999;-webkit-border-radius:6px;-moz-border-radius:6px;border-radius:6px;-webkit-box-shadow:0 3px 7px rgba(0,0,0,0.3);-moz-box-shadow:0 3px 7px rgba(0,0,0,0.3);box-shadow:0 3px 7px rgba(0,0,0,0.3);-webkit-background-clip:padding-box;-moz-background-clip:padding-box;background-clip:padding-box;outline:none}.modal.fade{-webkit-transition:opacity .3s linear, top .3s ease-out;-moz-transition:opacity .3s linear, top .3s ease-out;-o-transition:opacity .3s linear, top .3s ease-out;transition:opacity .3s linear, top .3s ease-out;top:-25%}
.modal.fade.in{top:10%}
.modal-header{padding:9px 15px;border-bottom:1px solid #eee}.modal-header .close{margin-top:2px}
.modal-header h3{margin:0;line-height:30px}
.modal-body{position:relative;overflow-y:auto;max-height:400px;padding:15px}
.modal-form{margin-bottom:0}
.modal-footer{padding:14px 15px 15px;margin-bottom:0;text-align:right;background-color:#f5f5f5;border-top:1px solid #ddd;-webkit-border-radius:0 0 6px 6px;-moz-border-radius:0 0 6px 6px;border-radius:0 0 6px 6px;-webkit-box-shadow:inset 0 1px 0 #fff;-moz-box-shadow:inset 0 1px 0 #fff;box-shadow:inset 0 1px 0 #fff;*zoom:1}.modal-footer:before,.modal-footer:after{display:table;content:"";line-height:0}
.modal-footer:after{clear:both}
.modal-footer .btn+.btn{margin-left:5px;margin-bottom:0}
.modal-footer .btn-group .btn+.btn{margin-left:-1px}
.modal-footer .btn-block+.btn-block{margin-left:0}
.tooltip{position:absolute;z-index:1030;display:block;visibility:visible;font-size:11px;line-height:1.4;opacity:0;filter:alpha(opacity=0)}.tooltip.in{opacity:.8;filter:alpha(opacity=80)}
.tooltip.top{margin-top:-3px;padding:5px 0}
.tooltip.right{margin-left:3px;padding:0 5px}
.tooltip.bottom{margin-top:3px;padding:5px 0}
.tooltip.left{margin-left:-3px;padding:0 5px}
.tooltip-inner{max-width:200px;padding:8px;color:#fff;text-align:center;text-decoration:none;background-color:#000;border-radius:4px;-webkit-border-radius:4px;-moz-border-radius:4px;border-radius:4px}
.tooltip-arrow{position:absolute;width:0;height:0;border-color:transparent;border-style:solid}
.tooltip.top .tooltip-arrow{bottom:0;left:50%;margin-left:-5px;border-width:5px 5px 0;border-top-color:#000}
.tooltip.right .tooltip-arrow{top:50%;left:0;margin-top:-5px;border-width:5px 5px 5px 0;border-right-color:#000}
.tooltip.left .tooltip-arrow{top:50%;right:0;margin-top:-5px;border-width:5px 0 5px 5px;border-left-color:#000}
.tooltip.bottom .tooltip-arrow{top:0;left:50%;margin-left:-5px;border-width:0 5px 5px;border-bottom-color:#000}
.popover{position:absolute;top:0;left:0;z-index:1010;display:none;max-width:276px;padding:1px;text-align:left;background-color:#fff;-webkit-background-clip:padding-box;-moz-background-clip:padding;background-clip:padding-box;border:1px solid #ccc;border:1px solid rgba(0,0,0,0.2);-webkit-border-radius:6px;-moz-border-radius:6px;border-radius:6px;-webkit-box-shadow:0 5px 10px rgba(0,0,0,0.2);-moz-box-shadow:0 5px 10px rgba(0,0,0,0.2);box-shadow:0 5px 10px rgba(0,0,0,0.2);white-space:normal}.popover.top{margin-top:-10px}
.popover.right{margin-left:10px}
.popover.bottom{margin-top:10px}
.popover.left{margin-left:-10px}
.popover-title{margin:0;padding:8px 14px;font-size:14px;font-weight:normal;line-height:18px;background-color:#f7f7f7;border-bottom:1px solid #ebebeb;border-radius:5px 5px 0 0;-webkit-border-radius:5px 5px 0 0;-moz-border-radius:5px 5px 0 0;border-radius:5px 5px 0 0}.popover-title:empty{display:none}
.popover-content{padding:9px 14px}
.popover .arrow,.popover .arrow:after{position:absolute;display:block;width:0;height:0;border-color:transparent;border-style:solid}
.popover .arrow{border-width:11px}
.popover .arrow:after{border-width:10px;content:""}
.popover.top .arrow{left:50%;margin-left:-11px;border-bottom-width:0;border-top-color:#999;border-top-color:rgba(0,0,0,0.25);bottom:-11px}.popover.top .arrow:after{bottom:1px;margin-left:-10px;border-bottom-width:0;border-top-color:#fff}
.popover.right .arrow{top:50%;left:-11px;margin-top:-11px;border-left-width:0;border-right-color:#999;border-right-color:rgba(0,0,0,0.25)}.popover.right .arrow:after{left:1px;bottom:-10px;border-left-width:0;border-right-color:#fff}
.popover.bottom .arrow{left:50%;margin-left:-11px;border-top-width:0;border-bottom-color:#999;border-bottom-color:rgba(0,0,0,0.25);top:-11px}.popover.bottom .arrow:after{top:1px;margin-left:-10px;border-top-width:0;border-bottom-color:#fff}
.popover.left .arrow{top:50%;right:-11px;margin-top:-11px;border-right-width:0;border-left-color:#999;border-left-color:rgba(0,0,0,0.25)}.popover.left .arrow:after{right:1px;border-right-width:0;border-left-color:#fff;bottom:-10px}
.thumbnails{margin-left:-20px;list-style:none;*zoom:1}.thumbnails:before,.thumbnails:after{display:table;content:"";line-height:0}
.thumbnails:after{clear:both}
.row-fluid .thumbnails{margin-left:0}
.thumbnails>li{float:left;margin-bottom:20px;margin-left:20px}
.thumbnail{display:block;padding:4px;line-height:20px;border:1px solid #ddd;-webkit-border-radius:4px;-moz-border-radius:4px;border-radius:4px;-webkit-box-shadow:0 1px 3px rgba(0,0,0,0.055);-moz-box-shadow:0 1px 3px rgba(0,0,0,0.055);box-shadow:0 1px 3px rgba(0,0,0,0.055);-webkit-transition:all .2s ease-in-out;-moz-transition:all .2s ease-in-out;-o-transition:all .2s ease-in-out;transition:all .2s ease-in-out}
a.thumbnail:hover,a.thumbnail:focus{border-color:#08c;-webkit-box-shadow:0 1px 4px rgba(0,105,214,0.25);-moz-box-shadow:0 1px 4px rgba(0,105,214,0.25);box-shadow:0 1px 4px rgba(0,105,214,0.25)}
.thumbnail>img{display:block;max-width:100%;margin-left:auto;margin-right:auto}
.thumbnail .caption{padding:9px;color:#555}
.media,.media-body{overflow:hidden;*overflow:visible;zoom:1}
.media,.media .media{margin-top:15px}
.media:first-child{margin-top:0}
.media-object{display:block}
.media-heading{margin:0 0 5px}
.media>.pull-left{margin-right:10px}
.media>.pull-right{margin-left:10px}
.media-list{margin-left:0;list-style:none}
.label,.badge{display:inline-block;padding:2px 4px;font-size:10.998px;font-weight:bold;line-height:14px;color:#fff;vertical-align:baseline;white-space:nowrap;text-shadow:0 -1px 0 rgba(0,0,0,0.25);background-color:#999}
.label{border-radius:3px;-webkit-border-radius:3px;-moz-border-radius:3px;border-radius:3px}
.badge{padding-left:9px;padding-right:9px;border-radius:9px;-webkit-border-radius:9px;-moz-border-radius:9px;border-radius:9px}
.label:empty,.badge:empty{display:none}
a.label:hover,a.label:focus,a.badge:hover,a.badge:focus{color:#fff;text-decoration:none;cursor:pointer}
.label-important,.badge-important{background-color:#b94a48}
.label-important[href],.badge-important[href]{background-color:#953b39}
.label-warning,.badge-warning{background-color:#f89406}
.label-warning[href],.badge-warning[href]{background-color:#c67605}
.label-success,.badge-success{background-color:#468847}
.label-success[href],.badge-success[href]{background-color:#356635}
.label-info,.badge-info{background-color:#3a87ad}
.label-info[href],.badge-info[href]{background-color:#2d6987}
.label-inverse,.badge-inverse{background-color:#333}
.label-inverse[href],.badge-inverse[href]{background-color:#1a1a1a}
.btn .label,.btn .badge{position:relative;top:-1px}
.btn-mini .label,.btn-mini .badge{top:0}
@-webkit-keyframes progress-bar-stripes{from{background-position:40px 0} to{background-position:0 0}}@-moz-keyframes progress-bar-stripes{from{background-position:40px 0} to{background-position:0 0}}@-ms-keyframes progress-bar-stripes{from{background-position:40px 0} to{background-position:0 0}}@-o-keyframes progress-bar-stripes{from{background-position:0 0} to{background-position:40px 0}}@keyframes progress-bar-stripes{from{background-position:40px 0} to{background-position:0 0}}.progress{overflow:hidden;height:20px;margin-bottom:20px;background-color:#f7f7f7;background-image:-moz-linear-gradient(top, #f5f5f5, #f9f9f9);background-image:-webkit-gradient(linear, 0 0, 0 100%, from(#f5f5f5), to(#f9f9f9));background-image:-webkit-linear-gradient(top, #f5f5f5, #f9f9f9);background-image:-o-linear-gradient(top, #f5f5f5, #f9f9f9);background-image:linear-gradient(to bottom, #f5f5f5, #f9f9f9);background-repeat:repeat-x;filter:progid:DXImageTransform.Microsoft.gradient(startColorstr='#fff5f5f5', endColorstr='#fff9f9f9', GradientType=0);-webkit-box-shadow:inset 0 1px 2px rgba(0,0,0,0.1);-moz-box-shadow:inset 0 1px 2px rgba(0,0,0,0.1);box-shadow:inset 0 1px 2px rgba(0,0,0,0.1);border-radius:4px;-webkit-border-radius:4px;-moz-border-radius:4px;border-radius:4px}
.progress .bar{width:0;height:100%;color:#fff;float:left;font-size:12px;text-align:center;text-shadow:0 -1px 0 rgba(0,0,0,0.25);background-color:#0e90d2;background-image:-moz-linear-gradient(top, #149bdf, #0480be);background-image:-webkit-gradient(linear, 0 0, 0 100%, from(#149bdf), to(#0480be));background-image:-webkit-linear-gradient(top, #149bdf, #0480be);background-image:-o-linear-gradient(top, #149bdf, #0480be);background-image:linear-gradient(to bottom, #149bdf, #0480be);background-repeat:repeat-x;filter:progid:DXImageTransform.Microsoft.gradient(startColorstr='#ff149bdf', endColorstr='#ff0480be', GradientType=0);-webkit-box-shadow:inset 0 -1px 0 rgba(0,0,0,0.15);-moz-box-shadow:inset 0 -1px 0 rgba(0,0,0,0.15);box-shadow:inset 0 -1px 0 rgba(0,0,0,0.15);-webkit-box-sizing:border-box;-moz-box-sizing:border-box;box-sizing:border-box;-webkit-transition:width .6s ease;-moz-transition:width .6s ease;-o-transition:width .6s ease;transition:width .6s ease}
.progress .bar+.bar{-webkit-box-shadow:inset 1px 0 0 rgba(0,0,0,.15), inset 0 -1px 0 rgba(0,0,0,.15);-moz-box-shadow:inset 1px 0 0 rgba(0,0,0,.15), inset 0 -1px 0 rgba(0,0,0,.15);box-shadow:inset 1px 0 0 rgba(0,0,0,.15), inset 0 -1px 0 rgba(0,0,0,.15)}
.progress-striped .bar{background-color:#149bdf;background-image:-webkit-gradient(linear, 0 100%, 100% 0, color-stop(.25, rgba(255,255,255,0.15)), color-stop(.25, transparent), color-stop(.5, transparent), color-stop(.5, rgba(255,255,255,0.15)), color-stop(.75, rgba(255,255,255,0.15)), color-stop(.75, transparent), to(transparent));background-image:-webkit-linear-gradient(45deg, rgba(255,255,255,0.15) 25%, transparent 25%, transparent 50%, rgba(255,255,255,0.15) 50%, rgba(255,255,255,0.15) 75%, transparent 75%, transparent);background-image:-moz-linear-gradient(45deg, rgba(255,255,255,0.15) 25%, transparent 25%, transparent 50%, rgba(255,255,255,0.15) 50%, rgba(255,255,255,0.15) 75%, transparent 75%, transparent);background-image:-o-linear-gradient(45deg, rgba(255,255,255,0.15) 25%, transparent 25%, transparent 50%, rgba(255,255,255,0.15) 50%, rgba(255,255,255,0.15) 75%, transparent 75%, transparent);background-image:linear-gradient(45deg, rgba(255,255,255,0.15) 25%, transparent 25%, transparent 50%, rgba(255,255,255,0.15) 50%, rgba(255,255,255,0.15) 75%, transparent 75%, transparent);-webkit-background-size:40px 40px;-moz-background-size:40px 40px;-o-background-size:40px 40px;background-size:40px 40px}
.progress.active .bar{-webkit-animation:progress-bar-stripes 2s linear infinite;-moz-animation:progress-bar-stripes 2s linear infinite;-ms-animation:progress-bar-stripes 2s linear infinite;-o-animation:progress-bar-stripes 2s linear infinite;animation:progress-bar-stripes 2s linear infinite}
.progress-danger .bar,.progress .bar-danger{background-color:#dd514c;background-image:-moz-linear-gradient(top, #ee5f5b, #c43c35);background-image:-webkit-gradient(linear, 0 0, 0 100%, from(#ee5f5b), to(#c43c35));background-image:-webkit-linear-gradient(top, #ee5f5b, #c43c35);background-image:-o-linear-gradient(top, #ee5f5b, #c43c35);background-image:linear-gradient(to bottom, #ee5f5b, #c43c35);background-repeat:repeat-x;filter:progid:DXImageTransform.Microsoft.gradient(startColorstr='#ffee5f5b', endColorstr='#ffc43c35', GradientType=0)}
.progress-danger.progress-striped .bar,.progress-striped .bar-danger{background-color:#ee5f5b;background-image:-webkit-gradient(linear, 0 100%, 100% 0, color-stop(.25, rgba(255,255,255,0.15)), color-stop(.25, transparent), color-stop(.5, transparent), color-stop(.5, rgba(255,255,255,0.15)), color-stop(.75, rgba(255,255,255,0.15)), color-stop(.75, transparent), to(transparent));background-image:-webkit-linear-gradient(45deg, rgba(255,255,255,0.15) 25%, transparent 25%, transparent 50%, rgba(255,255,255,0.15) 50%, rgba(255,255,255,0.15) 75%, transparent 75%, transparent);background-image:-moz-linear-gradient(45deg, rgba(255,255,255,0.15) 25%, transparent 25%, transparent 50%, rgba(255,255,255,0.15) 50%, rgba(255,255,255,0.15) 75%, transparent 75%, transparent);background-image:-o-linear-gradient(45deg, rgba(255,255,255,0.15) 25%, transparent 25%, transparent 50%, rgba(255,255,255,0.15) 50%, rgba(255,255,255,0.15) 75%, transparent 75%, transparent);background-image:linear-gradient(45deg, rgba(255,255,255,0.15) 25%, transparent 25%, transparent 50%, rgba(255,255,255,0.15) 50%, rgba(255,255,255,0.15) 75%, transparent 75%, transparent)}
.progress-success .bar,.progress .bar-success{background-color:#5eb95e;background-image:-moz-linear-gradient(top, #62c462, #57a957);background-image:-webkit-gradient(linear, 0 0, 0 100%, from(#62c462), to(#57a957));background-image:-webkit-linear-gradient(top, #62c462, #57a957);background-image:-o-linear-gradient(top, #62c462, #57a957);background-image:linear-gradient(to bottom, #62c462, #57a957);background-repeat:repeat-x;filter:progid:DXImageTransform.Microsoft.gradient(startColorstr='#ff62c462', endColorstr='#ff57a957', GradientType=0)}
.progress-success.progress-striped .bar,.progress-striped .bar-success{background-color:#62c462;background-image:-webkit-gradient(linear, 0 100%, 100% 0, color-stop(.25, rgba(255,255,255,0.15)), color-stop(.25, transparent), color-stop(.5, transparent), color-stop(.5, rgba(255,255,255,0.15)), color-stop(.75, rgba(255,255,255,0.15)), color-stop(.75, transparent), to(transparent));background-image:-webkit-linear-gradient(45deg, rgba(255,255,255,0.15) 25%, transparent 25%, transparent 50%, rgba(255,255,255,0.15) 50%, rgba(255,255,255,0.15) 75%, transparent 75%, transparent);background-image:-moz-linear-gradient(45deg, rgba(255,255,255,0.15) 25%, transparent 25%, transparent 50%, rgba(255,255,255,0.15) 50%, rgba(255,255,255,0.15) 75%, transparent 75%, transparent);background-image:-o-linear-gradient(45deg, rgba(255,255,255,0.15) 25%, transparent 25%, transparent 50%, rgba(255,255,255,0.15) 50%, rgba(255,255,255,0.15) 75%, transparent 75%, transparent);background-image:linear-gradient(45deg, rgba(255,255,255,0.15) 25%, transparent 25%, transparent 50%, rgba(255,255,255,0.15) 50%, rgba(255,255,255,0.15) 75%, transparent 75%, transparent)}
.progress-info .bar,.progress .bar-info{background-color:#4bb1cf;background-image:-moz-linear-gradient(top, #5bc0de, #339bb9);background-image:-webkit-gradient(linear, 0 0, 0 100%, from(#5bc0de), to(#339bb9));background-image:-webkit-linear-gradient(top, #5bc0de, #339bb9);background-image:-o-linear-gradient(top, #5bc0de, #339bb9);background-image:linear-gradient(to bottom, #5bc0de, #339bb9);background-repeat:repeat-x;filter:progid:DXImageTransform.Microsoft.gradient(startColorstr='#ff5bc0de', endColorstr='#ff339bb9', GradientType=0)}
.progress-info.progress-striped .bar,.progress-striped .bar-info{background-color:#5bc0de;background-image:-webkit-gradient(linear, 0 100%, 100% 0, color-stop(.25, rgba(255,255,255,0.15)), color-stop(.25, transparent), color-stop(.5, transparent), color-stop(.5, rgba(255,255,255,0.15)), color-stop(.75, rgba(255,255,255,0.15)), color-stop(.75, transparent), to(transparent));background-image:-webkit-linear-gradient(45deg, rgba(255,255,255,0.15) 25%, transparent 25%, transparent 50%, rgba(255,255,255,0.15) 50%, rgba(255,255,255,0.15) 75%, transparent 75%, transparent);background-image:-moz-linear-gradient(45deg, rgba(255,255,255,0.15) 25%, transparent 25%, transparent 50%, rgba(255,255,255,0.15) 50%, rgba(255,255,255,0.15) 75%, transparent 75%, transparent);background-image:-o-linear-gradient(45deg, rgba(255,255,255,0.15) 25%, transparent 25%, transparent 50%, rgba(255,255,255,0.15) 50%, rgba(255,255,255,0.15) 75%, transparent 75%, transparent);background-image:linear-gradient(45deg, rgba(255,255,255,0.15) 25%, transparent 25%, transparent 50%, rgba(255,255,255,0.15) 50%, rgba(255,255,255,0.15) 75%, transparent 75%, transparent)}
.progress-warning .bar,.progress .bar-warning{background-color:#faa732;background-image:-moz-linear-gradient(top, #fbb450, #f89406);background-image:-webkit-gradient(linear, 0 0, 0 100%, from(#fbb450), to(#f89406));background-image:-webkit-linear-gradient(top, #fbb450, #f89406);background-image:-o-linear-gradient(top, #fbb450, #f89406);background-image:linear-gradient(to bottom, #fbb450, #f89406);background-repeat:repeat-x;filter:progid:DXImageTransform.Microsoft.gradient(startColorstr='#fffbb450', endColorstr='#fff89406', GradientType=0)}
.progress-warning.progress-striped .bar,.progress-striped .bar-warning{background-color:#fbb450;background-image:-webkit-gradient(linear, 0 100%, 100% 0, color-stop(.25, rgba(255,255,255,0.15)), color-stop(.25, transparent), color-stop(.5, transparent), color-stop(.5, rgba(255,255,255,0.15)), color-stop(.75, rgba(255,255,255,0.15)), color-stop(.75, transparent), to(transparent));background-image:-webkit-linear-gradient(45deg, rgba(255,255,255,0.15) 25%, transparent 25%, transparent 50%, rgba(255,255,255,0.15) 50%, rgba(255,255,255,0.15) 75%, transparent 75%, transparent);background-image:-moz-linear-gradient(45deg, rgba(255,255,255,0.15) 25%, transparent 25%, transparent 50%, rgba(255,255,255,0.15) 50%, rgba(255,255,255,0.15) 75%, transparent 75%, transparent);background-image:-o-linear-gradient(45deg, rgba(255,255,255,0.15) 25%, transparent 25%, transparent 50%, rgba(255,255,255,0.15) 50%, rgba(255,255,255,0.15) 75%, transparent 75%, transparent);background-image:linear-gradient(45deg, rgba(255,255,255,0.15) 25%, transparent 25%, transparent 50%, rgba(255,255,255,0.15) 50%, rgba(255,255,255,0.15) 75%, transparent 75%, transparent)}
.accordion{margin-bottom:20px}
.accordion-group{margin-bottom:2px;border:1px solid #e5e5e5;border-radius:4px;-webkit-border-radius:4px;-moz-border-radius:4px;border-radius:4px}
.accordion-heading{border-bottom:0}
.accordion-heading .accordion-toggle{display:block;padding:8px 15px}
.accordion-toggle{cursor:pointer}
.accordion-inner{padding:9px 15px;border-top:1px solid #e5e5e5}
.carousel{position:relative;margin-bottom:20px;line-height:1}
.carousel-inner{overflow:hidden;width:100%;position:relative}
.carousel-inner>.item{display:none;position:relative;-webkit-transition:.6s ease-in-out left;-moz-transition:.6s ease-in-out left;-o-transition:.6s ease-in-out left;transition:.6s ease-in-out left}.carousel-inner>.item>img,.carousel-inner>.item>a>img{display:block;line-height:1}
.carousel-inner>.active,.carousel-inner>.next,.carousel-inner>.prev{display:block}
.carousel-inner>.active{left:0}
.carousel-inner>.next,.carousel-inner>.prev{position:absolute;top:0;width:100%}
.carousel-inner>.next{left:100%}
.carousel-inner>.prev{left:-100%}
.carousel-inner>.next.left,.carousel-inner>.prev.right{left:0}
.carousel-inner>.active.left{left:-100%}
.carousel-inner>.active.right{left:100%}
.carousel-control{position:absolute;top:40%;left:15px;width:40px;height:40px;margin-top:-20px;font-size:60px;font-weight:100;line-height:30px;color:#fff;text-align:center;background:#222;border:3px solid #fff;-webkit-border-radius:23px;-moz-border-radius:23px;border-radius:23px;opacity:.5;filter:alpha(opacity=50)}.carousel-control.right{left:auto;right:15px}
.carousel-control:hover,.carousel-control:focus{color:#fff;text-decoration:none;opacity:.9;filter:alpha(opacity=90)}
.carousel-indicators{position:absolute;top:15px;right:15px;z-index:5;margin:0;list-style:none}.carousel-indicators li{display:block;float:left;width:10px;height:10px;margin-left:5px;text-indent:-999px;background-color:#ccc;background-color:rgba(255,255,255,0.25);border-radius:5px}
.carousel-indicators .active{background-color:#fff}
.carousel-caption{position:absolute;left:0;right:0;bottom:0;padding:15px;background:#333;background:rgba(0,0,0,0.75)}
.carousel-caption h4,.carousel-caption p{color:#fff;line-height:20px}
.carousel-caption h4{margin:0 0 5px}
.carousel-caption p{margin-bottom:0}
.hero-unit{padding:60px;margin-bottom:30px;font-size:18px;font-weight:200;line-height:30px;color:inherit;background-color:#eee;border-radius:6px;-webkit-border-radius:6px;-moz-border-radius:6px;border-radius:6px}.hero-unit h1{margin-bottom:0;font-size:60px;line-height:1;color:inherit;letter-spacing:-1px}
.hero-unit li{line-height:30px}
.pull-right{float:right}
.pull-left{float:left}
.hide{display:none}
.show{display:block}
.invisible{visibility:hidden}
.affix{position:fixed}
@-ms-viewport{width:device-width}.hidden{display:none;visibility:hidden}
.visible-phone{display:none !important}
.visible-tablet{display:none !important}
.hidden-desktop{display:none !important}
.visible-desktop{display:inherit !important}
@media (min-width:768px) and (max-width:979px){.hidden-desktop{display:inherit !important} .visible-desktop{display:none !important} .visible-tablet{display:inherit !important} .hidden-tablet{display:none !important}}@media (max-width:767px){.hidden-desktop{display:inherit !important} .visible-desktop{display:none !important} .visible-phone{display:inherit !important} .hidden-phone{display:none !important}}.visible-print{display:none !important}
@media print{.visible-print{display:inherit !important} .hidden-print{display:none !important}}@media (min-width:1200px){.row{margin-left:-30px;*zoom:1}.row:before,.row:after{display:table;content:"";line-height:0} .row:after{clear:both} [class*="span"]{float:left;min-height:1px;margin-left:30px} .container,.navbar-static-top .container,.navbar-fixed-top .container,.navbar-fixed-bottom .container{width:1170px} .span12{width:1170px} .span11{width:1070px} .span10{width:970px} .span9{width:870px} .span8{width:770px} .span7{width:670px} .span6{width:570px} .span5{width:470px} .span4{width:370px} .span3{width:270px} .span2{width:170px} .span1{width:70px} .offset12{margin-left:1230px} .offset11{margin-left:1130px} .offset10{margin-left:1030px} .offset9{margin-left:930px} .offset8{margin-left:830px} .offset7{margin-left:730px} .offset6{margin-left:630px} .offset5{margin-left:530px} .offset4{margin-left:430px} .offset3{margin-left:330px} .offset2{margin-left:230px} .offset1{margin-left:130px} .row-fluid{width:100%;*zoom:1}.row-fluid:before,.row-fluid:after{display:table;content:"";line-height:0} .row-fluid:after{clear:both} .row-fluid [class*="span"]{display:block;width:100%;min-height:30px;-webkit-box-sizing:border-box;-moz-box-sizing:border-box;box-sizing:border-box;float:left;margin-left:2.564102564102564%;*margin-left:2.5109110747408616%} .row-fluid [class*="span"]:first-child{margin-left:0} .row-fluid .controls-row [class*="span"]+[class*="span"]{margin-left:2.564102564102564%} .row-fluid .span12{width:100%;*width:99.94680851063829%} .row-fluid .span11{width:91.45299145299145%;*width:91.39979996362975%} .row-fluid .span10{width:82.90598290598291%;*width:82.8527914166212%} .row-fluid .span9{width:74.35897435897436%;*width:74.30578286961266%} .row-fluid .span8{width:65.81196581196582%;*width:65.75877432260411%} .row-fluid .span7{width:57.26495726495726%;*width:57.21176577559556%} .row-fluid .span6{width:48.717948717948715%;*width:48.664757228587014%} .row-fluid .span5{width:40.17094017094017%;*width:40.11774868157847%} .row-fluid .span4{width:31.623931623931625%;*width:31.570740134569924%} .row-fluid .span3{width:23.076923076923077%;*width:23.023731587561375%} .row-fluid .span2{width:14.52991452991453%;*width:14.476723040552828%} .row-fluid .span1{width:5.982905982905983%;*width:5.929714493544281%} .row-fluid .offset12{margin-left:105.12820512820512%;*margin-left:105.02182214948171%} .row-fluid .offset12:first-child{margin-left:102.56410256410257%;*margin-left:102.45771958537915%} .row-fluid .offset11{margin-left:96.58119658119658%;*margin-left:96.47481360247316%} .row-fluid .offset11:first-child{margin-left:94.01709401709402%;*margin-left:93.91071103837061%} .row-fluid .offset10{margin-left:88.03418803418803%;*margin-left:87.92780505546462%} .row-fluid .offset10:first-child{margin-left:85.47008547008548%;*margin-left:85.36370249136206%} .row-fluid .offset9{margin-left:79.48717948717949%;*margin-left:79.38079650845607%} .row-fluid .offset9:first-child{margin-left:76.92307692307693%;*margin-left:76.81669394435352%} .row-fluid .offset8{margin-left:70.94017094017094%;*margin-left:70.83378796144753%} .row-fluid .offset8:first-child{margin-left:68.37606837606839%;*margin-left:68.26968539734497%} .row-fluid .offset7{margin-left:62.393162393162385%;*margin-left:62.28677941443899%} .row-fluid .offset7:first-child{margin-left:59.82905982905982%;*margin-left:59.72267685033642%} .row-fluid .offset6{margin-left:53.84615384615384%;*margin-left:53.739770867430444%} .row-fluid .offset6:first-child{margin-left:51.28205128205128%;*margin-left:51.175668303327875%} .row-fluid .offset5{margin-left:45.299145299145295%;*margin-left:45.1927623204219%} .row-fluid .offset5:first-child{margin-left:42.73504273504273%;*margin-left:42.62865975631933%} .row-fluid .offset4{margin-left:36.75213675213675%;*margin-left:36.645753773413354%} .row-fluid .offset4:first-child{margin-left:34.18803418803419%;*margin-left:34.081651209310785%} .row-fluid .offset3{margin-left:28.205128205128204%;*margin-left:28.0987452264048%} .row-fluid .offset3:first-child{margin-left:25.641025641025642%;*margin-left:25.53464266230224%} .row-fluid .offset2{margin-left:19.65811965811966%;*margin-left:19.551736679396257%} .row-fluid .offset2:first-child{margin-left:17.094017094017094%;*margin-left:16.98763411529369%} .row-fluid .offset1{margin-left:11.11111111111111%;*margin-left:11.004728132387708%} .row-fluid .offset1:first-child{margin-left:8.547008547008547%;*margin-left:8.440625568285142%} input,textarea,.uneditable-input{margin-left:0} .controls-row [class*="span"]+[class*="span"]{margin-left:30px} input.span12,textarea.span12,.uneditable-input.span12{width:1156px} input.span11,textarea.span11,.uneditable-input.span11{width:1056px} input.span10,textarea.span10,.uneditable-input.span10{width:956px} input.span9,textarea.span9,.uneditable-input.span9{width:856px} input.span8,textarea.span8,.uneditable-input.span8{width:756px} input.span7,textarea.span7,.uneditable-input.span7{width:656px} input.span6,textarea.span6,.uneditable-input.span6{width:556px} input.span5,textarea.span5,.uneditable-input.span5{width:456px} input.span4,textarea.span4,.uneditable-input.span4{width:356px} input.span3,textarea.span3,.uneditable-input.span3{width:256px} input.span2,textarea.span2,.uneditable-input.span2{width:156px} input.span1,textarea.span1,.uneditable-input.span1{width:56px} .thumbnails{margin-left:-30px} .thumbnails>li{margin-left:30px} .row-fluid .thumbnails{margin-left:0}}@media (min-width:768px) and (max-width:979px){.row{margin-left:-20px;*zoom:1}.row:before,.row:after{display:table;content:"";line-height:0} .row:after{clear:both} [class*="span"]{float:left;min-height:1px;margin-left:20px} .container,.navbar-static-top .container,.navbar-fixed-top .container,.navbar-fixed-bottom .container{width:724px} .span12{width:724px} .span11{width:662px} .span10{width:600px} .span9{width:538px} .span8{width:476px} .span7{width:414px} .span6{width:352px} .span5{width:290px} .span4{width:228px} .span3{width:166px} .span2{width:104px} .span1{width:42px} .offset12{margin-left:764px} .offset11{margin-left:702px} .offset10{margin-left:640px} .offset9{margin-left:578px} .offset8{margin-left:516px} .offset7{margin-left:454px} .offset6{margin-left:392px} .offset5{margin-left:330px} .offset4{margin-left:268px} .offset3{margin-left:206px} .offset2{margin-left:144px} .offset1{margin-left:82px} .row-fluid{width:100%;*zoom:1}.row-fluid:before,.row-fluid:after{display:table;content:"";line-height:0} .row-fluid:after{clear:both} .row-fluid [class*="span"]{display:block;width:100%;min-height:30px;-webkit-box-sizing:border-box;-moz-box-sizing:border-box;box-sizing:border-box;float:left;margin-left:2.7624309392265194%;*margin-left:2.709239449864817%} .row-fluid [class*="span"]:first-child{margin-left:0} .row-fluid .controls-row [class*="span"]+[class*="span"]{margin-left:2.7624309392265194%} .row-fluid .span12{width:100%;*width:99.94680851063829%} .row-fluid .span11{width:91.43646408839778%;*width:91.38327259903608%} .row-fluid .span10{width:82.87292817679558%;*width:82.81973668743387%} .row-fluid .span9{width:74.30939226519337%;*width:74.25620077583166%} .row-fluid .span8{width:65.74585635359117%;*width:65.69266486422946%} .row-fluid .span7{width:57.18232044198895%;*width:57.12912895262725%} .row-fluid .span6{width:48.61878453038674%;*width:48.56559304102504%} .row-fluid .span5{width:40.05524861878453%;*width:40.00205712942283%} .row-fluid .span4{width:31.491712707182323%;*width:31.43852121782062%} .row-fluid .span3{width:22.92817679558011%;*width:22.87498530621841%} .row-fluid .span2{width:14.3646408839779%;*width:14.311449394616199%} .row-fluid .span1{width:5.801104972375691%;*width:5.747913483013988%} .row-fluid .offset12{margin-left:105.52486187845304%;*margin-left:105.41847889972962%} .row-fluid .offset12:first-child{margin-left:102.76243093922652%;*margin-left:102.6560479605031%} .row-fluid .offset11{margin-left:96.96132596685082%;*margin-left:96.8549429881274%} .row-fluid .offset11:first-child{margin-left:94.1988950276243%;*margin-left:94.09251204890089%} .row-fluid .offset10{margin-left:88.39779005524862%;*margin-left:88.2914070765252%} .row-fluid .offset10:first-child{margin-left:85.6353591160221%;*margin-left:85.52897613729868%} .row-fluid .offset9{margin-left:79.8342541436464%;*margin-left:79.72787116492299%} .row-fluid .offset9:first-child{margin-left:77.07182320441989%;*margin-left:76.96544022569647%} .row-fluid .offset8{margin-left:71.2707182320442%;*margin-left:71.16433525332079%} .row-fluid .offset8:first-child{margin-left:68.50828729281768%;*margin-left:68.40190431409427%} .row-fluid .offset7{margin-left:62.70718232044199%;*margin-left:62.600799341718584%} .row-fluid .offset7:first-child{margin-left:59.94475138121547%;*margin-left:59.838368402492065%} .row-fluid .offset6{margin-left:54.14364640883978%;*margin-left:54.037263430116376%} .row-fluid .offset6:first-child{margin-left:51.38121546961326%;*margin-left:51.27483249088986%} .row-fluid .offset5{margin-left:45.58011049723757%;*margin-left:45.47372751851417%} .row-fluid .offset5:first-child{margin-left:42.81767955801105%;*margin-left:42.71129657928765%} .row-fluid .offset4{margin-left:37.01657458563536%;*margin-left:36.91019160691196%} .row-fluid .offset4:first-child{margin-left:34.25414364640884%;*margin-left:34.14776066768544%} .row-fluid .offset3{margin-left:28.45303867403315%;*margin-left:28.346655695309746%} .row-fluid .offset3:first-child{margin-left:25.69060773480663%;*margin-left:25.584224756083227%} .row-fluid .offset2{margin-left:19.88950276243094%;*margin-left:19.783119783707537%} .row-fluid .offset2:first-child{margin-left:17.12707182320442%;*margin-left:17.02068884448102%} .row-fluid .offset1{margin-left:11.32596685082873%;*margin-left:11.219583872105325%} .row-fluid .offset1:first-child{margin-left:8.56353591160221%;*margin-left:8.457152932878806%} input,textarea,.uneditable-input{margin-left:0} .controls-row [class*="span"]+[class*="span"]{margin-left:20px} input.span12,textarea.span12,.uneditable-input.span12{width:710px} input.span11,textarea.span11,.uneditable-input.span11{width:648px} input.span10,textarea.span10,.uneditable-input.span10{width:586px} input.span9,textarea.span9,.uneditable-input.span9{width:524px} input.span8,textarea.span8,.uneditable-input.span8{width:462px} input.span7,textarea.span7,.uneditable-input.span7{width:400px} input.span6,textarea.span6,.uneditable-input.span6{width:338px} input.span5,textarea.span5,.uneditable-input.span5{width:276px} input.span4,textarea.span4,.uneditable-input.span4{width:214px} input.span3,textarea.span3,.uneditable-input.span3{width:152px} input.span2,textarea.span2,.uneditable-input.span2{width:90px} input.span1,textarea.span1,.uneditable-input.span1{width:28px}}@media (max-width:767px){body{padding-left:20px;padding-right:20px} .navbar-fixed-top,.navbar-fixed-bottom,.navbar-static-top{margin-left:-20px;margin-right:-20px} .container-fluid{padding:0} .dl-horizontal dt{float:none;clear:none;width:auto;text-align:left} .dl-horizontal dd{margin-left:0} .container{width:auto} .row-fluid{width:100%} .row,.thumbnails{margin-left:0} .thumbnails>li{float:none;margin-left:0} [class*="span"],.uneditable-input[class*="span"],.row-fluid [class*="span"]{float:none;display:block;width:100%;margin-left:0;-webkit-box-sizing:border-box;-moz-box-sizing:border-box;box-sizing:border-box} .span12,.row-fluid .span12{width:100%;-webkit-box-sizing:border-box;-moz-box-sizing:border-box;box-sizing:border-box} .row-fluid [class*="offset"]:first-child{margin-left:0} .input-large,.input-xlarge,.input-xxlarge,input[class*="span"],select[class*="span"],textarea[class*="span"],.uneditable-input{display:block;width:100%;min-height:30px;-webkit-box-sizing:border-box;-moz-box-sizing:border-box;box-sizing:border-box} .input-prepend input,.input-append input,.input-prepend input[class*="span"],.input-append input[class*="span"]{display:inline-block;width:auto} .controls-row [class*="span"]+[class*="span"]{margin-left:0} .modal{position:fixed;top:20px;left:20px;right:20px;width:auto;margin:0}.modal.fade{top:-100px} .modal.fade.in{top:20px}}@media (max-width:480px){.nav-collapse{-webkit-transform:translate3d(0, 0, 0)} .page-header h1 small{display:block;line-height:20px} input[type="checkbox"],input[type="radio"]{border:1px solid #ccc} .form-horizontal .control-label{float:none;width:auto;padding-top:0;text-align:left} .form-horizontal .controls{margin-left:0} .form-horizontal .control-list{padding-top:0} .form-horizontal .form-actions{padding-left:10px;padding-right:10px} .media .pull-left,.media .pull-right{float:none;display:block;margin-bottom:10px} .media-object{margin-right:0;margin-left:0} .modal{top:10px;left:10px;right:10px} .modal-header .close{padding:10px;margin:-10px} .carousel-caption{position:static}}@media (max-width:979px){body{padding-top:0} .navbar-fixed-top,.navbar-fixed-bottom{position:static} .navbar-fixed-top{margin-bottom:20px} .navbar-fixed-bottom{margin-top:20px} .navbar-fixed-top .navbar-inner,.navbar-fixed-bottom .navbar-inner{padding:5px} .navbar .container{width:auto;padding:0} .navbar .brand{padding-left:10px;padding-right:10px;margin:0 0 0 -5px} .nav-collapse{clear:both} .nav-collapse .nav{float:none;margin:0 0 10px} .nav-collapse .nav>li{float:none} .nav-collapse .nav>li>a{margin-bottom:2px} .nav-collapse .nav>.divider-vertical{display:none} .nav-collapse .nav .nav-header{color:#777;text-shadow:none} .nav-collapse .nav>li>a,.nav-collapse .dropdown-menu a{padding:9px 15px;font-weight:bold;color:#777;border-radius:3px;-webkit-border-radius:3px;-moz-border-radius:3px;border-radius:3px} .nav-collapse .btn{padding:4px 10px 4px;font-weight:normal;border-radius:4px;-webkit-border-radius:4px;-moz-border-radius:4px;border-radius:4px} .nav-collapse .dropdown-menu li+li a{margin-bottom:2px} .nav-collapse .nav>li>a:hover,.nav-collapse .nav>li>a:focus,.nav-collapse .dropdown-menu a:hover,.nav-collapse .dropdown-menu a:focus{background-color:#f2f2f2} .navbar-inverse .nav-collapse .nav>li>a,.navbar-inverse .nav-collapse .dropdown-menu a{color:#999} .navbar-inverse .nav-collapse .nav>li>a:hover,.navbar-inverse .nav-collapse .nav>li>a:focus,.navbar-inverse .nav-collapse .dropdown-menu a:hover,.navbar-inverse .nav-collapse .dropdown-menu a:focus{background-color:#111} .nav-collapse.in .btn-group{margin-top:5px;padding:0} .nav-collapse .dropdown-menu{position:static;top:auto;left:auto;float:none;display:none;max-width:none;margin:0 15px;padding:0;background-color:transparent;border:none;-webkit-border-radius:0;-moz-border-radius:0;border-radius:0;-webkit-box-shadow:none;-moz-box-shadow:none;box-shadow:none} .nav-collapse .open>.dropdown-menu{display:block} .nav-collapse .dropdown-menu:before,.nav-collapse .dropdown-menu:after{display:none} .nav-collapse .dropdown-menu .divider{display:none} .nav-collapse .nav>li>.dropdown-menu:before,.nav-collapse .nav>li>.dropdown-menu:after{display:none} .nav-collapse .navbar-form,.nav-collapse .navbar-search{float:none;padding:10px 15px;margin:10px 0;border-top:1px solid #f2f2f2;border-bottom:1px solid #f2f2f2;-webkit-box-shadow:inset 0 1px 0 rgba(255,255,255,.1), 0 1px 0 rgba(255,255,255,.1);-moz-box-shadow:inset 0 1px 0 rgba(255,255,255,.1), 0 1px 0 rgba(255,255,255,.1);box-shadow:inset 0 1px 0 rgba(255,255,255,.1), 0 1px 0 rgba(255,255,255,.1)} .navbar-inverse .nav-collapse .navbar-form,.navbar-inverse .nav-collapse .navbar-search{border-top-color:#111;border-bottom-color:#111} .navbar .nav-collapse .nav.pull-right{float:none;margin-left:0} .nav-collapse,.nav-collapse.collapse{overflow:hidden;height:0} .navbar .btn-navbar{display:block} .navbar-static .navbar-inner{padding-left:10px;padding-right:10px}}@media (min-width:979px + 1){.nav-collapse.collapse{height:auto !important;overflow:visible !important}}@font-face{font-family:'FontAwesome';src:url('../components/font-awesome/font/fontawesome-webfont.eot?v=3.2.1');src:url('../components/font-awesome/font/fontawesome-webfont.eot?#iefix&v=3.2.1') format('embedded-opentype'),url('../components/font-awesome/font/fontawesome-webfont.woff?v=3.2.1') format('woff'),url('../components/font-awesome/font/fontawesome-webfont.ttf?v=3.2.1') format('truetype'),url('../components/font-awesome/font/fontawesome-webfont.svg#fontawesomeregular?v=3.2.1') format('svg');font-weight:normal;font-style:normal}[class^="icon-"],[class*=" icon-"]{font-family:FontAwesome;font-weight:normal;font-style:normal;text-decoration:inherit;-webkit-font-smoothing:antialiased;*margin-right:.3em}
[class^="icon-"]:before,[class*=" icon-"]:before{text-decoration:inherit;display:inline-block;speak:none}
.icon-large:before{vertical-align:-10%;font-size:1.3333333333333333em}
a [class^="icon-"],a [class*=" icon-"]{display:inline}
[class^="icon-"].icon-fixed-width,[class*=" icon-"].icon-fixed-width{display:inline-block;width:1.1428571428571428em;text-align:right;padding-right:.2857142857142857em}[class^="icon-"].icon-fixed-width.icon-large,[class*=" icon-"].icon-fixed-width.icon-large{width:1.4285714285714286em}
.icons-ul{margin-left:2.142857142857143em;list-style-type:none}.icons-ul>li{position:relative}
.icons-ul .icon-li{position:absolute;left:-2.142857142857143em;width:2.142857142857143em;text-align:center;line-height:inherit}
[class^="icon-"].hide,[class*=" icon-"].hide{display:none}
.icon-muted{color:#eee}
.icon-light{color:#fff}
.icon-dark{color:#333}
.icon-border{border:solid 1px #eee;padding:.2em .25em .15em;border-radius:3px;-webkit-border-radius:3px;-moz-border-radius:3px;border-radius:3px}
.icon-2x{font-size:2em}.icon-2x.icon-border{border-width:2px;border-radius:4px;-webkit-border-radius:4px;-moz-border-radius:4px;border-radius:4px}
.icon-3x{font-size:3em}.icon-3x.icon-border{border-width:3px;border-radius:5px;-webkit-border-radius:5px;-moz-border-radius:5px;border-radius:5px}
.icon-4x{font-size:4em}.icon-4x.icon-border{border-width:4px;border-radius:6px;-webkit-border-radius:6px;-moz-border-radius:6px;border-radius:6px}
.icon-5x{font-size:5em}.icon-5x.icon-border{border-width:5px;border-radius:7px;-webkit-border-radius:7px;-moz-border-radius:7px;border-radius:7px}
.pull-right{float:right}
.pull-left{float:left}
[class^="icon-"].pull-left,[class*=" icon-"].pull-left{margin-right:.3em}
[class^="icon-"].pull-right,[class*=" icon-"].pull-right{margin-left:.3em}
[class^="icon-"],[class*=" icon-"]{display:inline;width:auto;height:auto;line-height:normal;vertical-align:baseline;background-image:none;background-position:0 0;background-repeat:repeat;margin-top:0}
.icon-white,.nav-pills>.active>a>[class^="icon-"],.nav-pills>.active>a>[class*=" icon-"],.nav-list>.active>a>[class^="icon-"],.nav-list>.active>a>[class*=" icon-"],.navbar-inverse .nav>.active>a>[class^="icon-"],.navbar-inverse .nav>.active>a>[class*=" icon-"],.dropdown-menu>li>a:hover>[class^="icon-"],.dropdown-menu>li>a:hover>[class*=" icon-"],.dropdown-menu>.active>a>[class^="icon-"],.dropdown-menu>.active>a>[class*=" icon-"],.dropdown-submenu:hover>a>[class^="icon-"],.dropdown-submenu:hover>a>[class*=" icon-"]{background-image:none}
.btn [class^="icon-"].icon-large,.nav [class^="icon-"].icon-large,.btn [class*=" icon-"].icon-large,.nav [class*=" icon-"].icon-large{line-height:.9em}
.btn [class^="icon-"].icon-spin,.nav [class^="icon-"].icon-spin,.btn [class*=" icon-"].icon-spin,.nav [class*=" icon-"].icon-spin{display:inline-block}
.nav-tabs [class^="icon-"],.nav-pills [class^="icon-"],.nav-tabs [class*=" icon-"],.nav-pills [class*=" icon-"],.nav-tabs [class^="icon-"].icon-large,.nav-pills [class^="icon-"].icon-large,.nav-tabs [class*=" icon-"].icon-large,.nav-pills [class*=" icon-"].icon-large{line-height:.9em}
.btn [class^="icon-"].pull-left.icon-2x,.btn [class*=" icon-"].pull-left.icon-2x,.btn [class^="icon-"].pull-right.icon-2x,.btn [class*=" icon-"].pull-right.icon-2x{margin-top:.18em}
.btn [class^="icon-"].icon-spin.icon-large,.btn [class*=" icon-"].icon-spin.icon-large{line-height:.8em}
.btn.btn-small [class^="icon-"].pull-left.icon-2x,.btn.btn-small [class*=" icon-"].pull-left.icon-2x,.btn.btn-small [class^="icon-"].pull-right.icon-2x,.btn.btn-small [class*=" icon-"].pull-right.icon-2x{margin-top:.25em}
.btn.btn-large [class^="icon-"],.btn.btn-large [class*=" icon-"]{margin-top:0}.btn.btn-large [class^="icon-"].pull-left.icon-2x,.btn.btn-large [class*=" icon-"].pull-left.icon-2x,.btn.btn-large [class^="icon-"].pull-right.icon-2x,.btn.btn-large [class*=" icon-"].pull-right.icon-2x{margin-top:.05em}
.btn.btn-large [class^="icon-"].pull-left.icon-2x,.btn.btn-large [class*=" icon-"].pull-left.icon-2x{margin-right:.2em}
.btn.btn-large [class^="icon-"].pull-right.icon-2x,.btn.btn-large [class*=" icon-"].pull-right.icon-2x{margin-left:.2em}
.nav-list [class^="icon-"],.nav-list [class*=" icon-"]{line-height:inherit}
.icon-stack{position:relative;display:inline-block;width:2em;height:2em;line-height:2em;vertical-align:-35%}.icon-stack [class^="icon-"],.icon-stack [class*=" icon-"]{display:block;text-align:center;position:absolute;width:100%;height:100%;font-size:1em;line-height:inherit;*line-height:2em}
.icon-stack .icon-stack-base{font-size:2em;*line-height:1em}
.icon-spin{display:inline-block;-moz-animation:spin 2s infinite linear;-o-animation:spin 2s infinite linear;-webkit-animation:spin 2s infinite linear;animation:spin 2s infinite linear}
a .icon-stack,a .icon-spin{display:inline-block;text-decoration:none}
@-moz-keyframes spin{0%{-moz-transform:rotate(0deg)} 100%{-moz-transform:rotate(359deg)}}@-webkit-keyframes spin{0%{-webkit-transform:rotate(0deg)} 100%{-webkit-transform:rotate(359deg)}}@-o-keyframes spin{0%{-o-transform:rotate(0deg)} 100%{-o-transform:rotate(359deg)}}@-ms-keyframes spin{0%{-ms-transform:rotate(0deg)} 100%{-ms-transform:rotate(359deg)}}@keyframes spin{0%{transform:rotate(0deg)} 100%{transform:rotate(359deg)}}.icon-rotate-90:before{-webkit-transform:rotate(90deg);-moz-transform:rotate(90deg);-ms-transform:rotate(90deg);-o-transform:rotate(90deg);transform:rotate(90deg);filter:progid:DXImageTransform.Microsoft.BasicImage(rotation=1)}
.icon-rotate-180:before{-webkit-transform:rotate(180deg);-moz-transform:rotate(180deg);-ms-transform:rotate(180deg);-o-transform:rotate(180deg);transform:rotate(180deg);filter:progid:DXImageTransform.Microsoft.BasicImage(rotation=2)}
.icon-rotate-270:before{-webkit-transform:rotate(270deg);-moz-transform:rotate(270deg);-ms-transform:rotate(270deg);-o-transform:rotate(270deg);transform:rotate(270deg);filter:progid:DXImageTransform.Microsoft.BasicImage(rotation=3)}
.icon-flip-horizontal:before{-webkit-transform:scale(-1, 1);-moz-transform:scale(-1, 1);-ms-transform:scale(-1, 1);-o-transform:scale(-1, 1);transform:scale(-1, 1)}
.icon-flip-vertical:before{-webkit-transform:scale(1, -1);-moz-transform:scale(1, -1);-ms-transform:scale(1, -1);-o-transform:scale(1, -1);transform:scale(1, -1)}
a .icon-rotate-90:before,a .icon-rotate-180:before,a .icon-rotate-270:before,a .icon-flip-horizontal:before,a .icon-flip-vertical:before{display:inline-block}
.icon-glass:before{content:"\f000"}
.icon-music:before{content:"\f001"}
.icon-search:before{content:"\f002"}
.icon-envelope-alt:before{content:"\f003"}
.icon-heart:before{content:"\f004"}
.icon-star:before{content:"\f005"}
.icon-star-empty:before{content:"\f006"}
.icon-user:before{content:"\f007"}
.icon-film:before{content:"\f008"}
.icon-th-large:before{content:"\f009"}
.icon-th:before{content:"\f00a"}
.icon-th-list:before{content:"\f00b"}
.icon-ok:before{content:"\f00c"}
.icon-remove:before{content:"\f00d"}
.icon-zoom-in:before{content:"\f00e"}
.icon-zoom-out:before{content:"\f010"}
.icon-power-off:before,.icon-off:before{content:"\f011"}
.icon-signal:before{content:"\f012"}
.icon-gear:before,.icon-cog:before{content:"\f013"}
.icon-trash:before{content:"\f014"}
.icon-home:before{content:"\f015"}
.icon-file-alt:before{content:"\f016"}
.icon-time:before{content:"\f017"}
.icon-road:before{content:"\f018"}
.icon-download-alt:before{content:"\f019"}
.icon-download:before{content:"\f01a"}
.icon-upload:before{content:"\f01b"}
.icon-inbox:before{content:"\f01c"}
.icon-play-circle:before{content:"\f01d"}
.icon-rotate-right:before,.icon-repeat:before{content:"\f01e"}
.icon-refresh:before{content:"\f021"}
.icon-list-alt:before{content:"\f022"}
.icon-lock:before{content:"\f023"}
.icon-flag:before{content:"\f024"}
.icon-headphones:before{content:"\f025"}
.icon-volume-off:before{content:"\f026"}
.icon-volume-down:before{content:"\f027"}
.icon-volume-up:before{content:"\f028"}
.icon-qrcode:before{content:"\f029"}
.icon-barcode:before{content:"\f02a"}
.icon-tag:before{content:"\f02b"}
.icon-tags:before{content:"\f02c"}
.icon-book:before{content:"\f02d"}
.icon-bookmark:before{content:"\f02e"}
.icon-print:before{content:"\f02f"}
.icon-camera:before{content:"\f030"}
.icon-font:before{content:"\f031"}
.icon-bold:before{content:"\f032"}
.icon-italic:before{content:"\f033"}
.icon-text-height:before{content:"\f034"}
.icon-text-width:before{content:"\f035"}
.icon-align-left:before{content:"\f036"}
.icon-align-center:before{content:"\f037"}
.icon-align-right:before{content:"\f038"}
.icon-align-justify:before{content:"\f039"}
.icon-list:before{content:"\f03a"}
.icon-indent-left:before{content:"\f03b"}
.icon-indent-right:before{content:"\f03c"}
.icon-facetime-video:before{content:"\f03d"}
.icon-picture:before{content:"\f03e"}
.icon-pencil:before{content:"\f040"}
.icon-map-marker:before{content:"\f041"}
.icon-adjust:before{content:"\f042"}
.icon-tint:before{content:"\f043"}
.icon-edit:before{content:"\f044"}
.icon-share:before{content:"\f045"}
.icon-check:before{content:"\f046"}
.icon-move:before{content:"\f047"}
.icon-step-backward:before{content:"\f048"}
.icon-fast-backward:before{content:"\f049"}
.icon-backward:before{content:"\f04a"}
.icon-play:before{content:"\f04b"}
.icon-pause:before{content:"\f04c"}
.icon-stop:before{content:"\f04d"}
.icon-forward:before{content:"\f04e"}
.icon-fast-forward:before{content:"\f050"}
.icon-step-forward:before{content:"\f051"}
.icon-eject:before{content:"\f052"}
.icon-chevron-left:before{content:"\f053"}
.icon-chevron-right:before{content:"\f054"}
.icon-plus-sign:before{content:"\f055"}
.icon-minus-sign:before{content:"\f056"}
.icon-remove-sign:before{content:"\f057"}
.icon-ok-sign:before{content:"\f058"}
.icon-question-sign:before{content:"\f059"}
.icon-info-sign:before{content:"\f05a"}
.icon-screenshot:before{content:"\f05b"}
.icon-remove-circle:before{content:"\f05c"}
.icon-ok-circle:before{content:"\f05d"}
.icon-ban-circle:before{content:"\f05e"}
.icon-arrow-left:before{content:"\f060"}
.icon-arrow-right:before{content:"\f061"}
.icon-arrow-up:before{content:"\f062"}
.icon-arrow-down:before{content:"\f063"}
.icon-mail-forward:before,.icon-share-alt:before{content:"\f064"}
.icon-resize-full:before{content:"\f065"}
.icon-resize-small:before{content:"\f066"}
.icon-plus:before{content:"\f067"}
.icon-minus:before{content:"\f068"}
.icon-asterisk:before{content:"\f069"}
.icon-exclamation-sign:before{content:"\f06a"}
.icon-gift:before{content:"\f06b"}
.icon-leaf:before{content:"\f06c"}
.icon-fire:before{content:"\f06d"}
.icon-eye-open:before{content:"\f06e"}
.icon-eye-close:before{content:"\f070"}
.icon-warning-sign:before{content:"\f071"}
.icon-plane:before{content:"\f072"}
.icon-calendar:before{content:"\f073"}
.icon-random:before{content:"\f074"}
.icon-comment:before{content:"\f075"}
.icon-magnet:before{content:"\f076"}
.icon-chevron-up:before{content:"\f077"}
.icon-chevron-down:before{content:"\f078"}
.icon-retweet:before{content:"\f079"}
.icon-shopping-cart:before{content:"\f07a"}
.icon-folder-close:before{content:"\f07b"}
.icon-folder-open:before{content:"\f07c"}
.icon-resize-vertical:before{content:"\f07d"}
.icon-resize-horizontal:before{content:"\f07e"}
.icon-bar-chart:before{content:"\f080"}
.icon-twitter-sign:before{content:"\f081"}
.icon-facebook-sign:before{content:"\f082"}
.icon-camera-retro:before{content:"\f083"}
.icon-key:before{content:"\f084"}
.icon-gears:before,.icon-cogs:before{content:"\f085"}
.icon-comments:before{content:"\f086"}
.icon-thumbs-up-alt:before{content:"\f087"}
.icon-thumbs-down-alt:before{content:"\f088"}
.icon-star-half:before{content:"\f089"}
.icon-heart-empty:before{content:"\f08a"}
.icon-signout:before{content:"\f08b"}
.icon-linkedin-sign:before{content:"\f08c"}
.icon-pushpin:before{content:"\f08d"}
.icon-external-link:before{content:"\f08e"}
.icon-signin:before{content:"\f090"}
.icon-trophy:before{content:"\f091"}
.icon-github-sign:before{content:"\f092"}
.icon-upload-alt:before{content:"\f093"}
.icon-lemon:before{content:"\f094"}
.icon-phone:before{content:"\f095"}
.icon-unchecked:before,.icon-check-empty:before{content:"\f096"}
.icon-bookmark-empty:before{content:"\f097"}
.icon-phone-sign:before{content:"\f098"}
.icon-twitter:before{content:"\f099"}
.icon-facebook:before{content:"\f09a"}
.icon-github:before{content:"\f09b"}
.icon-unlock:before{content:"\f09c"}
.icon-credit-card:before{content:"\f09d"}
.icon-rss:before{content:"\f09e"}
.icon-hdd:before{content:"\f0a0"}
.icon-bullhorn:before{content:"\f0a1"}
.icon-bell:before{content:"\f0a2"}
.icon-certificate:before{content:"\f0a3"}
.icon-hand-right:before{content:"\f0a4"}
.icon-hand-left:before{content:"\f0a5"}
.icon-hand-up:before{content:"\f0a6"}
.icon-hand-down:before{content:"\f0a7"}
.icon-circle-arrow-left:before{content:"\f0a8"}
.icon-circle-arrow-right:before{content:"\f0a9"}
.icon-circle-arrow-up:before{content:"\f0aa"}
.icon-circle-arrow-down:before{content:"\f0ab"}
.icon-globe:before{content:"\f0ac"}
.icon-wrench:before{content:"\f0ad"}
.icon-tasks:before{content:"\f0ae"}
.icon-filter:before{content:"\f0b0"}
.icon-briefcase:before{content:"\f0b1"}
.icon-fullscreen:before{content:"\f0b2"}
.icon-group:before{content:"\f0c0"}
.icon-link:before{content:"\f0c1"}
.icon-cloud:before{content:"\f0c2"}
.icon-beaker:before{content:"\f0c3"}
.icon-cut:before{content:"\f0c4"}
.icon-copy:before{content:"\f0c5"}
.icon-paperclip:before,.icon-paper-clip:before{content:"\f0c6"}
.icon-save:before{content:"\f0c7"}
.icon-sign-blank:before{content:"\f0c8"}
.icon-reorder:before{content:"\f0c9"}
.icon-list-ul:before{content:"\f0ca"}
.icon-list-ol:before{content:"\f0cb"}
.icon-strikethrough:before{content:"\f0cc"}
.icon-underline:before{content:"\f0cd"}
.icon-table:before{content:"\f0ce"}
.icon-magic:before{content:"\f0d0"}
.icon-truck:before{content:"\f0d1"}
.icon-pinterest:before{content:"\f0d2"}
.icon-pinterest-sign:before{content:"\f0d3"}
.icon-google-plus-sign:before{content:"\f0d4"}
.icon-google-plus:before{content:"\f0d5"}
.icon-money:before{content:"\f0d6"}
.icon-caret-down:before{content:"\f0d7"}
.icon-caret-up:before{content:"\f0d8"}
.icon-caret-left:before{content:"\f0d9"}
.icon-caret-right:before{content:"\f0da"}
.icon-columns:before{content:"\f0db"}
.icon-sort:before{content:"\f0dc"}
.icon-sort-down:before{content:"\f0dd"}
.icon-sort-up:before{content:"\f0de"}
.icon-envelope:before{content:"\f0e0"}
.icon-linkedin:before{content:"\f0e1"}
.icon-rotate-left:before,.icon-undo:before{content:"\f0e2"}
.icon-legal:before{content:"\f0e3"}
.icon-dashboard:before{content:"\f0e4"}
.icon-comment-alt:before{content:"\f0e5"}
.icon-comments-alt:before{content:"\f0e6"}
.icon-bolt:before{content:"\f0e7"}
.icon-sitemap:before{content:"\f0e8"}
.icon-umbrella:before{content:"\f0e9"}
.icon-paste:before{content:"\f0ea"}
.icon-lightbulb:before{content:"\f0eb"}
.icon-exchange:before{content:"\f0ec"}
.icon-cloud-download:before{content:"\f0ed"}
.icon-cloud-upload:before{content:"\f0ee"}
.icon-user-md:before{content:"\f0f0"}
.icon-stethoscope:before{content:"\f0f1"}
.icon-suitcase:before{content:"\f0f2"}
.icon-bell-alt:before{content:"\f0f3"}
.icon-coffee:before{content:"\f0f4"}
.icon-food:before{content:"\f0f5"}
.icon-file-text-alt:before{content:"\f0f6"}
.icon-building:before{content:"\f0f7"}
.icon-hospital:before{content:"\f0f8"}
.icon-ambulance:before{content:"\f0f9"}
.icon-medkit:before{content:"\f0fa"}
.icon-fighter-jet:before{content:"\f0fb"}
.icon-beer:before{content:"\f0fc"}
.icon-h-sign:before{content:"\f0fd"}
.icon-plus-sign-alt:before{content:"\f0fe"}
.icon-double-angle-left:before{content:"\f100"}
.icon-double-angle-right:before{content:"\f101"}
.icon-double-angle-up:before{content:"\f102"}
.icon-double-angle-down:before{content:"\f103"}
.icon-angle-left:before{content:"\f104"}
.icon-angle-right:before{content:"\f105"}
.icon-angle-up:before{content:"\f106"}
.icon-angle-down:before{content:"\f107"}
.icon-desktop:before{content:"\f108"}
.icon-laptop:before{content:"\f109"}
.icon-tablet:before{content:"\f10a"}
.icon-mobile-phone:before{content:"\f10b"}
.icon-circle-blank:before{content:"\f10c"}
.icon-quote-left:before{content:"\f10d"}
.icon-quote-right:before{content:"\f10e"}
.icon-spinner:before{content:"\f110"}
.icon-circle:before{content:"\f111"}
.icon-mail-reply:before,.icon-reply:before{content:"\f112"}
.icon-github-alt:before{content:"\f113"}
.icon-folder-close-alt:before{content:"\f114"}
.icon-folder-open-alt:before{content:"\f115"}
.icon-expand-alt:before{content:"\f116"}
.icon-collapse-alt:before{content:"\f117"}
.icon-smile:before{content:"\f118"}
.icon-frown:before{content:"\f119"}
.icon-meh:before{content:"\f11a"}
.icon-gamepad:before{content:"\f11b"}
.icon-keyboard:before{content:"\f11c"}
.icon-flag-alt:before{content:"\f11d"}
.icon-flag-checkered:before{content:"\f11e"}
.icon-terminal:before{content:"\f120"}
.icon-code:before{content:"\f121"}
.icon-reply-all:before{content:"\f122"}
.icon-mail-reply-all:before{content:"\f122"}
.icon-star-half-full:before,.icon-star-half-empty:before{content:"\f123"}
.icon-location-arrow:before{content:"\f124"}
.icon-crop:before{content:"\f125"}
.icon-code-fork:before{content:"\f126"}
.icon-unlink:before{content:"\f127"}
.icon-question:before{content:"\f128"}
.icon-info:before{content:"\f129"}
.icon-exclamation:before{content:"\f12a"}
.icon-superscript:before{content:"\f12b"}
.icon-subscript:before{content:"\f12c"}
.icon-eraser:before{content:"\f12d"}
.icon-puzzle-piece:before{content:"\f12e"}
.icon-microphone:before{content:"\f130"}
.icon-microphone-off:before{content:"\f131"}
.icon-shield:before{content:"\f132"}
.icon-calendar-empty:before{content:"\f133"}
.icon-fire-extinguisher:before{content:"\f134"}
.icon-rocket:before{content:"\f135"}
.icon-maxcdn:before{content:"\f136"}
.icon-chevron-sign-left:before{content:"\f137"}
.icon-chevron-sign-right:before{content:"\f138"}
.icon-chevron-sign-up:before{content:"\f139"}
.icon-chevron-sign-down:before{content:"\f13a"}
.icon-html5:before{content:"\f13b"}
.icon-css3:before{content:"\f13c"}
.icon-anchor:before{content:"\f13d"}
.icon-unlock-alt:before{content:"\f13e"}
.icon-bullseye:before{content:"\f140"}
.icon-ellipsis-horizontal:before{content:"\f141"}
.icon-ellipsis-vertical:before{content:"\f142"}
.icon-rss-sign:before{content:"\f143"}
.icon-play-sign:before{content:"\f144"}
.icon-ticket:before{content:"\f145"}
.icon-minus-sign-alt:before{content:"\f146"}
.icon-check-minus:before{content:"\f147"}
.icon-level-up:before{content:"\f148"}
.icon-level-down:before{content:"\f149"}
.icon-check-sign:before{content:"\f14a"}
.icon-edit-sign:before{content:"\f14b"}
.icon-external-link-sign:before{content:"\f14c"}
.icon-share-sign:before{content:"\f14d"}
.icon-compass:before{content:"\f14e"}
.icon-collapse:before{content:"\f150"}
.icon-collapse-top:before{content:"\f151"}
.icon-expand:before{content:"\f152"}
.icon-euro:before,.icon-eur:before{content:"\f153"}
.icon-gbp:before{content:"\f154"}
.icon-dollar:before,.icon-usd:before{content:"\f155"}
.icon-rupee:before,.icon-inr:before{content:"\f156"}
.icon-yen:before,.icon-jpy:before{content:"\f157"}
.icon-renminbi:before,.icon-cny:before{content:"\f158"}
.icon-won:before,.icon-krw:before{content:"\f159"}
.icon-bitcoin:before,.icon-btc:before{content:"\f15a"}
.icon-file:before{content:"\f15b"}
.icon-file-text:before{content:"\f15c"}
.icon-sort-by-alphabet:before{content:"\f15d"}
.icon-sort-by-alphabet-alt:before{content:"\f15e"}
.icon-sort-by-attributes:before{content:"\f160"}
.icon-sort-by-attributes-alt:before{content:"\f161"}
.icon-sort-by-order:before{content:"\f162"}
.icon-sort-by-order-alt:before{content:"\f163"}
.icon-thumbs-up:before{content:"\f164"}
.icon-thumbs-down:before{content:"\f165"}
.icon-youtube-sign:before{content:"\f166"}
.icon-youtube:before{content:"\f167"}
.icon-xing:before{content:"\f168"}
.icon-xing-sign:before{content:"\f169"}
.icon-youtube-play:before{content:"\f16a"}
.icon-dropbox:before{content:"\f16b"}
.icon-stackexchange:before{content:"\f16c"}
.icon-instagram:before{content:"\f16d"}
.icon-flickr:before{content:"\f16e"}
.icon-adn:before{content:"\f170"}
.icon-bitbucket:before{content:"\f171"}
.icon-bitbucket-sign:before{content:"\f172"}
.icon-tumblr:before{content:"\f173"}
.icon-tumblr-sign:before{content:"\f174"}
.icon-long-arrow-down:before{content:"\f175"}
.icon-long-arrow-up:before{content:"\f176"}
.icon-long-arrow-left:before{content:"\f177"}
.icon-long-arrow-right:before{content:"\f178"}
.icon-apple:before{content:"\f179"}
.icon-windows:before{content:"\f17a"}
.icon-android:before{content:"\f17b"}
.icon-linux:before{content:"\f17c"}
.icon-dribbble:before{content:"\f17d"}
.icon-skype:before{content:"\f17e"}
.icon-foursquare:before{content:"\f180"}
.icon-trello:before{content:"\f181"}
.icon-female:before{content:"\f182"}
.icon-male:before{content:"\f183"}
.icon-gittip:before{content:"\f184"}
.icon-sun:before{content:"\f185"}
.icon-moon:before{content:"\f186"}
.icon-archive:before{content:"\f187"}
.icon-bug:before{content:"\f188"}
.icon-vk:before{content:"\f189"}
.icon-weibo:before{content:"\f18a"}
.icon-renren:before{content:"\f18b"}
code{color:#000}
pre{font-size:inherit;line-height:inherit}
.border-box-sizing{box-sizing:border-box;-moz-box-sizing:border-box;-webkit-box-sizing:border-box}
.corner-all{border-radius:4px}
.hbox{display:-webkit-box;-webkit-box-orient:horizontal;-webkit-box-align:stretch;display:-moz-box;-moz-box-orient:horizontal;-moz-box-align:stretch;display:box;box-orient:horizontal;box-align:stretch;display:flex;flex-direction:row;align-items:stretch}
.hbox>*{-webkit-box-flex:0;-moz-box-flex:0;box-flex:0;flex:none}
.vbox{display:-webkit-box;-webkit-box-orient:vertical;-webkit-box-align:stretch;display:-moz-box;-moz-box-orient:vertical;-moz-box-align:stretch;display:box;box-orient:vertical;box-align:stretch;display:flex;flex-direction:column;align-items:stretch}
.vbox>*{-webkit-box-flex:0;-moz-box-flex:0;box-flex:0;flex:none}
.hbox.reverse,.vbox.reverse,.reverse{-webkit-box-direction:reverse;-moz-box-direction:reverse;box-direction:reverse;flex-direction:row-reverse}
.hbox.box-flex0,.vbox.box-flex0,.box-flex0{-webkit-box-flex:0;-moz-box-flex:0;box-flex:0;flex:none;width:auto}
.hbox.box-flex1,.vbox.box-flex1,.box-flex1{-webkit-box-flex:1;-moz-box-flex:1;box-flex:1;flex:1}
.hbox.box-flex,.vbox.box-flex,.box-flex{-webkit-box-flex:1;-moz-box-flex:1;box-flex:1;flex:1}
.hbox.box-flex2,.vbox.box-flex2,.box-flex2{-webkit-box-flex:2;-moz-box-flex:2;box-flex:2;flex:2}
.box-group1{-webkit-box-flex-group:1;-moz-box-flex-group:1;box-flex-group:1}
.box-group2{-webkit-box-flex-group:2;-moz-box-flex-group:2;box-flex-group:2}
.hbox.start,.vbox.start,.start{-webkit-box-pack:start;-moz-box-pack:start;box-pack:start;justify-content:flex-start}
.hbox.end,.vbox.end,.end{-webkit-box-pack:end;-moz-box-pack:end;box-pack:end;justify-content:flex-end}
.hbox.center,.vbox.center,.center{-webkit-box-pack:center;-moz-box-pack:center;box-pack:center;justify-content:center}
.hbox.align-start,.vbox.align-start,.align-start{-webkit-box-align:start;-moz-box-align:start;box-align:start;align-items:flex-start}
.hbox.align-end,.vbox.align-end,.align-end{-webkit-box-align:end;-moz-box-align:end;box-align:end;align-items:flex-end}
.hbox.align-center,.vbox.align-center,.align-center{-webkit-box-align:center;-moz-box-align:center;box-align:center;align-items:center}
div.error{margin:2em;text-align:center}
div.error>h1{font-size:500%;line-height:normal}
div.error>p{font-size:200%;line-height:normal}
div.traceback-wrapper{text-align:left;max-width:800px;margin:auto}
body{background-color:#fff;position:absolute;left:0;right:0;top:0;bottom:0;overflow:visible}
div#header{display:none}
#ipython_notebook{padding-left:16px}
#noscript{width:auto;padding-top:16px;padding-bottom:16px;text-align:center;font-size:22px;color:#f00;font-weight:bold}
#ipython_notebook img{font-family:Verdana,"Helvetica Neue",Arial,Helvetica,Geneva,sans-serif;height:24px;text-decoration:none;color:#000}
#site{width:100%;display:none}
.ui-button .ui-button-text{padding:.2em .8em;font-size:77%}
input.ui-button{padding:.3em .9em}
.navbar span{margin-top:3px}
span#login_widget{float:right}
.nav-header{text-transform:none}
.navbar-nobg{background-color:transparent;background-image:none}
#header>span{margin-top:10px}
.modal_stretch{display:-webkit-box;-webkit-box-orient:vertical;-webkit-box-align:stretch;display:-moz-box;-moz-box-orient:vertical;-moz-box-align:stretch;display:box;box-orient:vertical;box-align:stretch;display:flex;flex-direction:column;align-items:stretch;height:80%}.modal_stretch .modal-body{max-height:none;flex:1}
@media (min-width:768px){.modal{width:700px;margin-left:-350px}}.center-nav{display:inline-block;margin-bottom:-4px}
.alternate_upload{background-color:none;display:inline}
.alternate_upload.form{padding:0;margin:0}
.alternate_upload input.fileinput{background-color:#f00;position:relative;opacity:0;z-index:2;width:295px;margin-left:163px;cursor:pointer;height:26px}
ul#tabs{margin-bottom:4px}
ul#tabs a{padding-top:4px;padding-bottom:4px}
ul.breadcrumb a:focus,ul.breadcrumb a:hover{text-decoration:none}
ul.breadcrumb i.icon-home{font-size:16px;margin-right:4px}
ul.breadcrumb span{color:#5e5e5e}
.list_toolbar{padding:4px 0 4px 0}
.list_toolbar [class*="span"]{min-height:26px}
.list_header{font-weight:bold}
.list_container{margin-top:4px;margin-bottom:20px;border:1px solid #ababab;border-radius:4px}
.list_container>div{border-bottom:1px solid #ababab}.list_container>div:hover .list-item{background-color:#f00}
.list_container>div:last-child{border:none}
.list_item:hover .list_item{background-color:#ddd}
.list_item a{text-decoration:none}
.list_header>div,.list_item>div{padding-top:4px;padding-bottom:4px;padding-left:7px;padding-right:7px;height:22px;line-height:22px}
.item_name{line-height:22px;height:26px}
.item_icon{font-size:14px;color:#5e5e5e;margin-right:7px}
.item_buttons{line-height:1em}
.toolbar_info{height:26px;line-height:26px}
input.nbname_input,input.engine_num_input{padding-top:3px;padding-bottom:3px;height:14px;line-height:14px;margin:0}
input.engine_num_input{width:60px}
.highlight_text{color:#00f}
#project_name>.breadcrumb{padding:0;margin-bottom:0;background-color:transparent;font-weight:bold}
.folder_icon:before{font-family:FontAwesome;font-weight:normal;font-style:normal;text-decoration:inherit;-webkit-font-smoothing:antialiased;*margin-right:.3em;content:"\f114"}
.notebook_icon:before{font-family:FontAwesome;font-weight:normal;font-style:normal;text-decoration:inherit;-webkit-font-smoothing:antialiased;*margin-right:.3em;content:"\f02d"}
.ansibold{font-weight:bold}
.ansiblack{color:#000}
.ansired{color:#8b0000}
.ansigreen{color:#006400}
.ansiyellow{color:#a52a2a}
.ansiblue{color:#00008b}
.ansipurple{color:#9400d3}
.ansicyan{color:#4682b4}
.ansigray{color:#808080}
.ansibgblack{background-color:#000}
.ansibgred{background-color:#f00}
.ansibggreen{background-color:#008000}
.ansibgyellow{background-color:#ff0}
.ansibgblue{background-color:#00f}
.ansibgpurple{background-color:#f0f}
.ansibgcyan{background-color:#0ff}
.ansibggray{background-color:#808080}
div.cell{border:1px solid transparent;display:-webkit-box;-webkit-box-orient:vertical;-webkit-box-align:stretch;display:-moz-box;-moz-box-orient:vertical;-moz-box-align:stretch;display:box;box-orient:vertical;box-align:stretch;display:flex;flex-direction:column;align-items:stretch}div.cell.selected{border-radius:4px;border:thin #ababab solid}
div.cell.edit_mode{border-radius:4px;border:thin #008000 solid}
div.cell{width:100%;padding:5px 5px 5px 0;margin:0;outline:none}
div.prompt{min-width:11ex;padding:.4em;margin:0;font-family:monospace;text-align:right;line-height:1.21429em}
@media (max-width:480px){div.prompt{text-align:left}}div.inner_cell{display:-webkit-box;-webkit-box-orient:vertical;-webkit-box-align:stretch;display:-moz-box;-moz-box-orient:vertical;-moz-box-align:stretch;display:box;box-orient:vertical;box-align:stretch;display:flex;flex-direction:column;align-items:stretch;-webkit-box-flex:1;-moz-box-flex:1;box-flex:1;flex:1}
div.input_area{width:800px;border:1px solid #cfcfcf;border-radius:4px;background:#f7f7f7;line-height:1.21429em}
div.prompt:empty{padding-top:0;padding-bottom:0}
div.input{page-break-inside:avoid;display:-webkit-box;-webkit-box-orient:horizontal;-webkit-box-align:stretch;display:-moz-box;-moz-box-orient:horizontal;-moz-box-align:stretch;display:box;box-orient:horizontal;box-align:stretch;display:flex;flex-direction:row;align-items:stretch}
@media (max-width:480px){div.input{display:-webkit-box;-webkit-box-orient:vertical;-webkit-box-align:stretch;display:-moz-box;-moz-box-orient:vertical;-moz-box-align:stretch;display:box;box-orient:vertical;box-align:stretch;display:flex;flex-direction:column;align-items:stretch}}div.input_prompt{color:#000080;border-top:1px solid transparent}
div.input_area>div.highlight{margin:.4em;border:none;padding:0;background-color:transparent}
div.input_area>div.highlight>pre{margin:0;border:none;padding:0;background-color:transparent}
.CodeMirror{line-height:1.21429em;height:auto;background:none;}
.CodeMirror-scroll{overflow-y:hidden;overflow-x:auto}
.CodeMirror-lines{padding:.4em}
.CodeMirror-linenumber{padding:0 8px 0 4px}
.CodeMirror-gutters{border-bottom-left-radius:4px;border-top-left-radius:4px}
.CodeMirror pre{padding:0;border:0;border-radius:0;-webkit-border-radius:0;-moz-border-radius:0;border-radius:0}
pre code{display:block;padding:.5em}
.highlight-base,pre code,pre .subst,pre .tag .title,pre .lisp .title,pre .clojure .built_in,pre .nginx .title{color:#000}
.highlight-string,pre .string,pre .constant,pre .parent,pre .tag .value,pre .rules .value,pre .rules .value .number,pre .preprocessor,pre .ruby .symbol,pre .ruby .symbol .string,pre .aggregate,pre .template_tag,pre .django .variable,pre .smalltalk .class,pre .addition,pre .flow,pre .stream,pre .bash .variable,pre .apache .tag,pre .apache .cbracket,pre .tex .command,pre .tex .special,pre .erlang_repl .function_or_atom,pre .markdown .header{color:#ba2121}
.highlight-comment,pre .comment,pre .annotation,pre .template_comment,pre .diff .header,pre .chunk,pre .markdown .blockquote{color:#408080;font-style:italic}
.highlight-number,pre .number,pre .date,pre .regexp,pre .literal,pre .smalltalk .symbol,pre .smalltalk .char,pre .go .constant,pre .change,pre .markdown .bullet,pre .markdown .link_url{color:#080}
pre .label,pre .javadoc,pre .ruby .string,pre .decorator,pre .filter .argument,pre .localvars,pre .array,pre .attr_selector,pre .important,pre .pseudo,pre .pi,pre .doctype,pre .deletion,pre .envvar,pre .shebang,pre .apache .sqbracket,pre .nginx .built_in,pre .tex .formula,pre .erlang_repl .reserved,pre .prompt,pre .markdown .link_label,pre .vhdl .attribute,pre .clojure .attribute,pre .coffeescript .property{color:#88f}
.highlight-keyword,pre .keyword,pre .id,pre .phpdoc,pre .aggregate,pre .css .tag,pre .javadoctag,pre .phpdoc,pre .yardoctag,pre .smalltalk .class,pre .winutils,pre .bash .variable,pre .apache .tag,pre .go .typename,pre .tex .command,pre .markdown .strong,pre .request,pre .status{color:#008000;font-weight:bold}
.highlight-builtin,pre .built_in{color:#008000}
pre .markdown .emphasis{font-style:italic}
pre .nginx .built_in{font-weight:normal}
pre .coffeescript .javascript,pre .javascript .xml,pre .tex .formula,pre .xml .javascript,pre .xml .vbscript,pre .xml .css,pre .xml .cdata{opacity:.5}
.cm-s-ipython span.cm-variable{color:#000}
.cm-s-ipython span.cm-keyword{color:#008000;font-weight:bold}
.cm-s-ipython span.cm-number{color:#080}
.cm-s-ipython span.cm-comment{color:#408080;font-style:italic}
.cm-s-ipython span.cm-string{color:#ba2121}
.cm-s-ipython span.cm-builtin{color:#008000}
.cm-s-ipython span.cm-error{color:#f00}
.cm-s-ipython span.cm-operator{color:#a2f;font-weight:bold}
.cm-s-ipython span.cm-meta{color:#a2f}
.cm-s-ipython span.cm-tab{background:url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADAAAAAMCAYAAAAkuj5RAAAAAXNSR0IArs4c6QAAAGFJREFUSMft1LsRQFAQheHPowAKoACx3IgEKtaEHujDjORSgWTH/ZOdnZOcM/sgk/kFFWY0qV8foQwS4MKBCS3qR6ixBJvElOobYAtivseIE120FaowJPN75GMu8j/LfMwNjh4HUpwg4LUAAAAASUVORK5CYII=);background-position:right;background-repeat:no-repeat}
div.output_wrapper{position:relative;display:-webkit-box;-webkit-box-orient:vertical;-webkit-box-align:stretch;display:-moz-box;-moz-box-orient:vertical;-moz-box-align:stretch;display:box;box-orient:vertical;box-align:stretch;display:flex;flex-direction:column;align-items:stretch}
div.output_scroll{height:24em;width:100%;overflow:auto;border-radius:4px;-webkit-box-shadow:inset 0 2px 8px rgba(0,0,0,0.8);-moz-box-shadow:inset 0 2px 8px rgba(0,0,0,0.8);box-shadow:inset 0 2px 8px rgba(0,0,0,0.8);display:block}
div.output_collapsed{margin:0;padding:0;display:-webkit-box;-webkit-box-orient:vertical;-webkit-box-align:stretch;display:-moz-box;-moz-box-orient:vertical;-moz-box-align:stretch;display:box;box-orient:vertical;box-align:stretch;display:flex;flex-direction:column;align-items:stretch}
div.out_prompt_overlay{height:100%;padding:0 .4em;position:absolute;border-radius:4px}
div.out_prompt_overlay:hover{-webkit-box-shadow:inset 0 0 1px #000;-moz-box-shadow:inset 0 0 1px #000;box-shadow:inset 0 0 1px #000;background:rgba(240,240,240,0.5)}
div.output_prompt{color:#8b0000}
div.output_area{padding:0;width: 800px;page-break-inside:avoid;display:-webkit-box;-webkit-box-orient:horizontal;-webkit-box-align:stretch;display:-moz-box;-moz-box-orient:horizontal;-moz-box-align:stretch;display:box;box-orient:horizontal;box-align:stretch;display:flex;flex-direction:row;align-items:stretch}div.output_area .MathJax_Display{text-align:left !important}
div.output_area .rendered_html table{margin-left:0;margin-right:0}
div.output_area .rendered_html img{margin-left:0;margin-right:0}
.output{display:-webkit-box;-webkit-box-orient:vertical;-webkit-box-align:stretch;display:-moz-box;-moz-box-orient:vertical;-moz-box-align:stretch;display:box;box-orient:vertical;box-align:stretch;display:flex;flex-direction:column;align-items:stretch}
@media (max-width:480px){div.output_area{display:-webkit-box;-webkit-box-orient:vertical;-webkit-box-align:stretch;display:-moz-box;-moz-box-orient:vertical;-moz-box-align:stretch;display:box;box-orient:vertical;box-align:stretch;display:flex;flex-direction:column;align-items:stretch}}div.output_area pre{margin:0;padding:0;border:0;vertical-align:baseline;color:#666;background-color:transparent;border-radius:0;-webkit-border-radius:0;-moz-border-radius:0;border-radius:0}
div.output_subarea{padding:.4em .4em 0 .4em;-webkit-box-flex:1;-moz-box-flex:1;box-flex:1;flex:1}
div.output_text{text-align:left;line-height:1.21429em}
div.output_stderr{background:#fdd;}
div.output_latex{text-align:left}
div.output_javascript:empty{padding:0}
.js-error{color:#8b0000}
div.raw_input_container{font-family:monospace;padding-top:5px}
span.raw_input_prompt{}
input.raw_input{font-family:inherit;font-size:inherit;color:inherit;width:auto;vertical-align:baseline;padding:0 .25em;margin:0 .25em}
input.raw_input:focus{box-shadow:none}
p.p-space{margin-bottom:10px}
.rendered_html{color:#000;}.rendered_html em{font-style:italic}
.rendered_html strong{font-weight:bold}
.rendered_html u{text-decoration:underline}
.rendered_html :link{text-decoration:underline}
.rendered_html :visited{text-decoration:underline}
.rendered_html h1{font-size:185.7%;margin:1.08em 0 0 0;font-weight:bold;line-height:1}
.rendered_html h2{font-size:157.1%;margin:1.27em 0 0 0;font-weight:bold;line-height:1}
.rendered_html h3{font-size:128.6%;margin:1.55em 0 0 0;font-weight:bold;line-height:1}
.rendered_html h4{font-size:100%;margin:2em 0 0 0;font-weight:bold;line-height:1}
.rendered_html h5{font-size:100%;margin:2em 0 0 0;font-weight:bold;line-height:1;font-style:italic}
.rendered_html h6{font-size:100%;margin:2em 0 0 0;font-weight:bold;line-height:1;font-style:italic}
.rendered_html h1:first-child{margin-top:.538em}
.rendered_html h2:first-child{margin-top:.636em}
.rendered_html h3:first-child{margin-top:.777em}
.rendered_html h4:first-child{margin-top:1em}
.rendered_html h5:first-child{margin-top:1em}
.rendered_html h6:first-child{margin-top:1em}
.rendered_html ul{list-style:disc;margin:0 2em}
.rendered_html ul ul{list-style:square;margin:0 2em}
.rendered_html ul ul ul{list-style:circle;margin:0 2em}
.rendered_html ol{list-style:decimal;margin:0 2em}
.rendered_html ol ol{list-style:upper-alpha;margin:0 2em}
.rendered_html ol ol ol{list-style:lower-alpha;margin:0 2em}
.rendered_html ol ol ol ol{list-style:lower-roman;margin:0 2em}
.rendered_html ol ol ol ol ol{list-style:decimal;margin:0 2em}
.rendered_html *+ul{margin-top:1em}
.rendered_html *+ol{margin-top:1em}
.rendered_html hr{color:#000;background-color:#000}
.rendered_html pre{margin:1em 2em}
.rendered_html pre,.rendered_html code{border:0;background-color:#fff;color:#000;font-size:100%;padding:0}
.rendered_html blockquote{margin:1em 2em}
.rendered_html table{margin-left:auto;margin-right:auto;border:1px solid #000;border-collapse:collapse}
.rendered_html tr,.rendered_html th,.rendered_html td{border:1px solid #000;border-collapse:collapse;margin:1em 2em}
.rendered_html td,.rendered_html th{text-align:left;vertical-align:middle;padding:4px}
.rendered_html th{font-weight:bold}
.rendered_html *+table{margin-top:1em}
.rendered_html p{text-align:justify}
.rendered_html *+p{margin-top:1em}
.rendered_html img{display:block;margin-left:auto;margin-right:auto}
.rendered_html *+img{margin-top:1em}
div.text_cell{width: 800px;padding:5px 5px 5px 0;display:-webkit-box;-webkit-box-orient:horizontal;-webkit-box-align:stretch;display:-moz-box;-moz-box-orient:horizontal;-moz-box-align:stretch;display:box;box-orient:horizontal;box-align:stretch;display:flex;flex-direction:row;align-items:stretch}
@media (max-width:480px){div.text_cell>div.prompt{display:none}}div.text_cell_render{font-family:monospace;outline:none;resize:none;width:600px;border-style:none;padding:.5em .5em .5em .4em;color:#000}
a.anchor-link:link{text-decoration:none;padding:0 20px;visibility:hidden}
h1:hover .anchor-link,h2:hover .anchor-link,h3:hover .anchor-link,h4:hover .anchor-link,h5:hover .anchor-link,h6:hover .anchor-link{visibility:visible}
div.cell.text_cell.rendered{padding:0}
.widget-area{page-break-inside:avoid;display:-webkit-box;-webkit-box-orient:horizontal;-webkit-box-align:stretch;display:-moz-box;-moz-box-orient:horizontal;-moz-box-align:stretch;display:box;box-orient:horizontal;box-align:stretch;display:flex;flex-direction:row;align-items:stretch}.widget-area .widget-subarea{padding:.44em .4em .4em 1px;margin-left:6px;box-sizing:border-box;-moz-box-sizing:border-box;-webkit-box-sizing:border-box;display:-webkit-box;-webkit-box-orient:vertical;-webkit-box-align:stretch;display:-moz-box;-moz-box-orient:vertical;-moz-box-align:stretch;display:box;box-orient:vertical;box-align:stretch;display:flex;flex-direction:column;align-items:stretch;-webkit-box-flex:2;-moz-box-flex:2;box-flex:2;flex:2;-webkit-box-align:start;-moz-box-align:start;box-align:start;align-items:flex-start}
.widget-hlabel{min-width:10ex;padding-right:8px;padding-top:3px;text-align:right;vertical-align:text-top}
.widget-vlabel{padding-bottom:5px;text-align:center;vertical-align:text-bottom}
.widget-hreadout{padding-left:8px;padding-top:3px;text-align:left;vertical-align:text-top}
.widget-vreadout{padding-top:5px;text-align:center;vertical-align:text-top}
.slide-track{border:1px solid #ccc;background:#fff;border-radius:4px;}
.widget-hslider{padding-left:8px;padding-right:5px;overflow:visible;width:348px;height:5px;max-height:5px;margin-top:11px;margin-bottom:10px;border:1px solid #ccc;background:#fff;border-radius:4px;display:-webkit-box;-webkit-box-orient:horizontal;-webkit-box-align:stretch;display:-moz-box;-moz-box-orient:horizontal;-moz-box-align:stretch;display:box;box-orient:horizontal;box-align:stretch;display:flex;flex-direction:row;align-items:stretch}.widget-hslider .ui-slider{border:0 !important;background:none !important;display:-webkit-box;-webkit-box-orient:horizontal;-webkit-box-align:stretch;display:-moz-box;-moz-box-orient:horizontal;-moz-box-align:stretch;display:box;box-orient:horizontal;box-align:stretch;display:flex;flex-direction:row;align-items:stretch;-webkit-box-flex:1;-moz-box-flex:1;box-flex:1;flex:1}.widget-hslider .ui-slider .ui-slider-handle{width:14px !important;height:28px !important;margin-top:-8px !important}
.widget-vslider{padding-bottom:8px;overflow:visible;width:5px;max-width:5px;height:250px;margin-left:12px;border:1px solid #ccc;background:#fff;border-radius:4px;display:-webkit-box;-webkit-box-orient:vertical;-webkit-box-align:stretch;display:-moz-box;-moz-box-orient:vertical;-moz-box-align:stretch;display:box;box-orient:vertical;box-align:stretch;display:flex;flex-direction:column;align-items:stretch}.widget-vslider .ui-slider{border:0 !important;background:none !important;margin-left:-4px;margin-top:5px;display:-webkit-box;-webkit-box-orient:vertical;-webkit-box-align:stretch;display:-moz-box;-moz-box-orient:vertical;-moz-box-align:stretch;display:box;box-orient:vertical;box-align:stretch;display:flex;flex-direction:column;align-items:stretch;-webkit-box-flex:1;-moz-box-flex:1;box-flex:1;flex:1}.widget-vslider .ui-slider .ui-slider-handle{width:28px !important;height:14px !important;margin-left:-9px}
.widget-text{width:350px;margin:0 !important}
.widget-listbox{width:364px;margin-bottom:0}
.widget-numeric-text{width:150px;margin:0 !important}
.widget-progress{width:363px}.widget-progress .bar{-webkit-transition:none;-moz-transition:none;-ms-transition:none;-o-transition:none;transition:none}
.widget-combo-btn{min-width:138px;}
.widget-box{margin:5px;-webkit-box-pack:start;-moz-box-pack:start;box-pack:start;justify-content:flex-start;box-sizing:border-box;-moz-box-sizing:border-box;-webkit-box-sizing:border-box;-webkit-box-align:start;-moz-box-align:start;box-align:start;align-items:flex-start}
.widget-hbox{margin:5px;-webkit-box-pack:start;-moz-box-pack:start;box-pack:start;justify-content:flex-start;box-sizing:border-box;-moz-box-sizing:border-box;-webkit-box-sizing:border-box;-webkit-box-align:start;-moz-box-align:start;box-align:start;align-items:flex-start;display:-webkit-box;-webkit-box-orient:horizontal;-webkit-box-align:stretch;display:-moz-box;-moz-box-orient:horizontal;-moz-box-align:stretch;display:box;box-orient:horizontal;box-align:stretch;display:flex;flex-direction:row;align-items:stretch}
.widget-hbox-single{margin:5px;-webkit-box-pack:start;-moz-box-pack:start;box-pack:start;justify-content:flex-start;box-sizing:border-box;-moz-box-sizing:border-box;-webkit-box-sizing:border-box;-webkit-box-align:start;-moz-box-align:start;box-align:start;align-items:flex-start;display:-webkit-box;-webkit-box-orient:horizontal;-webkit-box-align:stretch;display:-moz-box;-moz-box-orient:horizontal;-moz-box-align:stretch;display:box;box-orient:horizontal;box-align:stretch;display:flex;flex-direction:row;align-items:stretch;height:30px}
.widget-vbox{margin:5px;-webkit-box-pack:start;-moz-box-pack:start;box-pack:start;justify-content:flex-start;box-sizing:border-box;-moz-box-sizing:border-box;-webkit-box-sizing:border-box;-webkit-box-align:start;-moz-box-align:start;box-align:start;align-items:flex-start;display:-webkit-box;-webkit-box-orient:vertical;-webkit-box-align:stretch;display:-moz-box;-moz-box-orient:vertical;-moz-box-align:stretch;display:box;box-orient:vertical;box-align:stretch;display:flex;flex-direction:column;align-items:stretch}
.widget-vbox-single{margin:5px;-webkit-box-pack:start;-moz-box-pack:start;box-pack:start;justify-content:flex-start;box-sizing:border-box;-moz-box-sizing:border-box;-webkit-box-sizing:border-box;-webkit-box-align:start;-moz-box-align:start;box-align:start;align-items:flex-start;display:-webkit-box;-webkit-box-orient:vertical;-webkit-box-align:stretch;display:-moz-box;-moz-box-orient:vertical;-moz-box-align:stretch;display:box;box-orient:vertical;box-align:stretch;display:flex;flex-direction:column;align-items:stretch;width:30px}
.widget-modal{overflow:hidden;position:absolute !important;top:0;left:0;margin-left:0 !important}
.widget-modal-body{max-height:none !important}
.widget-container{box-sizing:border-box;-moz-box-sizing:border-box;-webkit-box-sizing:border-box;-webkit-box-align:start;-moz-box-align:start;box-align:start;align-items:flex-start}
.widget-radio-box{display:-webkit-box;-webkit-box-orient:vertical;-webkit-box-align:stretch;display:-moz-box;-moz-box-orient:vertical;-moz-box-align:stretch;display:box;box-orient:vertical;box-align:stretch;display:flex;flex-direction:column;align-items:stretch;box-sizing:border-box;-moz-box-sizing:border-box;-webkit-box-sizing:border-box;padding-top:4px}
.docked-widget-modal{overflow:hidden;position:relative !important;top:0 !important;left:0 !important;margin-left:0 !important}
body{background-color:#fff}
body.notebook_app{overflow:hidden}
@media (max-width:767px){body.notebook_app{padding-left:0;padding-right:0}}span#notebook_name{height:1em;line-height:1em;padding:3px;border:none;font-size:146.5%}
div#notebook_panel{margin:0 0 0 0;padding:0;-webkit-box-shadow:0 -1px 10px rgba(0,0,0,0.1);-moz-box-shadow:0 -1px 10px rgba(0,0,0,0.1);box-shadow:0 -1px 10px rgba(0,0,0,0.1)}
div#notebook{font-size:14px;line-height:20px;overflow-y:scroll;overflow-x:auto;width:100%;padding:1em 0 1em 0;margin:0;border-top:1px solid #ababab;outline:none;box-sizing:border-box;-moz-box-sizing:border-box;-webkit-box-sizing:border-box}
div.ui-widget-content{border:1px solid #ababab;outline:none}
pre.dialog{background-color:#f7f7f7;border:1px solid #ddd;border-radius:4px;padding:.4em;padding-left:2em}
p.dialog{padding:.2em}
pre,code,kbd,samp{white-space:pre-wrap}
#fonttest{font-family:monospace}
p{margin-bottom:0}
.end_space{height:200px}
.celltoolbar{border:thin solid #cfcfcf;border-bottom:none;background:#eee;border-radius:3px 3px 0 0;width:100%;-webkit-box-pack:end;height:22px;display:-webkit-box;-webkit-box-orient:horizontal;-webkit-box-align:stretch;display:-moz-box;-moz-box-orient:horizontal;-moz-box-align:stretch;display:box;box-orient:horizontal;box-align:stretch;display:flex;flex-direction:row;align-items:stretch;-webkit-box-direction:reverse;-moz-box-direction:reverse;box-direction:reverse;flex-direction:row-reverse}
.ctb_hideshow{display:none;vertical-align:bottom;padding-right:2px}
.celltoolbar>div{padding-top:0}
.ctb_global_show .ctb_show.ctb_hideshow{display:block}
.ctb_global_show .ctb_show+.input_area,.ctb_global_show .ctb_show+div.text_cell_input{border-top-right-radius:0;border-top-left-radius:0}
.celltoolbar .button_container select{margin:10px;margin-top:1px;margin-bottom:0;padding:0;font-size:87%;width:auto;display:inline-block;height:18px;line-height:18px;vertical-align:top}
.celltoolbar label{display:inline-block;height:15px;line-height:15px;vertical-align:top}
.celltoolbar label span{font-size:85%}
.celltoolbar input[type=checkbox]{margin:0;margin-left:4px;margin-right:4px}
.celltoolbar .ui-button{border:none;vertical-align:top;height:20px;min-width:30px}
.completions{position:absolute;z-index:10;overflow:hidden;border:1px solid #ababab;border-radius:4px;-webkit-box-shadow:0 6px 10px -1px #adadad;-moz-box-shadow:0 6px 10px -1px #adadad;box-shadow:0 6px 10px -1px #adadad}
.completions select{background:#fff;outline:none;border:none;padding:0;margin:0;overflow:auto;font-family:monospace;font-size:110%;color:#000;width:auto}
.completions select option.context{color:#0064cd}
#menubar .navbar-inner{min-height:28px;border-top:1px;border-radius:0 0 4px 4px}
#menubar .navbar{margin-bottom:8px}
.nav-wrapper{border-bottom:1px solid #d4d4d4}
#menubar li.dropdown{line-height:12px}
i.menu-icon{padding-top:4px}
ul#help_menu li a{overflow:hidden;padding-right:2.2em}ul#help_menu li a i{margin-right:-1.2em}
#notification_area{z-index:10}
.indicator_area{color:#777;padding:4px 3px;margin:0;width:11px;z-index:10;text-align:center}
#kernel_indicator{margin-right:-16px}
.edit_mode_icon:before{font-family:FontAwesome;font-weight:normal;font-style:normal;text-decoration:inherit;-webkit-font-smoothing:antialiased;*margin-right:.3em;content:"\f040"}
.command_mode_icon:before{font-family:FontAwesome;font-weight:normal;font-style:normal;text-decoration:inherit;-webkit-font-smoothing:antialiased;*margin-right:.3em;content:' '}
.kernel_idle_icon:before{font-family:FontAwesome;font-weight:normal;font-style:normal;text-decoration:inherit;-webkit-font-smoothing:antialiased;*margin-right:.3em;content:"\f10c"}
.kernel_busy_icon:before{font-family:FontAwesome;font-weight:normal;font-style:normal;text-decoration:inherit;-webkit-font-smoothing:antialiased;*margin-right:.3em;content:"\f111"}
.notification_widget{color:#777;padding:1px 12px;margin:2px 4px;z-index:10;border:1px solid #ccc;border-radius:4px;background:rgba(240,240,240,0.5)}.notification_widget.span{padding-right:2px}
div#pager_splitter{height:8px}
#pager-container{position:relative;padding:15px 0}
div#pager{font-size:14px;line-height:20px;overflow:auto;display:none}div#pager pre{line-height:1.21429em;color:#000;background-color:#f7f7f7;padding:.4em}
.quickhelp{display:-webkit-box;-webkit-box-orient:horizontal;-webkit-box-align:stretch;display:-moz-box;-moz-box-orient:horizontal;-moz-box-align:stretch;display:box;box-orient:horizontal;box-align:stretch;display:flex;flex-direction:row;align-items:stretch}
.shortcut_key{display:inline-block;width:20ex;text-align:right;font-family:monospace}
.shortcut_descr{display:inline-block;-webkit-box-flex:1;-moz-box-flex:1;box-flex:1;flex:1}
span#save_widget{padding:0 5px;margin-top:12px}
span#checkpoint_status,span#autosave_status{font-size:small}
@media (max-width:767px){span#save_widget{font-size:small} span#checkpoint_status,span#autosave_status{font-size:x-small}}@media (max-width:767px){span#checkpoint_status,span#autosave_status{display:none}}@media (min-width:768px) and (max-width:979px){span#checkpoint_status{display:none} span#autosave_status{font-size:x-small}}.toolbar{padding:0 10px;margin-top:-5px}.toolbar select,.toolbar label{width:auto;height:26px;vertical-align:middle;margin-right:2px;margin-bottom:0;display:inline;font-size:92%;margin-left:.3em;margin-right:.3em;padding:0;padding-top:3px}
.toolbar .btn{padding:2px 8px}
.toolbar .btn-group{margin-top:0}
.toolbar-inner{border:none !important;-webkit-box-shadow:none !important;-moz-box-shadow:none !important;box-shadow:none !important}
#maintoolbar{margin-bottom:0}
@-moz-keyframes fadeOut{from{opacity:1} to{opacity:0}}@-webkit-keyframes fadeOut{from{opacity:1} to{opacity:0}}@-moz-keyframes fadeIn{from{opacity:0} to{opacity:1}}@-webkit-keyframes fadeIn{from{opacity:0} to{opacity:1}}.bigtooltip{overflow:auto;height:200px;-webkit-transition-property:height;-webkit-transition-duration:500ms;-moz-transition-property:height;-moz-transition-duration:500ms;transition-property:height;transition-duration:500ms}
.smalltooltip{-webkit-transition-property:height;-webkit-transition-duration:500ms;-moz-transition-property:height;-moz-transition-duration:500ms;transition-property:height;transition-duration:500ms;text-overflow:ellipsis;overflow:hidden;height:80px}
.tooltipbuttons{position:absolute;padding-right:15px;top:0;right:0}
.tooltiptext{padding-right:30px}
.ipython_tooltip{max-width:700px;-webkit-animation:fadeOut 400ms;-moz-animation:fadeOut 400ms;animation:fadeOut 400ms;-webkit-animation:fadeIn 400ms;-moz-animation:fadeIn 400ms;animation:fadeIn 400ms;vertical-align:middle;background-color:#f7f7f7;overflow:visible;border:#ababab 1px solid;outline:none;padding:3px;margin:0;padding-left:7px;font-family:monospace;min-height:50px;-moz-box-shadow:0 6px 10px -1px #adadad;-webkit-box-shadow:0 6px 10px -1px #adadad;box-shadow:0 6px 10px -1px #adadad;border-radius:4px;position:absolute;z-index:2}.ipython_tooltip a{float:right}
.ipython_tooltip .tooltiptext pre{border:0;-webkit-border-radius:0;-moz-border-radius:0;border-radius:0;font-size:100%;background-color:#f7f7f7}
.pretooltiparrow{left:0;margin:0;top:-16px;width:40px;height:16px;overflow:hidden;position:absolute}
.pretooltiparrow:before{background-color:#f7f7f7;border:1px #ababab solid;z-index:11;content:"";position:absolute;left:15px;top:10px;width:25px;height:25px;-webkit-transform:rotate(45deg);-moz-transform:rotate(45deg);-ms-transform:rotate(45deg);-o-transform:rotate(45deg)}

    </style>
<style type="text/css">
    .highlight .hll { background-color: #ffffcc }
.highlight  { background: #f8f8f8; }
.highlight .c { color: #408080; font-style: italic } /* Comment */
.highlight .err { border: 1px solid #FF0000 } /* Error */
.highlight .k { color: #008000; font-weight: bold } /* Keyword */
.highlight .o { color: #666666 } /* Operator */
.highlight .cm { color: #408080; font-style: italic } /* Comment.Multiline */
.highlight .cp { color: #BC7A00 } /* Comment.Preproc */
.highlight .c1 { color: #408080; font-style: italic } /* Comment.Single */
.highlight .cs { color: #408080; font-style: italic } /* Comment.Special */
.highlight .gd { color: #A00000 } /* Generic.Deleted */
.highlight .ge { font-style: italic } /* Generic.Emph */
.highlight .gr { color: #FF0000 } /* Generic.Error */
.highlight .gh { color: #000080; font-weight: bold } /* Generic.Heading */
.highlight .gi { color: #00A000 } /* Generic.Inserted */
.highlight .go { color: #888888 } /* Generic.Output */
.highlight .gp { color: #000080; font-weight: bold } /* Generic.Prompt */
.highlight .gs { font-weight: bold } /* Generic.Strong */
.highlight .gu { color: #800080; font-weight: bold } /* Generic.Subheading */
.highlight .gt { color: #0044DD } /* Generic.Traceback */
.highlight .kc { color: #008000; font-weight: bold } /* Keyword.Constant */
.highlight .kd { color: #008000; font-weight: bold } /* Keyword.Declaration */
.highlight .kn { color: #008000; font-weight: bold } /* Keyword.Namespace */
.highlight .kp { color: #008000 } /* Keyword.Pseudo */
.highlight .kr { color: #008000; font-weight: bold } /* Keyword.Reserved */
.highlight .kt { color: #B00040 } /* Keyword.Type */
.highlight .m { color: #666666 } /* Literal.Number */
.highlight .s { color: #BA2121 } /* Literal.String */
.highlight .na { color: #7D9029 } /* Name.Attribute */
.highlight .nb { color: #008000 } /* Name.Builtin */
.highlight .nc { color: #0000FF; font-weight: bold } /* Name.Class */
.highlight .no { color: #880000 } /* Name.Constant */
.highlight .nd { color: #AA22FF } /* Name.Decorator */
.highlight .ni { color: #999999; font-weight: bold } /* Name.Entity */
.highlight .ne { color: #D2413A; font-weight: bold } /* Name.Exception */
.highlight .nf { color: #0000FF } /* Name.Function */
.highlight .nl { color: #A0A000 } /* Name.Label */
.highlight .nn { color: #0000FF; font-weight: bold } /* Name.Namespace */
.highlight .nt { color: #008000; font-weight: bold } /* Name.Tag */
.highlight .nv { color: #19177C } /* Name.Variable */
.highlight .ow { color: #AA22FF; font-weight: bold } /* Operator.Word */
.highlight .w { color: #bbbbbb } /* Text.Whitespace */
.highlight .mb { color: #666666 } /* Literal.Number.Bin */
.highlight .mf { color: #666666 } /* Literal.Number.Float */
.highlight .mh { color: #666666 } /* Literal.Number.Hex */
.highlight .mi { color: #666666 } /* Literal.Number.Integer */
.highlight .mo { color: #666666 } /* Literal.Number.Oct */
.highlight .sb { color: #BA2121 } /* Literal.String.Backtick */
.highlight .sc { color: #BA2121 } /* Literal.String.Char */
.highlight .sd { color: #BA2121; font-style: italic } /* Literal.String.Doc */
.highlight .s2 { color: #BA2121 } /* Literal.String.Double */
.highlight .se { color: #BB6622; font-weight: bold } /* Literal.String.Escape */
.highlight .sh { color: #BA2121 } /* Literal.String.Heredoc */
.highlight .si { color: #BB6688; font-weight: bold } /* Literal.String.Interpol */
.highlight .sx { color: #008000 } /* Literal.String.Other */
.highlight .sr { color: #BB6688 } /* Literal.String.Regex */
.highlight .s1 { color: #BA2121 } /* Literal.String.Single */
.highlight .ss { color: #19177C } /* Literal.String.Symbol */
.highlight .bp { color: #008000 } /* Name.Builtin.Pseudo */
.highlight .vc { color: #19177C } /* Name.Variable.Class */
.highlight .vg { color: #19177C } /* Name.Variable.Global */
.highlight .vi { color: #19177C } /* Name.Variable.Instance */
.highlight .il { color: #666666 } /* Literal.Number.Integer.Long */
    </style>


<style type="text/css">
/* Overrides of notebook CSS for static HTML export */
body {
  overflow: visible;
  padding: 8px;
}

div#notebook {
  overflow: visible;
  border-top: none;
}

@media print {
  div.cell {
    display: block;
    page-break-inside: avoid;
  } 
  div.output_wrapper { 
    display: block;
    page-break-inside: avoid; 
  }
  div.output { 
    display: block;
    page-break-inside: avoid; 
  }
}
</style>

<!-- Custom stylesheet, it must be in the same directory as the html file -->
<link rel="stylesheet" href="custom.css">

<!-- Loading mathjax macro -->
<!-- Load mathjax -->
    <script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS_HTML"></script>
    <!-- MathJax configuration -->
    <script type="text/x-mathjax-config">
    MathJax.Hub.Config({
        tex2jax: {
            inlineMath: [ ['$','$'], ["\\(","\\)"] ],
            displayMath: [ ['$$','$$'], ["\\[","\\]"] ],
            processEscapes: true,
            processEnvironments: true
        },
        // Center justify equations in code and markdown cells. Elsewhere
        // we use CSS to left justify single line equations in code cells.
        displayAlign: 'center',
        "HTML-CSS": {
            styles: {'.MathJax_Display': {"margin": 0}},
            linebreaks: { automatic: true }
        }
    });
    </script>
    <!-- End of mathjax configuration -->

</head>
<body>
  <div tabindex="-1" id="notebook" class="border-box-sizing">
    <div class="container" id="notebook-container">

<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="this-blog-aims-to-give-a-tutorial-on-how-to-write-a-prediction-model-in-python-in-less-than-a-breakfast-time-">This blog aims to give a tutorial on &quot;how to write a prediction model in Python in less than a breakfast time&quot;.</h3>
<h3 id="most-of-the-top-data-scientists-and-kagglers-build-their-first-effective-model-quickly-and-submit-the-simplest-solution-provides-a-bench-mark-solution-to-optimize-">Most of the top data scientists and Kagglers build their first effective model quickly and submit. The simplest solution provides a bench mark solution to optimize.</h3>
<h3 id="this-tutorial-is-to-show-you-how-to-predict-the-courtry-of-destination-a-user-is-going-to-book-on-airbnb-">This tutorial is to show you how to predict the courtry of destination a user is going to book on Airbnb.</h3>
<h3 id="i-will-divide-the-whole-job-into-small-tasks-with-each-giving-both-the-explaination-and-the-code-demo-without-further-ado-let-s-rock-">I will divide the whole job into small tasks, with each giving both the explaination and the code demo. Without further ado, let&#39;s rock!</h3>
<h3 id="the-tasks-are-">The tasks are :</h3>
<blockquote>
<ul>
<li>Data exploration</li>
<li>Data cleaning</li>
<li>Data modelling </li>
</ul>
</blockquote>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h4 id="step-1-data-exploration">Step 1 : Data Exploration</h4>
<ul>
<li>1.1 Load libraries</li>
<li>1.2 Load data</li>
<li>1.3 View data features/columns and summary</li>
<li>1.4 Get to know your variables : categorical, numerical, string, ID, target</li>
<li>1.5 First visualization of the data</li>
</ul>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">
In&nbsp;[8]:
</div>
<div class="inner_cell">
    <div class="input_area">
<div class="highlight"><pre><span class="c"># 1.1 Load libraries</span>
<span class="kn">import</span> <span class="nn">pandas</span> <span class="kn">as</span> <span class="nn">pd</span>
<span class="kn">from</span> <span class="nn">pandas</span> <span class="kn">import</span> <span class="n">Series</span><span class="p">,</span><span class="n">DataFrame</span>

<span class="c"># numpy, matplotlib, seaborn</span>
<span class="kn">import</span> <span class="nn">numpy</span> <span class="kn">as</span> <span class="nn">np</span>
<span class="kn">import</span> <span class="nn">matplotlib.pyplot</span> <span class="kn">as</span> <span class="nn">plt</span>
<span class="kn">import</span> <span class="nn">seaborn</span> <span class="kn">as</span> <span class="nn">sns</span>
<span class="n">sns</span><span class="o">.</span><span class="n">set_style</span><span class="p">(</span><span class="s">&#39;whitegrid&#39;</span><span class="p">)</span>
<span class="o">%</span><span class="k">matplotlib</span> <span class="n">inline</span>

<span class="c"># machine learning</span>
<span class="kn">from</span> <span class="nn">sklearn.linear_model</span> <span class="kn">import</span> <span class="n">LogisticRegression</span>
<span class="kn">from</span> <span class="nn">sklearn.svm</span> <span class="kn">import</span> <span class="n">SVC</span><span class="p">,</span> <span class="n">LinearSVC</span>
<span class="kn">from</span> <span class="nn">sklearn.ensemble</span> <span class="kn">import</span> <span class="n">RandomForestClassifier</span>
<span class="kn">from</span> <span class="nn">sklearn.neighbors</span> <span class="kn">import</span> <span class="n">KNeighborsClassifier</span>
<span class="kn">from</span> <span class="nn">sklearn.naive_bayes</span> <span class="kn">import</span> <span class="n">GaussianNB</span>
<span class="kn">from</span> <span class="nn">sklearn</span> <span class="kn">import</span> <span class="n">cross_validation</span>
<span class="kn">import</span> <span class="nn">xgboost</span> <span class="kn">as</span> <span class="nn">xgb</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">
In&nbsp;[71]:
</div>
<div class="inner_cell">
    <div class="input_area">
<div class="highlight"><pre><span class="c"># 1.2 Load data</span>
<span class="n">train</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">read_csv</span><span class="p">(</span><span class="s">&#39;Kaggle data comp 1/input/train_users_2.csv&#39;</span><span class="p">)</span>
<span class="n">test</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">read_csv</span><span class="p">(</span><span class="s">&#39;Kaggle data comp 1/input/test_users.csv&#39;</span><span class="p">)</span>
<span class="n">train</span><span class="p">[</span><span class="s">&#39;Type&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="s">&#39;Train&#39;</span> <span class="c">#Create a flag for Train and Test Data set</span>
<span class="n">test</span><span class="p">[</span><span class="s">&#39;Type&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="s">&#39;Test&#39;</span>
<span class="n">fullData</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">concat</span><span class="p">([</span><span class="n">train</span><span class="p">,</span><span class="n">test</span><span class="p">],</span><span class="n">axis</span><span class="o">=</span><span class="mi">0</span><span class="p">)</span> <span class="c"># Combined both Train and Test Data set</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">
In&nbsp;[72]:
</div>
<div class="inner_cell">
    <div class="input_area">
<div class="highlight"><pre><span class="k">print</span> <span class="n">train</span><span class="o">.</span><span class="n">shape</span><span class="p">,</span> <span class="n">test</span><span class="o">.</span><span class="n">shape</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>
(213451, 17) (62096, 16)

</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">
In&nbsp;[73]:
</div>
<div class="inner_cell">
    <div class="input_area">
<div class="highlight"><pre><span class="c"># 1.3 View the column names / summary of the dataset</span>
<span class="k">print</span> <span class="s">&#39;</span><span class="se">\n</span><span class="s">------------------------------------------------------------------</span><span class="se">\n</span><span class="s">&#39;</span>
<span class="k">print</span> <span class="s">&#39;Information of our data:&#39;</span><span class="p">,</span> <span class="n">fullData</span><span class="o">.</span><span class="n">info</span><span class="p">()</span>
<span class="k">print</span> <span class="s">&#39;</span><span class="se">\n</span><span class="s">------------------------------------------------------------------</span><span class="se">\n</span><span class="s">&#39;</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>

------------------------------------------------------------------

Information of our data:&lt;class &apos;pandas.core.frame.DataFrame&apos;&gt;
Int64Index: 275547 entries, 0 to 62095
Data columns (total 17 columns):
Type                       275547 non-null object
affiliate_channel          275547 non-null object
affiliate_provider         275547 non-null object
age                        158681 non-null float64
country_destination        213451 non-null object
date_account_created       275547 non-null object
date_first_booking         88908 non-null object
first_affiliate_tracked    269462 non-null object
first_browser              275547 non-null object
first_device_type          275547 non-null object
gender                     275547 non-null object
id                         275547 non-null object
language                   275547 non-null object
signup_app                 275547 non-null object
signup_flow                275547 non-null int64
signup_method              275547 non-null object
timestamp_first_active     275547 non-null int64
dtypes: float64(1), int64(2), object(14)
memory usage: 37.8+ MB
 None

------------------------------------------------------------------


</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">
In&nbsp;[74]:
</div>
<div class="inner_cell">
    <div class="input_area">
<div class="highlight"><pre><span class="c"># 1.4 Get to know your variables</span>
<span class="c"># Check the data types of all variables (or columns if you want)</span>
<span class="n">fullData</span><span class="o">.</span><span class="n">dtypes</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">
    Out[74]:</div>


<div class="output_text output_subarea output_pyout">
<pre>
Type                        object
affiliate_channel           object
affiliate_provider          object
age                        float64
country_destination         object
date_account_created        object
date_first_booking          object
first_affiliate_tracked     object
first_browser               object
first_device_type           object
gender                      object
id                          object
language                    object
signup_app                  object
signup_flow                  int64
signup_method               object
timestamp_first_active       int64
dtype: object
</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">
In&nbsp;[75]:
</div>
<div class="inner_cell">
    <div class="input_area">
<div class="highlight"><pre><span class="c"># 1.5 First Visualization of the data</span>
<span class="c"># Plot the distribution of the labels</span>
<span class="n">fig</span><span class="p">,</span> <span class="p">(</span><span class="n">axis1</span><span class="p">,</span> <span class="n">axis2</span><span class="p">)</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">subplots</span><span class="p">(</span><span class="mi">1</span><span class="p">,</span><span class="mi">2</span><span class="p">,</span><span class="n">figsize</span><span class="o">=</span><span class="p">(</span><span class="mi">15</span><span class="p">,</span><span class="mi">4</span><span class="p">))</span>
<span class="n">sns</span><span class="o">.</span><span class="n">countplot</span><span class="p">(</span><span class="n">x</span><span class="o">=</span><span class="s">&#39;country_destination&#39;</span><span class="p">,</span> <span class="n">data</span><span class="o">=</span><span class="n">fullData</span><span class="p">,</span> <span class="n">palette</span><span class="o">=</span><span class="s">&quot;husl&quot;</span><span class="p">,</span> <span class="n">ax</span> <span class="o">=</span> <span class="n">axis1</span><span class="p">)</span>
<span class="n">sns</span><span class="o">.</span><span class="n">countplot</span><span class="p">(</span><span class="n">x</span><span class="o">=</span><span class="s">&#39;country_destination&#39;</span><span class="p">,</span> <span class="n">data</span><span class="o">=</span><span class="n">train</span><span class="p">,</span> <span class="n">palette</span><span class="o">=</span><span class="s">&quot;husl&quot;</span><span class="p">,</span> <span class="n">ax</span> <span class="o">=</span> <span class="n">axis2</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">
    Out[75]:</div>


<div class="output_text output_subarea output_pyout">
<pre>
&lt;matplotlib.axes._subplots.AxesSubplot at 0x11ad87dd0&gt;
</pre>
</div>

</div>

<div class="output_area"><div class="prompt"></div>


<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
TQAAAABJRU5ErkJggg==
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h4 id="step-2-data-cleaning">Step 2 : Data Cleaning</h4>
<ul>
<li>1.1 Drop out unnecessary variables</li>
<li>1.2 Find out all categorical variables and process them one by one (loop)<ul>
<li>1.2.1 Visualze the distribution of the variable values</li>
<li>1.2.2 (optional) Date-type variable have to be split </li>
<li>1.2.3 (optional) Fill NaN values with median values</li>
<li>1.2.4 (optional) Make sure the data type of newly created variables is justified, e.g., &#39;Year&#39;, is an &#39;int&#39; instead of &#39;float&#39; type</li>
<li>1.2.5 (optional) Binary process (&#39;one value&#39; versus &#39;non- one value&#39;)</li>
<li>1.2.6 Look for new insights due to the use of new variables</li>
</ul>
</li>
<li>1.3 Convert any remaining non-numerical variables to numerical</li>
<li>1.4 Particular process of some important numerical variables, e.g., age</li>
</ul>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">
In&nbsp;[76]:
</div>
<div class="inner_cell">
    <div class="input_area">
<div class="highlight"><pre><span class="c"># 1.1 Drop unecessary columns, these columns won&#39;t be useful in analysis and prediction</span>
<span class="n">fullData</span> <span class="o">=</span> <span class="n">fullData</span><span class="o">.</span><span class="n">drop</span><span class="p">([</span><span class="s">&#39;date_account_created&#39;</span><span class="p">,</span> <span class="s">&#39;timestamp_first_active&#39;</span><span class="p">],</span> <span class="n">axis</span> <span class="o">=</span> <span class="mi">1</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">
In&nbsp;[77]:
</div>
<div class="inner_cell">
    <div class="input_area">
<div class="highlight"><pre><span class="c"># 1.2 Find out all categorical variables (choose those numerical variables, just change &#39;o&#39; to &#39;int64&#39;)</span>
<span class="n">colType</span> <span class="o">=</span> <span class="n">fullData</span><span class="o">.</span><span class="n">columns</span><span class="o">.</span><span class="n">to_series</span><span class="p">()</span><span class="o">.</span><span class="n">groupby</span><span class="p">(</span><span class="n">fullData</span><span class="o">.</span><span class="n">dtypes</span> <span class="o">==</span> <span class="s">&#39;O&#39;</span><span class="p">)</span><span class="o">.</span><span class="n">groups</span> 
<span class="n">colType</span><span class="p">[</span><span class="bp">True</span><span class="p">]</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">
    Out[77]:</div>


<div class="output_text output_subarea output_pyout">
<pre>
[&apos;Type&apos;,
 &apos;affiliate_channel&apos;,
 &apos;affiliate_provider&apos;,
 &apos;country_destination&apos;,
 &apos;date_first_booking&apos;,
 &apos;first_affiliate_tracked&apos;,
 &apos;first_browser&apos;,
 &apos;first_device_type&apos;,
 &apos;gender&apos;,
 &apos;id&apos;,
 &apos;language&apos;,
 &apos;signup_app&apos;,
 &apos;signup_method&apos;]
</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">
In&nbsp;[78]:
</div>
<div class="inner_cell">
    <div class="input_area">
<div class="highlight"><pre><span class="k">def</span> <span class="nf">FillNaNRandom</span><span class="p">(</span><span class="n">df</span><span class="p">,</span><span class="n">columnName</span><span class="p">):</span>
    <span class="n">count_col</span> <span class="o">=</span> <span class="nb">len</span><span class="p">(</span><span class="n">np</span><span class="o">.</span><span class="n">unique</span><span class="p">(</span><span class="n">df</span><span class="p">[</span><span class="n">columnName</span><span class="p">]</span><span class="o">.</span><span class="n">value_counts</span><span class="p">()))</span>
    <span class="n">count_nan</span> <span class="o">=</span> <span class="n">df</span><span class="p">[</span><span class="n">columnName</span><span class="p">]</span><span class="o">.</span><span class="n">isnull</span><span class="p">()</span><span class="o">.</span><span class="n">sum</span><span class="p">()</span>
    <span class="n">range_col</span> <span class="o">=</span> <span class="n">df</span><span class="p">[</span><span class="n">columnName</span><span class="p">]</span><span class="o">.</span><span class="n">value_counts</span><span class="p">()</span><span class="o">.</span><span class="n">index</span>
    <span class="k">print</span> <span class="s">&quot;There are </span><span class="si">%s</span><span class="s"> different values in the list of :</span><span class="se">\n</span><span class="si">%s</span><span class="s">&quot;</span> <span class="o">%</span> <span class="p">(</span><span class="nb">len</span><span class="p">(</span><span class="n">range_col</span><span class="p">),</span> <span class="n">range_col</span><span class="p">)</span>

    <span class="k">if</span> <span class="n">count_nan</span> <span class="o">&gt;</span> <span class="mi">0</span><span class="p">:</span>
        <span class="n">rand</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">random</span><span class="o">.</span><span class="n">randint</span><span class="p">(</span><span class="mi">0</span><span class="p">,</span> <span class="n">count_col</span><span class="p">,</span> <span class="n">size</span> <span class="o">=</span> <span class="n">count_nan</span><span class="p">)</span>
        
        <span class="c"># Create a random selection of the 7 possible categorical values for all </span>
        <span class="c"># &#39;count_ran_department&#39; (i.e., 6085) &#39;NaN&#39; records</span>
        <span class="n">RandforNaN</span> <span class="o">=</span> <span class="n">range_col</span><span class="p">[</span><span class="n">rand</span><span class="p">]</span>

        <span class="c"># Find indexes for the NaN values</span>
        <span class="n">NaNIndex</span> <span class="o">=</span> <span class="n">df</span><span class="p">[</span><span class="n">columnName</span><span class="p">]</span> <span class="o">!=</span> <span class="n">df</span><span class="p">[</span><span class="n">columnName</span><span class="p">]</span>
        <span class="n">df</span><span class="p">[</span><span class="n">columnName</span><span class="p">][</span><span class="n">NaNIndex</span><span class="p">]</span> <span class="o">=</span> <span class="n">RandforNaN</span>
        <span class="k">print</span> <span class="s">&#39;There are : </span><span class="si">%s</span><span class="s"> NaN values in this variable!&#39;</span> <span class="o">%</span> <span class="n">count_nan</span>
    <span class="k">else</span><span class="p">:</span>
        <span class="k">print</span> <span class="s">&#39;There is no NaN values for this variable!&#39;</span>
    <span class="k">return</span> <span class="n">df</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">
In&nbsp;[79]:
</div>
<div class="inner_cell">
    <div class="input_area">
<div class="highlight"><pre><span class="c"># There are 12 original categorical variables in total</span>
<span class="c"># 1. &#39;affiliate_channel&#39; variable</span>
<span class="c"># (1) Visualization</span>
<span class="n">fig</span><span class="p">,</span> <span class="n">axis1</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">subplots</span><span class="p">(</span><span class="mi">1</span><span class="p">,</span><span class="mi">1</span><span class="p">,</span><span class="n">sharex</span><span class="o">=</span><span class="bp">True</span><span class="p">,</span><span class="n">figsize</span><span class="o">=</span><span class="p">(</span><span class="mi">15</span><span class="p">,</span><span class="mi">4</span><span class="p">))</span>
<span class="n">sns</span><span class="o">.</span><span class="n">countplot</span><span class="p">(</span><span class="n">x</span><span class="o">=</span><span class="s">&#39;affiliate_channel&#39;</span><span class="p">,</span> <span class="n">data</span><span class="o">=</span><span class="n">fullData</span><span class="p">,</span> <span class="n">palette</span><span class="o">=</span><span class="s">&quot;husl&quot;</span><span class="p">,</span> <span class="n">ax</span><span class="o">=</span><span class="n">axis1</span><span class="p">)</span>

<span class="c"># (2) Fill NaN values randomly</span>
<span class="n">fullData</span> <span class="o">=</span> <span class="n">FillNaNRandom</span><span class="p">(</span><span class="n">fullData</span><span class="p">,</span> <span class="s">&#39;affiliate_channel&#39;</span><span class="p">)</span>

<span class="c"># (3) Binary process</span>
<span class="n">fullData</span><span class="p">[</span><span class="s">&quot;affiliate_channel&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="p">(</span><span class="n">fullData</span><span class="p">[</span><span class="s">&quot;affiliate_channel&quot;</span><span class="p">]</span> <span class="o">==</span> <span class="s">&#39;direct&#39;</span><span class="p">)</span><span class="o">.</span><span class="n">astype</span><span class="p">(</span><span class="nb">int</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>
There are 8 different values in the list of :
Index([u&apos;direct&apos;, u&apos;sem-brand&apos;, u&apos;sem-non-brand&apos;, u&apos;seo&apos;, u&apos;other&apos;, u&apos;api&apos;, u&apos;content&apos;, u&apos;remarketing&apos;], dtype=&apos;object&apos;)
There is no NaN values for this variable!

</pre>
</div>
</div>

<div class="output_area"><div class="prompt"></div>


<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
db34E0cNAAAAAElFTkSuQmCC
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">
In&nbsp;[80]:
</div>
<div class="inner_cell">
    <div class="input_area">
<div class="highlight"><pre><span class="c"># There are 12 categorical variables in total</span>
<span class="c"># 2. &#39;affiliate_provider&#39; variable</span>
<span class="c"># (1) Visualization</span>
<span class="n">fig</span><span class="p">,</span> <span class="n">axis1</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">subplots</span><span class="p">(</span><span class="mi">1</span><span class="p">,</span><span class="mi">1</span><span class="p">,</span><span class="n">sharex</span><span class="o">=</span><span class="bp">True</span><span class="p">,</span><span class="n">figsize</span><span class="o">=</span><span class="p">(</span><span class="mi">15</span><span class="p">,</span><span class="mi">4</span><span class="p">))</span>
<span class="n">sns</span><span class="o">.</span><span class="n">countplot</span><span class="p">(</span><span class="n">x</span><span class="o">=</span><span class="s">&#39;affiliate_provider&#39;</span><span class="p">,</span> <span class="n">data</span><span class="o">=</span><span class="n">fullData</span><span class="p">,</span> <span class="n">palette</span><span class="o">=</span><span class="s">&quot;husl&quot;</span><span class="p">,</span> <span class="n">ax</span><span class="o">=</span><span class="n">axis1</span><span class="p">)</span>

<span class="c"># (2) Fill NaN values randomly</span>
<span class="n">fullData</span> <span class="o">=</span> <span class="n">FillNaNRandom</span><span class="p">(</span><span class="n">fullData</span><span class="p">,</span> <span class="s">&#39;affiliate_provider&#39;</span><span class="p">)</span>

<span class="c"># (3) Binary process</span>
<span class="n">fullData</span><span class="p">[</span><span class="s">&quot;affiliate_provider&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="p">(</span><span class="n">fullData</span><span class="p">[</span><span class="s">&quot;affiliate_provider&quot;</span><span class="p">]</span> <span class="o">==</span> <span class="s">&#39;direct&#39;</span><span class="p">)</span><span class="o">.</span><span class="n">astype</span><span class="p">(</span><span class="nb">int</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>
There are 18 different values in the list of :
Index([u&apos;direct&apos;, u&apos;google&apos;, u&apos;other&apos;, u&apos;facebook&apos;, u&apos;bing&apos;, u&apos;craigslist&apos;, u&apos;padmapper&apos;, u&apos;vast&apos;, u&apos;yahoo&apos;, u&apos;facebook-open-graph&apos;, u&apos;gsp&apos;, u&apos;meetup&apos;, u&apos;email-marketing&apos;, u&apos;naver&apos;, u&apos;baidu&apos;, u&apos;yandex&apos;, u&apos;wayn&apos;, u&apos;daum&apos;], dtype=&apos;object&apos;)
There is no NaN values for this variable!

</pre>
</div>
</div>

<div class="output_area"><div class="prompt"></div>


<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">
In&nbsp;[81]:
</div>
<div class="inner_cell">
    <div class="input_area">
<div class="highlight"><pre><span class="c"># There are 12 categorical variables in total</span>
<span class="c"># 3. &#39;country_destination&#39; variable</span>
<span class="c"># (1) Visualization</span>
<span class="n">fig</span><span class="p">,</span> <span class="n">axis1</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">subplots</span><span class="p">(</span><span class="mi">1</span><span class="p">,</span><span class="mi">1</span><span class="p">,</span><span class="n">sharex</span><span class="o">=</span><span class="bp">True</span><span class="p">,</span><span class="n">figsize</span><span class="o">=</span><span class="p">(</span><span class="mi">15</span><span class="p">,</span><span class="mi">4</span><span class="p">))</span>
<span class="n">sns</span><span class="o">.</span><span class="n">countplot</span><span class="p">(</span><span class="n">x</span><span class="o">=</span><span class="s">&#39;country_destination&#39;</span><span class="p">,</span> <span class="n">data</span><span class="o">=</span><span class="n">fullData</span><span class="p">,</span> <span class="n">palette</span><span class="o">=</span><span class="s">&quot;husl&quot;</span><span class="p">,</span> <span class="n">ax</span><span class="o">=</span><span class="n">axis1</span><span class="p">)</span>

<span class="c"># (2) Binary process</span>
<span class="n">fullData</span><span class="p">[</span><span class="s">&quot;booked&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="p">(</span><span class="n">fullData</span><span class="p">[</span><span class="s">&#39;country_destination&#39;</span><span class="p">]</span><span class="o">!=</span> <span class="s">&#39;NDF&#39;</span><span class="p">)</span><span class="o">.</span><span class="n">astype</span><span class="p">(</span><span class="nb">int</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>


<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">
In&nbsp;[30]:
</div>
<div class="inner_cell">
    <div class="input_area">
<div class="highlight"><pre><span class="c"># There are 12 categorical variables in total</span>
<span class="c"># 4. &#39;date_first_booking&#39; variable</span>
<span class="c"># (1) Visualization</span>
<span class="n">fig</span><span class="p">,</span> <span class="n">axis1</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">subplots</span><span class="p">(</span><span class="mi">1</span><span class="p">,</span><span class="mi">1</span><span class="p">,</span><span class="n">sharex</span><span class="o">=</span><span class="bp">True</span><span class="p">,</span><span class="n">figsize</span><span class="o">=</span><span class="p">(</span><span class="mi">15</span><span class="p">,</span><span class="mi">4</span><span class="p">))</span>
<span class="n">sns</span><span class="o">.</span><span class="n">countplot</span><span class="p">(</span><span class="n">x</span><span class="o">=</span><span class="s">&#39;date_first_booking&#39;</span><span class="p">,</span> <span class="n">data</span><span class="o">=</span><span class="n">fullData</span><span class="p">,</span> <span class="n">palette</span><span class="o">=</span><span class="s">&quot;husl&quot;</span><span class="p">,</span> <span class="n">ax</span><span class="o">=</span><span class="n">axis1</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">
    Out[30]:</div>


<div class="output_text output_subarea output_pyout">
<pre>
&lt;matplotlib.axes._subplots.AxesSubplot at 0x114d9c2d0&gt;
</pre>
</div>

</div>

<div class="output_area"><div class="prompt"></div>


<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">
In&nbsp;[82]:
</div>
<div class="inner_cell">
    <div class="input_area">
<div class="highlight"><pre><span class="c"># Type : Date</span>
<span class="c"># (2) Split a &#39;date&#39; variable into 2 variables, i.e., &#39;year&#39; and &#39;month&#39;</span>
<span class="k">def</span> <span class="nf">get_year</span><span class="p">(</span><span class="n">date</span><span class="p">):</span>
    <span class="k">if</span> <span class="n">date</span> <span class="o">==</span> <span class="n">date</span><span class="p">:</span> <span class="c"># if the value is nan, nan is not equal to another nan</span>
        <span class="k">return</span> <span class="nb">int</span><span class="p">(</span><span class="nb">str</span><span class="p">(</span><span class="n">date</span><span class="p">)[:</span><span class="mi">4</span><span class="p">])</span>
    <span class="k">return</span> <span class="n">date</span>

<span class="k">def</span> <span class="nf">get_month</span><span class="p">(</span><span class="n">date</span><span class="p">):</span>
    <span class="k">if</span> <span class="n">date</span> <span class="o">==</span> <span class="n">date</span><span class="p">:</span> <span class="c"># if the value is nan, nan is not equal to another nan</span>
        <span class="k">return</span> <span class="nb">int</span><span class="p">(</span><span class="nb">float</span><span class="p">(</span><span class="nb">str</span><span class="p">(</span><span class="n">date</span><span class="p">)[</span><span class="mi">5</span><span class="p">:</span><span class="mi">7</span><span class="p">]))</span>
    <span class="k">return</span> <span class="n">date</span>

<span class="c"># Create Year and Month columns</span>
<span class="n">fullData</span><span class="p">[</span><span class="s">&#39;Year&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">fullData</span><span class="p">[</span><span class="s">&#39;date_first_booking&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">apply</span><span class="p">(</span><span class="n">get_year</span><span class="p">)</span>
<span class="n">fullData</span><span class="p">[</span><span class="s">&#39;Month&#39;</span><span class="p">]</span><span class="o">=</span> <span class="n">fullData</span><span class="p">[</span><span class="s">&#39;date_first_booking&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">apply</span><span class="p">(</span><span class="n">get_month</span><span class="p">)</span>

<span class="c"># (3) Fill NaN of the new created variables &#39;Year&#39; and &#39;Month&#39;</span>
<span class="n">fullData</span><span class="p">[</span><span class="s">&#39;Year&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="n">fullData</span><span class="p">[</span><span class="s">&#39;Year&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">median</span><span class="p">(),</span> <span class="n">inplace</span><span class="o">=</span><span class="bp">True</span><span class="p">)</span>
<span class="n">fullData</span><span class="p">[</span><span class="s">&#39;Month&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="n">fullData</span><span class="p">[</span><span class="s">&#39;Month&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">median</span><span class="p">(),</span> <span class="n">inplace</span><span class="o">=</span><span class="bp">True</span><span class="p">)</span>

<span class="nb">type</span><span class="p">(</span><span class="n">fullData</span><span class="p">[</span><span class="s">&#39;Year&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">iloc</span><span class="p">[</span><span class="mi">2</span><span class="p">])</span> <span class="c"># numpy.float64</span>

<span class="c"># (4) Be careful of the data type of &#39;Year&#39; and &#39;Month&#39; variables. </span>
<span class="c"># They are float instead of int. Convert &#39;float&#39; to &#39;int&#39;</span>
<span class="n">fullData</span><span class="p">[[</span><span class="s">&#39;Year&#39;</span><span class="p">,</span> <span class="s">&#39;Month&#39;</span><span class="p">]]</span> <span class="o">=</span> <span class="n">fullData</span><span class="p">[[</span><span class="s">&#39;Year&#39;</span><span class="p">,</span> <span class="s">&#39;Month&#39;</span><span class="p">]]</span><span class="o">.</span><span class="n">astype</span><span class="p">(</span><span class="nb">int</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">
In&nbsp;[83]:
</div>
<div class="inner_cell">
    <div class="input_area">
<div class="highlight"><pre><span class="c"># (5) Look for new insights</span>
<span class="c"># NOTICE : in year 2014 and 2015, there wasn&#39;t &quot;no-booking&quot;</span>
<span class="n">fig</span><span class="p">,</span> <span class="n">axis1</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">subplots</span><span class="p">(</span><span class="mi">1</span><span class="p">,</span><span class="mi">1</span><span class="p">,</span><span class="n">figsize</span><span class="o">=</span><span class="p">(</span><span class="mi">15</span><span class="p">,</span><span class="mi">4</span><span class="p">))</span>
<span class="n">sns</span><span class="o">.</span><span class="n">countplot</span><span class="p">(</span><span class="n">x</span><span class="o">=</span><span class="s">&quot;Year&quot;</span><span class="p">,</span><span class="n">hue</span><span class="o">=</span><span class="s">&quot;country_destination&quot;</span><span class="p">,</span> <span class="n">data</span><span class="o">=</span><span class="n">fullData</span><span class="p">,</span> 
              <span class="n">palette</span><span class="o">=</span><span class="s">&quot;husl&quot;</span><span class="p">,</span> <span class="n">order</span><span class="o">=</span><span class="p">[</span><span class="mi">2010</span><span class="p">,</span><span class="mi">2011</span><span class="p">,</span><span class="mi">2012</span><span class="p">,</span><span class="mi">2013</span><span class="p">,</span><span class="mi">2014</span><span class="p">,</span><span class="mi">2015</span><span class="p">],</span> <span class="n">ax</span><span class="o">=</span><span class="n">axis1</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">
    Out[83]:</div>


<div class="output_text output_subarea output_pyout">
<pre>
&lt;matplotlib.axes._subplots.AxesSubplot at 0x1189d3e50&gt;
</pre>
</div>

</div>

<div class="output_area"><div class="prompt"></div>


<div class="output_png output_subarea ">
<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAA4kAAAERCAYAAADWhOJSAAAABHNCSVQICAgIfAhkiAAAAAlwSFlz
AAALEgAACxIB0t1+/AAAIABJREFUeJzt3XmYVNW5sP27GIpBG0EGQY0WiCwTiUdtX0RRHGOMJ0Yx
ImokGuOUqJEMauCAKFGMiiThi9EEHBBwCBpPnNGjJioGYvo9MRJflppQCEYFlKEZm6G/P6qoNNrd
NHRVdVPcv+viovZTq1Y9WxfV9fRae+1EdXU1kiRJkiQBtGjqBCRJkiRJzYdFoiRJkiQpxyJRkiRJ
kpRjkShJkiRJyrFIlCRJkiTlWCRKkiRJknJaFbLzEMLhwE9jjMfViJ0LXBFjPDJ7fDFwCbABuDHG
+FQIoR0wFegKVALnxxiXhBD6Az/Ptn0uxjgm28do4JRsfFiM8fVCnpckSZIklaqCzSSGEK4BJgJt
asQOAS6scdwduBI4EvgycHMIIQl8B3gjxjgQuB8YmX3JXcA5McajgMNDCAeHEA4FBsYYDwfOBu4o
1DlJkiRJUqkr5HLTd4EzgARACKEzcBMwbHMM6AfMjDGujzGuyL7mIGAA8Gy2zbPAiSGEMiAZY5yX
jc8ATsy2fQ4gxrgAaJV9L0mSJEnSNipYkRhj/B2Z5Z+EEFoAdwM/AFbWaNYBWF7juBLYLRtfUU/s
0/Ha+pAkSZIkbaOCXpNYQznQG7gTaAt8IYQwHngJKKvRrgxYRqYYLKsnBpnicBlQVUcfkiRJkqRt
VJQiMbuRTF+AEMK+wEMxxh9kr0m8KYTQhkzx+HlgDjCTzEY0rwNfAV6OMVaGEKpCCL2AecBJwPXA
RuDWEMI44HNAixjjJ/XlU1FRUV2A05QkSZKkHUZ5eXmitngxisRPF2SJzbEY44chhAnAK2SWvo6I
Ma4LIdwJTA4hvAKsA87NvvYyYBrQEpixeRfTbLs/Zfv4bkOSKi8vb9RJSZIkSdKOqqKios7nEtXV
O9+kWkVFRbVFoiRJkqSdVUVFRZ0ziYXc3VSSJEmStIOxSJQkSZIk5VgkSpIkSZJyLBIlSZIkSTkW
iZIkSZKkHItESZIkSVKORaIkSZKkkjVjxgwqKyvz0tfpp5++Te2nT58OwCuvvMKTTz65Ta/985//
zHvvvceSJUu47bbbtum1jWWRKEmSJKlkTZ06lXXr1jXJe99zzz0AHH300Xz1q1/dptf+7ne/Y+nS
pXTp0oWrr766EOnVqVVR302SJEmS6rFy5Uquvvpqli5dSuvWrbn66qsZO3YsrVq1okePHowdO5Yn
nniCJUuWcMkllzB79myefvppLrnkEq655hp233130uk03/rWt+jevTtz585lxIgRXHTRRdx22220
bt2agQMH0qJFCy655BLS6TTjx49nwoQJteZzyy23UFFRQSqVYuPGjUBmZvCOO+4gkUhw/PHHc/HF
F3PfffcxY8YMNmzYwMUXX8zq1av54IMPuO666zjkkENYvHgxBx98MHfffTeJRIIFCxYwfPhwjjrq
KCZOnMhrr73GihUrOO644zjppJN49dVXefvtt7ntttu4+eabmTRpEnfeeScvvfQSAEOHDuXUU09l
6NChHHjggbz55pt06NCBX/3qVyQSiUb9P3AmUZIkSVKz8eCDD3LYYYfx0EMPcemllzJmzBjGjx/P
1KlT2WuvvXj00Ue3KIJqPv7ggw/42c9+xt13383999/PkUceyQEHHMDNN99MdXU1bdu25YEHHuDc
c8/lf/7nfwB44oknGDRoUK25vPnmm6TTaX77299yxRVXsHbtWqqrq7nlllu4++67eeCBB6ioqOAf
//gHzzzzDOPGjeOee+5h06ZNnH766fTo0YMxY8Zs0eeKFSu46667uPHGG3nwwQfZtGkTiUSCe++9
lwcffJDHH3+cPn36cPTRR3P99dfTtm1bAObOnUtFRQW//e1vmTJlCr/5zW9yy2gHDhzItGnTqKqq
IsbY6P8HFomSJEmSmo2FCxdy0EEHAXDUUUexZs0a9txzTwAOPfRQ/vnPf27RftOmTbnHPXv2pFWr
VnTr1u0zS0wTiQQ9e/YEoEOHDnTv3p1//OMfvPbaawwcOLDWXObPn8+BBx4IwD777MPuu+/O0qVL
WbRoEZdddhnf/OY3+eijj1iwYAE33HADP//5z7nyyivrXd66//77A9C1a1fWrVtHixYtWL16NT/6
0Y8YO3YsGzZsqPV18+bN4+CDDwagTZs29O7dm/fffx+APn36ANR63tvDIlGSJElSs9GzZ0/+/ve/
A5lNZ5YtW8YHH3wAQEVFBfvssw9t2rRh0aJFQGaGbbPallkmEgk2btxIdXX1Fs+ffvrpTJgwgb59
+9KyZcs6c3nzzTcBeP/991m6dCmdOnVi77335u6772bKlCmceeaZ7L///jz66KPcdNNNTJw4kTvv
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
RU5ErkJggg==
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">
In&nbsp;[84]:
</div>
<div class="inner_cell">
    <div class="input_area">
<div class="highlight"><pre><span class="c"># There are 12 original categorical variables in total</span>
<span class="c"># 5. &#39;first_affiliate_tracked&#39; variable</span>
<span class="c"># (1) Visualization</span>
<span class="n">fig</span><span class="p">,</span> <span class="n">axis1</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">subplots</span><span class="p">(</span><span class="mi">1</span><span class="p">,</span><span class="mi">1</span><span class="p">,</span><span class="n">sharex</span><span class="o">=</span><span class="bp">True</span><span class="p">,</span><span class="n">figsize</span><span class="o">=</span><span class="p">(</span><span class="mi">15</span><span class="p">,</span><span class="mi">4</span><span class="p">))</span>
<span class="n">sns</span><span class="o">.</span><span class="n">countplot</span><span class="p">(</span><span class="n">x</span><span class="o">=</span><span class="s">&#39;first_affiliate_tracked&#39;</span><span class="p">,</span> <span class="n">data</span><span class="o">=</span><span class="n">fullData</span><span class="p">,</span> <span class="n">palette</span><span class="o">=</span><span class="s">&quot;husl&quot;</span><span class="p">,</span> <span class="n">ax</span><span class="o">=</span><span class="n">axis1</span><span class="p">)</span>

<span class="c"># (2) Fill NaN values randomly</span>
<span class="n">fullData</span> <span class="o">=</span> <span class="n">FillNaNRandom</span><span class="p">(</span><span class="n">fullData</span><span class="p">,</span> <span class="s">&#39;first_affiliate_tracked&#39;</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>
There are 7 different values in the list of :
Index([u&apos;untracked&apos;, u&apos;linked&apos;, u&apos;omg&apos;, u&apos;tracked-other&apos;, u&apos;product&apos;, u&apos;marketing&apos;, u&apos;local ops&apos;], dtype=&apos;object&apos;)
There are : 6085 NaN values in this variable!

</pre>
</div>
</div>

<div class="output_area"><div class="prompt"></div>


<div class="output_png output_subarea ">
<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAA4kAAAERCAYAAADWhOJSAAAABHNCSVQICAgIfAhkiAAAAAlwSFlz
AAALEgAACxIB0t1+/AAAIABJREFUeJzt3XucXVV58PHfcJkQcAIKBLzwGkHziEZERgkBDKARBGtB
3lYF/Yg3kIuorfcIchHEe5Fqg4KW8ILaYqmXokkUgYS8COlUqFPwQWxmXmqrIUDIqJBAMu8fe83O
MU4mM2HOnGTm9/185jPnrLP22s8+++x9znPW2uu09ff3I0mSJEkSwHatDkCSJEmStPUwSZQkSZIk
1UwSJUmSJEk1k0RJkiRJUs0kUZIkSZJUM0mUJEmSJNV2aGbjETET+FRmHhURU4ErgN2ANuAtmdkT
EacCpwFPABdl5g0RMRm4BtgT6ANOycyVEXEIcGmpuygzLyzrOQ84rpS/LzOXNXO7JEmSJGm8alpP
YkR8iCopnFSKPgP8n8w8Avg4MCMi9gbOBg4FjgEuiYh24AzgrsycDVwNnFPauBw4KTMPB2ZGxIER
cRAwOzNnAm8EvtysbZIkSZKk8a6Zw03vA06k6jWEKhHcJyJ+BLwJ+AlwMLA0Mx/PzNVlmQOAw4AF
ZbkFwJyI6ADaM3N5KV8IzCl1FwFk5v3ADhGxexO3S5IkSZLGraYliZl5PdXwzwHTgIcy81XA/wM+
DHQAjzTU6QN2BaYAq4co27h8sDYkSZIkSSM0lhPXPAh8r9z+PvBSqqSvo6FOB7Bqo/LByqBKDgcr
H6gvSZIkSRqhpk5cs5FbgddQTUhzBNAN3AFcHBGTgJ2A/Uv5UqqJaJYBxwKLM7MvItZGxL7AcuBo
4HxgHfCZiPgcsA+wXWY+NFQgXV1d/aO/eZIkSZK07ejs7GwbrHwsksSBhOz9wJURcQZVT9/JmflI
RFwGLKHq1ZybmWsiYh4wPyKWAGuAk0sbpwPXAtsDCwdmMS31bittnDmcoDo7O0dl4yRJkiRpW9PV
1bXJx9r6+ydep1pXV1e/SaIkSZKkiaqrq2uTPYljeU2iJEmSJGkrZ5IoSZIkSaqZJEqSJEmSaiaJ
kiRJkqSaSaIkSZIkqWaSKEmSJEmqmSRKkiRJkmomiZIkSZKkmkmiJEmSJKlmkihJkiRJqpkkSpIk
SZJqJomSJEmSpJpJoiRJkiSpZpIoSZIkSaqZJEqSJEmSaiaJkiRJkqSaSaIkSZIkqWaSKEmSJEmq
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
fuyXJEmSpC3QsiQxM49quHvkII9fCVy5UdmjwOsHqXs7MGuUQ5QkSZKkCacVs5tKkiRJkrZSJomS
JEmSpJpJoiRJkiSpZpIoSZIkSaqZJEqSJEmSaiaJkiRJkqSaSaIkSZIkqWaSKEmSJEmqmSRKkiRJ
kmomiZIkSZKkmkmiJEmSJKlmkihJkiRJqpkkSpIkSZJqJomSJEmSpJpJoiRJkiSpZpIoSZIkSaqZ
JEqSJEmSaiaJkiRJkqSaSaIkSZIkqWaSKEmSJEmq7TCWK4uIHYGvA88GJgEXAfcAVwHrgW7grMzs
j4hTgdOAJ4CLMvOGiJgMXAPsCfQBp2Tmyog4BLi01F2UmReO5XZJkiRJ0ngx1j2JbwIeyMzZwKuB
LwOfB+aWsjbg+IjYGzgbOBQ4BrgkItqBM4C7St2rgXNKu5cDJ2Xm4cDMiDhwLDdKkiRJksaLsU4S
rwM+3rDux4GDMnNxKfshMAd4GbA0Mx/PzNXAfcABwGHAglJ3ATAnIjqA9sxcXsoXljYkSZIkSSM0
pkliZv4+M39XErvrqHoCG2PoA3YFpgCPbKJ89RBljeWSJEmSpBEa02sSASJiH+B64MuZ+c2I+EzD
w1OAVVRJX0dDeccg5YOVNbYxpK6urmHF29vby9Rh1VSzdHd309fX15S2e3t7m9Kuhsd9O741c/9K
kqTmGeuJa/YCFgFnZuZNpfhnEXFEZt4CHAvcCNwBXBwRk4CdgP2pJrVZChwHLCt1F2dmX0SsjYh9
geXA0cD5m4uls7NzWDF3dHSw4uY7h7+RGnUzZsxg+vTpTWm7o6ODm5Y1pWkNQ7P37Y13N6VpDVMz
968kSXpyhuo0G+uexLlUQ0E/HhED1ya+F7isTExzN/DtMrvpZcASquGoczNzTUTMA+ZHxBJgDXBy
aeN04Fpge2BhZvqxX5IkSZK2wJgmiZn5XqqkcGNHDlL3SuDKjcoeBV4/SN3bgVmjE6UkSZIkTVxj
PbupJEmSJGkrZpIoSZIkSaqZJEqSJEmSaiaJkiRJkqSaSaIkSZIkqWaSKEmSJEmqmSRKkiRJkmom
iZIkSZKkmkmiJEmSJKlmkihJkiRJqpkkSpIkSZJqJomSJEmSpJpJoiRJkiSptkOrA5AkaaTWrl1L
T09Pq8OY0KZNm0Z7e3urw5AkNYFJoiRpm9PT08MbvvpJJu/51FaHMiE9+sDD/MNpc5k+fXqrQ5Ek
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
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">
In&nbsp;[85]:
</div>
<div class="inner_cell">
    <div class="input_area">
<div class="highlight"><pre><span class="c"># There are 12 original categorical variables in total</span>
<span class="c"># 6. &#39;first_browser&#39; variable</span>
<span class="c"># (1) Visualization</span>
<span class="n">fig</span><span class="p">,</span> <span class="n">axis1</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">subplots</span><span class="p">(</span><span class="mi">1</span><span class="p">,</span><span class="mi">1</span><span class="p">,</span><span class="n">sharex</span><span class="o">=</span><span class="bp">True</span><span class="p">,</span><span class="n">figsize</span><span class="o">=</span><span class="p">(</span><span class="mi">15</span><span class="p">,</span><span class="mi">4</span><span class="p">))</span>
<span class="n">sns</span><span class="o">.</span><span class="n">countplot</span><span class="p">(</span><span class="n">x</span><span class="o">=</span><span class="s">&#39;first_browser&#39;</span><span class="p">,</span> <span class="n">data</span><span class="o">=</span><span class="n">fullData</span><span class="p">,</span> <span class="n">palette</span><span class="o">=</span><span class="s">&quot;husl&quot;</span><span class="p">,</span> <span class="n">ax</span><span class="o">=</span><span class="n">axis1</span><span class="p">)</span>

<span class="c"># (2) Fill NaN values randomly</span>
<span class="n">fullData</span> <span class="o">=</span> <span class="n">FillNaNRandom</span><span class="p">(</span><span class="n">fullData</span><span class="p">,</span> <span class="s">&#39;first_browser&#39;</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>
There are 55 different values in the list of :
Index([u&apos;Chrome&apos;, u&apos;Safari&apos;, u&apos;-unknown-&apos;, u&apos;Firefox&apos;, u&apos;Mobile Safari&apos;, u&apos;IE&apos;, u&apos;Chrome Mobile&apos;, u&apos;Android Browser&apos;, u&apos;AOL Explorer&apos;, u&apos;Opera&apos;, u&apos;Silk&apos;, u&apos;IE Mobile&apos;, u&apos;BlackBerry Browser&apos;, u&apos;Chromium&apos;, u&apos;Mobile Firefox&apos;, u&apos;Maxthon&apos;, u&apos;Apple Mail&apos;, u&apos;Sogou Explorer&apos;, u&apos;SiteKiosk&apos;, u&apos;RockMelt&apos;, u&apos;Iron&apos;, u&apos;IceWeasel&apos;, u&apos;Yandex.Browser&apos;, u&apos;Pale Moon&apos;, u&apos;CometBird&apos;, u&apos;SeaMonkey&apos;, u&apos;Camino&apos;, u&apos;TenFourFox&apos;, u&apos;Opera Mini&apos;, u&apos;wOSBrowser&apos;, u&apos;CoolNovo&apos;, u&apos;Avant Browser&apos;, u&apos;Opera Mobile&apos;, u&apos;Mozilla&apos;, u&apos;OmniWeb&apos;, u&apos;SlimBrowser&apos;, u&apos;Comodo Dragon&apos;, u&apos;Crazy Browser&apos;, u&apos;TheWorld Browser&apos;, u&apos;Flock&apos;, u&apos;Stainless&apos;, u&apos;PS Vita browser&apos;, u&apos;Googlebot&apos;, u&apos;Kindle Browser&apos;, u&apos;NetNewsWire&apos;, u&apos;Google Earth&apos;, u&apos;UC Browser&apos;, u&apos;Conkeror&apos;, u&apos;Outlook 2007&apos;, u&apos;IBrowse&apos;, u&apos;Palm Pre web browser&apos;, u&apos;IceDragon&apos;, u&apos;Nintendo Browser&apos;, u&apos;Arora&apos;, u&apos;Epic&apos;], dtype=&apos;object&apos;)
There is no NaN values for this variable!

</pre>
</div>
</div>

<div class="output_area"><div class="prompt"></div>


<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
AElFTkSuQmCC
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">
In&nbsp;[86]:
</div>
<div class="inner_cell">
    <div class="input_area">
<div class="highlight"><pre><span class="c"># There are 12 original categorical variables in total</span>
<span class="c"># 7. &#39;first_device_type&#39; variable</span>
<span class="c"># (1) Visualization</span>
<span class="n">fig</span><span class="p">,</span> <span class="n">axis1</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">subplots</span><span class="p">(</span><span class="mi">1</span><span class="p">,</span><span class="mi">1</span><span class="p">,</span><span class="n">sharex</span><span class="o">=</span><span class="bp">True</span><span class="p">,</span><span class="n">figsize</span><span class="o">=</span><span class="p">(</span><span class="mi">15</span><span class="p">,</span><span class="mi">4</span><span class="p">))</span>
<span class="n">sns</span><span class="o">.</span><span class="n">countplot</span><span class="p">(</span><span class="n">x</span><span class="o">=</span><span class="s">&#39;first_device_type&#39;</span><span class="p">,</span> <span class="n">data</span><span class="o">=</span><span class="n">fullData</span><span class="p">,</span> <span class="n">palette</span><span class="o">=</span><span class="s">&quot;husl&quot;</span><span class="p">,</span> <span class="n">ax</span><span class="o">=</span><span class="n">axis1</span><span class="p">)</span>

<span class="c"># (2) Fill NaN values randomly</span>
<span class="n">fullData</span> <span class="o">=</span> <span class="n">FillNaNRandom</span><span class="p">(</span><span class="n">fullData</span><span class="p">,</span> <span class="s">&#39;first_device_type&#39;</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>
There are 9 different values in the list of :
Index([u&apos;Mac Desktop&apos;, u&apos;Windows Desktop&apos;, u&apos;iPhone&apos;, u&apos;iPad&apos;, u&apos;Other/Unknown&apos;, u&apos;Android Phone&apos;, u&apos;Android Tablet&apos;, u&apos;Desktop (Other)&apos;, u&apos;SmartPhone (Other)&apos;], dtype=&apos;object&apos;)
There is no NaN values for this variable!

</pre>
</div>
</div>

<div class="output_area"><div class="prompt"></div>


<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">
In&nbsp;[87]:
</div>
<div class="inner_cell">
    <div class="input_area">
<div class="highlight"><pre><span class="c"># There are 12 original categorical variables in total</span>
<span class="c"># 8. &#39;Gender&#39; variable</span>
<span class="c"># (1) Visualization</span>
<span class="n">fig</span><span class="p">,</span> <span class="n">axis1</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">subplots</span><span class="p">(</span><span class="mi">1</span><span class="p">,</span><span class="mi">1</span><span class="p">,</span><span class="n">sharex</span><span class="o">=</span><span class="bp">True</span><span class="p">,</span><span class="n">figsize</span><span class="o">=</span><span class="p">(</span><span class="mi">15</span><span class="p">,</span><span class="mi">4</span><span class="p">))</span>
<span class="n">sns</span><span class="o">.</span><span class="n">countplot</span><span class="p">(</span><span class="n">x</span><span class="o">=</span><span class="s">&#39;gender&#39;</span><span class="p">,</span> <span class="n">data</span><span class="o">=</span><span class="n">fullData</span><span class="p">,</span> <span class="n">palette</span><span class="o">=</span><span class="s">&quot;husl&quot;</span><span class="p">,</span> <span class="n">ax</span><span class="o">=</span><span class="n">axis1</span><span class="p">)</span>

<span class="c"># (2) Assign other categories to either &#39;MALE&#39; or &#39;FEMALE&#39; category</span>
<span class="n">i</span> <span class="o">=</span> <span class="mi">0</span>
<span class="k">def</span> <span class="nf">get_gender</span><span class="p">(</span><span class="n">gender</span><span class="p">):</span>
    <span class="k">global</span> <span class="n">i</span>
    <span class="k">if</span> <span class="n">gender</span> <span class="o">!=</span> <span class="s">&#39;FEMALE&#39;</span> <span class="ow">and</span> <span class="n">gender</span> <span class="o">!=</span> <span class="s">&#39;MALE&#39;</span><span class="p">:</span>
        <span class="k">return</span> <span class="s">&#39;FEMALE&#39;</span> <span class="k">if</span> <span class="p">(</span><span class="n">i</span><span class="o">%</span><span class="k">2</span><span class="p">)</span> <span class="k">else</span> <span class="s">&#39;MALE&#39;</span>
    <span class="n">i</span> <span class="o">=</span> <span class="n">i</span><span class="o">+</span><span class="mi">1</span>
    <span class="k">return</span> <span class="n">gender</span>
<span class="n">fullData</span><span class="p">[</span><span class="s">&#39;gender&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">fullData</span><span class="p">[</span><span class="s">&#39;gender&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">apply</span><span class="p">(</span><span class="n">get_gender</span><span class="p">)</span>

<span class="c"># (3) Map &#39;MALE&#39;to &#39;0&#39; and &#39;FEMALE&#39; to &#39;1&#39;</span>
<span class="n">fullData</span><span class="p">[</span><span class="s">&quot;gender&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">fullData</span><span class="p">[</span><span class="s">&quot;gender&quot;</span><span class="p">]</span><span class="o">.</span><span class="n">map</span><span class="p">({</span><span class="s">&quot;FEMALE&quot;</span><span class="p">:</span> <span class="mi">1</span><span class="p">,</span> <span class="s">&quot;MALE&quot;</span><span class="p">:</span> <span class="mi">0</span><span class="p">})</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>


<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">
In&nbsp;[88]:
</div>
<div class="inner_cell">
    <div class="input_area">
<div class="highlight"><pre><span class="c"># (4) Look for insights</span>
<span class="n">fig</span><span class="p">,</span> <span class="p">(</span><span class="n">axis1</span><span class="p">,</span> <span class="n">axis2</span><span class="p">)</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">subplots</span><span class="p">(</span><span class="mi">2</span><span class="p">,</span><span class="mi">1</span><span class="p">,</span><span class="n">sharex</span><span class="o">=</span><span class="bp">True</span><span class="p">,</span><span class="n">figsize</span><span class="o">=</span><span class="p">(</span><span class="mi">15</span><span class="p">,</span><span class="mi">8</span><span class="p">))</span>
<span class="c"># frequency of country_destination for every gender</span>
<span class="n">sns</span><span class="o">.</span><span class="n">countplot</span><span class="p">(</span><span class="n">x</span><span class="o">=</span><span class="s">&quot;gender&quot;</span><span class="p">,</span><span class="n">hue</span><span class="o">=</span><span class="s">&quot;country_destination&quot;</span><span class="p">,</span> <span class="n">data</span><span class="o">=</span>
              <span class="n">fullData</span><span class="p">[</span><span class="n">fullData</span><span class="p">[</span><span class="s">&#39;country_destination&#39;</span><span class="p">]</span> <span class="o">!=</span> <span class="s">&#39;NDF&#39;</span><span class="p">],</span> <span class="n">palette</span><span class="o">=</span><span class="s">&quot;husl&quot;</span><span class="p">,</span> <span class="n">ax</span><span class="o">=</span><span class="n">axis1</span><span class="p">)</span>
<span class="c"># frequency of booked Vs no-booking users for every gender</span>
<span class="n">sns</span><span class="o">.</span><span class="n">countplot</span><span class="p">(</span><span class="n">x</span><span class="o">=</span><span class="s">&quot;gender&quot;</span><span class="p">,</span><span class="n">hue</span><span class="o">=</span><span class="s">&quot;booked&quot;</span><span class="p">,</span> <span class="n">data</span><span class="o">=</span><span class="n">fullData</span><span class="p">,</span> <span class="n">palette</span><span class="o">=</span><span class="s">&quot;husl&quot;</span><span class="p">,</span> <span class="n">ax</span><span class="o">=</span><span class="n">axis2</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">
    Out[88]:</div>


<div class="output_text output_subarea output_pyout">
<pre>
&lt;matplotlib.axes._subplots.AxesSubplot at 0x1197932d0&gt;
</pre>
</div>

</div>

<div class="output_area"><div class="prompt"></div>


<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
6N27Ny1bttxgLR999BEAn376KYsWLWKHHXZgt91245FHHmHcuHGcffbZ7LXXXjz77LPceeedjB49
moceegiATCazzr8bqnHGjBn89a9/ZcSIEVx00UUsW7Zs7Xdr6l5Ty7Rp0wD46quvmDFjBrvssssG
z3tLeYdQkiRJUtGce+653HDDDbz++uskk0l+/vOfc91115HJZNhll1244oorWLFiBY8//jgDBgyg
Z8+eGwyCAH369OHaa6/lmmuuWef7I488kqFDhzJ69OgN1rLffvux77770q9fP7p168b2229PIpHg
6quvZuDAgaxcuZJevXpx3nnnkUql6N+/P23atOG8884DoHfv3vzgBz/gW9/61np1rfl7jz32YOnS
pZx//vl0796dPfbYg2XLlrH//vvzH//xHwwbNoxEIsHee+/NgQceyHnnnUdNTQ0XX3wx22+//QbP
e0sl6qfXbVVlZWWmoqKi2GVs0MyZM/ns548XZcno/yz8jJ2u/J7PEEqSJGmbVl1dzaBBg3jssceK
XUpRVFZWUlFRsV569A6hJEmSpG3arFmzuO6667j66qsB+Oc//8kPf/jD9fpde+21NOUbSflgIJQk
SZK0TevZsyfPP//82s8777wz48aNK2JFTYebykiSJElSiTIQSpIkSVKJcsmoJEmSpGanpqaGdDqd
0zFTqRTJZDKnYzZ1BkJJkiRJzU46nabyjp+ye8dOORnvk8Wfw9BrSm73fQOhJEmSpGZp946dCvrq
tqlTp/LUU08xcuTItW0jRoxgzz33BOC3v/0tmUyG2tparrzySg4//PCC1bal8hoIQwgtgdFALyAD
XApUA48Cq4HpwBUxxkwIYRAwGFgJ3BFjnBhCaAM8DnQBqoCBMcaFIYRDgPuzfV+NMQ7L53lIkiRJ
UkMvgU8kElRVVfH444/zu9/9ju22247PPvuMfv368Yc//KEIVW6efG8qcyqwOsZ4BDAUuAu4DxgS
YzwSSACnhxC6AlcBhwEnAcNDCEngMmBatu9j2TEAfgGcnx33myGEPnk+D0mSJEklLpPJNNieTCap
ra3l17/+NXPnzmWnnXbitddeK3B1WyavgTDG+DxwSfZjClgEVMQYJ2fbXgaOB/4FmBJjrI0xLgFm
AQcAhwOvZPu+AhwfQigHkjHG2dn2SdkxJEmSJKngysrKGDt2LHPmzGHQoEEce+yxPPvss8Uuq1Hy
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
53DdddcxbFjT3+4kn5vK7Ay8ClweY3wj2/xKCOHqGON71C31fB/4I3BnCKE1dXcQ9wGmA1OAU4D3
gJOByTHGqhBCTQihBzAbOBG4rTH1VFRU5Ozccq28vJzP3izeqtfevXuX3PtWJEnrKua1yOuQpObk
29/+9ibbKioquPrqqwtVUqNsKOjm8w7hEOqWef44hLAmul8L/GcIoRaYDwyOMS4NIYwC3qLuWcMh
McbqEMJDwNgQwltANdA/O8alwHigJTApGy4lSZIkSZspn88QXgNc08BXRzTQdwww5mttK4BzGug7
FTg0R2VKkiRJUslqHlvfSJIkSZJyzkAoSZIkSSUqr7uMSpIkSVI+1NTUkE6nczpmKpUimUzmdMym
zkAoSZIkqdlJp9Pc+fN+7NC5LCfjLVr4FTdfOaHkdj02EEqSJElqlnboXEbnndsWdM6PP/6YESNG
sGLFCpYvX85RRx3FVVddBcDvfvc7br75ZiZNmsROOxXzTeON5zOEkiRJktQIS5Ys4Qc/+AE333wz
jz32GE8//TQzZ87kqaeeAmDChAn8+7//O08//XSRK208A6EkSZIkNcLrr7/OoYceSrdu3QBo0aIF
99xzD2eddRaffPIJS5Ys4eKLL+b5559n5cqVRa62cQyEkiRJktQICxYsYLfddlunrW3btrRq1Ypn
nnmGs846i/Lycvr06cOrr75apCo3j88QSpIkSVIj7LrrrvzlL39Zp23evHn8/e9/58UXX2S33Xbj
jTfe4Msvv2T8+PGccsopRaq08QyEkiRJkpqlRQu/KuhYRx99NA8//DD9+/dn9913p7a2lrvvvpu+
fftywAEHcP/996/te9JJJxFjJISQsxrzwUAoSZIkqdlJpVLcfOWEnI+5Me3bt+fuu+9m6NChrF69
mmXLlnHsscfyzjvvcO65567Tt1+/fowfP55hw4bltMZcMxBKkiRJanaSyWRR3hm43377MXbs2E32
u/jiiwtQzdZzUxlJkiRJKlEGQkmSJEkqUQZCSZIkSSpRBkJJkiRJKlFuKiNJkiSp2ampqSGdTud0
zFQqRTKZzOmYTZ2BUJIkSVKzk06nOWf0FbTp0j4n461YsJSnBz1QlJ1Li8lAKEmSJKlZatOlPW13
2b6gc37yySfce++9/POf/6SsrIyysjKuv/56Xn75ZV566SV22mknVq1aRfv27bnvvvsoLy8vaH2b
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
CAngIeDqBo5dEwL/DOwUQlgT/PoDxBiXAB+HEL4LkH3O8M28nYkkSV9jIJQkaSNijC9T9yzgB8BL
wN+B/wfcDvyeumWhAHdn/52pd3gGyGSXm55L3dLQSmCHev2+C1wcQpgG3Amc87XjJUnKm0Qm47VG
kqQNCSEcAvSKMT4WQmgFvANcEGOcvolDJUlq8gyEkiRtRAhhB+DXwC7Urax5NMY4srhVSZKUGwZC
SZIkSSpRPkMoSZIkSSXKQChJkiRJJcpAKEmSJEklykAoSZIkSSXKQChJkiRJJcpAKEmSJEklykAo
SZIkSSXKQChJkiRJJcpAKEmSJEklykAoSZIkSSXKQChJkiRJJcpAKEmSJEklykAoSZIkSSXKQChJ
kiRJJcpAKEmSJEklykAoSZIkSSXKQChJkiRJJcpAKEmSJEklykAoSZIkSSXKQChJkiRJJWq7fA0c
QmgBjAF6AauBQcAq4NHs5+nAFTHGTAhhEDAYWAncEWOcGEJoAzwOdAGqgIExxoUhhEOA+7N9X40x
DsvXOUiSJEnStiyfdwhPBNrFGI8AhgF3AfcBQ2KMRwIJ4PQQQlfgKuAw4CRgeAghCVwGTMv2fQwY
mh33F8D52XG/GULok8dzkCRJkqRtVj4D4Qpg+xBCAtgeqAEqYoyTs9+/DBwP/AswJcZYG2NcAswC
DgAOB17J9n0FOD6EUA4kY4yzs+2TsmNIkiRJkjZT3paMAlOAMmAG0Ak4DTiy3vdV1AXFDsCXG2hf
spG2Ne098lC7JEmSJG3z8hkIf0Tdnb+bQwi7AW8Arep93wFYTF3AK6/XXt5Ae0Nt9cfYqMrKyswW
noMkSZIkbRMqKioSX2/LZyBsx//ezVuUneuDEMJRMcY/ACcDrwN/BO4MIbSm7o7iPtRtODMFOAV4
L9t3coyxKoRQE0LoAcym7jnF2xpTTEVFRa7OS5IkSZKalcrKygbb8xkI7wV+FUJ4i7o7gzcBlcDo
7KYxfwWeye4yOgp4i7pnGofEGKtDCA8BY7PHVwP9s+NeCowHWgKTYozv5fEcJEmSJGmblchktv3V
lJWVlRnvEEqSJDU/NTU1pNPpYpchbVAqlSKZTBa7jE2qrKws+JJRSZIkaauk02nOe/jntOncqdil
SOtZsfBznrzkSnr16lXsUraYgVCSJElNWpvOnWjXdedilyFtk/L5HkJJkiRJUhNmIJQkSZKkEmUg
lCRJkqQSZSCs5ze/+Q1jx47domNvvPFGpk2btlnHPProozz33HNbNJ8kSZIkbS0DYT2JxHq7sG7W
sZt7/NbMJ0mSJElby11Gv+bNN9/k9ddfJ5PJcMcdd/Doo48yY8YMMpkM11xzDYceeijPPvssTz75
JC1atOCkk07iwgsvBCCTyTBp0iSef/557r//fqZOncoDDzxAIpHg2GOPZdCgQcycOZOhQ4fSrl07
EokEp512WpHPWJIkSVKpMhDWk8lk6Nq1K8OHD+f999/n7LPP5uSTT+aJJ57giy++4Hvf+x7jx49n
/PjxPP3007Ro0YKBAwdy1FFHAfDGG28wY8YMfvazn9GyZUt+8pOf8OSTT9K2bVsuu+wyjj32WO67
7z5uu+029t13X2688cYin7EkSZKkUmYgrCeRSHDggQcCsP/++7N06VIOOuggAHbccUfat2/PJ598
QgiB7bar+5/uG9/4BrNnzwbg/fffB2C77bbjiy++4J///CeXXnopAEuXLuWTTz5h7ty57LvvvgD0
6dOnoOcnSZIkSfX5DGE9mUyGv/zlLwB8+OGHtGnThj/96U8AfPHFFyxevJjddtuNGCMrV65k1apV
fPjhh+y+++4AXH/99fTp04exY8ey4447sttuu/HII48wbtw4zj77bPbaay/22GMP/vznPwMwffr0
4pyoJEmSJOEdwnUkEgnmz5/PwIEDSSQSTJw4kYcffpj+/ftTXV3NzTffzI477sj5559P//79WbVq
FSeccAIhhLXHX3nllfTr14/jjjuOq6++moEDB7Jy5Up69erFeeedxw033MBNN91EWVkZZWVlbiwj
SZIkqWgSmUym2DXkXWVlZaaioqLYZUiSJGkzzZw5kwuefYJ2XXcudinSepb945/86jvn06tXr2KX
skmVlZVUVFSsdzfKJaOSJEmSVKJcMippo2pqakin08UuQ2pQKpUimUwWuwxJkpotA6GkjUqn05z3
8M9p07lTsUuR1rFi4ec8ecmVzWKZjiRJTZWBUNImtencyWc3JEmStkF5DYQhhIHA97Mf2wDfAI4A
fgqsBqYDV8QYMyGEQcBgYCVwR4xxYgihDfA40AWoAgbGGBeGEA4B7s/2fTXGOCyf5yFJkiRJ26K8
BsIY41hgLEAI4efAGODHwJAY4+QQwkPA6SGEd4GrgArqguPbIYTXgMuAaTHGYSGEc4GhwLXAL4Az
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
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">
In&nbsp;[89]:
</div>
<div class="inner_cell">
    <div class="input_area">
<div class="highlight"><pre><span class="c"># There are 12 original categorical variables in total</span>
<span class="c"># 9. &#39;id&#39; variable</span>
<span class="c"># (1) Visualization</span>
<span class="n">fullData</span><span class="p">[</span><span class="s">&#39;id&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">iloc</span><span class="p">[</span><span class="mi">0</span><span class="p">]</span> <span class="c"># it shows &#39;gxn3p5htnn&#39;</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">
    Out[89]:</div>


<div class="output_text output_subarea output_pyout">
<pre>
&apos;gxn3p5htnn&apos;
</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">
In&nbsp;[90]:
</div>
<div class="inner_cell">
    <div class="input_area">
<div class="highlight"><pre><span class="c"># There are 12 original categorical variables in total</span>
<span class="c"># 10. &#39;language&#39; variable</span>
<span class="c"># (1) Visualization</span>
<span class="n">fig</span><span class="p">,</span> <span class="n">axis1</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">subplots</span><span class="p">(</span><span class="mi">1</span><span class="p">,</span><span class="mi">1</span><span class="p">,</span><span class="n">sharex</span><span class="o">=</span><span class="bp">True</span><span class="p">,</span><span class="n">figsize</span><span class="o">=</span><span class="p">(</span><span class="mi">15</span><span class="p">,</span><span class="mi">4</span><span class="p">))</span>
<span class="n">sns</span><span class="o">.</span><span class="n">countplot</span><span class="p">(</span><span class="n">x</span><span class="o">=</span><span class="s">&#39;language&#39;</span><span class="p">,</span> <span class="n">data</span><span class="o">=</span><span class="n">fullData</span><span class="p">,</span> <span class="n">palette</span><span class="o">=</span><span class="s">&quot;husl&quot;</span><span class="p">,</span> <span class="n">ax</span><span class="o">=</span><span class="n">axis1</span><span class="p">)</span>

<span class="c"># (2) Fill NaN values randomly</span>
<span class="n">fullData</span> <span class="o">=</span> <span class="n">FillNaNRandom</span><span class="p">(</span><span class="n">fullData</span><span class="p">,</span> <span class="s">&#39;language&#39;</span><span class="p">)</span>

<span class="c"># (3) Binary process</span>
<span class="n">fullData</span><span class="p">[</span><span class="s">&quot;language&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="p">(</span><span class="n">fullData</span><span class="p">[</span><span class="s">&quot;language&quot;</span><span class="p">]</span> <span class="o">==</span> <span class="s">&#39;en&#39;</span><span class="p">)</span><span class="o">.</span><span class="n">astype</span><span class="p">(</span><span class="nb">int</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>
There are 26 different values in the list of :
Index([u&apos;en&apos;, u&apos;zh&apos;, u&apos;fr&apos;, u&apos;es&apos;, u&apos;ko&apos;, u&apos;de&apos;, u&apos;it&apos;, u&apos;ru&apos;, u&apos;ja&apos;, u&apos;pt&apos;, u&apos;sv&apos;, u&apos;nl&apos;, u&apos;tr&apos;, u&apos;da&apos;, u&apos;pl&apos;, u&apos;no&apos;, u&apos;cs&apos;, u&apos;el&apos;, u&apos;th&apos;, u&apos;hu&apos;, u&apos;id&apos;, u&apos;fi&apos;, u&apos;ca&apos;, u&apos;is&apos;, u&apos;hr&apos;, u&apos;-unknown-&apos;], dtype=&apos;object&apos;)
There is no NaN values for this variable!

</pre>
</div>
</div>

<div class="output_area"><div class="prompt"></div>


<div class="output_png output_subarea ">
<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAA5EAAAERCAYAAADi/SNOAAAABHNCSVQICAgIfAhkiAAAAAlwSFlz
AAALEgAACxIB0t1+/AAAIABJREFUeJzt3X2cHWV99/HPJiEBZYNtAGkriiD5lTalwGpBggHu5gbB
IkpvH0AtoEJ5EKVP1kYkwB2KIlKMArGgAkK1gqJFbpNYNSSmCPFUsBH5RSCbYn0ID0IWK0kge/8x
s+Ww7m4mcWfOkv28X6+8snudOXNdc86cOfOd65pru/r7+5EkSZIkqYoJnW6AJEmSJOm5wxApSZIk
SarMEClJkiRJqswQKUmSJEmqzBApSZIkSarMEClJkiRJqmxSXSuOiInAVcB0oB84DVgPXANsAlYC
Z2Zmf0ScApwKPAXMy8xbI2IH4HpgF6APODEzH46Ig4DLymUXZ+YFZX1zgaPL8rMzc0Vd2yZJkiRJ
41WdPZF/AmzKzEOAc4C/Bz4CzMnMWUAXcGxE7AacBRwMHAlcFBGTgdOBu8tlryvXAbAAOL5c74ER
sV9EHADMyswDgTcDl9e4XZIkSZI0btUWIjPzy8Cfl7/uAfwc6MnMpWXZV4HZwCuA5Zm5MTPXAfcB
+wIzgYXlsguB2RHRDUzOzNVl+aJyHTOBxWW9DwKTImJaXdsmSZIkSeNVrfdEZubTEXEN8FHgBore
xwF9wE7AVODxYcrXjVBWZR2SJEmSpFFU+8Q6mXkSEMDVwPZtD00FHqMIhd1t5d1DlA9VVmUdkiRJ
kqRRVOfEOm8DXpSZFwG/BJ4GvhMRh2bmbcBRwNeBO4ELI2IKRcjch2LSneUUE+WsKJddmpl9EbEh
IvYEVgNHAOeV6744Ii4BdgcmZOajI7Wv1Wr1j/Y2S5IkSdJzSU9PT9fml3q22kIkcBNwTUTcBmwH
vAe4F7iqnDjnHuCmcnbW+cAyip7ROZm5PiKuBK6NiGUUs7qeUK73NIqhsROBRQOzsJbL3V6u44wq
Dezp6RmdLZUkSZKk55hWq7VVz+vq7x+fHXKtVqvfEClJkiRpvGq1WlvVE1n7PZGSJEmSpG2HIVKS
JEmSVJkhUpIkSZJUmSFSkiRJklSZIVKSJEmSVJkhUpIkSZJUmSFSkiRJklSZIVKSJEmSVJkhUpIk
SZJUmSFSkiRJklSZIVKSJEmSVJkhUpIkSZJUmSFSkiRJklSZIVKSJEmSVJkhUpIkSZJUmSFSkiRJ
klSZIVKSJEmSVJkhUpIkSZJUmSFSkiRJklSZIVKSJEmSVJkhUpIkSZJU2aRON6DTNmzYQG9vbyN1
7bHHHkyePLmRuiRJkiSpDuM+RPb29tKa91F2f8G0Wut58LFH4Jz3MH369FrrkSRJkqQ6jfsQCbD7
C6ax1867droZkiRJkjTmeU+kJEmSJKkyQ6QkSZIkqTJDpCRJkiSpMkOkJEmSJKkyQ6QkSZIkqbLa
ZmeNiO2ATwEvAaYA84AfAV8BVpWLXZGZN0bEKcCpwFPAvMy8NSJ2AK4HdgH6gBMz8+GIOAi4rFx2
cWZeUNY3Fzi6LD87M1fUtW2SJEmSNF7V2RP5FuChzJwFvBq4HDgA+EhmHl7+uzEidgPOAg4GjgQu
iojJwOnA3eXzrwPOKde7ADg+Mw8BDoyI/SLiAGBWZh4IvLmsS5IkSZI0yuoMkTcC57bVsxHoAV4T
EbdFxNURsSPwR8DyzNyYmeuA+4B9gZnAwvL5C4HZEdENTM7M1WX5ImB2uexigMx8EJgUEdNq3DZJ
kiRJGpdqC5GZ+YvMfKIMfjcC7wfuBP46Mw8FHgDmAt3A421P7QN2AqYC60YoG1w+1DokSZIkSaOo
1ol1ImJ34BvAdZn5OeDmzPxu+fDNwP4UobC77WndwGODyocqgyI8DlU+sLwkSZIkaRTVObHOCymG
mJ6Rmd8sixdGxLvLSW9mA9+h6J28MCKmANsD+wArgeUUE+WsAI4ClmZmX0RsiIg9gdXAEcB5wNPA
xRFxCbA7MCEzH91cG1utFmvWrGHXUdvqka1cuZK+vr6GapMkSZKk0VdbiATmUAwpPTciBu6NPBv4
h4jYCPwEOLUc8jofWEbRMzonM9dHxJXAtRGxDFgPnFCu4zTgBmAisGhgFtZyudvLdZxRpYE9PT10
d3ezdsldo7C5mzdjxgymT5/eSF2SJEmSNJJWq7VVz+vq7+8f5aY8N7Rarf6enh5WrVrF2o9fz147
19sfef/Da9n1XW81REqSJEkaE1qtFj09PV1b+rxa74mUJEmSJG1bDJGSJEmSpMoMkZIkSZKkygyR
kiRJkqTKDJGSJEmSpMoMkZIkSZKkygyRkiRJkqTKDJGSJEmSpMoMkZIkSZKkygyRkiRJkqTKDJGS
JEmSpMoMkZIkSZKkygyRkiRJkqTKDJGSJEmSpMoMkZIkSZKkygyRkiRJkqTKDJGSJEmSpMoMkZIk
SZKkygyRkiRJkqTKDJGSJEmSpMoMkZIkSZKkygyRkiRJkqTKDJGSJEmSpMoMkZIkSZKkygyRkiRJ
kqTKDJGSJEmSpMoMkZIkSZKkygyRkiRJkqTKDJGSJEmSpMoMkZIkSZKkyibVteKI2A74FPASYAow
D/gBcA2wCVgJnJmZ/RFxCnAq8BQwLzNvjYgdgOuBXYA+4MTMfDgiDgIuK5ddnJkXlPXNBY4uy8/O
zBV1bZskSZIkjVd19kS+BXgoM2cBrwYuBz4CzCnLuoBjI2I34CzgYOBI4KKImAycDtxdLnsdcE65
3gXA8Zl5CHBgROwXEQcAszLzQODNZV2SJEmSpFFWZ4i8ETi3rZ6NwAGZubQs+yowG3gFsDwzN2bm
OuA+YF9gJrCwXHYhMDsiuoHJmbm6LF9UrmMmsBggMx8EJkXEtBq3TZIkSZLGpdpCZGb+IjOfKIPf
jRQ9ie319QE7AVOBx4cpXzdCWZV1SJIkSZJGUW33RAJExO7AF4HLM/OzEXFx28NTgccoQmF3W3n3
EOVDlbWvY8Mw6xhRq9VizZo17LolG/VrWLlyJX19fQ3VJkmSJEmjr86JdV5IMcT0jMz8Zln83Yg4
NDNvA44Cvg7cCVwYEVOA7YF9KCbdWU4xUc6KctmlmdkXERsiYk9gNXAEcB7wNHBxRFwC7A5MyMxH
N9fGnp4euru7WbvkrlHb7pHMmDGD6dOnN1KXJEmSJI2k1Wpt1fPq7ImcQzGk9NyIGLg38j3A/HLi
nHuAm8rZWecDyyiGu87JzPURcSVwbUQsA9YDJ5TrOA24AZgILBqYhbVc7vZyHWfUuF2SJEmSNG51
9ff3d7oNHdFqtfp7enpYtWoVaz9+PXvtXO+g1vsfXsuu73qrPZGSJEmSxoRWq0VPT0/Xlj6vztlZ
JUmSJEnbGEOkJEmSJKkyQ6QkSZIkqTJDpCRJkiSpMkOkJEmSJKkyQ6QkSZIkqTJDpCRJkiSpMkOk
JEmSJKkyQ6QkSZIkqTJDpCRJkiSpMkOkJEmSJKkyQ6QkSZIkqTJDpCRJkiSpMkOkJEmSJKkyQ6Qk
SZIkqTJDpCRJkiSpMkOkJEmSJKkyQ6QkSZIkqTJDpCRJkiSpMkOkJEmSJKkyQ6QkSZIkqTJDpCRJ
kiSpss2GyIj42BBl19bTHEmSJEnSWDZpuAci4mpgL+DlETFj0HNeUHfDJEmSJEljz7AhErgQeAkw
HzgP6CrLnwLuqbdZkiRJkqSxaNgQmZmrgdXAvhExFdiJZ4LkjsCj9TdPkiRJkjSWjNQTCUBEzAHe
RxEa+9seemldjZIkSZIkjU2bDZHAO4G9MvOhuhsjSZIkSRrbqvyJjzXAz+tuiCRJkiRp7KvSE3kf
8K2I+Aawvizrz8wLqlQQEQcCH8zMwyNif+AW4Iflw1dk5o0RcQpwKsWkPfMy89aI2AG4HtgF6ANO
zMyHI+Ig4LJy2cUD7YiIucDRZfnZmbmiSvskSZIkSdVVCZH/Vf4b0DXcgoNFxHuBtwJPlEU9wKWZ
eWnbMrsBZ5WP7UARWL8GnA7cnZkXRMSbgHOAs4EFwOszc3VE3BoR+1H0qM7KzAMjYnfgC8AfVW2n
JEmSJKmazYbIzDzv11j/fcBxwGfK33uA6RFxLEVv5NkUYW95Zm4ENkbEfcC+wEzgQ+XzFgIfiIhu
YHI5cyzAImA2RQ/p4rK9D0bEpIiYlpmP/BptlyRJkiQNUmV21k1DFP84M1+0uedm5hcjYo+2ojuA
f8zM75azvs4F7gIeb1umj+LPiUwF1o1QNlC+J/Ak8MgQ6zBESpIkSdIoqtIT+T+T70TEdsDrgIO3
sr6bM3MgMN4MfAxYCnS3LdMNPEYRFrtHKIMiVD4GbBhmHSNqtVqsWbOGXbd8O7bKypUr6evra6g2
SZIkSRp9Ve6J/B/lkNMbI+KcraxvYUS8u5z0ZjbwHeBO4MKImAJsD+wDrASWU0yUswI4CliamX0R
sSEi9gRWA0cA5wFPAxdHxCXA7sCEzHx0c43p6emhu7ubtUvu2srN2TIzZsxg+vTpjdQlSZIkSSNp
tVpb9bwqw1lPbPu1C/h9npmltar+8v/TgMsjYiPwE+DUzHwiIuYDyygmyJmTmesj4krg2ohYVtZ3
Qts6bgAmAosGZmEtl7u9XMcZW9g+SZIkSVIFVXoiD+eZENgPPAy8qWoFmdlLOfw1M+8GDhlimauB
qweV/RJ44xDL3gG8cojy84Hzq7ZLkiRJkrTlqtwTeVJETAaiXH5lOaxVkiRJkjTOTNjcAhHxcmAV
cC3wKWBNRBxUd8MkSZIkSWNPleGs84E3lcNIKQPkfIq/7yhJkiRJGkc22xMJPH8gQAJk5rcpZlGV
JEmSJI0zVULkzyPidQO/RMTrgUfqa5IkSZIkaayqMpz1VOCWiPgkxZ/42ATMrLVVkiRJkqQxqUpP
5KuB/wZeDBxG0Qt5WH1NkiRJkiSNVVVC5J8Dh2TmLzLze8D+wFn1NkuSJEmSNBZVCZGTgA1tv2+g
GNIqSZIkSRpnqtwT+SXgGxHxzxT3RB4H/EutrZIkSZIkjUmb7YnMzL+l+LuQAbwU+GhmnlN3wyRJ
kiRJY0+Vnkgy80bgxprbIkmSJEka46rcEylJkiRJEmCIlCRJkiRtAUOkJEmSJKkyQ6QkSZIkqTJD
pCRJkiSpMkOkJEmSJKkyQ6QkSZIkqTJDpCRJkiSpMkOkJEmSJKkyQ6QkSZIkqTJDpCRJkiSpMkOk
JEmSJKkyQ6QkSZIkqTJDpCRJkiSpMkOkJEmSJKkyQ6QkSZIkqTJDpCRJkiSpskl1VxARBwIfzMzD
I+JlwDXAJmAlcGZm9kfEKcCpwFPAvMy8NSJ2AK4HdgH6gBMz8+GIOAi4rFx2cWZeUNYzFzi6LD87
M1fUvW2SJEmSNN7U2hMZEe8FrgKmlEWXAnMycxbQBRwbEbsBZwEHA0cCF0XEZOB04O5y2euAc8p1
LACOz8xDgAMjYr+IOACYlZkHAm8GLq9zuyRJkiRpvKp7OOt9wHEUgRHggMxcWv78VWA28ApgeWZu
zMx15XP2BWYCC8tlFwKzI6IbmJyZq8vyReU6ZgKLATLzQWBSREyrdcskSZIkaRyqNURm5hcphpcO
6Gr7uQ/YCZgKPD5M+boRyqqsQ5IkSZI0imq/J3KQTW0/TwUeowiF3W3l3UOUD1XWvo4Nw6xjRK1W
izVr1rDrlm3DVlu5ciV9fX0N1SZJkiRJo6/pEPndiDg0M28DjgK+DtwJXBgRU4DtgX0oJt1ZTjFR
zopy2aWZ2RcRGyJiT2A1cARwHvA0cHFEXALsDkzIzEc315ienh66u7tZu+Su0d7OIc2YMYPp06c3
UpckSZIkjaTVam3V85oKkf3l/38FXFVOnHMPcFM5O+t8YBnF8No5mbk+Iq4Ero2IZcB64IRyHacB
NwATgUUDs7CWy91eruOMhrZLkiRJksaVrv7+/s0vtQ1qtVr9PT09rFq1irUfv569dq53UOv9D69l
13e91Z5ISZIkSWNCq9Wip6ena/NLPlvds7NKkiRJkrYhhkhJkiRJUmWGSEmSJElSZYZISZIkSVJl
hkhJkiRJUmWGSEmSJElSZYZISZIkSVJlhkhJkiRJUmWGSEmSJElSZYZISZIkSVJlhkhJkiRJUmWG
SEmSJElSZYZISZIkSVJlhkhJkiRJUmWGSEmSJElSZYZISZIkSVJlhkhJkiRJUmWGSEmSJElSZYZI
SZIkSVJlhkhJkiRJUmWGSEmSJElSZYZISZIkSVJlhkhJkiRJUmWGSEmSJElSZYZISZIkSVJlhkhJ
kiRJUmWGSEmSJElSZYZISZIkSVJlhkhJkiRJUmWTOlFpRPw78Hj56wPARcA1wCZgJXBmZvZHxCnA
qcBTwLzMvDUidgCuB3YB+oATM/PhiDgIuKxcdnFmXtDkNkmSJEnSeNB4T2REbA+QmYeX/94BXArM
ycxZQBdwbETsBpwFHAwcCVwUEZOB04G7y2WvA84pV70AOD4zDwEOjIj9Gt0wSZIkSRoHOtET+YfA
8yJiUVn/+4EDMnNp+fhXgSOAp4HlmbkR2BgR9wH7AjOBD5XLLgQ+EBHdwOTMXF2WLwJmA3c1sUGS
JEmSNF504p7IXwAfzswjgdOAGwY93gfsBEzlmSGvg8vXjVDWXi5JkiRJGkWdCJGrKINjZv4QeAR4
YdvjU4HHKEJhd1t59xDlQ5W1r0OSJEmSNIo6MZz1ZIphqWdGxG9ThL/FEXFoZt4GHAV8HbgTuDAi
pgDbA/tQTLqzHDgaWFEuuzQz+yJiQ0TsCaymGA573uYa0mq1WLNmDbuO9hYOY+XKlfT19TVUmyRJ
kiSNvk6EyE8Cn46IgXsgT6bojbyqnDjnHuCmcnbW+cAyih7TOZm5PiKuBK6NiGXAeuCEcj0DQ2Mn
Aosyc8XmGtLT00N3dzdrlzRz6+SMGTOYPn16I3VJkiRJ0khardZWPa/xEJmZTwFvG+Khw4ZY9mrg
6kFlvwTeOMSydwCvHJ1WSpIkSZKG0ol7IiVJkiRJz1GGSEmSJElSZYZISZIkSVJlhkhJkiRJUmWG
SEmSJElSZYZISZIkSVJlhkhJkiRJUmWGSEmSJElSZYZISZIkSVJlhkhJkiRJUmWGSEmSJElSZYZI
SZIkSVJlhkhJkiRJUmWGSEmSJElSZYZISZIkSVJlhkhJkiRJUmWGSEmSJElSZYZISZIkSVJlhkhJ
kiRJUmWGSEmSJElSZYZISZIkSVJlhkhJkiRJUmWGSEmSJElSZYZISZIkSVJlhkhJkiRJUmWGSEmS
JElSZYZISZIkSVJlhkhJkiRJUmWGSEmSJElSZZM63YDREhETgCuAfYH1wDsz8/7OtkqSJEmSti3b
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
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">
In&nbsp;[91]:
</div>
<div class="inner_cell">
    <div class="input_area">
<div class="highlight"><pre><span class="c"># There are 12 original categorical variables in total</span>
<span class="c"># 11-12. &#39;signup_method&#39; and &#39;signup_flow&#39; variable</span>
<span class="c"># (1) Visualization</span>
<span class="n">fig</span><span class="p">,</span> <span class="n">axis1</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">subplots</span><span class="p">(</span><span class="mi">1</span><span class="p">,</span><span class="mi">1</span><span class="p">,</span><span class="n">sharex</span><span class="o">=</span><span class="bp">True</span><span class="p">,</span><span class="n">figsize</span><span class="o">=</span><span class="p">(</span><span class="mi">15</span><span class="p">,</span><span class="mi">4</span><span class="p">))</span>
<span class="n">sns</span><span class="o">.</span><span class="n">countplot</span><span class="p">(</span><span class="n">x</span><span class="o">=</span><span class="s">&#39;signup_method&#39;</span><span class="p">,</span> <span class="n">data</span><span class="o">=</span><span class="n">fullData</span><span class="p">,</span> <span class="n">palette</span><span class="o">=</span><span class="s">&quot;husl&quot;</span><span class="p">,</span> <span class="n">ax</span><span class="o">=</span><span class="n">axis1</span><span class="p">)</span>

<span class="c"># (2) Fill NaN values randomly</span>
<span class="n">fullData</span> <span class="o">=</span> <span class="n">FillNaNRandom</span><span class="p">(</span><span class="n">fullData</span><span class="p">,</span> <span class="s">&#39;signup_method&#39;</span><span class="p">)</span>
<span class="n">fullData</span> <span class="o">=</span> <span class="n">FillNaNRandom</span><span class="p">(</span><span class="n">fullData</span><span class="p">,</span> <span class="s">&#39;signup_flow&#39;</span><span class="p">)</span>

<span class="c"># (3) Binary process</span>
<span class="n">fullData</span><span class="p">[</span><span class="s">&quot;signup_method&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="p">(</span><span class="n">fullData</span><span class="p">[</span><span class="s">&quot;signup_method&quot;</span><span class="p">]</span> <span class="o">==</span> <span class="s">&quot;basic&quot;</span><span class="p">)</span><span class="o">.</span><span class="n">astype</span><span class="p">(</span><span class="nb">int</span><span class="p">)</span>
<span class="n">fullData</span><span class="p">[</span><span class="s">&quot;signup_flow&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="p">(</span><span class="n">fullData</span><span class="p">[</span><span class="s">&quot;signup_flow&quot;</span><span class="p">]</span> <span class="o">==</span> <span class="mi">3</span><span class="p">)</span><span class="o">.</span><span class="n">astype</span><span class="p">(</span><span class="nb">int</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>
There are 4 different values in the list of :
Index([u&apos;basic&apos;, u&apos;facebook&apos;, u&apos;google&apos;, u&apos;weibo&apos;], dtype=&apos;object&apos;)
There is no NaN values for this variable!
There are 18 different values in the list of :
Int64Index([0, 25, 12, 3, 2, 23, 24, 1, 8, 6, 21, 5, 20, 16, 15, 14, 10, 4], dtype=&apos;int64&apos;)
There is no NaN values for this variable!

</pre>
</div>
</div>

<div class="output_area"><div class="prompt"></div>


<div class="output_png output_subarea ">
<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAA4oAAAERCAYAAAA9s1lRAAAABHNCSVQICAgIfAhkiAAAAAlwSFlz
AAALEgAACxIB0t1+/AAAG1ZJREFUeJzt3Xm0ZWV5J+BfIZagFhrBMRJRY73BEKKWBhGDmqA4JE4d
49S2IS2oGKLdcZksgooG2yFoG4xDIhpBTUxjzOBChsQBkDhgaUgq2C8SqQpJbBUUKA1SDLf/2Lvk
7vJW1QXuAJfnWYt17/n2Pt95N+vu2ud3vu98e9XMzEwAAABgq12WuwAAAABuWQRFAAAAJgRFAAAA
JgRFAAAAJgRFAAAAJgRFAAAAJnZdrI6r6vZJ3p/kfknukOS4JF9N8oEk1yfZkORl3T1TVYcnOSLJ
tUmO6+5Tq2r3JB9Kcvckm5O8sLsvrapHJnn7uO+Z3f368fVem+TJY/sruvu8xTo2AACAlWwxRxSf
n+Tb3X1wkicmeWeStyY5emxbleRpVXWvJEcleVSSQ5O8sapWJ3lpkvPHfU9OcszY73uSPLe7H53k
gKp6SFU9LMnB3X1AkueMrwUAAMBNsJhB8ZQkr5n1OtckeVh3nz22nZbkkCSPSHJud1/T3VcmuSjJ
/kkOSnL6uO/pSQ6pqjVJVnf3xWP7GWMfByU5M0m6+5Iku1bVnot4bAAAACvWogXF7v5+d39vDHen
ZBgRnP16m5PcJckeSa7YTvuVO2ibTx8AAADcSIu6mE1V7Z3kU0lO7u4/y/DdxK32SHJ5huC3Zlb7
mjna52qbTx8AAADcSIu5mM09M0wHPbK7Pz02f6WqHtPdZyV5UpJPJvlikjdU1R2S7JZk3wwL3Zyb
YXGa88Z9z+7uzVW1paoekOTiJE9IcmyS65K8paqOT7J3kl26+zs7qm/9+vUzC3rAAAAAtzLr1q1b
NVf7ogXFJEdnmP75mqra+l3Flyc5YVys5oIkHx1XPT0hyTkZRjiP7u6rq+rdSU6qqnOSXJ3keWMf
L0ny4SS3S3LG1tVNx/0+N/Zx5HwKXLdu3QIcJrAQtmzZko0bNy53GbBd++yzT1avXr3cZQDAglm/
fv12t62ambltDqytX79+RlCEW44LL7wwx5/wrNxtz92WuxT4Ed+57Ad55W+ekrVr1y53KQCwYNav
X78sI4oAN8rd9twtd7/nHZe7DACA27xFXcwGAACAWx9BEQAAgAlBEQAAgAlBEQAAgAlBEQAAgAlB
EQAAgAlBEQAAgAlBEQAAgAlBEQAAgAlBEQAAgAlBEQAAgAlBEQAAgAlBEQAAgAlBEQAAgAlBEQAA
gAlBEQAAgAlBEQAAgAlBEQAAgAlBEQAAgAlBEQAAgAlBEQAAgAlBEQAAgAlBEQAAgAlBEQAAgAlB
EQAAgAlBEQAAgAlBEQAAgAlBEQAAgAlBEQAAgAlBEQAAgAlBEQAAgAlBEQAAgAlBEQAAgAlBEQAA
gAlBEQAAgAlBEQAAgAlBEQAAgAlBEQAAgAlBEQAAgAlBEQAAgAlBEQAAgAlBEQAAgAlBEQAAgAlB
EQAAgAlBEQAAgAlBEQAAgAlBEQAAgIldF/sFquqAJG/q7sdV1UOTfDzJ18bN7+ruU6rq8CRHJLk2
yXHdfWpV7Z7kQ0nunmRzkhd296VV9cgkbx/3PbO7Xz++zmuTPHlsf0V3n7fYxwYAALASLWpQrKpX
JfmvSb43Nq1L8rbuftusfe6V5Khx2+5JPltVf5vkpUnO7+7XV9WzkxyT5BVJ3pPkGd19cVWdWlUP
yTAyenB3H1BVeyf5iyQ/t5jHBgAAsFIt9tTTi5I8M8mq8fG6JE+pqrOq6sSqunOGQHdud1/T3VeO
z9k/yUFJTh+fd3qSQ6pqTZLV3X3x2H5GkkPGfc9Mku6+JMmuVbXnIh8bAADAirSoQbG7P5ZhKuhW
X0jyyu5+TJKvJ3ltkjVJrpi1z+Ykd0myR5Ird9C2bftcfQAAAHAjLfp3FLfxl929NdD9ZZJ3JDk7
Q1jcak2SyzMEwjU7aEuGgHh5ki3b6WOH1q9ff+OPAFgUmzZtWu4SYIc2bNiQzZs3L3cZALAkljoo
nl5VvzkuNHNIki8l+WKSN1TVHZLslmTfJBuSnJthcZrzkjwpydndvbmqtlTVA5JcnOQJSY5Ncl2S
t1TV8Un2TrJLd39nZ8WsW7duoY8PuInWrFmTL56/3FXA9u23335Zu3btcpcBAAtmRwNnSxUUZ8af
L0nyzqq6Jsk3khzR3d+rqhOSnJNhKuzR3X11Vb07yUlVdU6Sq5M8b1YfH05yuyRnbF3ddNzvc2Mf
Ry7RcQEAAKw4q2ZmZna+1wq0fv36GSOKcMtx4YUX5v0ffkHufs87Lncp8CO+/c3/zK8//4NGFAFY
UdavX59169atmmvbYq96CgAAwK2MoAgAAMCEoAgAAMCEoAgAAMCEoAgAAMCEoAgAAMCEoAgAAMCE
oAgAAMCEoAgAAMCEoAgAAMCEoAgAAMCEoAgAAMCEoAgAAMCEoAgAAMCEoAgAAMCEoAgAAMCEoAgA
AMCEoAgAAMCEoAgAAMCEoAgAAMCEoAgAAMCEoAgAAMCEoAgAAMCEoAgAAMCEoAgAAMCEoAgAAMCE
oAgAAMCEoAgAAMCEoAgAAMCEoAgAAMCEoAgAAMCEoAgAAMCEoAgAAMCEoAgAAMCEoAgAAMCEoAgA
AMCEoAgAAMCEoAgAAMCEoAgAAMCEoAgAAMCEoAgAAMDEToNiVb1jjraTFqccAAAAltuu29tQVScm
eWCSh1fVfts8566LXRgAAADLY7tBMckbktwvyQlJjk2yamy/NskFi1sWAAAAy2W7QbG7L05ycZL9
q2qPJHfJDWHxzkm+s/jlAQAAsNR2NKKYJKmqo5P8ToZgODNr0/0XqygAAACWz06DYpIXJXlgd397
sYsBAABg+c3n9hibknx3sQsBAADglmE+I4oXJflsVX0qydVj20x3v34+L1BVByR5U3c/rqp+MskH
klyfZEOSl3X3TFUdnuSIDAvlHNfdp1bV7kk+lOTuSTYneWF3X1pVj0zy9nHfM7fWUVWvTfLksf0V
3X3efOoDAABgaj4jiv+e5PQkW8bHq3LDojY7VFWvSvLeJHcYm96W5OjuPnjs42lVda8kRyV5VJJD
k7yxqlYneWmS88d9T05yzNjHe5I8t7sfneSAqnpIVT0sycHdfUCS5yR553zqAwAA4EftdESxu4+9
Gf1flOSZST44Pn5Yd589/n5akickuS7Jud19TZJrquqiJPsnOSjJm8d9T0/y6qpak2T1uCJrkpyR
5JAMI51njvVeUlW7VtWe3X3ZzagdAADgNmk+q55eP0fzf3T3fXf23O7+WFXtM6tp9kjk5gy33Ngj
yRXbab9yB21b2x+Q5AdJLpujD0ERAADgRprPiOIPp6dW1e2TPD3DNNGbYnbo3CPJ5RmC35pZ7Wvm
aJ+rbXYfW7bTxw6tX7/+xlUPLJpNmzYtdwmwQxs2bMjmzZuXuwwAWBLzWczmh8bpoadU1TE73Xlu
X6mqx3T3WUmelOSTSb6Y5A1VdYckuyXZN8NCN+dmWJzmvHHfs7t7c1VtqaoHJLk4w9TVYzNMX31L
VR2fZO8ku3T3d3ZWzLp1627iYQALbc2aNfni+ctdBWzffvvtl7Vr1y53GQCwYHY0cDafqacvnPVw
VZKfzg2rn87XzPjzt5K8d1ys5oIkHx1XPT0hyTkZFtc5uruvrqp3Jzmpqs4ZX+95Yx8vSfLhJLdL
csbW1U3H/T439nHkjawPAACA0XxGFB+XG4LeTJJLkzx7vi/Q3RszTlXt7q8leewc+5yY5MRt2q5K
8qtz7PuFJAfO0f66JK+bb10AAADMbT7fUfy1cQSwxv03jFNQAQAAWIF2eh/Fqnp4kguTnJTk/Uk2
jTe9BwAAYAWaz9TTE5I8e5zymTEknpDk5xazMAAAAJbHTkcUk9xpa0hMku7+fIbVSQEAAFiB5hMU
v1tVT9/6oKqeETeyBwAAWLHmM/X0iCQfr6r3Zbg9xvVJDlrUqgAAAFg28xlRfGKS/0zyExlubXFZ
5rjFBQAAACvDfILii5M8uru/393/mOShSY5a3LIAAABYLvMJirsm2TLr8ZYM008BAABYgebzHcW/
SvKpqvrzDN9RfGaSv1nUqgAAAFg2Ox1R7O7fznDfxEpy/yR/0N3HLHZhAAAALI/5jCimu09Jcsoi
1wIAAMAtwHy+owgAAMBtiKAIAADAhKAIAADAhKAIAADAhKAIAADAhKAIAADAhKAIAADAhKAIAADA
hKAIAADAhKAIAADAhKAIAADAxK7LXcBKsWXLlmzcuHG5y4A57bPPPlm9evVylwEAwK2EoLhANm7c
mPXH/UH2vuuey10KTFxy+WXJMS/P2rVrl7sUAABuJQTFBbT3XffMA/e6x3KXAQAAcLP4jiIAAAAT
giIAAAATgiIAAAATgiIAAAATgiIAAAATgiIAAAATgiIAAAATgiIAAAATgiIAAAATgiIAAAATgiIA
AAATgiIAAAATgiIAAAATgiIAAAATgiIAAAATgiIAAAATgiIAAAATgiIAAAATgiIAAAATgiIAAAAT
giIAAAATgiIAAAATuy7Hi1bVl5NcMT78epI3JvlAkuuTbEjysu6eqarDkxyR5Nokx3X3qVW1e5IP
Jbl7ks1JXtjdl1bVI5O8fdz3zO5+/VIeEwAAwEqx5COKVbVbknT348b//nuStyU5ursPTrIqydOq
6l5JjkryqCSHJnljVa1O8tIk54/7npzkmLHr9yR5bnc/OskBVfWQJT0wAACAFWI5RhR/Nskdq+qM
8fV/N8nDuvvscftpSZ6Q5Lok53b3NUmuqaqLkuyf5KAkbx73PT3Jq6tqTZLV3X3x2H5GkkOS/MNS
HBAAAMBKshzfUfx+kt/v7kOTvCTJh7fZvjnJXZLskRump27bfuUO2ma3AwAAcCMtx4jihUkuSpLu
/lpVXZbkobO275Hk8gzBb82s9jVztM/VNruPHVq/fv1NO4I5bNq0KfdYsN5gYW3YsCGbN29e7jJ2
aNOmTctdAuzQreE8AoCFshxB8bAMU0hfVlX3yRDwzqyqx3T3WUmelOSTSb6Y5A1VdYckuyXZN8NC
N+cmeXKS88Z9z+7uzVW1paoekOTiDFNXj91ZIevWrVuwg1qzZk2+9RkzXbll2m+//bJ27drlLmOH
1qxZky+ev9xVwPbdGs4jALgxdjRwthxB8X1J/qSqtn4n8bAklyV577hYzQVJPjquenpCknMyTJE9
uruvrqp3Jzmpqs5JcnWS5439bJ3GerskZ3T3eUt3SAAAACvHkgfF7r42yQvm2PTYOfY9McmJ27Rd
leRX59j3C0kOXJgqAQAAbruWYzEbAAAAbsEERQAAACYERQAAACYERQAAACYERQAAACYERQAAACYE
RQAAACYERQAAACYERQAAACYERQAAACYERQAAACYERQAAACYERQAAACYERQAAACYERQAAACYERQAA
ACYERQAAACYERQAAACYERQAAACYERQAAACYERQAAACYERQAAACYERQAAACYERQAAACYERQAAACYE
RQAAACYERQAAACYERQAAACYERQAAACYERQAAACYERQAAACYERQAAACYERQAAACYERQAAACYERQAA
ACYERQAAACYERQAAACYERQAAACYERQAAACYERQAAACYERQAAACYERQAAACYERQAAACYERQAAACYE
RQAAACYERQAAACYERQAAACZ2Xe4CFkpV7ZLkXUn2T3J1khd1978sb1UAAAC3PismKCZ5epLV3f2o
qjogyVvHNgBY8bZs2ZKNGzcudxmwXfvss09Wr1693GUA87SSguJBSU5Pku7+QlU9fJnrAYAls3Hj
xjznj/4wu++153KXAj/iqksvy0de/BtZu3btcpcCzNNKCop7JLly1uPrqmqX7r5+uQoCgKW0+157
5k73uudylwHACrCSguKVSdbMerzkIfGSyy9bypeDebnk8styj+UuYp6+c9kPlrsEmNOt5W/zqktd
h7hlujX9bV544YXLXQLMaalH5FfNzMws6Qsulqp6ZpJf7u7DquqRSV7d3U/Z3v7r169fGQcOAABw
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
AJj4/3nlOfr2s/LzAAAAAElFTkSuQmCC
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">
In&nbsp;[92]:
</div>
<div class="inner_cell">
    <div class="input_area">
<div class="highlight"><pre><span class="c"># 1.3 Process remaining &#39;object&#39; type variables</span>
<span class="c"># We will create a corresponding unique numerical value </span>
<span class="c"># for each non-numerical value in a column.</span>
<span class="n">ID_col</span> <span class="o">=</span> <span class="s">&#39;user_id&#39;</span>
<span class="n">target_col</span> <span class="o">=</span> <span class="s">&#39;country_destination&#39;</span>

<span class="kn">from</span> <span class="nn">sklearn</span> <span class="kn">import</span> <span class="n">preprocessing</span>

<span class="k">for</span> <span class="n">f</span> <span class="ow">in</span> <span class="n">fullData</span><span class="o">.</span><span class="n">columns</span><span class="p">:</span>
    <span class="k">if</span> <span class="n">f</span> <span class="o">==</span> <span class="n">target_col</span> <span class="ow">or</span> <span class="n">f</span> <span class="o">==</span> <span class="n">ID_col</span> <span class="ow">or</span> <span class="n">f</span> <span class="o">==</span> <span class="s">&#39;Type&#39;</span><span class="p">:</span> <span class="k">continue</span>
    <span class="k">if</span> <span class="n">fullData</span><span class="p">[</span><span class="n">f</span><span class="p">]</span><span class="o">.</span><span class="n">dtype</span> <span class="o">==</span> <span class="s">&#39;object&#39;</span><span class="p">:</span>
        <span class="n">lbl</span> <span class="o">=</span> <span class="n">preprocessing</span><span class="o">.</span><span class="n">LabelEncoder</span><span class="p">()</span>
        <span class="n">lbl</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">np</span><span class="o">.</span><span class="n">unique</span><span class="p">(</span><span class="nb">list</span><span class="p">(</span><span class="n">fullData</span><span class="p">[</span><span class="n">f</span><span class="p">]</span><span class="o">.</span><span class="n">values</span><span class="p">)))</span>
        <span class="n">fullData</span><span class="p">[</span><span class="n">f</span><span class="p">]</span> <span class="o">=</span> <span class="n">lbl</span><span class="o">.</span><span class="n">transform</span><span class="p">(</span><span class="nb">list</span><span class="p">(</span><span class="n">fullData</span><span class="p">[</span><span class="n">f</span><span class="p">]</span><span class="o">.</span><span class="n">values</span><span class="p">))</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">
In&nbsp;[93]:
</div>
<div class="inner_cell">
    <div class="input_area">
<div class="highlight"><pre><span class="n">fullData</span><span class="o">.</span><span class="n">dtypes</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">
    Out[93]:</div>


<div class="output_text output_subarea output_pyout">
<pre>
Type                        object
affiliate_channel            int64
affiliate_provider           int64
age                        float64
country_destination         object
date_first_booking           int64
first_affiliate_tracked      int64
first_browser                int64
first_device_type            int64
gender                       int64
id                           int64
language                     int64
signup_app                   int64
signup_flow                  int64
signup_method                int64
booked                       int64
Year                         int64
Month                        int64
dtype: object
</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">
In&nbsp;[94]:
</div>
<div class="inner_cell">
    <div class="input_area">
<div class="highlight"><pre><span class="c"># 1.4 Particular process of numerical variable &#39;age&#39;</span>
<span class="c"># 1.4.1 Find and remove outliers by assigning all age values &gt; 100 to NaN, </span>
<span class="c"># these NaN values will be replaced with real ages below</span>
<span class="n">a</span> <span class="o">=</span> <span class="n">fullData</span><span class="o">.</span><span class="n">age</span><span class="o">.</span><span class="n">values</span>
<span class="n">fullData</span><span class="p">[</span><span class="s">&#39;age&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">where</span><span class="p">(</span><span class="n">a</span> <span class="o">&gt;</span><span class="mi">100</span><span class="p">,</span> <span class="n">np</span><span class="o">.</span><span class="n">nan</span><span class="p">,</span> <span class="n">a</span><span class="p">)</span>

<span class="c"># get average, std, and number of NaN values in fullData</span>
<span class="n">average_age</span>   <span class="o">=</span> <span class="n">fullData</span><span class="o">.</span><span class="n">age</span><span class="o">.</span><span class="n">mean</span><span class="p">()</span>
<span class="n">std_age</span>       <span class="o">=</span> <span class="n">fullData</span><span class="o">.</span><span class="n">age</span><span class="o">.</span><span class="n">std</span><span class="p">()</span>
<span class="n">count_nan_age</span> <span class="o">=</span> <span class="n">fullData</span><span class="o">.</span><span class="n">age</span><span class="o">.</span><span class="n">isnull</span><span class="p">()</span><span class="o">.</span><span class="n">sum</span><span class="p">()</span>
<span class="k">print</span> <span class="n">count_nan_age</span>

<span class="c"># generate random numbers between (mean - std) &amp; (mean + std)</span>
<span class="n">rand</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">random</span><span class="o">.</span><span class="n">randint</span><span class="p">(</span><span class="n">average_age</span> <span class="o">-</span> <span class="n">std_age</span><span class="p">,</span> <span class="n">average_age</span> <span class="o">+</span> <span class="n">std_age</span><span class="p">,</span> <span class="n">size</span> <span class="o">=</span> <span class="n">count_nan_age</span><span class="p">)</span>

<span class="c"># fill NaN values in Age column with random values generated</span>
<span class="n">fullData</span><span class="p">[</span><span class="s">&quot;age&quot;</span><span class="p">][</span><span class="n">np</span><span class="o">.</span><span class="n">isnan</span><span class="p">(</span><span class="n">fullData</span><span class="o">.</span><span class="n">age</span><span class="p">)]</span> <span class="o">=</span> <span class="n">rand</span>

<span class="c"># convert type to integer</span>
<span class="n">fullData</span><span class="p">[</span><span class="s">&#39;age&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">fullData</span><span class="o">.</span><span class="n">age</span><span class="o">.</span><span class="n">astype</span><span class="p">(</span><span class="nb">int</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>
119556

</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">
In&nbsp;[96]:
</div>
<div class="inner_cell">
    <div class="input_area">
<div class="highlight"><pre><span class="c"># 1.4.2 Check our converting, see if it makes sense</span>
<span class="n">fig</span><span class="p">,</span> <span class="p">(</span><span class="n">axis1</span><span class="p">,</span> <span class="n">axis2</span><span class="p">)</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">subplots</span><span class="p">(</span><span class="mi">1</span><span class="p">,</span><span class="mi">2</span><span class="p">,</span><span class="n">figsize</span><span class="o">=</span><span class="p">(</span><span class="mi">15</span><span class="p">,</span><span class="mi">4</span><span class="p">))</span>

<span class="c"># frequency for age values(in case there was a booking)</span>
<span class="n">fullData</span><span class="p">[</span><span class="s">&#39;age&#39;</span><span class="p">][</span><span class="n">fullData</span><span class="o">.</span><span class="n">country_destination</span> <span class="o">!=</span> <span class="s">&#39;NDF&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">hist</span><span class="p">(</span><span class="n">ax</span><span class="o">=</span><span class="n">axis1</span><span class="p">)</span>

<span class="c"># cut age values into ranges </span>
<span class="n">fullData</span><span class="p">[</span><span class="s">&#39;age_range&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">cut</span><span class="p">(</span><span class="n">fullData</span><span class="o">.</span><span class="n">age</span><span class="p">,</span> <span class="p">[</span><span class="mi">0</span><span class="p">,</span> <span class="mi">20</span><span class="p">,</span> <span class="mi">40</span><span class="p">,</span> <span class="mi">60</span><span class="p">,</span> <span class="mi">80</span><span class="p">,</span> <span class="mi">100</span><span class="p">])</span>

<span class="c"># frequency of country_destination for every age range</span>
<span class="n">sns</span><span class="o">.</span><span class="n">countplot</span><span class="p">(</span><span class="n">x</span><span class="o">=</span><span class="s">&quot;age_range&quot;</span><span class="p">,</span><span class="n">hue</span><span class="o">=</span><span class="s">&quot;country_destination&quot;</span><span class="p">,</span> <span class="n">data</span><span class="o">=</span>
              <span class="n">fullData</span><span class="p">[</span><span class="n">fullData</span><span class="o">.</span><span class="n">country_destination</span> <span class="o">!=</span> <span class="s">&#39;NDF&#39;</span><span class="p">],</span> <span class="n">palette</span><span class="o">=</span><span class="s">&quot;husl&quot;</span><span class="p">,</span> 
              <span class="n">ax</span><span class="o">=</span><span class="n">axis2</span><span class="p">)</span>

<span class="c"># drop age_range</span>
<span class="n">fullData</span><span class="o">.</span><span class="n">drop</span><span class="p">([</span><span class="s">&#39;age_range&#39;</span><span class="p">],</span> <span class="n">axis</span><span class="o">=</span><span class="mi">1</span><span class="p">,</span> <span class="n">inplace</span><span class="o">=</span><span class="bp">True</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>


<div class="output_png output_subarea ">
<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAA3UAAAERCAYAAADc9I5FAAAABHNCSVQICAgIfAhkiAAAAAlwSFlz
AAALEgAACxIB0t1+/AAAIABJREFUeJzs3Xl8VNX9//HXgAwhEBYhCC44IPrRihSNRURF3KtfrUtF
lDZ1KagVLX5rXaC4lCJoRap8S13ABQE3tHWjCn6tFcSvaPOrCrV81JqJoqiALGFLQpLfH3eCCUw2
GDIzmffz8eBB7pmTcz/nzmTufOaee06osrISERERERERSU8tkh2AiIiIiIiI7DwldSIiIiIiImlM
SZ2IiIiIiEgaU1InIiIiIiKSxpTUiYiIiIiIpDEldSIiIiIiImlsj/oqmNlo4CygFfBHYBHwKFAB
LAVGunulmY0ALge2AuPdfa6ZtQFmAblAMXCxu68yswHAPbG68919XMJ7JiIispuZ2f8D1sU2PwUm
onOkiIg0sTqv1JnZYOBodx8IDAZ6AXcDY9x9EBACzjazbsA1wEDgNGCimYWBXwDvx+o+BoyNNX0/
cJG7HwscZWb9Et0xERGR3cnMsgDc/YTYv58Dk9E5UkREmlh9V+pOBZaY2XNAe+B64OfuviD2+Mux
OuXAIncvA8rM7BOgL3AMcGes7ivAzWaWA4TdvTBWPg84GXgvQX0SERFpCt8Hss1sHsH59DfAETpH
iohIU6svqcsF9gPOJLhK9yLBN49VioEOBAnfulrK19dRVlXea+fCFxERSZqNwF3u/pCZHUiQmFWn
c6SIiDSJ+iZKWUUwnn+ru38EbCE46VRpD6wlOAHlVCvPiVMer6x6GyIiIunkI2A2gLt/DKwG9qr2
uM6RIiLSJOq7UvcmMAqYbGZ7A9nAa2Z2vLu/AZwOvAa8A9xuZq2BLOAQghvEFwFnAO/G6i5w92Iz
KzWzXkAhwdCU2+oLtKCgoHIn+iciImkoLy8vVH+tpLuUYBjlyNg5MgeY39TnSJ0fRUQyS7xzZJ1J
XWx2rkFm9g7BVb2rgCgwLXaT94fAM7GZvaYAC2P1xrh7iZndB8wws4VACTAs1vSVBN9utgTmufu7
DexAQ6o1OwUFBep7hsrk/mdy3yGz+19QUJDsEBrqIeARM6u6h+5Sgqt1TX6OzNTXiohIpqntHFnv
kgbufmOc4sFx6k0Hpm9Xthm4IE7dxcDR9e1bREQkVbn7ViA/zkOD49TVOVJERHYbLT4uIiIiIiKS
xpTUiYiIiIiIpDEldSIiIiIiImlMSZ2IiIiIiEgaU1InIiIiIiKSxuqd/VIEoLS0lGg02uT7LSoq
Iicnh0gkQjgcbvL9i4iIiIikOiV10iDRaJT80Y+T3aFrk+970+wPmDlxGAcddFCT71tERHY0b948
Bg4cSE5Ozi63dc455/Dcc881uP6cOXMYMmQICxcuZN26dZx55pkN/t133nmHbt26kZ2dzSOPPML1
11+/MyGLiKQcJXXSYNkdutKu0z7JDkNERJJs1qxZ5OXlJSSpa6yHH36YIUOGcNxxxzX6d//85z9z
0UUX0aNHDyV0ItKsKKkTERFp5jZs2MD111/PmjVraNWqFddffz0TJkxgjz32oHv37kyYMIEXX3yR
VatWcfnll7N48WL++te/cvnll3PDDTew5557Eo1GufTSS+nWrRvLli1jzJgxDB8+nLvuuotWrVox
aNAgWrRoweWXX040GmXy5MlMmTIlbjx33nknBQUFRCIRysvLAVi4cCFTp04lFApx4oknMmLECB59
9FHmzZvH1q1bGTFiBJs2bWLFihXccsstHH744axcuZJ+/frx0EMPEQqF+Pzzzxk9ejTHHnss06ZN
46233mL9+vWccMIJnHrqqbz55pt89NFH3HXXXUycOJHp06dz33338frrrwOQn5/PWWedRX5+Poce
eihLliyhffv2/OlPfyIUCjXZ8yUi0liaKEVERKSZe+KJJzjyyCN58sknueKKKxg3bhyTJ09m1qxZ
7LPPPjz77LM1kpbqP69YsYI//OEPPPTQQzz22GMMHDiQgw8+mIkTJ1JZWUlWVhaPP/44w4YN43//
938BePHFFzn33HPjxrJkyRKi0ShPP/00V199NVu2bKGyspI777yThx56iMcff5yCggL+85//8PLL
LzNp0iQefvhhKioqOOecc+jevTvjxo2r0eb69eu5//77GT9+PE888QQVFRWEQiEeeeQRnnjiCV54
4QUOOuggjjvuOG677TaysrIAWLZsGQUFBTz99NPMnDmTBx98kOLiYgAGDRrE7NmzKS0txd0T+nyI
iCSakjoREZFmbvny5fTt2xeAY489ls2bN7P33nsDcMQRR/Dpp5/WqF9RUbHt5549e7LHHnvQtWtX
SkpKatQLhUL07NkTgPbt29OtWzf+85//8NZbbzFo0KC4sRQVFXHooYcC0KNHD/bcc0/WrFnDN998
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
iYikFl2pExERkZTyySefkJ+fv237v//7v7eVrVu3jpKSEs466yzOPffcJEYpIpI6lNSJiIhISund
u3eNoZbLly/fVlZSUsKVV15J586dadFCA45EREDDL0VERCSNtG7dmkmTJjF16lSWLVuW7HBERFKC
rtSJiIhIrVau3tzkbYVCoTrLOnfuzI033sitt97KU089lbD4RETSlZI6ERERiSsSiXDZr55OeJt1
2XfffXnyySfrLTvrrLM466yzEhqbiEi6UlInIiIicYXD4TrXlBMRkdSge+pERERERETSmJI6ERER
ERGRNKakTkREREREJI0pqRMREREREUljmihFRERE4iotLSUajSa0zUgkQjgcTmibIiKZTkmdiIiI
xBWNRrn9j0Po1CUrIe2tWbWF31w9p94ZNT/++GMmTZrE5s2b2bRpE8cffzzXXHMNAH/961/5zW9+
w7x58+jatWtC4hIRSXdK6kRERKRWnbpk0WWv7Cbb3/r16/nVr37F1KlT6dGjBxUVFYwaNYqnnnqK
oUOHMmfOHH72s5/x9NNPc/XVVzdZXCIiqUz31ImIiEjKeO211zj66KPp0aMHAC1atODOO+/kvPPO
4/PPP2f9+vUMHz6c559/nq1btyY5WhGR1KCkTkRERFLGypUr2XfffWuUZWdn06pVK5555hnOO+88
cnJy6NevH/Pnz09SlCIiqUXDL0VERCRl7L333vzrX/+qUbZ8+XK+/PJLXnzxRfbdd19ef/111q1b
x+zZsznjjDOSFKmISOpoUFJnZl2BAuAkoAJ4NPb/UmCku1ea2QjgcmArMN7d55pZG2AWkAsUAxe7
+yozGwDcE6s7393HJbZbIiIiko4GDx7MAw88wLBhw9hvv/0oKyvjjjvuoH///vTt25d77rlnW93T
TjsNd8fMkhixiEjy1ZvUmVkr4AFgIxACJgNj3H2Bmd0HnG1mbwPXAHlAG+BNM3sV+AXwvruPM7Oh
wFjgWuB+4Fx3LzSzuWbWz93f2x0dFBERkZ23ZtWWJm2rXbt23HHHHYwdO5aKigo2btzIiSeeyFtv
vcXQoUNr1B0yZAizZ89m3Dh9Nywima0hV+ruAu4DRse2j3D3BbGfXwZOBcqBRe5eBpSZ2SdAX+AY
4M5Y3VeAm80sBwi7e2GsfB5wMqCkTkREJIVEIhF+c/WchLdZn0MPPZQZM2bUW2/48OEJiEhEJP3V
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
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">
In&nbsp;[97]:
</div>
<div class="inner_cell">
    <div class="input_area">
<div class="highlight"><pre><span class="n">fullData</span><span class="o">.</span><span class="n">dtypes</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">
    Out[97]:</div>


<div class="output_text output_subarea output_pyout">
<pre>
Type                       object
affiliate_channel           int64
affiliate_provider          int64
age                         int64
country_destination        object
date_first_booking          int64
first_affiliate_tracked     int64
first_browser               int64
first_device_type           int64
gender                      int64
id                          int64
language                    int64
signup_app                  int64
signup_flow                 int64
signup_method               int64
booked                      int64
Year                        int64
Month                       int64
dtype: object
</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h4 id="step-3-data-modelling">Step 3 : Data modelling</h4>
<ul>
<li>Final drop of unnecessary columns </li>
<li>Defining traning and testing sets</li>
<li>Convert &#39;target_col&#39; to numerical values</li>
<li>Drop variables that are not useful for prediction</li>
<li>Select a model and use the model to predict</li>
</ul>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">
In&nbsp;[98]:
</div>
<div class="inner_cell">
    <div class="input_area">
<div class="highlight"><pre><span class="c"># Final drop of unnecessary columns</span>
<span class="n">fullData</span> <span class="o">=</span> <span class="n">fullData</span><span class="o">.</span><span class="n">drop</span><span class="p">([</span><span class="s">&#39;booked&#39;</span><span class="p">,</span><span class="s">&#39;id&#39;</span><span class="p">,</span><span class="s">&#39;Year&#39;</span><span class="p">,</span><span class="s">&#39;Month&#39;</span><span class="p">],</span><span class="n">axis</span><span class="o">=</span><span class="mi">1</span><span class="p">)</span>
<span class="n">fullData</span><span class="o">.</span><span class="n">dtypes</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">
    Out[98]:</div>


<div class="output_text output_subarea output_pyout">
<pre>
Type                       object
affiliate_channel           int64
affiliate_provider          int64
age                         int64
country_destination        object
date_first_booking          int64
first_affiliate_tracked     int64
first_browser               int64
first_device_type           int64
gender                      int64
language                    int64
signup_app                  int64
signup_flow                 int64
signup_method               int64
dtype: object
</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">
In&nbsp;[99]:
</div>
<div class="inner_cell">
    <div class="input_area">
<div class="highlight"><pre><span class="c"># Defining traning and testing sets</span>
<span class="n">X_train</span> <span class="o">=</span> <span class="n">fullData</span><span class="o">.</span><span class="n">ix</span><span class="p">[</span><span class="n">fullData</span><span class="o">.</span><span class="n">Type</span> <span class="o">==</span> <span class="s">&#39;Train&#39;</span><span class="p">,</span><span class="s">&#39;Type&#39;</span><span class="p">:]</span>

<span class="n">Y_train</span> <span class="o">=</span> <span class="n">X_train</span><span class="p">[</span><span class="s">&quot;country_destination&quot;</span><span class="p">]</span>
<span class="n">X_train</span> <span class="o">=</span> <span class="n">X_train</span><span class="o">.</span><span class="n">drop</span><span class="p">([</span><span class="s">&quot;Type&quot;</span><span class="p">,</span> <span class="s">&#39;country_destination&#39;</span><span class="p">],</span><span class="n">axis</span><span class="o">=</span><span class="mi">1</span><span class="p">)</span>

<span class="k">print</span><span class="p">(</span><span class="s">&#39;---------&#39;</span><span class="p">)</span>
<span class="n">X_train</span><span class="o">.</span><span class="n">info</span><span class="p">()</span>
<span class="k">print</span><span class="p">(</span><span class="s">&#39;---------&#39;</span><span class="p">)</span>
<span class="n">X_test</span>  <span class="o">=</span> <span class="n">fullData</span><span class="o">.</span><span class="n">ix</span><span class="p">[</span><span class="n">fullData</span><span class="o">.</span><span class="n">Type</span> <span class="o">==</span> <span class="s">&#39;Test&#39;</span><span class="p">,</span><span class="s">&#39;Type&#39;</span><span class="p">:]</span>
<span class="n">X_test</span> <span class="o">=</span> <span class="n">X_test</span><span class="o">.</span><span class="n">drop</span><span class="p">([</span><span class="s">&quot;Type&quot;</span><span class="p">,</span> <span class="s">&#39;country_destination&#39;</span><span class="p">],</span><span class="n">axis</span><span class="o">=</span><span class="mi">1</span><span class="p">)</span>
<span class="n">X_test</span><span class="o">.</span><span class="n">info</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>
---------
&lt;class &apos;pandas.core.frame.DataFrame&apos;&gt;
Int64Index: 213451 entries, 0 to 213450
Data columns (total 12 columns):
affiliate_channel          213451 non-null int64
affiliate_provider         213451 non-null int64
age                        213451 non-null int64
date_first_booking         213451 non-null int64
first_affiliate_tracked    213451 non-null int64
first_browser              213451 non-null int64
first_device_type          213451 non-null int64
gender                     213451 non-null int64
language                   213451 non-null int64
signup_app                 213451 non-null int64
signup_flow                213451 non-null int64
signup_method              213451 non-null int64
dtypes: int64(12)
memory usage: 21.2 MB
---------
&lt;class &apos;pandas.core.frame.DataFrame&apos;&gt;
Int64Index: 62096 entries, 0 to 62095
Data columns (total 12 columns):
affiliate_channel          62096 non-null int64
affiliate_provider         62096 non-null int64
age                        62096 non-null int64
date_first_booking         62096 non-null int64
first_affiliate_tracked    62096 non-null int64
first_browser              62096 non-null int64
first_device_type          62096 non-null int64
gender                     62096 non-null int64
language                   62096 non-null int64
signup_app                 62096 non-null int64
signup_flow                62096 non-null int64
signup_method              62096 non-null int64
dtypes: int64(12)
memory usage: 6.2 MB

</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">
In&nbsp;[100]:
</div>
<div class="inner_cell">
    <div class="input_area">
<div class="highlight"><pre><span class="c"># Convert &#39;country_destination&#39; to numerical values</span>
<span class="c"># Get the name list of all countries </span>
<span class="n">range_countries</span> <span class="o">=</span> <span class="n">fullData</span><span class="o">.</span><span class="n">country_destination</span><span class="o">.</span><span class="n">value_counts</span><span class="p">()</span><span class="o">.</span><span class="n">index</span>

<span class="c"># Get the dictionary of the target column</span>
<span class="n">country_num_dic</span> <span class="o">=</span> <span class="nb">dict</span><span class="p">(</span><span class="nb">zip</span><span class="p">(</span><span class="n">range_countries</span><span class="p">,</span><span class="nb">range</span><span class="p">(</span><span class="nb">len</span><span class="p">(</span><span class="n">range_countries</span><span class="p">))))</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">
In&nbsp;[101]:
</div>
<div class="inner_cell">
    <div class="input_area">
<div class="highlight"><pre><span class="k">print</span> <span class="n">country_num_dic</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>
{&apos;FR&apos;: 3, &apos;NL&apos;: 9, &apos;PT&apos;: 11, &apos;CA&apos;: 7, &apos;DE&apos;: 8, &apos;IT&apos;: 4, &apos;US&apos;: 1, &apos;NDF&apos;: 0, &apos;other&apos;: 2, &apos;AU&apos;: 10, &apos;GB&apos;: 5, &apos;ES&apos;: 6}

</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">
In&nbsp;[102]:
</div>
<div class="inner_cell">
    <div class="input_area">
<div class="highlight"><pre><span class="c"># Create training labels</span>
<span class="n">Y_train</span>    <span class="o">=</span> <span class="n">train</span><span class="p">[</span><span class="s">&#39;country_destination&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">map</span><span class="p">(</span><span class="n">country_num_dic</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">
In&nbsp;[103]:
</div>
<div class="inner_cell">
    <div class="input_area">
<div class="highlight"><pre><span class="c"># Select the model &#39;Random Forests&#39;</span>
<span class="n">random_forest</span> <span class="o">=</span> <span class="n">RandomForestClassifier</span><span class="p">(</span><span class="n">n_estimators</span><span class="o">=</span><span class="mi">100</span><span class="p">)</span>
<span class="n">random_forest</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">X_train</span><span class="p">,</span> <span class="n">Y_train</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">
    Out[103]:</div>


<div class="output_text output_subarea output_pyout">
<pre>
RandomForestClassifier(bootstrap=True, class_weight=None, criterion=&apos;gini&apos;,
            max_depth=None, max_features=&apos;auto&apos;, max_leaf_nodes=None,
            min_samples_leaf=1, min_samples_split=2,
            min_weight_fraction_leaf=0.0, n_estimators=100, n_jobs=1,
            oob_score=False, random_state=None, verbose=0,
            warm_start=False)
</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">
In&nbsp;[104]:
</div>
<div class="inner_cell">
    <div class="input_area">
<div class="highlight"><pre><span class="c"># Use &#39;Random Forest&#39; model to predict on the training set</span>
<span class="n">Y_pred</span> <span class="o">=</span> <span class="n">random_forest</span><span class="o">.</span><span class="n">predict</span><span class="p">(</span><span class="n">X_test</span><span class="p">)</span>

<span class="n">random_forest</span><span class="o">.</span><span class="n">score</span><span class="p">(</span><span class="n">X_train</span><span class="p">,</span> <span class="n">Y_train</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">
    Out[104]:</div>


<div class="output_text output_subarea output_pyout">
<pre>
0.99654721692566439
</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">
In&nbsp;[105]:
</div>
<div class="inner_cell">
    <div class="input_area">
<div class="highlight"><pre><span class="c"># Use &#39;Random Forest&#39; model to predict on the testing set</span>
<span class="n">random_forest</span><span class="o">.</span><span class="n">score</span><span class="p">(</span><span class="n">X_test</span><span class="p">,</span> <span class="n">Y_pred</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">
    Out[105]:</div>


<div class="output_text output_subarea output_pyout">
<pre>
1.0
</pre>
</div>

</div>

</div>
</div>

</div>
    </div>
  </div>
</body>

