



Documentation **GitHub** MarkDown   <https://github.github.com/gfm/>  
Documentation MarkDown              <https://spec.commonmark.org/0.29/>

Wiki  <https://en.wikipedia.org/wiki/Markdown>



---
# My Markdown Cheat Sheet / Examples 

## Line Break

<table>
<thead>
  <tr>
    <th><span style="font-weight:bold">Name</span></th>
    <th><span style="font-weight:bold">Soure code Markdown</span></th>
    <th><span style="font-weight:bold">Output Markdown</span></th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>Hard Line Breaks</td>
    <td>Hello  (two spaces) <br>World<br></td>
    <td>Hello<br>World<br></td>
  </tr>
  <tr>
    <td><span style="font-weight:bold">Warning:</span><br>" \ " (at the end of line) also will break line</td>
    <td>Hello\<br>World<br></td>
    <td>Hello<br>World</td>
  </tr>
  <tr>
    <td></td>
    <td>Hello<br>World<br></td>
    <td>Hello World<br></td>
  </tr>
  <tr>
    <td></td>
    <td>Hello <br><br>World<br></td>
    <td>Hello <br><br>World<br></td>
  </tr>
</tbody>
</table>


## Text

<table>
<thead>
  <tr>
    <th><span style="font-weight:bold">Name</span></th>
    <th><span style="font-weight:bold">Soure code Markdown</span></th>
    <th><span style="font-weight:bold">Output Markdown</span></th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>Strong Emphasis (Bold)</td>
    <td>**Hello World**</td>
    <td><span style="font-weight:bold">Hello World</span></td>
  </tr>
  <tr>
    <td>Emphasis (Italic)</td>
    <td>*Hello World*</td>
    <td><span style="font-style:italic">Hello World</span></td>
  </tr>
  <tr>
    <td>Text Color<br><span style="font-weight:bold">Warning:</span><br>Text Color is not supported,<br> so You can try use html</td>
    <td><p>&lt;p style="color: green"&gt;Hello World&lt;/p&gt;</p><br>(This is html)</td>
    <td><p style="color:green">Hello World</p></td>
  </tr>
</tbody>
</table>


## Links 

<table>
<thead>
  <tr>
    <th><span style="font-weight:bold">Name</span></th>
    <th><span style="font-weight:bold">Soure code Markdown</span></th>
    <th><span style="font-weight:bold">Output Markdown</span></th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>Autolinks (Link Destination)<br></td>
    <td>&lt;https://web.site&gt;</td>
    <td><span style="color:rgb(53, 49, 255)">https://web.site</span></td>
  </tr>
  <tr>
    <td>Link Text<br></td>
    <td>[Your Text](https://web.site)<br></td>
    <td><span style="color:rgb(53, 49, 255)">Your Text</span><br></td>
  </tr>
  <tr>
    <td>Relative Link</td>
    <td>[Your Text](Path/to/other_file.md)</td>
    <td><span style="color:rgb(53, 49, 255)">Your Text</span></td>
  </tr>
</tbody>
</table>


## Images

<table>
<thead>
  <tr>
    <th><span style="font-weight:bold">Name</span></th>
    <th><span style="font-weight:bold">Soure code Markdown</span></th>
    <th><span style="font-weight:bold">Output Markdown</span></th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>Images</td>
    <td>![text](/Path/to/file.jpeg)</td>
    <td>Your Image</td>
  </tr>
</tbody>
</table>


## Frames

<table>
<thead>
  <tr>
    <th><span style="font-weight:bold">Name</span></th>
    <th><span style="font-weight:bold">Soure code Markdown</span></th>
    <th><span style="font-weight:bold">Output Markdown</span></th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>Block Quotes <br><span style="font-weight:bold">Warning:</span><br>Default is " &gt; " for line,<br>but this style is more difficult <br>to convert to another</td>
    <td>&lt;blockquote&gt;<br>Hello<br> World<br>&lt;/blockquote&gt;<br> (this is html)<br></td>
    <td><blockquote>Hello<br> World</blockquote></td>
  </tr>
  <tr>
    <td>Code Spans</td>
    <td>```<br>Hello<br> World<br>```</td>
    <td><code>Hello<br> World</code></td>
  </tr>
  <tr>
    <td>Code With Syntax Highlighting</td>
    <td>```sh<br>Hello<br> World<br>```</td>
    <td><code>Hello<br> World</code></td>
  </tr>
</tbody>
</table>

---


---
# GitHub Trics 

## 2. Creating new folders in GitHub repository via the we browser.
When you trying add new file, try add " / ".
If you want edit folder, edit file inside this folder and click "Backspace" key on keyboard.

#
## 3. Where can you found about " markdown "  syntax.
- <https://help.github.com/en/github/writing-on-github/basic-writing-and-formatting-syntax>
- <https://www.markdownguide.org/basic-syntax/>

============================

I tried also use AsciDoc with Markdown on GitHub, but it not worked or I don't know how use it.
When I trying open web.asciidoc, web browser trying open to download it.

Documentation AsciiDoc  <https://github.com/asciidoc/asciidoc/blob/master/doc/asciidoc.txt>

Wiki <https://en.wikipedia.org/wiki/.adoc>
