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

And add mmdc to PATH:

```bash
export PATH="./node_modules/.bin:$PATH" 
```


7. Convert markdown to RST: https://cloudconvert.com/md-to-rst
8. Install 
9. Instal latex tools: 

   ```bash
   sudo apt-get install texlive-full
   sudo apt-get install latexmk
   sudo apt-get install pdflatex
   ```

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

You'll have to do some additional configuration if using pdflatext o generate pdf:

Install babel for Brazilian Portuguese (if that's the case):

```tlmgr install babel-portuges```
