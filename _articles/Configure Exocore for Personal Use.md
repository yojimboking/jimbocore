---
published: true
topic:
subtitle:
date: 2022-09-26
tags: 
---

# Configure Exocore for Personal Use

## Change your Username and Homepage
Navigate to `/exocore/data/user.yml`. Open the file in any text-editor (e.g. Notepad or TextEdit) and look for `user_name: Remilia Corporation`. Change this to whatever name you want to appear on the left sidebar.

## Change your Homepage Content

In the same `/exocore/data/user.yml` file, you will also see `welcome_header` and `welcome_subtitle`. These control the title and subtitle that appear on your homepage.

On the root folder you will find `index.md`, this can be edited like any other article as your homepage with the addition of the title and header from the `user.yml` file. Make sure you keep the following frontmatter at the top of the markdown file: 
```---
layout: home
title: home
---```

## Change your Profile Picture

The profile picture that appears on the left sidebar is located at `assets/img/pfp.png`, you can replace this file with any .png. Note that it will be resized into a square. If you want to use a .jpg, navigate to `/exocore/data/user.yml`, open it in a text editor, and change the filename for `profile_pic:` to whatever your file is called.

## Change your Social Media Card Image
The social media card that appears when your site is linked on social media sites like Twitter, Facebook, etc. is located at `assets/img/pfp.png`, you can replace this file with any .png. Note that a dimension of 1200x800 or more is recommended. If you want to use a .jpg, navigate to `/config.yml`, open it in a text editor, and change the filename for `image:` to whatever your file is called.

## Change your Site's Title and URL 
Navigate to ```/_config.yml``` to change the Title and URL of your exocore. All other settings can be left as is.

## Change the Theme
The Exocore ships with multiple themes to choose from. Navigate to `/styles.scss` and look for the line that says `//Uncomment one of the following lines to choose a theme:`. To select a theme, remove `//` from the line of the theme you want to try, and add `//` to the previously active theme ("yotsuba" by default).