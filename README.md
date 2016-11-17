# CEREMONY

A static site generator, as simple as I could imagine it.

## Installation

    pip install ceremony

## Dependencies

* jinja2
* markdown
* sass

## Usage

    usage: ceremony [-h] [-v] [-C] [COMMAND] [ARGS [ARGS ...]]

    Website building tool

    positional arguments:
      COMMAND         Command to execute [watch | init | make] (default: make)
      ARGS            Arguments to command (default: None)

    optional arguments:
      -h, --help      show this help message and exit
      -v, --verbose   Verbal exuberance mode (default: False)
      -C, --no-cache  Disable the mstat cache (default: False)

To create a new site, run

    ceremony init [<site-directory>]

All this does is create the default directory layout in the current
directory or `<site-directory>`, which is

    build/        The generated site is written here.
    pages/        The source .md and .html documents go here.
    layouts/      The Jinja2 templates go here.
    css/          SCSS and CSS files go here.
    js/           Files here are copied to build/js/
    img/          Files here are copied to build/img/

To generate the site, run

    ceremony

To watch the source files and regenerate on changes, run

    ceremony watch

## `pages/`

The files in `pages/` are processed into actual webpages via the
jinja2 templates in `layouts/`. The general structure of all pages in
`pages/` is:

    <key>: <value>
    <key>: <value>
    ...

    <text>

The values set at the top of the file are available from the jinja2
template as `{{<key>}}`. The text (everything following the key:value
section) is available as `{{text}}`. This is true with the exception
of a few special values:

* `layout`: This selects the base layout (name of jinja2 template minus `.html` extension)
* `pretty_url`: Don't prettify the generated URL layout.

### `layout`

The layout determines the base template used for the generated page. Maybe I should have called it `template` instead...

The text of the post (post-processed markdown or raw html depending on the source file type) is available to the templates as the `{{text}}` variable.

Here's an example layout:

    <!doctype html>
    <html>
      <head>
        <title>{{title}}</title>
      </head>
      <body>
        {{text}}
      </body>
    </html>

### `pretty_url`

Set to true by default. If set, `my_page.md` becomes
`my_page/index.html` in the `build/` directory. If set to `false`,
`my_page.md` generates `my_page.html`.


