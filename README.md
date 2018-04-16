# Getting Started with Hugo
Today we're going to use Hugo to generate our first static site! Open up your Terminal and follow along with these instructions.
## Install Hugo
Then verify the new install.
```
brew install hugo
hugo version
```
## Create a new site
```
hugo new site quickstart
```

## Add a theme
See themes.gohugo.io for a list of themes to consider. This quickstart uses the beautiful Ananke theme.
```
cd quickstart;
git init;
git submodule add https://github.com/budparr/gohugo-theme-ananke.git themes/ananke;

# Edit your config.toml configuration file
# and add the Ananke theme.
echo 'theme = "ananke"' >> config.toml
```

## Configure the theme
Open up `config.toml` in Atom and change the title to whatever you want:

```
baseURL = "https://example.org/"
languageCode = "en-us"
title = "CS52's First Hugo Site"
theme = "ananke"
```



# Adding Content
In Hugo, everything is a page. Typically, you'll have a `content` folder with all your pages.
Within the `content` folder, pages are further organized under directories. In our current project, we should automatically have a `content/posts` directory.
After your site is configured, we can add our first post.

### Our first post
*Note:* Make sure you're in your top-level directory (where your config file is located) or else Hugo will complain at you.

```
hugo new posts/my-first-post.md
```
Take a look at the tree organization of the `content` directory:

```
content
└── posts
    └── my-first-post.md
```


If you open up this newly created file, you'll see that Hugo has already pre-configured some of the settings for the page. It'll look something like this:

```
---
title: "My First Post"
date: 2018-04-13T12:01:29-04:00
draft: true
---

```

Notice that we've specified `draft: true`. This allows us to create and work on drafts before publishing them, which is very helpful for a live blog. Feel free to add some Markdown content below the header.

Now we can test out the site with the drafts toggle on:

```
hugo server -D
```

![alt text](images/firstpost.png)

Notice how Hugo automatically styles your post for you! Where did this come from? If you take a look inside the `themes/ananke` directory, you'll see our theme comes with built-in html layouts under the `post` directory, as well as a `_default` directory and a `partials` directory which contain more instructions to automatically style all new content we create.

### Adding images

What if we want to add images to our Markdown files? Hugo provides a few ways to do this. First, store your images in the `static/` directory. This is where Hugo automatically looks for static content. It's also common practice to add an additional `static/img/` directory specifically for images, but that's up to you.

Add some images to `static`:

```
├── static
│   ├── post-1.jpg
│   └── post-2.jpg
```

Then you can simply include them any of your Markdown files:

```
![image](/post-1.jpg)
```
Great!

![image](images/addimage.png)


### Adding a nav bar
Adding additional layouts such as a top nav bar with links to pages within your site is incredibly easy.

First, we need to create pages for some of the links we want to include in our navbar.

```
hugo new content/about.md
hugo new content/getting-started.md
```

Add some Markdown content in each of these pages.

Now we need to create a menu. In the `config.toml` file, add the following code to create the navbar menu:

```
[menu]

  [[menu.main]]
    identifier = "about"
    name = "About"
    pre = "<i class='fa fa-heart'></i>"
    url = "/about/"
    weight = -110

  [[menu.main]]
    name = "Getting Started"
    pre = "<i class='fa fa-road'></i>"
    url = "/getting-started/"
    weight = -100

  [[menu.main]]
    name = "Posts"
    pre = "<i class='fa fa-road'></i>"
    url = "/posts/"
    weight = -100
```
