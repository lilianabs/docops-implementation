We need to install a Static Site Generator (SSG) to create our documentation site. For this implementation of Docs as Code, we'll be using [Mkdocs](https://www.mkdocs.org/) because it is very simple and enables us to customize the documentation site using a theme.

## Prerequisites

Before we create our Mkdocs static site, we need to install Python 3 so that we can use the `pip` command to install Mkdocs, and the Mkdocs Material theme. After installing (or verifying that you have) Python 3 on your local system, execute the following commands:

* **Install Mkdocs:**

     ```
       pip install mkdocs
     ```

* **Install the Mkdocs Material theme:**

     ```
       pip install mkdocs-material
     ```

## Create the documentation site

We can now create our documentation site:

1. In the terminal, change the current working directory to the location where we want to store the repository’s contents using the **change directory** (cd) command.
1. Create the Static Site Mkdocs project: 

    ```
      mkdocs new documentation-site-name
    ```

Mkdocs creates the directory documentation-site-name with the following contents:

```
.
├── docs
│   └── index.md
└── mkdocs.yml 
```

You can preview the documentation site on your local system with the command `mkdocs serve`.

## Add the Material theme to the documentation site

We add the material theme to our documentation site:

1. Open the mkdocs.yml configuration file.
1. In this file, enter the following settings:

```
      site_name: 'Name of your documentation site'
      theme:
      theme:
        name: material
        logo: images/typewriter.png
        palette:
          primary: white
          accent: white
        font:
          text: 'Roboto'
          code: 'Roboto Mono'
      nav:
          - Home: index.md

```
The settings above are the configuration of this documentation site. However, we can do more customizations to the [Material theme](https://squidfunk.github.io/mkdocs-material/customization/) so that we can add our own css file and override the HTML code that Mkdocs creates. 