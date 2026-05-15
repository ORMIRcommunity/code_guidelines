# Documentation

**🚧 Page under construction 🚧**

Documentation is important because [xxx]

---

## What Python documentation style (docstrings) do I use?
We use [NumPy style docstrings](https://numpydoc.readthedocs.io/en/latest/format.html)
to document our code.
Docstrings describe the functionality and parameters of code and are enclosed in triple quotes (`""" ... """`). 
They are typically placed at the beginning of the module, class, function, or method they describe. 
Here is the example of Numpy style docstrings for functions:

```
def my_function(input1, input2):
    """This function does ...

    Parameters
    ----------
    input1 : type
        Description of input1
    input2 : type
        Description of input2

    Returns
    -------
    output : int
        Description of output
    """

    # function body
    return output
```
The documentation is between the header and the body, and it contains at least the following sections:
- Description: An explanation of what the function does
- Parameters: A description of each parameter the function accepts, including name, data type, definition, and default values
- Returns: A description of the values returned by the function, including name, data type, definition, and any special cases
You can find a complete description of Numpy style docstrings on the [Numpy website](https://numpydoc.readthedocs.io/en/latest/format.html)

---

## How do I create NumPy-style documentation (docstrings) fast?

With your AI of preference (Claude Code, ChatGPT, etc)! Example of command:

> write docstrings in Numpy style for the following function: [paste your function]

*Important*: Double-check the content of the AI and correct wherever needed!

---

## How do I publish documentation *automatically* using Read the Docs?
[Read the Docs](https://docs.readthedocs.io/en/stable/)is a tool to generate code from docstrings and to host and publish documentation on the web. To learn how to use Read the Docs follow their step-by-step tutorial. An excellent example of Read the Docs is the [documentation of Ciclope](https://ciclope.readthedocs.io/en/).

---

## How do I publish documentation *manually* using Sphinx?
[Sphinx](https://www.sphinx-doc.org/en) is a tool to write and generate documentation from docstrings.
You can find guidelines on how to use Sphynx here.

---

## How do I create a website using Jupyter Book?
[To be updated for jupyter book 2]
You can find comprehensive guidelines and a template on the Jupyter Book website. In a nutshell:
1. For each website page, create one .md or .ipynb file and write the content using markdown
2. Create a _toc.yml and a _config.yml files (see examples here)
3. Install Jupyter Book with the command pip install jupyter-book
4. Create your book with the command jupyter-book build book_name
5. The created .html files will be in the folder _build/html

---

## How do I deploy my Jupyter Book website on GitHub using CI?
[To be updated for jupyter book 2]
CI (Continuous Integration) is a tool that allows you to automate procedures, and in GitHub it is called Actions. Deploying a Jupyter Book website using Actions is very convenient because it automates the building process, ensuring that your site is continuously and seamlessly updated with every change pushed to the repository. You can find detailed information on how to deploy a Jupyter Book website using Actions here. Briefly:
1. Make sure that your repository contains all the website content files, (that is, .md and/or .ipynb files, together with figures, etc.), _config.yml and _toc.yml. Note: You do not need to push the _built folder because GitHub Action will create the .html files of your website
2. In the same repository, add the following files from this ORMIR template folder: requirements.txt, .nojekyll, and .github/workflows/ci.yml (note that .nojekyll and .github/workflows/ci.yml are hidden files)
3. Go to your GitHub repository on GitHub.com. In the top bar, click on Settings, and in the appearing left panel, click on Pages. Under Build and deployment, Source, select GitHub Actions
4. Every time you push new content to the repository, the book will be automatically created and the new .html files will be automatically deployed to your website. You can follow the progress by clicking Actions on the top bar of the GitHub repository
