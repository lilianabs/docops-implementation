We use use the prose linter [Vale](https://errata-ai.gitbook.io/vale/) the enforce the use of a style guide. Before configuring the style that we want to use, we need to install Vale with the command `brew install vale` (we need to install the package manager [brew](https://brew.sh/)). 

Vale has an extension system to define the rules that you want to validate. We define this rules by creating YAML files and a configuration file `.vale.ini`. For this implementation, we use the [Google developer documentation style guide](https://developers.google.com/style) YAML files.

1. Go to the [Vale-compatible](https://github.com/errata-ai/Google/releases) implementation of the Google developer documentation guide repository.
2. Download the latest release of the `Google.zip` file.
3. In the terminal, change the current working directory to the `documentation-site-name` directory.
4. Create the folder styles:
   
    ```
      mkdir styles
    ```

5. Unzip the Google.zip file in the styles directory:
   
    ```
      unzip Google.zip -d styles/
    ```

6. Create the file `.vale.ini` in the `documentation-site-name` directory.
7. Copy and paste the following text into the `.vale.ini` file:

```
StylesPath = styles
MinAlertLevel = warning

[*.md]
BasedOnStyles = Google
```

To run vale on an `.md` file run the command `vale file.md`.