
You can find the tic-tac-toe game at https://simgeekiz.github.io/tic-tac-toe

# Deploying a React App to GitHub Pages

# Introduction

This project is created using `create-react-app`
This project is a React app—hosted on GitHub Pages—which you can then customize.

# Tutorial

## Prerequisites

1. Node and npm

    ```shell
    $ node --version
    v16.13.2

    $ npm --version
    8.1.2
    ```

## Procedure

### 1. Create an **empty** repository on GitHub

### 2. Create a React app

1. Create a React app named `app`:
  
    ```shell
    $ npx create-react-app app
    ```

2. Enter the newly-created folder:
  
    ```shell
    $ cd app
    ```

### 3. Install the `gh-pages` npm package

    ```shell
    $ npm install gh-pages --save-dev
    ```

Now, the `gh-pages` npm package is installed on your computer and the React app's dependence upon it is documented in the React app's `package.json` file.

### 4. Add a `homepage` property to the `package.json` file

1. Add a `homepage` property in this format\*: `https://{username}.github.io/{repo-name}`

    > \* For a [project site](https://pages.github.com/#project-site)

    ```diff
    {
      "name": "app",
      "version": "0.1.0",
    + "homepage": "https://simgeekiz.github.io/app",
      "private": true,
    ```

### 5. Add deployment scripts to the `package.json` file

1. Open the `package.json` file in a text editor and add a `predeploy` property and a `deploy` property to the `scripts` object:

    ```diff
    "scripts": {
    +   "predeploy": "npm run build",
    +   "deploy": "gh-pages -d build",
        "start": "react-scripts start",
        "build": "react-scripts build",
    ```

Now we added the deployment scripts to React app's `package.json` file.

### 6. Add a "remote" that points to the GitHub repository

1. Add a remote to the local Git repository.

    You can do that by issuing a command in this format: 
    
    ```shell
    $ git init
    $ git remote add origin https://github.com/{username}/{repo-name}.git
    ```
    > #### Branch names: `master` vs. `main`
    > See the branch name in your configurations
    ```shell
    $ git config --global init.defaultBranch
    ```
    > If you want to replace the branch name for that repository you can do it by;
     ```shell
    $ git branch -m main
    ```

    > That command tells Git where I want it to push things whenever I—or the `gh-pages` npm package acting on my behalf—issue the `$ git push` command from within this local Git repository.

At this point, the local repository has a "remote" whose URL points to the GitHub repository you created in Step 1.

### 7. Push the React app to the GitHub repository

1. Push the React app to the GitHub repository

    ```shell
    $ npm run deploy
    ```

    > This will cause the `predeploy` and `deploy` scripts defined in `package.json` to run.
    >
    > Under the hood, the `predeploy` script will build a distributable version of the React app and store it in a folder named `build`. Then, the `deploy` script will push the contents of that folder to a new commit on the `gh-pages` branch of the GitHub repository, creating that branch if it doesn't already exist.

    > By default, the new commit on the `gh-pages` branch will have a commit message of "Updates". You can specify a custom commit message via the `-m` option, like this:
    > ```shell
    > $ npm run deploy -- -m "Deploy React app to GitHub Pages"
    > ```

Now, the GitHub repository contains a branch named `gh-pages`, which contains the files that make up the distributable version of the React app. However, we haven't configured GitHub Pages to _serve_ those files yet.

### 8. Configure GitHub Pages

1. Navigate to the **GitHub Pages** settings page
   1. In your web browser, navigate to the GitHub repository
   1. Above the code browser, click on the tab labeled "Settings"
   1. In the sidebar, in the "Code and automation" section, click on "Pages"
1. Configure the "Build and deployment" settings like this: 
   1. **Source**: Deploy from a branch
   2. **Branch**: 
      - Branch: `gh-pages`
      - Folder: `/ (root)`
1. Click on the "Save" button

At this point, the React app is accessible to anyone who visits the `homepage` URL you specified.

### 9. Store the React app's _source code_ on GitHub

> In a previous step, the `gh-pages` npm package pushed the distributable version of the React app to a branch named `gh-pages` in the GitHub repository. However, the _source code_ of the React app is not yet stored on GitHub.

> In this step, we will store the source code of the React app on GitHub.

1. Commit the changes you made while you were following this tutorial, to the `main` branch of the local Git repository; then, push that branch up to the `main` branch of the GitHub repository.

    ```shell
    $ git add .
    $ git commit -m "Configure React app for deployment to GitHub Pages"
    $ git push origin main
    ```

> GitHub repository will have two branches: `main` and `gh-pages`. The `main` branch will contain the React app's source code, while the `gh-pages` branch will contain the distributable version of the React app.

