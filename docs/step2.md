We create a GitHub repository to store our documentation site:

1. Go to your GitHub account.
1. Click the **New** button.
1. Enter the new repository’s name in the Repository name text field.
1. Leave the Initialize this repository with a README option unselected.
1. In a terminal change the current working directory to the documentation-site-name directory.
1. Run the following commands:

```
echo "# documentation-site-name" >> README.md
git init
git add README.md
git commit -m "first commit"
git remote add origin https://github.com/your-user-name/documentation-site-name.git
git push -u origin master
```

We can now use the git commands `add`, `commit`, and `push` to keep track of the changes to the files of our documentation site and store them.