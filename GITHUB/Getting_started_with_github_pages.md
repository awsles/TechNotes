# Getting Started with Github Pages
Along with this TechNotes github repository, I decided to also give [github pages](https://pages.github.com) a try.
As I often find, the documentation provided - while decent - has certain gaps for someone completely unfamiliar with
Jekyll. SO I thought I would provide some helpful tips as I go along (before I too, become too skilled that I no longer
recognize what was a challenge when I started).

I will add notes as Ia go along. Sometimes this is just a matter pf having handy links all in one place

**Comments and contributions are welcomed!**

## Steps
Getting started with github pages was super easy.  Be aware that all content published via
github pages is PUBLIC, even if your repository is private.

1) **/docs or not?**
-- Decide whether you will use the entire repository for pages or just everythin within the /docs folder.
I chose to use a /docs folder as my publishing branch so that I could
keep other stuff in the repository without having it automatically published. 
If you want to use the /docs folder, then you must create this first and put a simple README.md inside.

2) **Enable Pages**
-- Follow the steps [here](https://pages.github.com/) by scrolling down the page and following the steps.
In a nutshell, you go to the **Settings** area of your repository, scroll down and select your Source
as decided in step 1 above. And then choose a theme to get you started.

![](https://pages.github.com/images/launch-theme-chooser@2x.png?raw=true)

3) **Create index.md**
-- Create a simple index.md in either the root folder or in /docs (depending on where your root is).

4) **Update README.md**
-- Now you can optionally update your README.md to include the [sample theme page](https://pages-themes.github.io/slate/) with markdown.
I like to do this so that I have a handly markdown cheat sheet.
You can copy the raw code from [here](https://raw.githubusercontent.com/pages-themes/slate/master/index.md).


## Resources
In addition to tech notes, below are some additional related resources:

* [About GitHub Pages and Jekyll](https://help.github.com/en/github/working-with-github-pages/adding-a-theme-to-your-github-pages-site-using-jekyll)
-- One of the 1st steps is to add a theme to the pages. Github pages provides about a dozen built-in themes.

* [Adding a theme to your GitHub Pages site using Jekyll](https://help.github.com/en/github/working-with-github-pages/adding-a-theme-to-your-github-pages-site-using-jekyll)
-- Personalize your site by adding and customizing a theme.

* [About Plugins](https://jekyllrb.com/docs/plugins/)
-- Jekyll has a plugin system with hooks that allow you to create custom generated content specific to your site.
This is useful for certain extensions such as using 

* [Jemoji](https://github.com/github/gemoji)
-- Use github emojis in your documentation.
