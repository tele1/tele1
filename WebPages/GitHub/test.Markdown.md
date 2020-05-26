



Documentation **GitHub** MarkDown   https://github.github.com/gfm/  
Documentation MarkDown              https://spec.commonmark.org/0.29/

Wiki  https://en.wikipedia.org/wiki/Markdown



---
# This test web, not use this in practise for now
# Examples

<table style="width: 100%; border-collapse: collapse;" border="1">
<tbody>
<tr style="height: 23px;">
<td style="width: 50%; text-align: center; height: 23px;"><strong>Source code</strong></td>
<td style="width: 50%; text-align: center; height: 23px;"><strong>Rendered Markdown</strong></td>
</tr>
<tr style="height: 21px;">
<td style="width: 50%; height: 21px;">Hello&nbsp; (two spaces) <br />World</td>
<td style="width: 50%; height: 21px;">
<p>Hello <br />World</p>
</td>
</tr>
<tr style="height: 21px;">
<td style="width: 50%; height: 21px;">
<p>Hello <br />&nbsp; (empty line)<br />World</p>
</td>
<td style="width: 50%; height: 21px;">
<p>Hello</p>
<p>World</p>
</td>
</tr>
<tr style="height: 21px;">
<td style="width: 50%; height: 21px;">
<p>**Hello World**</p>
</td>
<td style="width: 50%; height: 21px;">
<pre><code class="language-markdown"></code></pre>
<pre><strong>Hello World</strong></pre>
</td>
</tr>
<tr style="height: 21px;">
<td style="width: 50%; height: 21px;">
<p>*Hello World*</p>
</td>
<td style="width: 50%; height: 21px;"><em>Hello World</em></td>
</tr>
<tr style="height: 21px;">
<td style="width: 50%; height: 21px;">&nbsp;</td>
<td style="width: 50%; height: 21px;">&nbsp;</td>
</tr>
</tbody>
</table>


---

# GitHub Trics.

#
## 1. " relative link " in Markdown file.
```
[a relative link](other_file.md)
```
https://stackoverflow.com/questions/7653483/github-relative-link-in-markdown-file.

#
## 2. Creating new folders in GitHub repository via the we browser.
When you trying add new file, try add " / ".
If you want edit folder, edit file inside this folder and click "Backspace" key on keyboard.

#
## 3. Where can you found about " markdown "  syntax.
- https://help.github.com/en/github/writing-on-github/basic-writing-and-formatting-syntax
- https://www.markdownguide.org/basic-syntax/

============================

I tried also use AsciDoc with Markdown on GitHub, but it not worked.
When I trying open web.asciidoc, web browser trying open to download it.

Documentation AsciiDoc  https://github.com/asciidoc/asciidoc/blob/master/doc/asciidoc.txt

Wiki https://en.wikipedia.org/wiki/.adoc
