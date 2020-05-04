# How to create a page

Create a new repository and use this as a template. 

Name your repository with the course name you want in the address. The address will be in format `https://centria.github.io/<repository>/`.  
Use only letters, numbers and dashes in the repository name!

In your new repository, go to SETTINGS. Scroll down to GitHub Pages and select `master branch` as your source. If you want to use another branch, select that instead. DO NOT CHOOSE A THEME. This template uses a remote theme and is already set up.

Your page should be ready and online. This might take a few minutes. If the page does not come up, create a commit and push it to your repository.


## Page structure

The pages are in the folder `docs`. At the beginning of the page is some `YML` which define the structure and order of the pages.  

You can also have subpages for your pages. For that, the default order of pages is something like follows:

```
[. . .]
├── part1
│   ├── index.md
│   ├── part1-1.md
│   ├── part1-2.md
│   ├── part1-3.md
│   ├── part1-4.md
│   └── part1-5.md
├── part2
│   ├── index.md
[. . .]
```

The YML of a parent, i.e. the `index.md` contains for example the following information:

```yml
---
title: "Part 1 - The beginning"
permalink: /part1/
nav_order: 1
published: true
has_children: true
has_toc: true
---
```

And for the child:

```yml
---
title: "Printing and reading"
parent: "Part 1 - The beginning"
permalink: /part1/1/
nav_order: 1
published: true
---
```
