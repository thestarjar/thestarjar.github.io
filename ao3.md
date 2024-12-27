Guide to spoiler-hover and replace-hover text on Ao3

## Hover-Spoiler Content Warnings
Include in workskin:

```
.spoiler {
  color: #878787;
  background-color: #878787;
}

.spoiler:hover {
  color: inherit;
  background-color: inherit;
}

.screenreader {
  position: absolute;
  left: -10000px;
  top: auto;
  width: 1px;
  height: 1px;
  overflow: hidden;
}
```

HTML: this must be in the chapter NOTES (or body); it will not work right in the summary
```
<a href="#postspoiler" class="screenreader">Skip Content Warnings</a>
Hover/tap or highlight for content warnings:
<p class="spoiler">
warning 1 <br/>
warning 2 <br/>
warning 3
</p>
<p id="postspoiler" class="screenreader">End of warnings</p>
```

As long as the user has workskins enabled, the "Skip Content Warnings" link and the "End of Warnings" indicator (which the skip link jumps to, which is why it's included) will not show up to anyone except people using screen readers.

## Text that Changes on Hover
Include in workskin:
```
.hovernote:hover .hasnote {
  display: none;
}
.thenote {
  display: none;
}
.hovernote:hover .thenote {
  display: inline;
}
```

Replacable text in body (this can be inline with a paragraph, or whatever you want)

`<span class="hovernote"><span class="hasnote">NORMALLY DISPLAYED TEXT</span><span class="thenote">THIS TEXT APPEARS ON HOVER</span></span>`

## Personal Workflow
I love dying and being dead

Note: I write [initial text//hover text] in my writing draft, the find-replace below (in step 8) assumes that's how it was written

1. Dump my rich text draft into [textmark](https://textmark.js.org/)
2. Copy from there to Notepad++
3. CTRL+H for find/replace and turn on REGULAR EXPRESSION mode
4. Stick a `<p>` at the very start and `</p>` at the very end
5. Replace all `\r\n\r\n` with `</p><p>`
6. Replace all `_(.*?)_` with `<em>$1</em>`
7. Replace all `\*\*(.*?)\*\*` with `<strong>$1</strong>`
8. Replace all `\[(.*)//(.*)\]` with `<span class="hovernote"><span class="hasnote">[$1]</span><span class="thenote">[*$2]</span></span>`
9. Paste to Ao3 HTML EDITOR
