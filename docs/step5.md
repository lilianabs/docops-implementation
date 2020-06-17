We implement a continuous deployment (CD) workflow that includes the following stages:

* **Build** the documentation site.
* **Deploy** the documentation site to [Netlify](https://www.netlify.com/).

We use [GitHub Actions](https://github.com/features/actions) to implement this workflow. Everytime we push updates to the master branch in the documentation site GitHub repository, GitHub Actions triggers the workflow that we define below.

To implement the CD workflow we need to perform the following steps:

* Create a new site in Netlify.
* Obtain a personal access token from Netlify.
* Obtain the site ID from Netlify.
* Create the continuous deployment workflow.

## Create a new site in Netlify

We need to build our documentation site locally before we deploy it to Netlify for the first time. In a terminal, go to the `documentation-site-name` directory and run the command `mkdocs build`. Mkdocs creates a directory `site` that contains the HTML files of the documentation site.

To create a new site in Netlify to deploy our documentation site:

1. Go to [Netlify](https://www.netlify.com/).
1. Sign up for a free account.
1. Click the **Sites** tab.
1. Drag and drop the `site` directory into the drag and drop area.

    Netlify deploys your documentation site and shows the web address of it.

## Obtain a personal access token from Netlify

To obtain a personal access token:

1. Go to **User settings**.
1. Click **Applications**.
1. In the **Personal access tokens** section, click the **New access token** button.
1. Enter a description for the token.
1. Click the **Generate token** button.
1. Keep the personal access token in a safe place.

## Obtain the site ID from Netlify

To obtain the site ID of the documentation site:

1. Go to the **Sites** dashboard.
1. Click the documentation site.
1. Click the **Site settings** button.
1. Copy the value for **API ID*.

## Create the continuous deployment workflow

We create the continuous deployment workflow:

1. In the `static-site-name/.github/workflows` directory, create the `continuous-deployment.yml` file.
1. Copy and paste the following text into the file continuous-deployment.yml:

```

name: Continuous Deployment
on:
  push:
    branches:
      - master

jobs:
  deploy:
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

      - name: Publish
        uses: netlify/actions/cli@master
        with:
          args: deploy --dir=site --functions=functions --prod
        env:
          NETLIFY_SITE_ID: ${{ secrets.NETLIFY_SITE_ID }}
          NETLIFY_AUTH_TOKEN: ${{ secrets.MY_TOKEN_SECRET }}

```

Now, we add the values for the secrets variables:

1. In the documentation site GitHub repository, click the Settings tab.
1. On the left side menu, select the Secrets option.  
1. Select the Add new secret option.
1. Add the following secrets:
   
    * NETLIFY_SITE_ID
    * MY_TOKEN_SECRET

Use the values that we obtained in sections [Obtain a personal access token from Netlify](#obtain-a-personal-access-token-from-netlify) and [Obtain the site ID from Netlify](#obtain-the-site-id-from-netlify). Then, we push the changes to the documentation site GitHub repository.

After we create a pull request and merge the changes GitHub Actions triggers the CD workflow and deploys the documentation site to Netlify. To view our documentation site we click the *URL* that Netlify assigns to it.