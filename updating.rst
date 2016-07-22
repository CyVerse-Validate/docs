.. _updating:

Updating the docs
=================

Updating the documentation is easy and should be done as users discover useful tips and tricks along their own workflows. All documentation is stored on github in plain-text at https://github.com/CyVerse-Validate/docs.

Accessing the source
--------------------

**from the terminal**

from your working directory, download the project from github::

     git clone https://github.com/cyverse-validate/docs.git

cd into the new folder, ls to view files::

     vim filename.rst

i to start writing, wq to save and close. For VIM resources, try https://danielmiessler.com/study/vim/, or type vimtutor at your terminal.

Follow the standard git commit process to request changes. For a full introduction see

- https://yangsu.github.io/pull-request-tutorial/
- http://swcarpentry.github.io/git-novice/

After a change has been made to the master repository, `readthedocs <https://readthedocs.org>`_ automatically builds fresh html documentation hosted on their servers.

**from the desktop**

browse to https://github.com/CyVerse-Validate/validate-doc

click "Clone or Download" at the right. You can use the github desktop app or work with the compressed folder using the text editor of your choice. For comprehensive edits you may wish to use `Atom <https://atom.io>`_ with the language-sphinx package enabled with the documentation directory selected as your project folder.


For more on Sphinx / Read the Docs, see:

- http://www.sphinx-doc.org/en/stable/rest.html
- http://docs.readthedocs.io/en/latest/


Updating table of contents
--------------------------

One unique feature of Sphinx is its ability to cross reference between pages and maintain a hierarchy of separate documents, making it preferable to other markdown languages for documenting extensible projects. These features are handled using unique directives documented <here>. The most important of these will be “toctree” where you define your table of contents. To add an additional page, you’d update index.rst to include the new document, and create a new text document "filename.rst”. The formatting is fairly self-explanatory; see the existing index for an example.

Building Sphinx html on your own machine
-----------------------------------------

To preview the documentation, you'll need to compile html files using the command::

  make html

from the project root. Fix any warnings or errors that appear (generally caused by the existence of unlinked files or absence of linked ones), and view the html output in your default browser with::

  open _build/html/index.html

On a windows machine, run make.bat instead.
