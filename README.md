# sphinxTutorial

There is very few I can say about Sphinx; you should read 
[Sphinx's Official Documentation page](https://www.sphinx-doc.org/en/master) for a proper introduction.

Rather, this repository is a tutorial on how to make Sphinx work under Windows and Linux, for some personal projects of 
mine. The requirements I have are:

* The documentation uses [mermaid](https://mermaid-js.github.io/mermaid/#/) graphs;
* The documentation needs to be published to [GitHub Pages](https://pages.github.com/);
* A well-formatted PDF must be generated.

The repository https://github.com/CTISM-Prof-Henry/gitEssentials complies with above requirements, and was done following
this repository's tutorial. Use it as reference.

## Pre-requisites

This tutorial makes some assumptions on your previous knowledge. More specifically, it assumes that you have previous
knowledge on:

* GitHub;
* git;
* Windows and/or Linux command line;
* Python and its flavor Anaconda.

## Installation

Follow the steps below to install Sphinx on either Linux or Windows.

<details>
    <summary><h3>Installation for Windows</h3></summary>

1. **(optional - only for this tutorial)** Fork this repository on GitHub, and then clone it to your machine 
2. **(optional - only for this tutorial)** On `.gitignore`, at the bottom of the document, change these lines

   ```.gitignore
   # SPHINX TUTORIAL: comment lines below
   docs/
   docsource/
   source/
   make.bat
   Makefile
   # SPHINX TUTORIAL: comment lines above
   ```
   
   to these lines

   ```.gitignore
   # SPHINX TUTORIAL: comment lines below
   # docs/
   # docsource/
   # source/
   # make.bat
   # Makefile
   # SPHINX TUTORIAL: comment lines above
   ```

3. Download and install Python Anaconda: https://www.anaconda.com/products/distribution
4. [Add conda to PATH](https://www.mathworks.com/matlabcentral/answers/94933-how-do-i-edit-my-system-path-in-windows)
   * This can be done either through the Installation Wizard, or after installation (though it's easier using the Wizard)
   * Add the path where conda was installed to User's PATH variable
5. Open a command line window (`Windows + R` keys, type `cmd`, hit `Enter`)
6. Navigate to this repository's folder with `cd` (e.g. `cd C:\Users\username\sphinxTutorial`)
7. Create a new conda environment: 

   ```bash
   conda create --name sphinx pip --yes
   ```

8. Activate it:

   ```bash
   conda activate sphinx
   ```
   
9. Install libraries:

   ```bash
   pip install --requirement requirements.txt
   ```

10. Run sphinx-quickstart:

    ```bash
    sphinx-quickstart
    ```
   
    You'll be prompted to answer some questions:

    * For this tutorial, I personally prefer to separate build and docs folders, so I would choose `y` in the 
      *Separate source and build directories (y/n):* question. But you can do otherwise in future projects.
    * Insert a project name. For this tutorial, we will use **sphinxTutorial**
    * Insert your (full) name
    * Insert a project release number (e.g. `0.1`, `0.2`, `1.0`, etc)
    * Insert project's language. For brazilian Portuguese, use `pt_BR` 

11. Follow now the [Sphinx Tutorial](https://www.sphinx-doc.org/en/master/usage/quickstart.html) on how to prepare
    `.rst` files. This tutorial will not teach you how to create RestructuredText files, but you can find a cheatsheet 
    [here](https://github.com/ralsina/rst-cheatsheet/blob/master/rst-cheatsheet.rst). This tutorial will also
    proceed with the files as they were created by `sphinx-quickstart`.

12. We need to modify `make.bat` to add two new `make` commands:
    * `make github`: generates html files and moves to `docs` folder;
    * `remove_latex_files`: removes previous latex files from `build/latex` folder (LaTeX can render wrong pdfs if old
      files are not removed)

    Also, you should make sure that `SOURCEDIR` and `BUILDDIR` are set to the right folders:
   
    ```shell
    set SOURCEDIR=source
    set BUILDDIR=build
    ```

    Your `make.bat` should look like this:

    ```shell
    @ECHO OFF
   
    pushd %~dp0
   
    REM Command file for Sphinx documentation
   
    if "%SPHINXBUILD%" == "" (
        set SPHINXBUILD=sphinx-build
    )
    set SOURCEDIR=source
    set BUILDDIR=build
    set DOCSDIR=docs
   
    %SPHINXBUILD% >NUL 2>NUL
    if errorlevel 9009 (
        echo.
        echo.The 'sphinx-build' command was not found. Make sure you have Sphinx
        echo.installed, then set the SPHINXBUILD environment variable to point
        echo.to the full path of the 'sphinx-build' executable. Alternatively you
        echo.may add the Sphinx directory to PATH.
        echo.
        echo.If you don't have Sphinx installed, grab it from
        echo.https://www.sphinx-doc.org/
        exit /b 1
    )
   
    if "%1" == "" goto help
   
    if "%1" == "github" goto github
   
    if "%1" == "remove_latex_files" goto remove_latex_files
   
    %SPHINXBUILD% -M %1 %SOURCEDIR% %BUILDDIR% %SPHINXOPTS% %O%
    goto end
   
    :help
    %SPHINXBUILD% -M help %SOURCEDIR% %BUILDDIR% %SPHINXOPTS% %O%
    goto end
   
    :github
    %SPHINXBUILD% -M html %SOURCEDIR% %BUILDDIR% %SPHINXOPTS% %O%
    @robocopy %BUILDDIR%\html %DOCSDIR% * /E
    goto end
   
    :remove_latex_files
    @del /S /Q %BUILDDIR%\latex\*
    goto end
   
    :end
    popd
    ```

13. To properly deploy html files to GitHub pages, create a `docs` folder, and add a `.nojekyll` file inside it
    * Check the spelling! The name of the file must be exactly `.nojekyll` (no blank spaces)
14. Enable GitHub pages for your repository. See **Publishing from a branch** on 
    [this tutorial](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)
    for a step-by-step tutorial. Make sure that you use the folder `docs` for the documentation!
15. Run `make github` from the command line, and then commit/push changes to remote to verify if all is working properly.

</details>

<details>
    <summary><h3>Installation for Linux</h3></summary>

1. First install sphinx:

   ```bash
   apt-get install python3-sphinx
   ```

2. Then run a configuration command:

   ```bash
   sphinx-quickstart
   ```

   More information in [this link](https://www.sphinx-doc.org/en/master/usage/quickstart.html). 
   **(and yes, you should read these docs!)**

3. If you're using mermaid graphs, you need to install an adequate library, 
   [sphinxcontrib-mermaid](https://github.com/mgaitan/sphinxcontrib-mermaid):

   ```bash
   pip install sphinxcontrib-mermaid
   ```

4. For publishing sphinx documentation to GitHub Pages, follow this tutorial: [link](https://www.docslikecode.com/articles/github-pages-python-sphinx/) 
   * Some configuration files could be founded in [this](https://github.com/annegentle/create-demo) repository 
5. To generate pdf from a sphinx documentation, install [PdfLaTeX](https://gist.github.com/rain1024/98dd5e2c6c8c28f9ea9d):

   ```bash
   sudo apt-get install texlive-latex-base texlive-fonts-recommended texlive-fonts-extra texlive-latex-extra
   ```

   Then install mermaid-cli:

   ```bash
   yarn add mermaid.cli
   ```

   **Note:** if problems are encountering when trying to install with yarn, try this:

   ```bash
   sudo apt remove cmdtest
   sudo apt remove yarn
   curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
   echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
   sudo apt-get update
   sudo apt-get install yarn -y
   ```

   And add `mmdc` to PATH:

   ```bash
   export PATH="./node_modules/.bin:$PATH" 
   ```

6. Convert markdown to RST: https://cloudconvert.com/md-to-rst
7. Install 
8. Install latex tools: 

   ```bash
   sudo apt-get install texlive-full
   sudo apt-get install latexmk
   sudo apt-get install pdflatex
   ```
   
</details>

## Usage

Follow the steps below to generate documentation with Sphinx on either Linux or Windows.

<details>
    <summary><h3>Using on Windows</h3></summary>

Generating mermaid graphs and latex files/pdf is currently unavailable on Windows. Rather, use instructions below to 
generate html documentation:

1. Open a command line window (`Windows + R` keys, type `cmd`, hit `Enter`)
2. Navigate to this repository's folder with `cd` (e.g. `cd C:\Users\username\sphinxTutorial`)
3. Activate sphinx conda environment:

   ```bash 
   conda activate sphinx
   ```

4. To generate html files:

   ```bash
   make html
   ```
   
   Or, alternatively, to generate html files **and** move them to docs folder (for GitHub pages):

   ```bash
   make github
   ```

</details>

<details>
    <summary><h3>Using on Linux</h3></summary>

3. To Generate PDF with pdflatex:

   ```bash
   make latex
   cd build/latex
   pdflatex <name of file>
   ```

You'll have to do some additional configuration if using pdflatext o generate pdf:

Install babel for Brazilian Portuguese (if that's the case):

```tlmgr install babel-portuges```

</details>

## Known issues

### Mermaid graphs make `make latex` hang forever

This happens because the syntax of the graph is incompatible with the version run by `mmdc`. `mmdc` displays an error
message, but this isn't shown to the end user, and the process runs forever.

The workaround here is to put mermaid graphs in `.mmd` files and render then with `mmdc`:

```bash
mmdc -i some_diagram.mmd -o some_diagram.png
```

Which will then display the error message (which you should correct). Once all is fixed, include generated `.pngs` 
into `.rst` documentation.

## Additional resources

* [Sphinx documentation](https://www.sphinx-doc.org/en/master)
* [RestructuredText cheatsheet](https://github.com/ralsina/rst-cheatsheet/blob/master/rst-cheatsheet.rst)
* [GitHub pages](https://pages.github.com/)
  * [Generating docs from branch](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)
* [mermaid documentation](https://mermaid-js.github.io/mermaid/#/)
* [mermaid live](https://mermaid.live)

