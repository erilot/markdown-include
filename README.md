# Markdown-Include

This is an extension to [Python-Markdown](https://pythonhosted.org/Markdown/)
which provides an "include" function, similar to that found in
LaTeX (and also the C pre-processor and Fortran). I originally wrote it for my
[FORD](https://github.com/cmacmackin/ford) Fortran auto-documentation generator.


## Installation

** Note: this fork is a work in progress. The following instructions will install
the original package, not this one. **

This module can now be installed using ``pip``.

    pip install markdown-include


## Usage
This module can be used in a program in the following way:

```python
import markdown
html = markdown.markdown(source, extensions=['markdown_include.include'])
```

The syntax for use within your Markdown files is ``{!filename!}``. This
statement will be replaced by the contents of ``filename``. Markdown-Include
will work recursively, so any included files within ``filename`` will also be
included. This replacement is done prior to any other
Markdown processing, so any Markdown syntax that you want can be used within
your included files. Note that this is a change from the previous version.
It was felt that this syntax was less likely to conflict with any code
fragments present in the Markdown.

By default, all file-names are evaluated relative to the location from which
Markdown is being called. If you would like to change the directory relative to
which paths are evaluated, then this can be done by specifying the extension
setting ``base_path``.


```python
import markdown
from markdown_include.include import MarkdownInclude

# Markdown Extensions
markdown_include = MarkdownInclude(
    configs={'base_path':'/srv/content/', 'encoding': 'iso-8859-1'}
)
html = markdown.markdown(source, extensions=[markdown_include])
```

For MkDocs, configure your mkdocs.yml file as follows:
```yaml
markdown_extensions:
  - markdown_include.include:
      base_path: docs
```

## ChangeLog
### Version 0.5.1
Bugfix for a syntax error.
### Version 0.5
Corrected some errors in documentation and merged in commits of
[diegobz](https://github.com/diegobz) to add support for encoding and tidy up
the source code.
### Version 0.4
Fixed problem related to passing configurations to the extension.
### Version 0.3
Added support for Python 3.
### Version 0.2
Changed the API to be less likely to conflict with other syntax.
### Version 0.1
Initial release.
