# Markx
## Help
Last update: 9 Feb 2013

[Markx] is a Markdown editor specifically designed for academic and scientific authoring. It highlights several advantages of Markdown (plain-text, multiple format conversion, easy version control) while still supplying the basic features which are a must for academic publications (citations, math rendering, layouts).

### Writing Markdown
[Markdown] is a markup language.

Markdown is very easy to learn and there are many online tutorials, just use Google.

#### Markdown Flavor
You should use **Pandoc-flavored Markdown** as both converters ([Pandoc] and [Docverter] use that). The HTML preview on the right is processed using [PageDown], so there could be some thing it doesn't process like Pandoc does (found something? open an [issue]).

#### Math
You can use $LaTeX$. Just write it between `$`s or `\\(` and `\\)` for inline equations and `$$`s or `\\[` and `\\]` for display mode:

- Inline mode $e=mc^2$
- Display mode: $$\frac{df(x)}{dt}=lim_{x \to 0}{\frac{f(x+h)-f(x)}{h}}$$

#### Citations
You should create a new `config.py` file in the Markx repository with the key-value pair 
```
BIB_FILE = r'/path/to/bib/file'
```
replacing `/path/to/bib/file` with the *absolute* path to a `.bib` BibTeX citations file (no `~`s in the path). If you don't have one than Markx doesn't support your citation format yet. If you use Mendeley it is easy to set it up to [sync to a BibTeX file](http://blog.mendeley.com/tipstricks/howto-use-mendeley-to-create-citations-using-latex-and-bibtex/). If you do not supply a path to a `.bib` file you will not be able to use the citations features of Markx. 

To insert a citation, get the citation key - usually the last name of the first author, with a capital initial, and the year of publication, without spaces. If the `.bib` file has more than one publication with that key they are post-fixed with lowercase letters. Then add the citation key to the editor, wrapped by `[@` and `]`.
For example: `[@Drake1991]`. Markx doesn't currently preview the citation keys in the previewed text, but it does:

1. create a bibliography at the bottom of the preview text
1. allows you to download a `.bib` file corresponding to the citation keys in the Markdown text
1. send the bibliography to [Pandoc] for conversion

You must click the *update citations* <i class="icon-books"></i> button after adding, removing or changing citaiton keys, as they will not be updated in real-time.

### Toolbar
1. Use the *GitHub* <i class="icon-github-2"></i> button to **sign-in to [GitHub]** (see more details below).
1. Use the *Screen* <i class="icon-screen"></i> button to change between **editor**, **preview** and **dual** modes.
1. Use the *Books* <i class="icon-books"></i> button to **parse citation keys** such as [@Drake1991].
1. Use the *Download* <i class="icon-download-2"></i> button to **download and convert** the Markdown text to various format or to download a *BibTeX* file of the citations referenced in the text.
1. Click on **P** or **D** to **change the Markdown converter** between [Pandoc] and [Docverter]. 
  - Pandoc: must be installed on local machine, can't process image URLs, slow conversion to PDF on Windows, requires *pdflatex* to convert to PDF.
 - Docverter: must be connected to the internet to be used, doesn't process citation keys and bibliography.
1. Click the *Code* <i class="icon-code"></i> button to get change the **code highlighting styles**. Example code above.
1. The grey box with the numbers displays the **word count**.

### GitHub Integration
**Your [GitHub] username and password are never sent to the Markx server**. They are sent by JavaScript to directly to the GitHub API server using [Github.js]. Your credentials are not saved in cookies and are removed from the browser memory as soon as the sign in is complete. You can also sign out of GitHub by clicking the *sign out* <i class="icon-exit"></i> button. If you would like to check the security of this feature please view the `signinToGithub` function in [markx.js] and open an [issue] if you find any problems.

After you sign in to GitHub you can use the GitHub toolbar to:

1. Click the  *GitHub* <i class="icon-github-2"></i> button - this doesn't do anything right now.
1. Change the username - doesn't do anything yet.
1. **Choose a repository** that belongs to the specified user.
1. Click the first *folder* <i class="icon-folder-open"></i> button  to load the **branch list**
1. **Choose a branch** if the selected repository
1. Click the second *folder* <i class="icon-folder-open"></i> button  to **load the files list** (currently only loads a single level, no subfolders)
1. **Choose a file** in the selected branch
1. Click the *download* <i class="icon-cloud-download"></i> button to **pull the file** to the editor. The current contents will be deleted without saving them.
1. Click the *upload* <i class="icon-cloud-upload"></i> button to **push the editor contents** to the selected file. This will create a new *commit* on the repository. You must **fill a commit message** before pushing. Commit messages should be ~50 characters and briefly explain the reason for this commit. After the push is finalized you will get a success or failure message.
1. Click the *sign out* <i class="icon-exit"></i> button in the general toolbar to **sign out of GitHub**.

There is currently no support for creation of new files. You can [do that on GitHub](https://github.com/blog/1327-creating-files-on-github) very easily or in the traditional way via the terminal/command line (`touch <filename>`, `git add <filename>`, `git commit <filename> -m "new file"`, `git push`). 

There is also no way to commit the `.bib` citations file to GitHub via Markx. These features will be added in the future.

### Editor Toolbar
The buttons above the editor window are part of the [PageDown] markdown editor. They allow quick shortcuts to common Markdown markups.

### Support
The best way to get support is to open an [issue]. If you can't open issue because you don't have a [GitHub] user, just get one, they are free. 

### Contribution
We would love for you to contribute to Markx. The project code is hosted in [GitHub][Markx]. Fork the project or open an [issue] so we can talk on how we can collaborate. 

The server side is written in Python with the [Flask] web framework (Ruby and Node equivalents are Sinatra and Express) and [requests] for connecting to [Docverter].
The two Markdown converters are [Pandoc] and [Docverter], which is a cloud-based Pandoc.

The client side is written with HTML+CSS+JS, using the JavaScript libraries:

1. [Twitter Bootstrap] and [jQuery] for the UI
1. [PageDown] as the Markdown editor and real-time HTML converter 
1. [Github.js] for the GitHub API
1. [BibTeX-js] for previewing the bibliography
1. [Google Code Prettifier] for code highlighting
1. [MathJax] for math rendering

## References
The references header is **your** job, [Pandoc] will only create a citation list, without a header. However, it will always put it at the end of the output file (at least via Markx) so you can just put a *References* header at the end of your file.

[Markdown]: http://daringfireball.net/projects/markdown/
[Pandoc]: http://johnmacfarlane.net/pandoc
[Python]: http://python.org/
[Flask]: http://flask.pocoo.org/
[Twitter Bootstrap]: http://blog.getbootstrap.com/
[Google Code Prettifier]: http://code.google.com/p/google-code-prettify/
[Icomoon Free]: http://keyamoon.com/icomoon/
[MathJax]: http://mathjax.org/
[PageDown]: http://code.google.com/p/pagedown/
[BibTeX-js]: http://bibtex-js.googlecode.com/
[Stack Overflow]: http://stackoverflow.com/
[git]: http://git-scm.com/
[BibTeX]: http://www.bibtex.org/
[GitHub]: https://github.com/
[Github.js]: https://github.com/michael/github
[Docverter]: http://www.docverter.com/
[issue]: https://github.com/yoavram/markx/issues
[markx.js]: https://github.com/yoavram/markx/blob/master/static/js/markx.js
[Markx]: https://github.com/yoavram/markx
[requests]: http://python-requests.org/
	