# About this repo and GitHub Pages

This is just a landing page / front page with my real content published on
other subdomains.

## Publish on Github Pages

By using GitHub pages (or similar), you can publish static web pages for free.

The following instructions also show how to configure your own custom DNS domain
to point to your GitHub Pages.


# Background

See GitHub documentation:
- [Creating a GitHub Pages site](https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site)
- [Configuring a publishing source for your GitHub Pages site](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)
- [Managing a custom domain for your GitHub Pages site](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site)
- [Securing your GitHub Pages site with HTTPS](https://docs.github.com/en/pages/getting-started-with-github-pages/securing-your-github-pages-site-with-https)

# Update DNS if the plan is to use a custom DNS domain, and no website yet exists

This should be done if you plan to use your own custom DNS domain.
Otherwise `https://<your-github-account>.github.io/` will be used.

As it can take some time for DNS updates to propagate, and for old cached DNS
data to time out, start by updating the DNS records for your domain.
For details, see the
[GitHub documentation](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site#configuring-a-subdomain).

If you have an active website, wait to update your DNS until you have your
GitHub Pages set up.

In my case, I added the following to my BIND/named DNS zone configuration:
```
                        IN      A       185.199.108.153
                        IN      A       185.199.109.153
                        IN      A       185.199.110.153
                        IN      A       185.199.111.153
                        IN      AAAA    2606:50c0:8000::153
                        IN      AAAA    2606:50c0:8001::153
                        IN      AAAA    2606:50c0:8002::153
                        IN      AAAA    2606:50c0:8003::153
www                     IN      CNAME   mem-.github.io.
```

# Create a GitHub repository matching the required naming standard

See the
[GitHub documentation](https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site).

Repository name: \<your-github-account\>.github.io

Description: The landing page for www&#46;<your.domain>

Optionally select the README and/or .gitignore

Click `Create repository`.


# Add your web content to the repository

## Set up you local repository 

Use one of the methods described on the page that appeared when the repository
was created. I descided to use the `create a new repository on the command line`.

```bash
cd <your-local-git-repo-home-path>/
mkdir www.<your.domain>
cd www.<your.domain>/
git init
git checkout -b main   # if the unborn branch is named master
```

## Create a .gitignore file

```bash
cat << '_EOT' > .gitignore  # single quote _EOT tag to keep $ sign and not process as a variable
# -*- mode: gitignore; -*-
# Line above is an Emacs tag to select correct edit mode

### Classic editor files to ignore
## Emacs, for more examples see https://github.com/github/gitignore/blob/main/Global/Emacs.gitignore
*~
\#*\#
.\#*

## VScode, for more examples see https://github.com/github/gitignore/blob/main/Global/VisualStudioCode.gitignore
.vscode/*


### Classic OS releated files to ignore
## Windows, for more examples see https://github.com/github/gitignore/blob/main/Global/Windows.gitignore
# Windows thumbnail cache files
Thumbs.db

# Folder config file
[Dd]esktop.ini

# Recycle Bin used on file shares
$RECYCLE.BIN/

# Windows shortcuts
*.lnk

## Mac OS-X, for more examples see https://github.com/github/gitignore/blob/main/Global/macOS.gitignore
# General
.DS_Store
.AppleDouble
.LSOverride
Icon[]

# Thumbnails
._*


### My classic config files ans similar to ignore
# Local git config that overides or adds settings from ~/.gitconfig
.gitconfig
# Any files related to Bash
.bash*

## Files used by 'direnv', see https://direnv.net/
.env
.envrc
_EOT
```

```bash
git add .gitignore
git commit -m "Added .gitignore file" .gitignore
```

## Create a README.md file

I added a simplified version of this webpage to the README.md.

```bash
git add README.md
git commit -m "First version of README.md" README.md
```

## Add the actual web content

I decided to put the web content in `docs`.

```bash
mkdir docs
```

Add your web content.

```bash
git add docs/
git commit -m "First version of web content" docs/
```

## Push your first version to GitHub

```bash
git remote add origin https://github.com/<your-github-account>/<your-github-account>.github.io.git
git push -u origin main
```

# Publish your GitHub Pages

See the
[GitHub documentation](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site#publishing-from-a-branch).

Branch: main

Folder: /docs

Click `Save`

See also the following if you want to
[configure a custom domain for your GitHub Pages site](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site).

Custom domain: <your.domain>

## Pull the updated repository to your local machine

When you publish your website with a custum DNS domain, GitHub creates a `CNAME`
file in the folder selected for the web content.

```bash
git pull origin
```

# Update DNS, if not done above

This will move all new traffic from your old website to GitHub Pages.

This should be done if you plan to use your own custom DNS domain.
Otherwise `https://<your-github-account>.github.io/` will be used.

For example settings, see above.

# Add HTTPS (TLS) when your site is working

See
[Securing your GitHub Pages site with HTTPS](https://docs.github.com/en/pages/getting-started-with-github-pages/securing-your-github-pages-site-with-https).
