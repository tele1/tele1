



Documentation **GitHub** MarkDown   <https://github.github.com/gfm/>  
Documentation MarkDown              <https://spec.commonmark.org/0.29/>

Wiki  <https://en.wikipedia.org/wiki/Markdown>

Basic Syntax  
- <https://help.github.com/en/github/writing-on-github/basic-writing-and-formatting-syntax>
- <https://www.markdownguide.org/basic-syntax/>

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
    <td>Backslash escapes <br> Ignoring Markdown formatting</td>
    <td>\*Hello World\*</td>
    <td>\*Hello World\*</td>
  </tr>
  <tr>
    <td><span style="font-weight:bold">Warning:</span><br>Text Color is not supported,<br> but You can try use html</td>
    <td><p>&lt;p style="color: green"&gt;Hello World&lt;/p&gt;</p><br><br><span style="font-weight:bold">(This is html)</span></td>
    <td><p style="color:green">Hello World</p></td>
  </tr>
  <tr>
    <td>ATX headings</td>
    <td># Hello World 1<br> <br>## Hello World 2<br> <br>### Hello World 3<br> <br>#### Hello World 4<br> <br>##### Hello World 5<br> <br>###### Hello World 6</td>
    <td><h1>Hello World 1</h1><br><h2>Hello World 2</h2><br><h3>Hello World 3</h3><br><h4>Hello World 4</h4><br><h5>Hello World 5</h5><br><h6>Hello World 6</h6></td>
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
  <tr>
    <td>Link To Header<br> <br>A very convenient way:<br> Open file on Github and click your ATX header<br>and you will have open link with header<br> <br> <span style="font-weight:bold">Warning:</span><br>* Convert link to lowercase letters <br>* Replace each space with '-' <br>* Remove punctuations other than "-" and "_" <br>Because link to header may not work.</td>
    <td>[Your Text](#github-trics)</td>
    <td> <a href="#github-trics">Your Text</a></td>
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
    <td><span style="font-weight:bold">Warning:</span><br>Default for Block Quotes is <br> &gt; Your Text  <br>for for each quoted line <br>but this style is more difficult <br>to convert to another style for me</td>
    <td>&lt;blockquote&gt;<br>Hello<br> World<br>&lt;/blockquote&gt;<br> <br><span style="font-weight:bold">(This is html)</span><br></td>
    <td><blockquote>Hello<br> World</blockquote></td>
  </tr>
  <tr>
    <td>Code Spans / Code Block</td>
    <td>```<br>Hello<br> World<br>```</td>
    <td><code>Hello<br> World</code></td>
  </tr>
  <tr>
    <td>Code With Syntax Highlighting</td>
    <td>```sh<br>Hello<br> World<br>```</td>
    <td><code>Hello<br> World</code></td>
  </tr>
  <tr>
    <td><span style="font-weight:bold">Warning:</span><br>Code Block also is the line which contains at the beginning 8 spaces or two tabs.”</td>
    <td>(8 spaces or 2 tabs)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Hello World</td>
    <td><code>Hello<br> World</code></td>
  </tr>
  <tr>
    <td>Simple Table<br></td>
    <td><p>| 1 | 2 |<br />| --- | --- |<br />| 3 | 4 |</p></td>
    <td><table><thead><tr><th>1</th><th>2</th></tr></thead><tbody><tr><th>3</th><th>4</th></tr></tbody></table></td>
  </tr>
  <tr>
    <td><span style="font-weight:bold">Warning:</span><br>More advanced table you can try build in html<br> <br>One Cell From The Table In Html</td>
    <td><p>&lt;table&gt;<br>&lt;thead&gt;<br>&nbsp;&nbsp;&lt;tr&gt;<br>&nbsp;&nbsp;&nbsp;&nbsp;&lt;th&gt;One Cell&lt;/th&gt;<br>&nbsp;&nbsp;&lt;/tr&gt;<br>&lt;/thead&gt;<br>&lt;tbody&gt;<br>&lt;/tbody&gt;<br>&lt;/table&gt;<br> <br><span style="font-weight:bold">(This is html)</p></td>
    <td><table><thead><tr><th>One Cell</th></tr></thead><tbody></tbody></table></td>
  </tr>
  <tr>
    <td>Other Example Table In Html</td>
    <td><p>&lt;table&gt;&lt;thead&gt;&lt;tr&gt;&lt;th&gt;External Cell&lt;br&gt;&lt;table&gt;&lt;thead&gt;&lt;tr&gt;&lt;th&gt;Middle Cell&lt;/th&gt;&lt;/tr&gt;&lt;/thead&gt;&lt;tbody&gt;&lt;/tbody&gt;&lt;/table&gt;&lt;/th&gt;&lt;/tr&gt;&lt;/thead&gt;&lt;tbody&gt;&lt;/tbody&gt;&lt;/table&gt;<br> <br><span style="font-weight:bold">(This is html)</p></td>
    <td><table><thead><tr><th>External Cell<br><table><thead><tr><th>Middle Cell</th></tr></thead><tbody></tbody></table></th></tr></thead><tbody></tbody></table></td>
  </tr>
  <tr>
    <td>Thematic breaks / Horizontal rule / Line</td>
    <td><p>---</p></td>
    <td><hr width="100%"></td>
  </tr>
</tbody>
</table>


<table>
<thead>
  <tr>
    <th>1</th>
    <th>2</th>
  </tr>
</thead>
<tbody>
  <tr>
    <th><table><thead><tr><th>1</th></tr></thead><tbody></tbody></table></th>
    <th><table><thead><tr><th>1</th><th>2</th></tr></thead><tbody><tr><th>3</th><th>4</th></tr></tbody></table></th>
  </tr>
</tbody>
</table>


---

== Test Line

I tried also use AsciDoc with Markdown on GitHub, but it not worked or I don't know how use it.  
When I trying open web.asciidoc, web browser trying open to download it.

Documentation AsciiDoc  <https://github.com/asciidoc/asciidoc/blob/master/doc/asciidoc.txt>

Wiki <https://en.wikipedia.org/wiki/.adoc>

---

# GitHub Trics

## 1. Creating new folders in GitHub repository via the we browser.

When you trying add new file, try add " / ".  
If you want edit folder, edit file inside this folder and click "Backspace" key on keyboard.


