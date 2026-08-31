# Minha-msg-pros-cria-2
# Creating a GitHub Pages site with Jekyll

You can use Jekyll to create a GitHub Pages site in a new or existing repository.

> \[!NOTE] While the `github-pages` gem remains supported for some workflows, GitHub Actions is now the recommended approach for deploying and automating GitHub Pages sites.

## Prerequisites

Before you can use Jekyll to create a GitHub Pages site, you must install Jekyll and Git. For more information, see [Installation](https://jekyllrb.com/docs/installation/) in the Jekyll documentation and [Set up Git](/en/get-started/git-basics/set-up-git).

We recommend using [Bundler](https://bundler.io/) to install and run Jekyll. Bundler manages Ruby gem dependencies, reduces Jekyll build errors, and prevents environment-related bugs. To install Bundler:

1. Install Ruby. For more information, see [Installing Ruby](https://www.ruby-lang.org/en/documentation/installation/) in the Ruby documentation.
2. Install Bundler. For more information, see [Bundler](https://bundler.io/).

<div class="ghd-tool mac">

> \[!TIP]
> If you see a Ruby error when you try to install Jekyll using Bundler, you may need to use a package manager, such as [RVM](https://rvm.io/) or [Homebrew](https://brew.sh/), to manage your Ruby installation. For more information, see [Troubleshooting](https://jekyllrb.com/docs/troubleshooting/#jekyll--macos) in the Jekyll documentation.

</div>

## Creating a repository for your site

You can either create a repository or choose an existing repository for your site.

If you want to create a GitHub Pages site for a repository where not all of the files in the repository are related to the site, you will be able to configure a publishing source for your site. For example, you can have a dedicated branch and folder to hold your site source files, or you can use a custom GitHub Actions workflow to build and deploy your site source files.

If the account that owns the repository uses GitHub Free or GitHub Free for organizations, the repository must be public.

If you want to create a site in an existing repository, skip to the [Creating your site](#creating-your-site) section.

1. In the upper-right corner of any page, select <svg version="1.1" width="16" height="16" viewBox="0 0 16 16" class="octicon octicon-plus" aria-label="Create something new" role="img"><path d="M7.75 2a.75.75 0 0 1 .75.75V7h4.25a.75.75 0 0 1 0 1.5H8.5v4.25a.75.75 0 0 1-1.5 0V8.5H2.75a.75.75 0 0 1 0-1.5H7V2.75A.75.75 0 0 1 7.75 2Z"></path></svg>, then click **New repository**.

   ![Screenshot of a GitHub dropdown menu showing options to create new items. The menu item "New repository" is outlined in dark orange.](/assets/images/help/repository/repo-create-global-nav-update.png)

2. Use the **Owner** dropdown menu to select the account you want to own the repository.
   ![Screenshot of the owner menu for a new GitHub repository. The menu shows two options, octocat and github.](/assets/images/help/repository/create-repository-owner.png)

3. Type a name for your repository and an optional description. If you're creating a user or organization site, your repository must be named `<user>.github.io` or `<organization>.github.io`. If your user or organization name contains uppercase letters, you must lowercase the letters.
   For more information, see [What is GitHub Pages?](/en/pages/getting-started-with-github-pages/what-is-github-pages#types-of-github-pages-sites).
   ![Screenshot of GitHub Pages settings in a repository. The repository name field contains the text "octocat.github.io" and is outlined in dark orange.](/assets/images/help/pages/create-repository-name-pages.png)

4. Choose a repository visibility. For more information, see [About repositories](/en/repositories/creating-and-managing-repositories/about-repositories#about-repository-visibility).

## Creating your site

Before you can create your site, you must have a repository for your site on GitHub. If you're not creating your site in an existing repository, see [Creating a repository for your site](#creating-a-repository-for-your-site).

> \[!WARNING]
> GitHub Pages sites are publicly available on the internet, even if the repository for the site is private (if your plan or organization allows it). If you have sensitive data in your site's repository, you may want to remove the data before publishing. For more information, see [About repositories](/en/repositories/creating-and-managing-repositories/about-repositories#about-repository-visibility).

1. Open <span class="platform-mac">Terminal</span><span class="platform-linux">Terminal</span><span class="platform-windows">Git Bash</span>.

2. If you don't already have a local copy of your repository, navigate to the location where you want to store your site's source files, replacing PARENT-FOLDER with the folder you want to contain the folder for your repository.

   ```shell
   cd PARENT-FOLDER
   ```

3. If you haven't already, initialize a local Git repository, replacing REPOSITORY-NAME with the name of your repository.

   ```shell
   git init REPOSITORY-NAME
   > Initialized empty Git repository in /REPOSITORY-NAME/.git/
   # Creates a new folder on your computer, initialized as a Git repository
   ```

4. Change directories to the repository.

   ```shell
   cd REPOSITORY-NAME
   # Changes the working directory
   ```

5. Decide which publishing source you want to use. For more information, see [Configuring a publishing source for your GitHub Pages site](/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site).

6. Navigate to the publishing source for your site. For more information, see [Configuring a publishing source for your GitHub Pages site](/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site).
   For example, if you chose to publish your site from the `docs` folder on the default branch, create and change directories to the `docs` folder.

   ```shell
   mkdir docs
   # Creates a new folder called docs
   cd docs
   ```

   If you chose to publish your site from the `gh-pages` branch, create and checkout the `gh-pages` branch.

   ```shell
   git checkout --orphan gh-pages
   # Creates a new branch, with no history or contents, called gh-pages, and switches to the gh-pages branch
   git rm -rf .
   # Removes the contents from your default branch from the working directory
   ```

7. To create a new Jekyll site, use the `jekyll new` command in your repository's root directory:

   ```shell
   jekyll new --skip-bundle .
   # Creates a Jekyll site in the current directory
   ```

8. Open the Gemfile that Jekyll created.

9. Add "#" to the beginning of the line that starts with `gem "jekyll"` to comment out this line.

10. Add the `github-pages` gem by editing the line starting with `# gem "github-pages"`. Change this line to:

    ```ruby
    gem "github-pages", "~> GITHUB-PAGES-VERSION", group: :jekyll_plugins
    ```

    Replace GITHUB-PAGES-VERSION with the latest supported version of the `github-pages` gem. You can find this version here: [Dependency versions](https://pages.github.com/versions.json).

    The correct version Jekyll will be installed as a dependency of the `github-pages` gem.

11. Save and close the Gemfile.

12. From the command line, run `bundle install`.

13. Open the `.gitignore` file that Jekyll created and ignore the gems lock file by adding this line:

    ```shell
    Gemfile.lock
    ```

14. Optionally, make any necessary edits to the `_config.yml` file. This is required for relative paths when the repository is hosted in a subdirectory. For more information, see [Splitting a subfolder out into a new repository](/en/get-started/using-git/splitting-a-subfolder-out-into-a-new-repository).

    ```yaml
    domain: my-site.github.io       # if you want to force HTTPS, specify the domain without the http at the start, e.g. example.com
    url: https://my-site.github.io  # the base hostname and protocol for your site, e.g. http://example.com
    baseurl: /REPOSITORY-NAME/      # place folder name if the site is served in a subfolder
    ```

15. Optionally, test your site locally. For more information, see [Testing your GitHub Pages site locally with Jekyll](/en/pages/setting-up-a-github-pages-site-with-jekyll/testing-your-github-pages-site-locally-with-jekyll).

16. Add and commit your work.

    ```shell
    git add .
    git commit -m 'Initial GitHub pages site with Jekyll'
    ```

17. Add your repository on GitHub.com as a remote, replacing  USER with the account that owns the repository and REPOSITORY with the name of the repository.

    ```shell

    git remote add origin https://github.com/USER/REPOSITORY.git

    ```

18. Push the repository to GitHub, replacing BRANCH with the name of the branch you're working on.

    ```shell
    git push -u origin BRANCH
    ```

19. Configure your publishing source. For more information, see [Configuring a publishing source for your GitHub Pages site](/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site).

20. On GitHub, navigate to your site's repository.

21. Under your repository name, click **<svg version="1.1" width="16" height="16" viewBox="0 0 16 16" class="octicon octicon-gear" aria-label="gear" role="img"><path d="M8 0a8.2 8.2 0 0 1 .701.031C9.444.095 9.99.645 10.16 1.29l.288 1.107c.018.066.079.158.212.224.231.114.454.243.668.386.123.082.233.09.299.071l1.103-.303c.644-.176 1.392.021 1.82.63.27.385.506.792.704 1.218.315.675.111 1.422-.364 1.891l-.814.806c-.049.048-.098.147-.088.294.016.257.016.515 0 .772-.01.147.038.246.088.294l.814.806c.475.469.679 1.216.364 1.891a7.977 7.977 0 0 1-.704 1.217c-.428.61-1.176.807-1.82.63l-1.102-.302c-.067-.019-.177-.011-.3.071a5.909 5.909 0 0 1-.668.386c-.133.066-.194.158-.211.224l-.29 1.106c-.168.646-.715 1.196-1.458 1.26a8.006 8.006 0 0 1-1.402 0c-.743-.064-1.289-.614-1.458-1.26l-.289-1.106c-.018-.066-.079-.158-.212-.224a5.738 5.738 0 0 1-.668-.386c-.123-.082-.233-.09-.299-.071l-1.103.303c-.644.176-1.392-.021-1.82-.63a8.12 8.12 0 0 1-.704-1.218c-.315-.675-.111-1.422.363-1.891l.815-.806c.05-.048.098-.147.088-.294a6.214 6.214 0 0 1 0-.772c.01-.147-.038-.246-.088-.294l-.815-.806C.635 6.045.431 5.298.746 4.623a7.92 7.92 0 0 1 .704-1.217c.428-.61 1.176-.807 1.82-.63l1.102.302c.067.019.177.011.3-.071.214-.143.437-.272.668-.386.133-.066.194-.158.211-.224l.29-1.106C6.009.645 6.556.095 7.299.03 7.53.01 7.764 0 8 0Zm-.571 1.525c-.036.003-.108.036-.137.146l-.289 1.105c-.147.561-.549.967-.998 1.189-.173.086-.34.183-.5.29-.417.278-.97.423-1.529.27l-1.103-.303c-.109-.03-.175.016-.195.045-.22.312-.412.644-.573.99-.014.031-.021.11.059.19l.815.806c.411.406.562.957.53 1.456a4.709 4.709 0 0 0 0 .582c.032.499-.119 1.05-.53 1.456l-.815.806c-.081.08-.073.159-.059.19.162.346.353.677.573.989.02.03.085.076.195.046l1.102-.303c.56-.153 1.113-.008 1.53.27.161.107.328.204.501.29.447.222.85.629.997 1.189l.289 1.105c.029.109.101.143.137.146a6.6 6.6 0 0 0 1.142 0c.036-.003.108-.036.137-.146l.289-1.105c.147-.561.549-.967.998-1.189.173-.086.34-.183.5-.29.417-.278.97-.423 1.529-.27l1.103.303c.109.029.175-.016.195-.045.22-.313.411-.644.573-.99.014-.031.021-.11-.059-.19l-.815-.806c-.411-.406-.562-.957-.53-1.456a4.709 4.709 0 0 0 0-.582c-.032-.499.119-1.05.53-1.456l.815-.806c.081-.08.073-.159.059-.19a6.464 6.464 0 0 0-.573-.989c-.02-.03-.085-.076-.195-.046l-1.102.303c-.56.153-1.113.008-1.53-.27a4.44 4.44 0 0 0-.501-.29c-.447-.222-.85-.629-.997-1.189l-.289-1.105c-.029-.11-.101-.143-.137-.146a6.6 6.6 0 0 0-1.142 0ZM11 8a3 3 0 1 1-6 0 3 3 0 0 1 6 0ZM9.5 8a1.5 1.5 0 1 0-3.001.001A1.5 1.5 0 0 0 9.5 8Z"></path></svg> Settings**. If you cannot see the "Settings" tab, select the **<svg version="1.1" width="16" height="16" viewBox="0 0 16 16" class="octicon octicon-kebab-horizontal" aria-label="More" role="img"><path d="M8 9a1.5 1.5 0 1 0 0-3 1.5 1.5 0 0 0 0 3ZM1.5 9a1.5 1.5 0 1 0 0-3 1.5 1.5 0 0 0 0 3Zm13 0a1.5 1.5 0 1 0 0-3 1.5 1.5 0 0 0 0 3Z"></path></svg>** dropdown menu, then click **Settings**.

    ![Screenshot of a repository header showing the tabs. The "Settings" tab is highlighted by a dark orange outline.](/assets/images/help/repository/repo-actions-settings.png)

22. In the "Code, planning, and automation" section of the sidebar, click **<svg version="1.1" width="16" height="16" viewBox="0 0 16 16" class="octicon octicon-browser" aria-label="browser" role="img"><path d="M0 2.75C0 1.784.784 1 1.75 1h12.5c.966 0 1.75.784 1.75 1.75v10.5A1.75 1.75 0 0 1 14.25 15H1.75A1.75 1.75 0 0 1 0 13.25ZM14.5 6h-13v7.25c0 .138.112.25.25.25h12.5a.25.25 0 0 0 .25-.25Zm-6-3.5v2h6V2.75a.25.25 0 0 0-.25-.25ZM5 2.5v2h2v-2Zm-3.25 0a.25.25 0 0 0-.25.25V4.5h2v-2Z"></path></svg> Pages**.

23. To see your published site, under "GitHub Pages", click **<svg version="1.1" width="16" height="16" viewBox="0 0 16 16" class="octicon octicon-link-external" aria-label="link-external" role="img"><path d="M3.75 2h3.5a.75.75 0 0 1 0 1.5h-3.5a.25.25 0 0 0-.25.25v8.5c0 .138.112.25.25.25h8.5a.25.25 0 0 0 .25-.25v-3.5a.75.75 0 0 1 1.5 0v3.5A1.75 1.75 0 0 1 12.25 14h-8.5A1.75 1.75 0 0 1 2 12.25v-8.5C2 2.784 2.784 2 3.75 2Zm6.854-1h4.146a.25.25 0 0 1 .25.25v4.146a.25.25 0 0 1-.427.177L13.03 4.03 9.28 7.78a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042l3.75-3.75-1.543-1.543A.25.25 0 0 1 10.604 1Z"></path></svg> Visit site**.
    ![Screenshot of a confirmation message for GitHub Pages listing the site's URL. The gray "Visit site" button is outlined in orange.](/assets/images/help/pages/click-pages-url-to-preview.png)

    > \[!NOTE]
    > It can take up to 10 minutes for changes to your site to publish after you push the changes to GitHub. If you don't see your GitHub Pages site changes reflected in your browser after an hour, see [About Jekyll build errors for GitHub Pages sites](/en/pages/setting-up-a-github-pages-site-with-jekyll/about-jekyll-build-errors-for-github-pages-sites).

24. Your GitHub Pages site is built and deployed with a GitHub Actions workflow. For more information, see [Viewing workflow run history](/en/actions/how-tos/monitor-workflows/view-workflow-run-history).

    > \[!NOTE]
    > GitHub Actions is free for public repositories. Usage charges apply for private and internal repositories that go beyond the monthly allotment of free minutes. For more information, see [Billing and usage](/en/actions/concepts/billing-and-usage).

> \[!NOTE]
>
> * If you are publishing from a branch and your site has not published automatically, make sure someone with admin permissions and a verified email address has pushed to the publishing source.
> * Commits pushed by a GitHub Actions workflow that uses the `GITHUB_TOKEN` do not trigger a GitHub Pages build.

## Next steps

To add a new page or post to your site, see [Adding content to your GitHub Pages site using Jekyll](/en/pages/setting-up-a-github-pages-site-with-jekyll/adding-content-to-your-github-pages-site-using-jekyll).

You can add a Jekyll theme to your GitHub Pages site to customize the look and feel of your site. For more information, see [Adding a theme to your GitHub Pages site using Jekyll](/en/pages/setting-up-a-github-pages-site-with-jekyll/adding-a-theme-to-your-github-pages-site-using-jekyll).

# Creating a GitHub Pages site

You can create a GitHub Pages site in a new or existing repository.

## Creating a repository for your site

You can either create a repository or choose an existing repository for your site.

If you want to create a GitHub Pages site for a repository where not all of the files in the repository are related to the site, you will be able to configure a publishing source for your site. For example, you can have a dedicated branch and folder to hold your site source files, or you can use a custom GitHub Actions workflow to build and deploy your site source files.

If the account that owns the repository uses GitHub Free or GitHub Free for organizations, the repository must be public.

If you want to create a site in an existing repository, skip to the [Creating your site](#creating-your-site) section.

1. In the upper-right corner of any page, select <svg version="1.1" width="16" height="16" viewBox="0 0 16 16" class="octicon octicon-plus" aria-label="Create something new" role="img"><path d="M7.75 2a.75.75 0 0 1 .75.75V7h4.25a.75.75 0 0 1 0 1.5H8.5v4.25a.75.75 0 0 1-1.5 0V8.5H2.75a.75.75 0 0 1 0-1.5H7V2.75A.75.75 0 0 1 7.75 2Z"></path></svg>, then click **New repository**.

   ![Screenshot of a GitHub dropdown menu showing options to create new items. The menu item "New repository" is outlined in dark orange.](/assets/images/help/repository/repo-create-global-nav-update.png)

2. Use the **Owner** dropdown menu to select the account you want to own the repository.
   ![Screenshot of the owner menu for a new GitHub repository. The menu shows two options, octocat and github.](/assets/images/help/repository/create-repository-owner.png)

   > \[!NOTE]
   > If you're a managed user account, you can only publish GitHub Pages sites from repositories owned by organizations. For more information, see [GitHub Pages limits](/en/enterprise-cloud@latest/pages/getting-started-with-github-pages/github-pages-limits#limits-for-enterprise-managed-users).

3. Type a name for your repository and an optional description. If you're creating a user or organization site, your repository must be named `<user>.github.io` or `<organization>.github.io`. If your user or organization name contains uppercase letters, you must lowercase the letters.
   For more information, see [What is GitHub Pages?](/en/enterprise-cloud@latest/pages/getting-started-with-github-pages/what-is-github-pages#types-of-github-pages-sites).
   ![Screenshot of GitHub Pages settings in a repository. The repository name field contains the text "octocat.github.io" and is outlined in dark orange.](/assets/images/help/pages/create-repository-name-pages.png)

4. Choose a repository visibility. For more information, see [About repositories](/en/enterprise-cloud@latest/repositories/creating-and-managing-repositories/about-repositories#about-repository-visibility).

5. Toggle **Add README** to **On**.

6. Click **Create repository**.

## Creating your site

Before you can create your site, you must have a repository for your site on GitHub. If you're not creating your site in an existing repository, see [Creating a repository for your site](#creating-a-repository-for-your-site).

> \[!WARNING]
> Unless your enterprise uses Enterprise Managed Users, GitHub Pages sites are publicly available on the internet by default, even if the repository for the site is private or internal. You can publish a site privately by managing access control for the site. Otherwise, if you have sensitive data in your site's repository, you may want to remove the data before publishing. For more information, see [About repositories](/en/enterprise-cloud@latest/repositories/creating-and-managing-repositories/about-repositories#about-repository-visibility) and [Changing the visibility of your GitHub Pages site](/en/enterprise-cloud@latest/pages/getting-started-with-github-pages/changing-the-visibility-of-your-github-pages-site).

1. On GitHub, navigate to your site's repository.

2. Decide which publishing source you want to use. See [Configuring a publishing source for your GitHub Pages site](/en/enterprise-cloud@latest/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site).

3. Create the entry file for your site. GitHub Pages will look for an `index.html`, `index.md`, or `README.md` file as the entry file for your site.

   If your publishing source is a branch and folder, the entry file must be at the top level of the source folder on the source branch. For example, if your publishing source is the `/docs` folder on the `main` branch, your entry file must be located in the `/docs` folder on a branch called `main`.

   If your publishing source is a GitHub Actions workflow, the artifact that you deploy must include the entry file at the top level of the artifact. Instead of adding the entry file to your repository, you may choose to have your GitHub Actions workflow generate your entry file when the workflow runs.

4. Configure your publishing source. See [Configuring a publishing source for your GitHub Pages site](/en/enterprise-cloud@latest/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site).

5. Your GitHub Pages site is built and deployed with a GitHub Actions workflow. For more information, see [Viewing workflow run history](/en/enterprise-cloud@latest/actions/how-tos/monitor-workflows/view-workflow-run-history).

   > \[!NOTE]
   > GitHub Actions is free for public repositories. Usage charges apply for private and internal repositories that go beyond the monthly allotment of free minutes. For more information, see [Billing and usage](/en/enterprise-cloud@latest/actions/concepts/billing-and-usage).

## Viewing your published site

1. Under your repository name, click **<svg version="1.1" width="16" height="16" viewBox="0 0 16 16" class="octicon octicon-gear" aria-label="gear" role="img"><path d="M8 0a8.2 8.2 0 0 1 .701.031C9.444.095 9.99.645 10.16 1.29l.288 1.107c.018.066.079.158.212.224.231.114.454.243.668.386.123.082.233.09.299.071l1.103-.303c.644-.176 1.392.021 1.82.63.27.385.506.792.704 1.218.315.675.111 1.422-.364 1.891l-.814.806c-.049.048-.098.147-.088.294.016.257.016.515 0 .772-.01.147.038.246.088.294l.814.806c.475.469.679 1.216.364 1.891a7.977 7.977 0 0 1-.704 1.217c-.428.61-1.176.807-1.82.63l-1.102-.302c-.067-.019-.177-.011-.3.071a5.909 5.909 0 0 1-.668.386c-.133.066-.194.158-.211.224l-.29 1.106c-.168.646-.715 1.196-1.458 1.26a8.006 8.006 0 0 1-1.402 0c-.743-.064-1.289-.614-1.458-1.26l-.289-1.106c-.018-.066-.079-.158-.212-.224a5.738 5.738 0 0 1-.668-.386c-.123-.082-.233-.09-.299-.071l-1.103.303c-.644.176-1.392-.021-1.82-.63a8.12 8.12 0 0 1-.704-1.218c-.315-.675-.111-1.422.363-1.891l.815-.806c.05-.048.098-.147.088-.294a6.214 6.214 0 0 1 0-.772c.01-.147-.038-.246-.088-.294l-.815-.806C.635 6.045.431 5.298.746 4.623a7.92 7.92 0 0 1 .704-1.217c.428-.61 1.176-.807 1.82-.63l1.102.302c.067.019.177.011.3-.071.214-.143.437-.272.668-.386.133-.066.194-.158.211-.224l.29-1.106C6.009.645 6.556.095 7.299.03 7.53.01 7.764 0 8 0Zm-.571 1.525c-.036.003-.108.036-.137.146l-.289 1.105c-.147.561-.549.967-.998 1.189-.173.086-.34.183-.5.29-.417.278-.97.423-1.529.27l-1.103-.303c-.109-.03-.175.016-.195.045-.22.312-.412.644-.573.99-.014.031-.021.11.059.19l.815.806c.411.406.562.957.53 1.456a4.709 4.709 0 0 0 0 .582c.032.499-.119 1.05-.53 1.456l-.815.806c-.081.08-.073.159-.059.19.162.346.353.677.573.989.02.03.085.076.195.046l1.102-.303c.56-.153 1.113-.008 1.53.27.161.107.328.204.501.29.447.222.85.629.997 1.189l.289 1.105c.029.109.101.143.137.146a6.6 6.6 0 0 0 1.142 0c.036-.003.108-.036.137-.146l.289-1.105c.147-.561.549-.967.998-1.189.173-.086.34-.183.5-.29.417-.278.97-.423 1.529-.27l1.103.303c.109.029.175-.016.195-.045.22-.313.411-.644.573-.99.014-.031.021-.11-.059-.19l-.815-.806c-.411-.406-.562-.957-.53-1.456a4.709 4.709 0 0 0 0-.582c-.032-.499.119-1.05.53-1.456l.815-.806c.081-.08.073-.159.059-.19a6.464 6.464 0 0 0-.573-.989c-.02-.03-.085-.076-.195-.046l-1.102.303c-.56.153-1.113.008-1.53-.27a4.44 4.44 0 0 0-.501-.29c-.447-.222-.85-.629-.997-1.189l-.289-1.105c-.029-.11-.101-.143-.137-.146a6.6 6.6 0 0 0-1.142 0ZM11 8a3 3 0 1 1-6 0 3 3 0 0 1 6 0ZM9.5 8a1.5 1.5 0 1 0-3.001.001A1.5 1.5 0 0 0 9.5 8Z"></path></svg> Settings**. If you cannot see the "Settings" tab, select the **<svg version="1.1" width="16" height="16" viewBox="0 0 16 16" class="octicon octicon-kebab-horizontal" aria-label="More" role="img"><path d="M8 9a1.5 1.5 0 1 0 0-3 1.5 1.5 0 0 0 0 3ZM1.5 9a1.5 1.5 0 1 0 0-3 1.5 1.5 0 0 0 0 3Zm13 0a1.5 1.5 0 1 0 0-3 1.5 1.5 0 0 0 0 3Z"></path></svg>** dropdown menu, then click **Settings**.

   ![Screenshot of a repository header showing the tabs. The "Settings" tab is highlighted by a dark orange outline.](/assets/images/help/repository/repo-actions-settings.png)
2. In the "Code, planning, and automation" section of the sidebar, click **<svg version="1.1" width="16" height="16" viewBox="0 0 16 16" class="octicon octicon-browser" aria-label="browser" role="img"><path d="M0 2.75C0 1.784.784 1 1.75 1h12.5c.966 0 1.75.784 1.75 1.75v10.5A1.75 1.75 0 0 1 14.25 15H1.75A1.75 1.75 0 0 1 0 13.25ZM14.5 6h-13v7.25c0 .138.112.25.25.25h12.5a.25.25 0 0 0 .25-.25Zm-6-3.5v2h6V2.75a.25.25 0 0 0-.25-.25ZM5 2.5v2h2v-2Zm-3.25 0a.25.25 0 0 0-.25.25V4.5h2v-2Z"></path></svg> Pages**.
3. Optionally, if you're publishing a project site from a private or internal repository, choose the visibility for your site. Under "GitHub Pages," select the visibility dropdown menu, then select public or private.
   ![Screenshot of Pages settings for a repository. The visibility dropdown, currently set to "Private," is outlined in dark orange.](/assets/images/help/pages/public-or-private-visibility.png)
   > \[!NOTE]
   > To publish a GitHub Pages site privately, your organization must use GitHub Enterprise Cloud. For more information about how you can try GitHub Enterprise Cloud for free, see [Setting up a trial of GitHub Enterprise Cloud](/en/enterprise-cloud@latest/admin/overview/setting-up-a-trial-of-github-enterprise-cloud).
4. To see your published site, under "GitHub Pages," click **<svg version="1.1" width="16" height="16" viewBox="0 0 16 16" class="octicon octicon-link-external" aria-label="link-external" role="img"><path d="M3.75 2h3.5a.75.75 0 0 1 0 1.5h-3.5a.25.25 0 0 0-.25.25v8.5c0 .138.112.25.25.25h8.5a.25.25 0 0 0 .25-.25v-3.5a.75.75 0 0 1 1.5 0v3.5A1.75 1.75 0 0 1 12.25 14h-8.5A1.75 1.75 0 0 1 2 12.25v-8.5C2 2.784 2.784 2 3.75 2Zm6.854-1h4.146a.25.25 0 0 1 .25.25v4.146a.25.25 0 0 1-.427.177L13.03 4.03 9.28 7.78a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042l3.75-3.75-1.543-1.543A.25.25 0 0 1 10.604 1Z"></path></svg> Visit site**.

> \[!NOTE]
> It can take up to 10 minutes for changes to your site to publish after you push the changes to GitHub. If you don't see your GitHub Pages site changes reflected in your browser after an hour, see [About Jekyll build errors for GitHub Pages sites](/en/enterprise-cloud@latest/pages/setting-up-a-github-pages-site-with-jekyll/about-jekyll-build-errors-for-github-pages-sites).
> \[!NOTE]
>
> * If you are publishing from a branch and your site has not published automatically, make sure someone with admin permissions and a verified email address has pushed to the publishing source.
> * Commits pushed by a GitHub Actions workflow that uses the `GITHUB_TOKEN` do not trigger a GitHub Pages build.

## Static site generators

GitHub Pages publishes any static files that you push to your repository. You can create your own static files or use a static site generator to build your site for you. You can also customize your own build process locally or on another server.

If you use a custom build process or a static site generator other than Jekyll, you can write a GitHub Actions workflow to build and publish your site. GitHub provides workflow templates for several static site generators. For more information, see [Configuring a publishing source for your GitHub Pages site](/en/enterprise-cloud@latest/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site).

If you publish your site from a source branch, GitHub Pages will use Jekyll to build your site by default. If you want to use a static site generator other than Jekyll, we recommend that you write a GitHub Actions to build and publish your site instead. Otherwise, disable the Jekyll build process by creating an empty file called `.nojekyll` in the root of your publishing source, then follow your static site generator's instructions to build your site locally.

> \[!NOTE] GitHub Pages does not support server-side languages such as PHP, Ruby, or Python.

## MIME types on GitHub Pages

A MIME type is a header that a server sends to a browser, providing information about the nature and format of the files the browser requested. GitHub Pages supports more than 750 MIME types across thousands of file extensions. The list of supported MIME types is generated from the [mime-db project](https://github.com/jshttp/mime-db).

While you can't specify custom MIME types on a per-file or per-repository basis, you can add or modify MIME types for use on GitHub Pages. For more information, see [the mime-db contributing guidelines](https://github.com/jshttp/mime-db#adding-custom-media-types).

## Next steps

You can add more pages to your site by creating more new files. Each file will be available on your site in the same directory structure as your publishing source. For example, if the publishing source for your project site is the `gh-pages` branch, and you create a new file called `/about/contact-us.md` on the `gh-pages` branch, the file will be available at `https://<user>.github.io/<repository>/about/contact-us.html`.

You can also add a theme to customize your site’s look and feel. For more information, see [Adding a theme to your GitHub Pages site using Jekyll](/en/enterprise-cloud@latest/pages/setting-up-a-github-pages-site-with-jekyll/adding-a-theme-to-your-github-pages-site-using-jekyll).

## Further reading

* [About GitHub Pages and Jekyll](/en/enterprise-cloud@latest/pages/setting-up-a-github-pages-site-with-jekyll/about-github-pages-and-jekyll).
* [Troubleshooting Jekyll build errors for GitHub Pages sites](/en/enterprise-cloud@latest/pages/setting-up-a-github-pages-site-with-jekyll/troubleshooting-jekyll-build-errors-for-github-pages-sites)
* [Managing branches within your repository](/en/enterprise-cloud@latest/pull-requests/how-tos/commit-changes/managing-branches-within-your-repository)
* [Creating new files](/en/enterprise-cloud@latest/repositories/working-with-files/managing-files/creating-new-files)
* [Troubleshooting 404 errors for GitHub Pages sites](/en/enterprise-cloud@latest/pages/getting-started-with-github-pages/troubleshooting-404-errors-for-github-pages-sites)
* # Troubleshooting 404 errors for GitHub Pages sites

This guide will help you troubleshoot common reasons you may be seeing a 404 error.

## Troubleshooting 404 errors

In this guide you'll find common reasons you may be seeing a 404 error while building your GitHub Pages site.

* [GitHub's Status page](#githubs-status-page)
* [DNS setup](#dns-setup)
* [Browser cache](#browser-cache)
* [`index.html` file](#indexhtml-file)
* [Directory contents](#directory-contents)
* [Custom domain](#custom-domain)
* [Repository](#repository)

### GitHub's Status page

If you see a 404 error while building a GitHub Pages site, first check GitHub's [Status page](https://githubstatus.com) for any active incidents.

### DNS setup

Make sure GitHub's DNS records are set up correctly with your DNS provider. For more information, see [Managing a custom domain for your GitHub Pages site](/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site).

### Browser cache

If your GitHub Pages site is private and you see a 404 error, you may need to clear your browser's cache. For more information on clearing your cache, see your browser's documentation.

### `index.html` file

GitHub Pages will look for an `index.html` file as the entry file for your site.

* Make sure you have an `index.html` file in the repository for your site on GitHub. For more information, see [Creating a GitHub Pages site](/en/pages/getting-started-with-github-pages/creating-a-github-pages-site#creating-your-site).

* The entry file must be at the top level of your chosen publishing source. For example, if your publishing source is the `/docs` directory on the `main` branch, your entry file must be located in the `/docs` directory on a branch called `main`.

  If your publishing source is a branch and directory, the entry file must be at the top level of the source directory on the source branch. For example, if your publishing source is the `/docs` directory on the `main` branch, your entry file must be located in the `/docs` directory on a branch called `main`.

  If your publishing source is a GitHub Actions workflow, the artifact that you deploy must include the entry file at the top level of the artifact. Instead of adding the entry file to your repository, you may choose to have your GitHub Actions workflow generate your entry file when the workflow runs.

* The name of the `index.html` file is case sensitive. For example, `Index.html` will not work.

* The name of the file should be `index.html`, not `index.HTML` or any other variation.

### Directory contents

Check that your directory contents are in the root directory.

### Custom domain

If you're using a custom domain, make sure it's set up correctly. For more information, see [About custom domains and GitHub Pages](/en/pages/configuring-a-custom-domain-for-your-github-pages-site/about-custom-domains-and-github-pages).

* The `CNAME` record should always point to `<USER>.github.io` or `<ORGANIZATION>.github.io`, excluding the repository name. For more information about how to create the correct record, see your DNS provider's documentation.
* If you are able to access your landing page, but encounter broken links throughout, it is likely because you either didn't have a custom domain name before or are reverting back from having a custom domain name. In such cases, changing the routing path does not initiate a rebuild of the page. The recommended solution is to ensure that your site rebuilds automatically when adding or removing a custom domain name. This may involve configuring a commit author and modifying the custom domain name settings.

### Repository

Check whether your repository meets the following requirements.

* The branch you are using to publish your site must be the `main` or default branch.
* The repository must have a commit pushed to it by someone with admin permissions for the repository, such as the repository owner.
* Switching the repository's visibility from public to private or vice versa will change the URL of your GitHub Pages site, which will result in broken links until the site is rebuilt.
* If you are using a private repository for the GitHub Pages site, please check if your GitHub Pro, GitHub Team, or GitHub Enterprise Cloud subscription is still active. If you renew the plan, the GitHub Pages site will be automatically re-deployed. Otherwise, you can change your repository's visibility to public to continue using GitHub Pages for free.

If you are still receiving a 404 error, start a [GitHub Community discussion](https://github.com/orgs/community/discussions/categories/pages) in the Pages category.
