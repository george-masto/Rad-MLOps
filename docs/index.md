# Welcome to MkDocs

For full documentation visit [mkdocs.org](https://www.mkdocs.org).

## Commands

* `mkdocs new [dir-name]` - Create a new project.
* `mkdocs serve` - Start the live-reloading docs server.
* `mkdocs build` - Build the documentation site.
* `mkdocs -h` - Print help message and exit.

## Project layout

    mkdocs.yml    # The configuration file.
    docs/
        index.md  # The documentation homepage.
        ...       # Other markdown pages, images and other files.

## Code Annotation Examples

Testing writing `code` here.

```
Testing writing code block here

```

Testing `py` code here

```py
import tensorflow as tf
def just_a_function():
    ASSET_DIR = './'
    asset = 'test'
```
adding file name as title

```py title='this_is_filename.py'
import tensorflow as tf
def just_a_function():
    ASSET_DIR = './'
    asset = 'test'
```
adding line numbers

```py title='this_is_filename.py' linenums="1"
import tensorflow as tf
def just_a_function():
    ASSET_DIR = './'
    asset = 'test'
```
Highlighting lines

```py title='this_is_filename.py' linenums="1" hl_lines="2 3"
import tensorflow as tf
def just_a_function():
    ASSET_DIR = './'
    asset = 'test'
```

Emojis

:smile:

:fontawesome-regular-face-laugh-wink:

:octicons-heart-fill-24:{ .heart }