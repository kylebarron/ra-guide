# Creating Reports

As an RA, you'll likely be writing data reports, call notes, documentation, etc. I strongly suggest you use a lightweight, very simple markup language called Markdown. It's extremely popular and becoming even more widespread online, so there's a good chance you've seen it before.

## What is Markdown?

Markdown is a very simple syntax for creating documents. You can learn almost everything you might need to know in 5 minutes. [Here are](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet) some [cheat sheets](https://guides.github.com/pdfs/markdown-cheatsheet-online.pdf). This document is written in Markdown ([source](https://github.com/kylebarron/ra-guide/)).

The beauty of Markdown is that it can be very easily converted into many other formats, e.g. `.docx`, `.pdf`, `.tex`, `.html`, using free and open source programs.

For each of my research projects, I write documentation in Markdown format and then create outputs as a PDF using Pandoc and as a website with Mkdocs.


### Pandoc

[Pandoc](https://pandoc.org/) is a "universal document converter". It converts documents between many different formats. Given a single Markdown file, it can convert to `.docx`, `.pdf`, `.tex`, or `.html` files. This is incredibly helpful because I can focus on writing, and abstract from styles.

If you're viewing this documentation as a PDF, it was created by Pandoc.

### Mkdocs

[Mkdocs](https://www.mkdocs.org/) is a documentation website generator. You give it Markdown files and it creates a beautiful, responsive website (especially if you use the [Mkdocs-Material](https://squidfunk.github.io/mkdocs-material/) extension theme). You don't have to know anything about websites.


If you're viewing this documentation as a website, it was created by Mkdocs with Mkdocs-Material.

## Markdown Alternatives

### Microsoft Word

I can't stand Microsoft Word. It's very difficult to use with Git version control. It's nearly impossible to automate the process of creating a report, because you have to copy and paste an image into the document each time. It's also inflexible and difficult to convert into other file formats. Microsoft Word lets you save to PDF, but the result is ugly compared to a PDF file created from LaTeX.

There are times when I need to solicit feedback on a document from someone who is only familiar with Microsoft Word. In this case, I use Pandoc to convert the Markdown file to Word, and share that generated file.

### LaTeX

LaTeX creates beautiful PDF output, but its syntax can be quite cumbersome. Markdown keeps the benefits of LaTeX-created PDF output while simplifying the syntax. When you use Pandoc to convert a Markdown file to PDF, it first converts to `.tex` and then hands the file to LaTeX.

LaTeX is also difficult to convert to other file types. It's difficult to convert to HTML for placement online. It's more difficult to solicit feedback on a document from someone who's unfamiliar with LaTeX.

### LyX

I don't like Microsoft Word, and LyX imitates that interface, so I'm not a fan of LyX either. Lyx also removes some of the benefits of using version control.
