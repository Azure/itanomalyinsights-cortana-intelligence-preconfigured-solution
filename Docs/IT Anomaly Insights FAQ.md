 StackEdit – Editor               // Use ?debug to serve original JavaScript 
files instead of minified window.baseDir = 'res'; if 
(!/(\?|&)debug($|&)/.test(location.search)) { window.baseDir += '-min'; } 
window.require = { baseUrl: window.baseDir, deps: ['main'] };   
MathJax.Hub.Config({ skipStartupTypeset: true, "HTML-CSS": { preferredFont: 
"TeX", availableFonts: [ "TeX" ], linebreaks: { automatic: true }, EqnChunk: 10, 
imageFont: null }, tex2jax: { inlineMath: [["$","$"],["\\\\(","\\\\)"]], 
displayMath: [["$$","$$"],["\\[","\\]"]], processEscapes: true }, TeX: 
$.extend({ noUndefined: { attributes: { mathcolor: "red", mathbackground: 
"#FFEEEE", mathsize: "90%" } }, Safe: { allow: { URLs: "safe", classes: "safe", 
cssIDs: "safe", styles: "safe", fontsize: "all" } } }, undefined), messageStyle: 
"none" }); @media (min-width: 0px) { #wmd-input { font-size: 16px; }
 #preview-contents { font-size: 16px; } }@media (min-width: 600px) { #wmd-input 
{ font-size: 17px; } #preview-contents { font-size: 17px; } }@media (min-width: 
1200px) { #wmd-input { font-size: 18px; } #preview-contents { font-size: 18px; }
 }@keyframes working-indicator-bar0 { 0% { opacity:0.25; } 0.01% { opacity:0.25; 
} 0.02% { opacity:1; } 50.01% { opacity:0.25; } 100% { opacity:0.25; }
 }@-webkit-keyframes working-indicator-bar0 { 0% { opacity:0.25; } 0.01% { 
opacity:0.25; } 0.02% { opacity:1; } 50.01% { opacity:0.25; } 100% { 
opacity:0.25; } }@keyframes working-indicator-bar1 { 0% { opacity:0.25; } 20.01% 
{ opacity:0.25; } 20.02% { opacity:1; } 70.01% { opacity:0.25; } 100% { 
opacity:0.25; } }@-webkit-keyframes working-indicator-bar1 { 0% { opacity:0.25; 
} 20.01% { opacity:0.25; } 20.02% { opacity:1; } 70.01% { opacity:0.25; } 100% { 
opacity:0.25; } }@keyframes working-indicator-bar2 { 0% { opacity:0.25; } 40.01% 
{ opacity:0.25; } 40.02% { opacity:1; } 90.01% { opacity:0.25; } 100% { 
opacity:0.25; } }@-webkit-keyframes working-indicator-bar2 { 0% { opacity:0.25; 
} 40.01% { opacity:0.25; } 40.02% { opacity:1; } 90.01% { opacity:0.25; } 100% { 
opacity:0.25; } }.MathJax_Hover_Frame {border-radius: .25em; 
-webkit-border-radius: .25em; -moz-border-radius: .25em; -khtml-border-radius: 
.25em; box-shadow: 0px 0px 15px #83A; -webkit-box-shadow: 0px 0px 15px #83A; 
-moz-box-shadow: 0px 0px 15px #83A; -khtml-box-shadow: 0px 0px 15px #83A; 
border: 1px solid #A6D ! important; display: inline-block; position: absolute}
 .MathJax_Menu_Button .MathJax_Hover_Arrow {position: absolute; cursor: pointer; 
display: inline-block; border: 2px solid #AAA; border-radius: 4px; 
-webkit-border-radius: 4px; -moz-border-radius: 4px; -khtml-border-radius: 4px; 
font-family: 'Courier New',Courier; font-size: 9px; color: #F0F0F0}
 .MathJax_Menu_Button .MathJax_Hover_Arrow span {display: block; 
background-color: #AAA; border: 1px solid; border-radius: 3px; line-height: 0; 
padding: 4px} .MathJax_Hover_Arrow:hover {color: white!important; border: 2px 
solid #CCC!important} .MathJax_Hover_Arrow:hover span {background-color: 
#CCC!important} #MathJax_About {position: fixed; left: 50%; width: auto; 
text-align: center; border: 3px outset; padding: 1em 2em; background-color: 
#DDDDDD; color: black; cursor: default; font-family: message-box; font-size: 
120%; font-style: normal; text-indent: 0; text-transform: none; line-height: 
normal; letter-spacing: normal; word-spacing: normal; word-wrap: normal; 
white-space: nowrap; float: none; z-index: 201; border-radius: 15px; 
-webkit-border-radius: 15px; -moz-border-radius: 15px; -khtml-border-radius: 
15px; box-shadow: 0px 10px 20px #808080; -webkit-box-shadow: 0px 10px 20px 
#808080; -moz-box-shadow: 0px 10px 20px #808080; -khtml-box-shadow: 0px 10px 
20px #808080} #MathJax_About.MathJax_MousePost {outline: none} .MathJax_Menu 
{position: absolute; background-color: white; color: black; width: auto; 
padding: 2px; border: 1px solid #CCCCCC; margin: 0; cursor: default; font: menu; 
text-align: left; text-indent: 0; text-transform: none; line-height: normal; 
letter-spacing: normal; word-spacing: normal; word-wrap: normal; white-space: 
nowrap; float: none; z-index: 201; box-shadow: 0px 10px 20px #808080; 
-webkit-box-shadow: 0px 10px 20px #808080; -moz-box-shadow: 0px 10px 20px 
#808080; -khtml-box-shadow: 0px 10px 20px #808080} .MathJax_MenuItem {padding: 
2px 2em; background: transparent} .MathJax_MenuArrow {position: absolute; right: 
.5em; padding-top: .25em; color: #666666; font-family: 'Arial unicode MS'; 
font-size: .75em} .MathJax_MenuActive .MathJax_MenuArrow {color: white}
 .MathJax_MenuArrow.RTL {left: .5em; right: auto} .MathJax_MenuCheck {position: 
absolute; left: .7em; font-family: 'Arial unicode MS'} .MathJax_MenuCheck.RTL 
{right: .7em; left: auto} .MathJax_MenuRadioCheck {position: absolute; left: 
1em} .MathJax_MenuRadioCheck.RTL {right: 1em; left: auto} .MathJax_MenuLabel 
{padding: 2px 2em 4px 1.33em; font-style: italic} .MathJax_MenuRule {border-top: 
1px solid #CCCCCC; margin: 4px 1px 0px} .MathJax_MenuDisabled {color: GrayText}
 .MathJax_MenuActive {background-color: Highlight; color: HighlightText}
 .MathJax_MenuDisabled:focus, .MathJax_MenuLabel:focus {background-color: 
#E8E8E8} .MathJax_ContextMenu:focus {outline: none} .MathJax_ContextMenu 
.MathJax_MenuItem:focus {outline: none} #MathJax_AboutClose {top: .2em; right: 
.2em} .MathJax_Menu .MathJax_MenuClose {top: -10px; left: -10px}
 .MathJax_MenuClose {position: absolute; cursor: pointer; display: inline-block; 
border: 2px solid #AAA; border-radius: 18px; -webkit-border-radius: 18px; 
-moz-border-radius: 18px; -khtml-border-radius: 18px; font-family: 'Courier 
New',Courier; font-size: 24px; color: #F0F0F0} .MathJax_MenuClose span {display: 
block; background-color: #AAA; border: 1.5px solid; border-radius: 18px; 
-webkit-border-radius: 18px; -moz-border-radius: 18px; -khtml-border-radius: 
18px; line-height: 0; padding: 8px 0 6px} .MathJax_MenuClose:hover {color: 
white!important; border: 2px solid #CCC!important} .MathJax_MenuClose:hover span 
{background-color: #CCC!important} .MathJax_MenuClose:hover:focus {outline: 
none} .MathJax_Preview .MJXf-math {color: inherit!important} 
.MJX_Assistive_MathML {position: absolute!important; top: 0; left: 0; clip: 
rect(1px, 1px, 1px, 1px); padding: 1px 0 0 0!important; border: 0!important; 
height: 1px!important; width: 1px!important; overflow: hidden!important; 
display: block!important; -webkit-touch-callout: none; -webkit-user-select: 
none; -khtml-user-select: none; -moz-user-select: none; -ms-user-select: none; 
user-select: none} .MJX_Assistive_MathML.MJX_Assistive_MathML_Block {width: 
100%!important} #MathJax_Zoom {position: absolute; background-color: #F0F0F0; 
overflow: auto; display: block; z-index: 301; padding: .5em; border: 1px solid 
black; margin: 0; font-weight: normal; font-style: normal; text-align: left; 
text-indent: 0; text-transform: none; line-height: normal; letter-spacing: 
normal; word-spacing: normal; word-wrap: normal; white-space: nowrap; float: 
none; -webkit-box-sizing: content-box; -moz-box-sizing: content-box; box-sizing: 
content-box; box-shadow: 5px 5px 15px #AAAAAA; -webkit-box-shadow: 5px 5px 15px 
#AAAAAA; -moz-box-shadow: 5px 5px 15px #AAAAAA; -khtml-box-shadow: 5px 5px 15px 
#AAAAAA} #MathJax_ZoomOverlay {position: absolute; left: 0; top: 0; z-index: 
300; display: inline-block; width: 100%; height: 100%; border: 0; padding: 0; 
margin: 0; background-color: white; opacity: 0; filter: alpha(opacity=0)}
 #MathJax_ZoomFrame {position: relative; display: inline-block; height: 0; 
width: 0} #MathJax_ZoomEventTrap {position: absolute; left: 0; top: 0; z-index: 
302; display: inline-block; border: 0; padding: 0; margin: 0; background-color: 
white; opacity: 0; filter: alpha(opacity=0)} .MathJax_Preview {color: #888}
 #MathJax_Message {position: fixed; left: 1px; bottom: 2px; background-color: 
#E6E6E6; border: 1px solid #959595; margin: 0px; padding: 2px 8px; z-index: 102; 
color: black; font-size: 80%; width: auto; white-space: nowrap}
 #MathJax_MSIE_Frame {position: absolute; top: 0; left: 0; width: 0px; z-index: 
101; border: 0px; margin: 0px; padding: 0px} .MathJax_Error {color: #CC0000; 
font-style: italic} .MJXp-script {font-size: .8em} .MJXp-right 
{-webkit-transform-origin: right; -moz-transform-origin: right; 
-ms-transform-origin: right; -o-transform-origin: right; transform-origin: 
right} .MJXp-bold {font-weight: bold} .MJXp-italic {font-style: italic}
 .MJXp-scr {font-family: MathJax_Script,'Times New 
Roman',Times,STIXGeneral,serif} .MJXp-frak {font-family: MathJax_Fraktur,'Times 
New Roman',Times,STIXGeneral,serif} .MJXp-sf {font-family: 
MathJax_SansSerif,'Times New Roman',Times,STIXGeneral,serif} .MJXp-cal 
{font-family: MathJax_Caligraphic,'Times New Roman',Times,STIXGeneral,serif}
 .MJXp-mono {font-family: MathJax_Typewriter,'Times New 
Roman',Times,STIXGeneral,serif} .MJXp-largeop {font-size: 150%}
 .MJXp-largeop.MJXp-int {vertical-align: -.2em} .MJXp-math {display: 
inline-block; line-height: 1.2; text-indent: 0; font-family: 'Times New 
Roman',Times,STIXGeneral,serif; white-space: nowrap; border-collapse: collapse}
 .MJXp-display {display: block; text-align: center; margin: 1em 0} .MJXp-math 
span {display: inline-block} .MJXp-box {display: block!important; text-align: 
center} .MJXp-box:after {content: " "} .MJXp-rule {display: block!important; 
margin-top: .1em} .MJXp-char {display: block!important} .MJXp-mo {margin: 0 
.15em} .MJXp-mfrac {margin: 0 .125em; vertical-align: .25em} .MJXp-denom 
{display: inline-table!important; width: 100%} .MJXp-denom > * {display: 
table-row!important} .MJXp-surd {vertical-align: top} .MJXp-surd > * {display: 
block!important} .MJXp-script-box > * {display: table!important; height: 50%}
 .MJXp-script-box > * > * {display: table-cell!important; vertical-align: top}
 .MJXp-script-box > *:last-child > * {vertical-align: bottom} .MJXp-script-box > 
* > * > * {display: block!important} .MJXp-mphantom {visibility: hidden}
 .MJXp-munderover {display: inline-table!important} .MJXp-over {display: 
inline-block!important; text-align: center} .MJXp-over > * {display: 
block!important} .MJXp-munderover > * {display: table-row!important}
 .MJXp-mtable {vertical-align: .25em; margin: 0 .125em} .MJXp-mtable > * 
{display: inline-table!important; vertical-align: middle} .MJXp-mtr {display: 
table-row!important} .MJXp-mtd {display: table-cell!important; text-align: 
center; padding: .5em 0 0 .5em} .MJXp-mtr > .MJXp-mtd:first-child {padding-left: 
0} .MJXp-mtr:first-child > .MJXp-mtd {padding-top: 0} .MJXp-mlabeledtr {display: 
table-row!important} .MJXp-mlabeledtr > .MJXp-mtd:first-child {padding-left: 0}
 .MJXp-mlabeledtr:first-child > .MJXp-mtd {padding-top: 0} .MJXp-merror 
{background-color: #FFFF88; color: #CC0000; border: 1px solid #CC0000; padding: 
1px 3px; font-style: normal; font-size: 90%} .MJXp-scale0 {-webkit-transform: 
scaleX(.0); -moz-transform: scaleX(.0); -ms-transform: scaleX(.0); -o-transform: 
scaleX(.0); transform: scaleX(.0)} .MJXp-scale1 {-webkit-transform: scaleX(.1); 
-moz-transform: scaleX(.1); -ms-transform: scaleX(.1); -o-transform: scaleX(.1); 
transform: scaleX(.1)} .MJXp-scale2 {-webkit-transform: scaleX(.2); 
-moz-transform: scaleX(.2); -ms-transform: scaleX(.2); -o-transform: scaleX(.2); 
transform: scaleX(.2)} .MJXp-scale3 {-webkit-transform: scaleX(.3); 
-moz-transform: scaleX(.3); -ms-transform: scaleX(.3); -o-transform: scaleX(.3); 
transform: scaleX(.3)} .MJXp-scale4 {-webkit-transform: scaleX(.4); 
-moz-transform: scaleX(.4); -ms-transform: scaleX(.4); -o-transform: scaleX(.4); 
transform: scaleX(.4)} .MJXp-scale5 {-webkit-transform: scaleX(.5); 
-moz-transform: scaleX(.5); -ms-transform: scaleX(.5); -o-transform: scaleX(.5); 
transform: scaleX(.5)} .MJXp-scale6 {-webkit-transform: scaleX(.6); 
-moz-transform: scaleX(.6); -ms-transform: scaleX(.6); -o-transform: scaleX(.6); 
transform: scaleX(.6)} .MJXp-scale7 {-webkit-transform: scaleX(.7); 
-moz-transform: scaleX(.7); -ms-transform: scaleX(.7); -o-transform: scaleX(.7); 
transform: scaleX(.7)} .MJXp-scale8 {-webkit-transform: scaleX(.8); 
-moz-transform: scaleX(.8); -ms-transform: scaleX(.8); -o-transform: scaleX(.8); 
transform: scaleX(.8)} .MJXp-scale9 {-webkit-transform: scaleX(.9); 
-moz-transform: scaleX(.9); -ms-transform: scaleX(.9); -o-transform: scaleX(.9); 
transform: scaleX(.9)} .MathJax_PHTML .noError {vertical-align: -2px; font-size: 
90%; text-align: left; color: black; padding: 1px 3px; border: 1px solid}  









  


  offline 






   


   




   




   


   


   





   IT Anomaly Insights Preconfigured Solution
   


   


  IT Anomaly Insights Preconfigured Solution 


  Hello! 


[IT Anomaly Insights Preconfigured Solution](https://gallery.cortanaintelligence.com/solutiontemplate/c0cc7d49409b4be99fa99dcf8ccba98b)
====================================
Frequently Asked Questions (FAQs)
------------------------------------------

### Deployment Failures 
When the [Cortana Intelligence Quick Start](https://start.cortanaintelligence.com/) (CIQS) portal reports a failure to deploy the solution, please navigate to the Resource Group link provided in the deployment page, which will take you to the Azure portal. Under Settings -> Deployment tab you will be able to see the deployments and get more logs if there were failures. 
Here are the most frequently encountered issues when deploying the solution:
>1. Deployment of Azure Data Factory failed with error code MaxOnDemandComputeCoresReached and message “HDI Not enough cores for deployment”.
**Solution:** ADF reserves a certain number of cores for on-demand clusters in each Azure Region and this message indicated that your subscription has already reached the limit for this region. You will need to delete unused ADF pipelines or preconfigured solutions in order to free up some cores or try deploying in another region that might have room. Alternatively, you can also raise a customer request via Azure portal to increase the ADF reserved quota for HDI cores, for this region if you need more capacity.
2. Deployment latencies – my deployment is taking too long, what is happening?
**Solution:** The solution deploys multiple Azure resources as part of the deployment and customers may notice longer durations occasionally especially in some busy Azure regions. Please try a different region if that is possible or contact us.

Please, feel free to [contact us](adpcs_support@microsoft.com) with any additional questions you might have.
Thanks!

> Written with [StackEdit](https://stackedit.io/).













IT Anomaly Insights Preconfigured Solution


Frequently Asked Questions (FAQs)


Deployment Failures

When the Cortana Intelligence Quick Start (CIQS) portal reports a failure to 
deploy the solution, please navigate to the Resource Group link provided in the 
deployment page, which will take you to the Azure portal. Under Settings -> 
Deployment tab you will be able to see the deployments and get more logs if 
there were failures. 
 Here are the most frequently encountered issues when deploying the solution:

  Deployment of Azure Data Factory failed with error code 
  MaxOnDemandComputeCoresReached and message “HDI Not enough cores for 
  deployment”. 
  Solution: ADF reserves a certain number of cores for on-demand clusters in 
  each Azure Region and this message indicated that your subscription has 
  already reached the limit for this region. You will need to delete unused ADF 
  pipelines or preconfigured solutions in order to free up some cores or try 
  deploying in another region that might have room. Alternatively, you can also 
  raise a customer request via Azure portal to increase the ADF reserved quota 
  for HDI cores, for this region if you need more capacity.
  Deployment latencies – my deployment is taking too long, what is happening? 
  Solution: The solution deploys multiple Azure resources as part of the 
  deployment and customers may notice longer durations occasionally especially 
  in some busy Azure regions. Please try a different region if that is possible 
  or contact us.

Please, feel free to contact us with any additional questions you might have. 
 Thanks!


Written with StackEdit.



 
 
  

Markdown syntax



Phrase Emphasis
*italic*   **bold**
_italic_   __bold__

Links

Inline:
An [example](http://url.com/ "Title")

Reference-style labels (titles are optional):
An [example][id]. Then, anywhere
else in the doc, define the link:

  [id]: http://example.com/  "Title"

Images

Inline (titles are optional):
![alt text](/path/img.jpg "Title")

Reference-style:
![alt text][id]

[id]: /url/to/img.jpg "Title"

Headers

Setext-style:
Header 1
========

Header 2
--------

atx-style (closing #'s are optional):
# Header 1 #

## Header 2 ##

###### Header 6

Lists

Ordered, without paragraphs:
1.  Foo
2.  Bar

Unordered, with paragraphs:
*   A list item.

    With multiple paragraphs.

*   Bar

You can nest them:
*   Abacus
    * answer
*   Bubbles
    1.  bunk
    2.  bupkis
        * BELITTLER
    3. burper
*   Cunning

Blockquotes
> Email-style angle brackets
> are used for blockquotes.

> > And, they can be nested.

> #### Headers in blockquotes
>
> * You can quote a list.
> * Etc.

Code Spans
`<code>` spans are delimited
by backticks.

You can include literal backticks
like `` `this` ``.

Preformatted Code Blocks

Indent every line of a code block by at least 4 spaces or 1 tab.
This is a normal paragraph.

    This is a preformatted
    code block.

Horizontal Rules

Three or more dashes or asterisks:
---

* * *

- - - -

Manual Line Breaks

End a line with two or more spaces:
Roses are red,
Violets are blue.

Based on the Markdown syntax guide, by Fletcher T. Penney.


  

Table of contents



  IT Anomaly Insights Preconfigured Solution Frequently Asked Questions (FAQs) 
      Deployment Failures




 1334  

Statistics



Characters: 1334 

Words: 248 

Paragraphs: 12 

  

HTML code

  

× 

Search for  

Replace with  


0 found 

Search Replace All 


 Case sensitive  

 Regular expression  





  


 StackEdit Viewer 



 Synchronize
Open, save, collaborate in the Cloud 

  "IT Anomaly Insights Preconfigured Solution" is already synchronized.


   Force synchronization


   Manage synchronization


   Open from CouchDB new


   Save on CouchDB new


   Open from Dropbox


   Save on Dropbox


   Open from Google Drive


   Save on Google Drive

   Open from Google Drive
  (2nd account)
   Save on Google Drive
  (2nd account)
   Open from Google Drive
  (3rd account)
   Save on Google Drive
  (3rd account)


Publish
Export to the web 

  "IT Anomaly Insights Preconfigured Solution" is already published.


   Update publication


   Manage publication


   Blogger 


   Blogger Page 


   Dropbox 


   Gist 


   GitHub 


   Google Drive 


   SSH server 


   Tumblr 


   WordPress 



Sharing
Share document links 

 Import from disk

 Export to disk


   As Markdown


   As HTML


   Using template


   As PDF sponsor


 Import from URL

 Convert HTML to Markdown

   Settings


   About


  

   New document


   Delete document


   Manage documents


 



  Hello!


  IT Anomaly Insights Preconfigured Solution



  Hello!


  IT Anomaly Insights Preconfigured Solution





× 
Manage documents
 Try Classeur beta!

Please consider sponsoring StackEdit for $5/year (or sign in if you're already a 
sponsor).


   Selection 

     Select all


     Unselect all



     Move to folder


     Delete



   Create folder 


   2


   1



The following documents will be deleted locally:

Please choose a destination folder:



Cancel OK Close 




× 
Hyperlink
 Try Classeur beta!

Please consider sponsoring StackEdit for $5/year (or sign in if you're already a 
sponsor).

Please provide the link URL and an optional title:

 

Cancel OK 




× 
Image
 Try Classeur beta!

Please consider sponsoring StackEdit for $5/year (or sign in if you're already a 
sponsor).

Please provide the image URL and an optional title:

 

 Import from Google+ Cancel OK 




× 
Google+ image import
 Try Classeur beta!

Please consider sponsoring StackEdit for $5/year (or sign in if you're already a 
sponsor).



 

Title (optional) 

Size limit (optional) 
 px 

Cancel OK 




× 
Delete
 Try Classeur beta!

Please consider sponsoring StackEdit for $5/year (or sign in if you're already a 
sponsor).

Are you sure you want to delete "IT Anomaly Insights Preconfigured Solution"? 


Note: It won't delete the file on synchronized locations.

Cancel Delete 




× 
Import from URL
 Try Classeur beta!

Please consider sponsoring StackEdit for $5/year (or sign in if you're already a 
sponsor).

Please provide a link to a Markdown document.


URL 

Cancel OK 




× 
Import from disk
 Try Classeur beta!

Please consider sponsoring StackEdit for $5/year (or sign in if you're already a 
sponsor).

Please select your Markdown files here:



Or drag and drop your Markdown files here:

Drop files here

Close 




× 
Convert HTML to Markdown
 Try Classeur beta!

Please consider sponsoring StackEdit for $5/year (or sign in if you're already a 
sponsor).

Please select your HTML files here:



Or drag and drop your HTML files here:

Drop files here

Or insert your HTML code here:

Close OK 




× 
Save on Google Drive


Please consider sponsoring StackEdit for $5/year (or sign in if you're already a 
sponsor).

This will save "IT Anomaly Insights Preconfigured Solution" to your  Google 
Drive account and keep it synchronized. 


Folder ID (optional) 

 Open folder 

If no folder ID is supplied, the file will be created in your root folder. 

Existing file ID (optional) 

This will overwrite the existing file on the server. 

Options   


Tip: You can move or rename the file afterwards within Google Drive.

 Setup AutoSync Cancel OK 




× 
Save on Google Drive (2nd account)


Please consider sponsoring StackEdit for $5/year (or sign in if you're already a 
sponsor).

This will save "IT Anomaly Insights Preconfigured Solution" to your  Google 
Drive account and keep it synchronized. 


Folder ID (optional) 

 Open folder 

If no folder ID is supplied, the file will be created in your root folder. 

Existing file ID (optional) 

This will overwrite the existing file on the server. 

Options   


Tip: You can move or rename the file afterwards within Google Drive.

 Setup AutoSync Cancel OK 




× 
Save on Google Drive (3rd account)


Please consider sponsoring StackEdit for $5/year (or sign in if you're already a 
sponsor).

This will save "IT Anomaly Insights Preconfigured Solution" to your  Google 
Drive account and keep it synchronized. 


Folder ID (optional) 

 Open folder 

If no folder ID is supplied, the file will be created in your root folder. 

Existing file ID (optional) 

This will overwrite the existing file on the server. 

Options   


Tip: You can move or rename the file afterwards within Google Drive.

 Setup AutoSync Cancel OK 




× 
AutoSync to Google Drive


Please consider sponsoring StackEdit for $5/year (or sign in if you're already a 
sponsor).

AutoSync feature automatically saves all documents to your  Google Drive account 
and keep them synchronized. 





 Disabled  

 New documents (not current)  

 Every document not yet synchronized  


Folder ID (optional) 

 
 

If no folder ID is supplied, files will be created in your root folder. 


Note: Removing a local document will not delete the linked file on Google Drive.

Cancel OK 




× 
AutoSync to Google Drive (2nd account)


Please consider sponsoring StackEdit for $5/year (or sign in if you're already a 
sponsor).

AutoSync feature automatically saves all documents to your  Google Drive account 
and keep them synchronized. 





 Disabled  

 New documents (not current)  

 Every document not yet synchronized  


Folder ID (optional) 

 
 

If no folder ID is supplied, files will be created in your root folder. 


Note: Removing a local document will not delete the linked file on Google Drive.

Cancel OK 




× 
AutoSync to Google Drive (3rd account)


Please consider sponsoring StackEdit for $5/year (or sign in if you're already a 
sponsor).

AutoSync feature automatically saves all documents to your  Google Drive account 
and keep them synchronized. 





 Disabled  

 New documents (not current)  

 Every document not yet synchronized  


Folder ID (optional) 

 
 

If no folder ID is supplied, files will be created in your root folder. 


Note: Removing a local document will not delete the linked file on Google Drive.

Cancel OK 




× 
Save on Dropbox
 Try Classeur beta!

Please consider sponsoring StackEdit for $5/year (or sign in if you're already a 
sponsor).

This will save "IT Anomaly Insights Preconfigured Solution" to your  Dropbox
 account and keep it synchronized. 


File path 

File path is composed of both folder and filename. 

Note: Dropbox file path does not depend on document title.
  The title of your document will not be synchronized.
  Destination folder must exist.
  Any existing file at this location will be overwritten.

Cancel OK 




× 
Open from CouchDB



Filter by tag none  Add   Remove   
 Try Classeur beta!

Please consider sponsoring StackEdit for $5/year (or sign in if you're already a 
sponsor).

 Careful: You're using the public CouchDB instance. Anybody can open, edit and 
delete your files there! To setup your own CouchDB instance click here. 


Document ID 

Multiple IDs can be provided (space separated)

   Selection 

     Unselect all



     Delete







Please wait...

No document.
 More documents! 
The following documents will be removed from CouchDB:


Open by ID... Cancel Delete Cancel Open Cancel Open 




× 
Save on CouchDB
 Try Classeur beta!

Please consider sponsoring StackEdit for $5/year (or sign in if you're already a 
sponsor).

 Careful: You're using the public CouchDB instance. Anybody can open, edit and 
delete your files there! To setup your own CouchDB instance click here. 

This will save "IT Anomaly Insights Preconfigured Solution" to CouchDB and keep 
it synchronized. 


Tip: You can use a YAML front matter to specify tags for your document.

Alternatively, you can place comma separated tags in square brackets at the 
beginning of the document title.

Cancel OK 




× 
Synchronization
 Try Classeur beta!

Please consider sponsoring StackEdit for $5/year (or sign in if you're already a 
sponsor).

"IT Anomaly Insights Preconfigured Solution" is synchronized with the following 
location(s): 



Note: Removing a synchronized location will not delete any file.

Close 




× 
Publish on  
 Try Classeur beta!

Please consider sponsoring StackEdit for $5/year (or sign in if you're already a 
sponsor).


Host 

Host must be accessible publicly, unless you're hosting your own StackEdit 
instance. 

Port (optional) 

Username 

Password 

Repository 

Branch 

File path 

File path is composed of both folder and filename. 

Filename 

Existing ID (optional) 

Public 

 

Blog URL 

Blog hostname 

WordPress site 

Jetpack plugin is required for self-hosted sites. 

Update existing post ID (optional) 

Update existing page ID (optional) 

File path 

File path is composed of both folder and filename. 

File ID (optional) 

If no file ID is supplied, a new file will be created in your Google Drive root 
folder. You can move the file afterwards within Google Drive.

Force filename (optional) 

If no file name is supplied, the document title will be used.

Format 

 Markdown  

 HTML  

 Template  





 Custom template  (?) 





Tip: You can use a YAML front matter to specify the title and the tags/labels of 
your publication.

Interpreted variables: title, tags, published, date.


Tip: You can use a YAML front matter to specify the title of your page.

Interpreted variables: title.


About URL: For newly created page , Blogger API will append a generated number 
to the url like about-me-1234.html, if you deeply care about your URL naming, 
you should first create the page on Blogger and then update them with StackEdit 
specifying the pageId when publishing. 

About page visibility: Blogger API does not respect published status for 
pages.When publishing the page to Blogger, the page will be live but not added 
to the page listing. You should arrange the page listing from Blogger dashboard. 

Cancel OK 




× 
Publication
 Try Classeur beta!

Please consider sponsoring StackEdit for $5/year (or sign in if you're already a 
sponsor).

"IT Anomaly Insights Preconfigured Solution" is published on the following
 location(s): 



Note: Removing a publish location will not delete the actual publication.

Close 




× 
Sharing
 Try Classeur beta!

Please consider sponsoring StackEdit for $5/year (or sign in if you're already a 
sponsor).

Collaborate on "IT Anomaly Insights Preconfigured Solution" using the following 
link(s):

No sharing link yet! 



Note: To collaborate on this document, just save it on CouchDB. To collaborate 
via Google Drive or Dropbox, you have to share the file manually from Google 
Drive/Dropbox websites.


Share a read-only version of "IT Anomaly Insights Preconfigured Solution" using 
the following link(s):

No sharing link yet! 



Note: To share a read-only version of this document, just publish it as a Gist 
in Markdown format.


Tip: You can open any markdown URL within StackEdit Viewer using viewer#!url=.

Close 




× 
Settings

  Basic


  Advanced


  Extensions


  Utils

 Try Classeur beta!

Please consider sponsoring StackEdit for $5/year (or sign in if you're already a 
sponsor).




Layout orientation 

 Horizontal  

 Vertical  

Theme 

BlueDefaultGrayNightSchoolSolarized LightSolarized Dark




 Markdown Extra/GitHub Flavored Markdown syntax  




 LaTeX mathematical expressions using $ and $$ delimiters  

Google Drive multi-accounts  

1 account 2 accounts 3 accounts 

Please sign in first with Google. Once linked with your Google accounts, 
changing account is not possible unless you reset the application.



Edit mode 

 Left-To-Right  

 Right-To-Left  

Editor's font style 

 Rich  

 Rich Monospaced  

 Monospaced  

Font size ratio 
 

Max width ratio 
 

Cursor focus ratio 
 

Lazy rendering (?)  

 

Default content (?)  

Default template (?)  

PDF template (?)  

PDF options (?)  

Markdown MIME type  

text/plain text/x-markdown 

Permissions 

 Allow StackEdit to open any document in Google Drive  
Existing authorization has to be revoked in Google Dashboard for this change to 
take effect.




 Allow StackEdit to open any document in Dropbox  
If unchecked, access will be restricted to folder /Applications/StackEdit for 
existing files.




 Allow StackEdit to access private repositories in GitHub  
Existing authorization has to be revoked in GitHub settings for this change to 
take effect.

GitHub commit message 

CouchDB URL 

Setup your own CouchDB...





 enabled  
Button "HTML code"  


Adds a "HTML code" button over the preview.


Template (?)  



 enabled  
Button "Markdown syntax  


Adds a "Markdown syntax" button over the preview.



 enabled  
Button "Statistics"  


Adds a "Document statistics" button over the preview.


Title  RegExp  

Title  RegExp  

Title  RegExp  



 enabled  
Button "Synchronize"  


Adds a "Synchronize documents" button in the navigation bar.


Sync period (0: manual) 
 ms 

Sync shortcut (?) 



 enabled  
Button "Viewer"  


Adds a "Viewer" button over the preview.



 enabled  
Document Selector  


Allows toggling document with keyboard shortcuts.


Order by 

Document title Most recently used 

"Previous" shortcut (?) 

"Next" shortcut (?) 



 enabled  
Find and Replace  


Helps find and replace text in the current document.


Shortcut (?) 



 enabled  
Google Analytics  


Sends anonymous statistics about usage and errors to help improve StackEdit.



 enabled  
HTML Sanitizer  


Prevents cross-site-scripting attacks (XSS).

 Careful: Disable at your own risk!



 enabled  
Markdown Email  


Converts email addresses in the form <email@example.com> into clickable links.



 enabled  
Markdown Extra  


Adds extra features to the original Markdown syntax.


Tables 

 

Definition lists 

 

Special attributes 

 

Footnotes 

 

Comments 

 

SmartyPants 

 

GFM newlines 

 

GFM intra-word stars/underscores 

 

GFM strikethrough 

 

GFM fenced code blocks 

 

Syntax highlighter 

None Prettify Highlight.js 

More info



 enabled  
MathJax  


Allows StackEdit to interpret LaTeX mathematical expressions.


TeX configuration 

tex2jax configuration 

More info



 enabled  
Notifications  


Shows notification messages in the bottom-right corner of the screen.


Timeout 
 ms 



 enabled  
Partial Rendering  


Renders modified sections only.


Note: Document sections are based on title elements (h1, h2...). Therefore if
 your document does not contain any title, performance will not be increased.



 enabled  
Scroll Sync  


Binds together editor and preview scrollbars.


Note: The mapping between Markdown and HTML is based on the position of the 
title elements (h1, h2...) in the page. Therefore if your document does not 
contain any title, the mapping will be linear and consequently less accurate.



 enabled  
Shortcuts  


Maps keyboard shortcuts to JavaScript functions.


Mapping (?)  



 enabled  
Table of Contents  


Generates a table of contents when a [TOC] marker is found.


Marker RegExp 

Max depth 
 

Button over preview 

 



 enabled  
UML Diagrams  


Creates UML diagrams from plain text description.


Flow charts options (JSON)  


Sequence diagrams:
More info```sequence
Alice->Bob: Hello Bob, how are you?
Bob-->Alice: I am good thanks!
```

Flow charts:
More info```flow
st=>start: Start
e=>end
op=>operation: My Operation
cond=>condition: Yes or No?
st->op->cond
cond(yes)->e
cond(no)->op
```


Note: Markdown Extra extension has to be enabled with GFM fenced code blocks 
option.



 enabled  
UserCustom extension  


Allows users to implement their own extension.


JavaScript code (?)  

More info

Create your own extension...



 Hello! document

 Welcome tour


 Import docs & settings

 Export docs & settings
 

 Load default settings

 Reset application

 StackEdit recovery

Cancel OK 





Ooops...
 Try Classeur beta!

Please consider sponsoring StackEdit for $5/year (or sign in if you're already a 
sponsor).

StackEdit has stopped because another instance was running in the same browser.


If you want to reopen StackEdit, click on "Reload".

Reload 





Redirection
 Try Classeur beta!

Please consider sponsoring StackEdit for $5/year (or sign in if you're already a 
sponsor).



Please click OK to proceed.

Cancel OK 





Reset application
 Try Classeur beta!

Please consider sponsoring StackEdit for $5/year (or sign in if you're already a 
sponsor).

This will delete all your local documents.

Are you sure?

Cancel OK 





Import documents and settings
 Try Classeur beta!

Please consider sponsoring StackEdit for $5/year (or sign in if you're already a 
sponsor).

This will delete all existing local documents.

Are you sure?

Cancel OK 





Add Google Drive account
 Try Classeur beta!

Please consider sponsoring StackEdit for $5/year (or sign in if you're already a 
sponsor).

To perform this request, you need to configure another Google Drive account in 
StackEdit.

Do you want to proceed?

No Yes 





Sponsor only!
 Try Classeur beta!

Please consider sponsoring StackEdit for $5/year (or sign in if you're already a 
sponsor).

This feature is restricted to sponsor users as it's a web service hosted on 
Amazon EC2. Note that sponsoring StackEdit would cost you only $5/year.

To see how a PDF looks click here.


Tip: PDFs are fully customizable via Settings>Advanced>PDF template/options.

Close 





×   Try Classeur beta!


Please consider sponsoring StackEdit for $5/year (or sign in if you're already a 
sponsor).

 
  About:GitHub project / issue tracker 
  Chrome app (thanks for your review!) 
  Follow on Twitter 
  Follow on Facebook 
  Follow on Google+ 
  Developers:Benoit Schweblin
  Pete Eigel (contributor)
  wiibaa (contributor)
  Daniel Hug (contributor)
  Kevin Brey (themer)

With special thanks to Smileupps for CouchDB hosting. 
  Sponsorship: 
StackEdit 4.3.14 – Privacy Policy
Copyright 2013-2014 Benoit Schweblin
Licensed under an Apache License 

Close 

