Landslide
=========

---

Overview
========

Generates a slideshow using the slides that power
[the html5-slides presentation](http://apirocks.com/html5/html5.html).

![demo](http://adamzap.com/random/landslide.png)

A sample slideshow is [here](http://adamzap.com/random/landslide.html).

---

News
====

10/19/10
--------

Version 0.8.2 is tagged and pushed to [pypi](http://pypi.python.org/pypi/landslide/0.8.2).

This release fixes some unicode and theme issues.

Thanks to Olivier Verdier, millette, and n1k0 (as always).

09/21/10
--------

Version 0.8.1 is tagged and pushed to [pypi](http://pypi.python.org/pypi/landslide/0.8.1).

This release fixes an issue in the "light" theme. The help and table of
contents side bars were toggled on by default, but this has been fixed.

---

News
====

09/06/10
--------

Version 0.8.0 is tagged and pushed to [pypi](http://pypi.python.org/pypi/landslide/0.8.0). New features:

- Added new `light` theme (agonzalezro) (#14)
- Slide source files are now displayable in presentation (n1k0), press `s` to toggle
- Press `h` to toggle a help sidebar
- Greatly improved Restructured Text support
- Themes will now fall back to the default theme for most missing files
- Improved project file structure and pypi compatibility (harobed) (#15)
- Fix for presentations with more than 48 slides (mtrythall and ipmb) (#17)
- Many small bug fixes and other improvements

Many thanks to n1k0, agonzalezro, harobed, mtrythall, and ipmb for helping to make this release possible.

Also a big thanks to [Lincoln Loop](http://lincolnloop.com/) for supporting and using Landslide!!

---

News
====

07/15/10
--------

Version 0.6.0 is tagged and pushed to [pypi](http://pypi.python.org/pypi/landslide/0.6.0). New features:

- Navigate your slideshow using arrow keys or the space bar
- Press `t` to toggle a table of contents for your presentation
- Press `n` to toggle slide number/source file visibility
- Press `2` to toggle notes in your slides (specify with the .notes macro)
- Press `3` to switch to 3D display (using latest WebKit versions)
- ReST (Restructured Text) support. It's kind of experimental!
- Theme support. Develop your own themes!
- Macros. Easily add functionality to landslide slideshows!
- Many bug fixes

06/24/10
--------

- Version 0.4.0 is tagged, and Landslide is on [pypi](http://pypi.python.org/pypi/landslide/0.4.0).
- Landslide installs as a command line script if you install it via `easy_install` or `pip`.

---

Features
========

- Write your slide contents easily using the [Markdown](http://daringfireball.net/projects/markdown/syntax) or [ReStructuredText](http://docutils.sourceforge.net/rst.html) syntaxes
- [HTML5](http://dev.w3.org/html5/spec/), Web based, stand-alone document (embedded local images), fancy transitions
- PDF export (using [PrinceXML](http://www.princexml.com/) if available)

---

Requirements
============

`python` and the following modules:

- `jinja2`
- `pygments` for code blocks syntax coloration

Eventually:

- `markdown` if you use Markdown syntax for your slide contents
- `docutils` if you use ReStructuredText syntax for your slide contents

---

Formatting
==========

### Markdown

- To create a title slide, render a single `h1` element (eg. `# My Title`)
- Separate your slides with a horizontal rule (`---` in markdown) except at the end of md files
- Your other slides should have a heading that renders to an `h1` element
- To highlight blocks of code, put !`{lang}` where `{lang}` is the pygment supported language identifier as the first indented line

### ReStructuredText

- Use headings for slide titles
- Separate your slides using an horizontal rule (`----` in RST) except at the end of RST files

---

Rendering
=========

- Put your markdown or rst content in a file, eg `slides.md` or `slides.rst`
- Run `landslide slides.md` or `landslide slides.rst`
- Enjoy your newly generated `presentation.html`

As a proof of concept, you can even transform this annoying `README` into a fancy presentation:

    $ landslide README.md && open presentation.html

Or get it as a PDF document, at least if PrinceXML is installed and available on your system:

    $ landslide README.md -d readme.pdf
    $ open readme.pdf

---

Viewing
=======

- Press `left arrow` and `right arrow` to navigate
- Press `t` to toggle a table of contents for your presentation. Slide titles are links
- Press `n` to toggle slide number visibility
- Press '2' to toggle notes in your slides (specify with the .notes macro)
- Browser zooming is supported

---

Commandline Options
===================

Several options are available using the command line:

    $ landslide/landslide 
    Usage: landslide [options] input.md ...

    Generates fancy HTML5 or PDF slideshows from Markdown sources

    Options:
      -h, --help            show this help message and exit
      -b, --debug           Will display any exception trace to stdin
      -d FILE, --destination=FILE
                            The path to the to the destination file: .html or .pdf
                            extensions allowed (default: presentation.html)
      -e ENCODING, --encoding=ENCODING
                            The encoding of your files (defaults to utf8)
      -i, --embed           Embed base64-encoded images in presentation
      -t THEME, --theme=THEME
                            A theme name, or path to a landlside theme directory
      -o, --direct-ouput    Prints the generated HTML code to stdin; won't work
                            with PDF export
      -q, --quiet           Won't write anything to stdin (silent mode)
      -v, --verbose         Write informational messages to stdin (enabled by
                            default)

    Note: PDF export requires the `prince` program: http://princexml.com/

---

Presentation Configuration
==========================

Landslide allows to configure your presentation using a `cfg` configuration file, therefore easing the aggregation of source directories and the reuse of them accross presentations. Landslide configuration files use the `cfg` syntax. If you know `ini` files, you get the picture. Below is a sample configuration file:

    [landslide]
    theme  = /path/to/my/beautiful/theme
    source = 0_my_first_slides.md
             a_directory
             another_directory
             now_a_slide.markdown
             another_one.rst
    destination = myWonderfulPresentation.html

Please just don't forget to declare the `[landslide]` section. To generate the presentation as configured, just run:

    $ cd /path/to/my/presentation/sources
    $ landslide config.cfg

---

Macros
======

You can use macros to enhance your presentation:

Notes
-----

Add notes to your slides using the `.notes:` keyword, eg.:

    # My Slide Title

    .notes: These are my notes, hidden by default

    My visible content goes here

You can toggle display of notes by pressing the `2` key.

Some other macros are also available by default: `.fx: foo bar` will add the `foo` and `bar` classes to the corresponding slide `<div>` element, easing styling of your presentation using CSS.

---

Registering Macros
==================

so macros are used to transform the HTML contents of your slide.

You can register your own macros by creating `landslide.macro.Macro` derived classes, implementing a `process(content, source=None)` method and returning a tuple containing the modified contents and some css classes you may be wanting to add to your slide `<div>` element. For example:

    !python
    import landslide
    class MyMacro(Macro):
      def process(self, content, source=None):
        return content + '<p>plop</p>', ['plopped_slide']
    
    g = generator.Generator(source='toto.md')
    g.register_macro(MyMacro)
    print g.render()

This will render any slide as below:

    !html
    <div class="slide plopped_slide">
      <header><h2>foo</h2></header>
      <section>
        <p>my slide contents</p>
        <p>plop></p>
      </section>
    </div>

---

Advanced Usage
==============

### Setting Custom Destination File

    $ landslide slides.md -d ~/MyPresentations/KeynoteKiller.html

### Working with Directories

    $ landslide slides/

### Working with Direct Output

    $ landslide slides.md -o | tidy

### Using an Alternate Landslide Theme

    $ landslide slides.md -t mytheme
    $ landslide slides.md -t /path/to/theme/dir

### Embedding Base-64-Encoded Images

    $ landslide slides.md -i

### Exporting to PDF

    $ landslide slides.md -d PowerpointIsDead.pdf

---

Theming
=======

A Landslide theme is a directory following this simple structure:

    mytheme/
    |-- base.html
    |-- css
    |   |-- print.css
    |   `-- screen.css
    `-- js
        `-- slides.js

If a theme does not provide HTML and JS files, those from the default theme will be used. CSS is not optional.

---

Theme Variables
---------------

The `base.html` must be a [Jinja2 template file](http://jinja.pocoo.org/2/documentation/templates) where you can harness the following template variables:

- `css`: the stylesheet contents, available via two keys, `print` and `screen`, both having:
  - a `path_url` key storing the url to the asset file path 
  - a `contents` key storing the asset contents
- `js`: the javascript contents, having:
  - a `path_url` key storing the url to the asset file path 
  - a `contents` key storing the asset contents
- `slides`: the slides list, each one having these properties:
  - `header`: the slide title
  - `content`: the slide contents
  - `number`: the slide number
- `embed`: is the current document a standalone one?
- `num_slides`: the number of slides in current presentation
- `toc`: the Table of Contents, listing sections of the document. Each section has these properties available:
  - `title`: the section title
  - `number`: the slide number of the section
  - `sub`: subsections, if any

---

Styles Scope
============

* To change HTML5 presentation styles, tweak the `css/screen.css` stylesheet bundled with the theme you are using
* For PDF, modify the `css/print.css`

---

Authors
=======

Original Author and Development Lead
------------------------------------

- Adam Zapletal (adamzap@gmail.com)

Co-Author
---------

- Nicolas Perriault (nperriault@gmail.com)

Contributors
------------

- Vincent Agnano (vincent.agnano@particul.es)
- Brad Cupit
- Stéphane Klein (stephane@harobed.org)
- Peter Baumgartner
- Michael Trythall (m@mtrythall.com)
- agonzalezro
- Olivier Verdier

---

Authors
=======

Base Template Authors and Contributors (html5-slides)
-----------------------------------------------------

- Marcin Wichary (mwichary@google.com)
- Ernest Delgado (ernestd@google.com)
- Alex Russell (slightlyoff@chromium.org)


[![Bitdeli Badge](https://d2weczhvl823v0.cloudfront.net/svetlyak40wt/landslide/trend.png)](https://bitdeli.com/free "Bitdeli Badge")

