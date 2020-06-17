We implement a continuous integration (CI) workflow that includes the following stages:

* **Build** the documentation site.
* **Validate** the HTML output.

We use [GitHub Actions](https://github.com/features/actions) to implement this workflow. Everytime we create a pull request in the documentation site GitHub repository, GitHub Actions triggers the workflow that we define below.

It is possible to add Vale to the continuous integration workflow. However, for this implementations we run Vale locally before we commit and push our updates to the GitHub repository of our documentation site.

To create the continuous integration workflow:

1. In the terminal, change the current working directory to the `documentation-site-name` directory.
1. Create the directory `documentation-site-name/.github/workflows`.
1. In the directory created in the previous step, create the file `continuous-integration.yml`.
1. Copy and paste the following text into the file continuous-integration.yml:

```
name: Continuous Integration

on: [pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2

      - name: Setup Python
        uses: actions/setup-python@v1
        with:
          python-version: 3.7
      - name: Install dependencies and run tests
        run: |
          pip install -r requirements.txt
      - run: mkdocs build

      - name: HTMLProofer
        uses: chabad360/htmlproofer@v1.1
        with:
          directory: "./site"
          arguments: --disable-external

```

We save the file `continuous-integration.yml` and push our changes to the documentation site GitHub repository. In this workflow, we use Ubuntu to run the continuous integration workflow. Also, we define the tasks to build the documentation site (using the command `mkdocs build`) and validate the HTML output using [HTMLProofer](https://github.com/gjtorikian/html-proofer). 