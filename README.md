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
   * Make sure to select option to run `conda init` in the process! Otherwise you'll have to install it again
4. Open a command line window 
5. Navigate to this repository's folder with `cd` (e.g. `cd /home/henry/sphinxTutorial`)
6. Create a new conda environment: 

   ```bash
   conda create --name sphinx pip --yes
   ```

7. Activate it:

   ```bash
   conda activate sphinx
   ```
   
8. Install libraries:

   ```bash
   pip install --requirement requirements.txt
   ```

9. Run sphinx-quickstart:

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

10. Follow now the [Sphinx Tutorial](https://www.sphinx-doc.org/en/master/usage/quickstart.html) on how to prepare
    `.rst` files. This tutorial will not teach you how to create RestructuredText files, but you can find a cheatsheet 
    [here](https://github.com/ralsina/rst-cheatsheet/blob/master/rst-cheatsheet.rst). This tutorial will also
    proceed with the files as they were created by `sphinx-quickstart`.

11. We need to modify `Makefile` to add two new `make` commands:
    * `make github`: generates html files and moves to `docs` folder;
    * `remove_latex_files`: removes previous latex files from `build/latex` folder (LaTeX can render wrong pdfs if old
      files are not removed)

    Also, you should make sure that `SOURCEDIR` and `BUILDDIR` are set to the right folders:
   
    ```bash
    SOURCEDIR     = source
    BUILDDIR      = build
    ```

    Your `Makefile` should look like this:

    ```bash
    # Minimal makefile for Sphinx documentation
    #
    
    # You can set these variables from the command line, and also
    # from the environment for the first two.
    SPHINXOPTS    ?=
    SPHINXBUILD   ?= sphinx-build
    SOURCEDIR     = source
    BUILDDIR      = build
    
    # Put it first so that "make" without argument is like "make help".
    help:
        @$(SPHINXBUILD) -M help "$(SOURCEDIR)" "$(BUILDDIR)" $(SPHINXOPTS) $(O)
    
    .PHONY: help Makefile
    
    
    github:
        @make html
        @cp -a build/html/. ./docs
    
    
    remove_latex_files:
        rm -f -r build/latex/*
    
    
    # Catch-all target: route all unknown targets to Sphinx using the new
    # "make mode" option.  $(O) is meant as a shortcut for $(SPHINXOPTS).
    %: Makefile
        @$(SPHINXBUILD) -M $@ "$(SOURCEDIR)" "$(BUILDDIR)" $(SPHINXOPTS) $(O)

    ```

12. To properly deploy html files to GitHub pages, create a `docs` folder, and add a `.nojekyll` file inside it
    * Check the spelling! The name of the file must be exactly `.nojekyll` (no blank spaces)
13. Enable GitHub pages for your repository. See **Publishing from a branch** on 
    [this tutorial](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)
    for a step-by-step tutorial. Make sure that you use the folder `docs` for the documentation!
14. Run `make github` from the command line, and then commit/push changes to remote to verify if all is working properly.
15. To generate mermaid graphs, you need to install [mermaid.cli](https://github.com/mermaid-js/mermaid-cli) locally in 
    your machine, using [yarn](https://classic.yarnpkg.com/lang/en/docs/install/)
    
    ```bash
    sudo apt-get install yarn
    yarn add mermaid.cli
    ```

16. Add `mmdc` to PATH. Run the following command in the terminal (you'll need to repeat it every time you want to 
    re-generate mermaid graphs):

    ```bash
    export PATH="./node_modules/.bin:$PATH" 
    ```

17. To generate pdfs with latex, install [pdflatex](https://www.math.rug.nl/~trentelman/jacob/pdflatex/pdflatex.html) 
    and other tools:

    ```bash
    sudo apt-get install texlive-full
    sudo apt-get install latexmk
    sudo apt-get install pdflatex
    ```

18. Create a new file, `generate_all.sh`, and add these lines:

   ```bash
   # activate sphinx environment before running this file!
   # conda activate sphinx
   export PATH=$PATH:node_modules/.bin
   # add instructions to generate mermaid graphs from files here:
   # mmdc -i some_graph.mmd -o some_graph.png
   make remove_latex_files
   make github
   make latex
   (cd build/latex && pdflatex main.tex)
   (cd build/latex && pdflatex main.tex)
   ```

   Replace `# mmdc -i some_graph.mmd -o some_graph.png` with a command to generate custom mermaid graphs from `.mmd` 
   files.

19. Add or append some configurations to `source/conf.py`:

    * General configuration section:
      * `extensions = ['sphinxcontrib.mermaid']`
    * Latex configuration section (create one section with comment characters if not present):
      * `latex_engine = 'pdflatex'`
      * If using Brazilian portuguese, add 
        ```python
        latex_elements = {
             'babel': r'\usepackage[brazil]{babel}'
        }
        ```
      * ```python
        latex_documents = [
            (master_doc, 'main.tex', 'Python Essentials', 'Henry Cagnini', 'manual'),
        ]
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

1. Open a command line window 
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
   
   Finally, to generate latex files:

   ```bash
   make latex
   ```
   
   Then, access folder `build/latex` and compile the document with `pdflatex`:

   ```bash
   pdflatex <entry tex file>
   ```
   
   Where `<entry tex file>` is the main tex file (e.g. `main.tex`, `pdflatex main.tex`)

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

### Cannot install `mermaid.cli` with yarn

Try to run the following commands:

```bash
sudo apt remove cmdtest
sudo apt remove yarn
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
sudo apt-get update
sudo apt-get install yarn -y
```

## Additional resources

* [Sphinx documentation](https://www.sphinx-doc.org/en/master)
* [RestructuredText cheatsheet](https://github.com/ralsina/rst-cheatsheet/blob/master/rst-cheatsheet.rst)
* [GitHub pages](https://pages.github.com/)
  * [Generating docs from branch](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)
* [mermaid documentation](https://mermaid-js.github.io/mermaid/#/)
* [mermaid live](https://mermaid.live)

