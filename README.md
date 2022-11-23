# sphinxTutorial

The repository https://github.com/CTISM-Prof-Henry/gitEssentials is already configured with the below tutorial. Use it as reference.

1. First install sphinx:

```bash
apt-get install python3-sphinx
```

2. Then run a configuration command:

```bash
sphinx-quickstart
```

More information in [this link](https://www.sphinx-doc.org/en/master/usage/quickstart.html). **(and yes, you should read these docs!)**

3. If you're using mermaid graphs, you need to install an adequate library, [sphinxcontrib-mermaid](https://github.com/mgaitan/sphinxcontrib-mermaid):

```bash
pip install sphinxcontrib-mermaid
```

4. For publishing sphinx documentation to Github Pages, follow this tutorial: [link](https://www.docslikecode.com/articles/github-pages-python-sphinx/) 
  * Some configuration files could be founded in [this](https://github.com/annegentle/create-demo) repository 
5. To generate pdf from a sphinx documentation, install [PdfLaTeX](https://gist.github.com/rain1024/98dd5e2c6c8c28f9ea9d):

```bash
sudo apt-get install texlive-latex-base texlive-fonts-recommended texlive-fonts-extra texlive-latex-extra
```

Then install mermaid-cli:


```bash
npm install mermaid.cli
```

And add mmdc to PATH:

```bash
export PATH="./node_modules/.bin:$PATH" 
```


7. Convert markdown to RST: https://cloudconvert.com/md-to-rst
8. Install 


## Usage

To generate the docs for github:

```bash
make github
```

To Generate PDF:

```bash
make latex
cd build/latex
pdflatex <name of file>
```
