# Installation

## Installation for Linux

16. First install sphinx:

    ```bash
    apt-get install python3-sphinx
    ```

17. Then run a configuration command:

    ```bash
    sphinx-quickstart
    ```

    More information in [this link](https://www.sphinx-doc.org/en/master/usage/quickstart.html). 
    **(and yes, you should read these docs!)**

18. If you're using mermaid graphs, you need to install an adequate library, 
    [sphinxcontrib-mermaid](https://github.com/mgaitan/sphinxcontrib-mermaid):

    ```bash
    pip install sphinxcontrib-mermaid
    ```

19. For publishing sphinx documentation to GitHub Pages, follow this tutorial: [link](https://www.docslikecode.com/articles/github-pages-python-sphinx/) 
    * Some configuration files could be founded in [this](https://github.com/annegentle/create-demo) repository 
20. To generate pdf from a sphinx documentation, install [PdfLaTeX](https://gist.github.com/rain1024/98dd5e2c6c8c28f9ea9d):

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

21. Convert markdown to RST: https://cloudconvert.com/md-to-rst
22. Install 
23. Install latex tools: 

    ```bash
    sudo apt-get install texlive-full
    sudo apt-get install latexmk
    sudo apt-get install pdflatex
    ```