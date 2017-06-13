# Deploying a React App to GitHub Pages

# Introduction

In this tutorial, I'll show you how I deployed a React app--which I created using `create-react-app`--to GitHub Pages.

You can visit the deployed app, at [https://gitname.github.io/react-gh-pages/](https://gitname.github.io/react-gh-pages/).

This repository contains the files related to the app. The `master` branch contains the app's source code (the code the app's developers edit), and the `gh-pages` branch contains a *built* version of the app (i.e. the code that GitHub Pages serves to the app's visitors).

The remainder of this document contains a tutorial on creating a React app (using `create-react-app`) and deploying that app to GitHub Pages.

# Tutorial

## Prerequisites

1. An adequate version of [`Node.js`](https://nodejs.org/) is installed. Here's the adequate version I use:

    ```sh
    $ node --version
    v6.10.1
    ```

2. An adequate version of  [`npm`](https://nodejs.org/) is installed. Here's the adequate version I use:

    ```sh
    $ npm --version
    3.10.10
    ```
3. An adequate version of [`create-react-app`](https://github.com/facebookincubator/create-react-app) is installed. Here's the adequate version I use:

    ```sh
    $ create-react-app --version
    1.3.1
    ```

    In the case of `create-react-app`, you can either install it globally (i.e. `$ npm install -g create-react-app`) or install it locally (i.e. `$ npm install create-react-app`). If you choose the latter, you will have to specify its path whenever you invoke it (e.g. `path/to/node_modules/.bin/create-react-app`).

4. A GitHub account. :octocat:

## Procedure

1. Create an empty repository on GitHub. (2 minutes)

    * For this tutorial, I'll create a repository named `react-gh-pages`
    * By empty, I mean *without* a `README.me` file, a `.gitignore` file, a `LICENSE` file, or any other files.

2. Create a new React app on your development machine. (5 minutes)

    ```sh
    $ create-react-app react-gh-pages
    ```
    
    * I opted to give the app the same name as my GitHub repository. However, you can name them differently from one another.
    * This is the app you will deploy to GitHub Pages in an upcoming step.
    * This will create a new folder named `react-gh-pages` on your development machine (or whatever you named your app).
    * This command will take approximately 5 minutes to run (or more/less, depending upon the enthusiasm of your computer).

3. Install the `gh-pages` package as a *dev-dependency* of that React app. (1 minute)

    ```
    $ cd react-gh-pages
    $ npm install --save-dev gh-pages
    ```

4. Edit the app's `package.json` file to work with GitHub Pages. (3 minutes)

    * At the top level, add a `homepage` field. Define its value to be the string `http://{username}.github.io/{repo-name}`, where `{username}` is your GitHub username, and `{repo-name}` is the name of the GitHub repository you created in step 1. Since my GitHub username is `gitname` and the name of my GitHub repository is `react-gh-pages`, I added the following:
    
    ```js
    //...
    "homepage": "http://gitname.github.io/react-gh-pages"
    ```
    
    * In the existing `scripts` field, add a `predeploy` field and a `deploy` field, each having the values shown below:

    ```js
    "scripts": {
      //...
      "predeploy": "npm run build",
      "deploy": "gh-pages -d build"
    }
    ```

5. Create a git repository in the app folder. (1 minute)

    ```
    $ git init
    Initialized empty Git repository in C:/path/to/react-gh-pages/.git/
    ```

6. Add the GitHub repository as a *remote* in your local git repository. (1 minute)

    ```
    $ git remote add origin https://github.com/gitname/react-gh-pages.git
    ```
    
    * This will make it so the `gh-pages` package knows where you want it to deploy your app.
    * It will also make it so git knows where you want it to push your source code (i.e. the commits on your `master` branch).

7. Generate a *production build* of your app, and deploy it to GitHub Pages. (2 minutes)

    ```
    $ npm run deploy
    ```
    
    * That's it! Your app is now accessible at the URL you specific in step 4. In my case, my app is accessible at: https://gitname.github.io/react-gh-pages/
    * I recommend exploring the GitHub repository at this point. When I explored it, I noticed that, although a `master` branch did not exist, a `gh-pages` branch did exist. I noticed the latter contained the *built* app code, as opposed to the source code.

8. Optionally, commit your source code to the master branch and push it to GitHub.

    ```
    $ git add .
    $ git commit -m "Create a React app and publish it to GitHub Pages"
    $ git push origin master
    ```

    * I recommend exploring the GitHub repository once again at this point. When I did that, I noticed that a `master` branch now existed, and it contained the source code of my app.
    * So, the `master` branch holds the source code, and the `gh-pages` branch holds the *built* app code.

# References

1. [Facebook's own tutorial on deploying a React app to GitHub Pages](https://github.com/facebookincubator/create-react-app/blob/master/packages/react-scripts/template/README.md#github-pages)

# Notes

* I created this React app using [`create-react-app`](https://github.com/facebookincubator/create-react-app). By default, apps created using `create-react-app` have a README.md file that looks like [this](https://github.com/facebookincubator/create-react-app/blob/master/packages/react-scripts/template/README.md). Indeed, the README.md file you're now reading originally looked like that. I have since changed it to look the way it looks today.
* Special thanks to GitHub, Inc., for providing us this awesome means for hosting content and sharing information.
* And now, time to turn the boilerplate `create-react-app` code into something unique!