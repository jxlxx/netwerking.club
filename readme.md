# netwerking.club

This a collection of notes loosely based on the textbook `Computer Networks: A Systems Approach` by Bruce S. Davie and Larry L. Peterson.

The static site if generated via gohugo: https://gohugo.io/

The hugo theme is `hugo-book`: https://github.com/alex-shpak/hugo-book/

# Getting Started

To run this application you need to have go and hugo.


If you already have all the dependecies on your machine, 

```bash

git clone git@github.com:jxlxx/netwerking.club.git
cd netwerking.club/website
hugo server

```

There is also a nix flake, so you can do:

```bash

git clone git@github.com:jxlxx/netwerking.club.git
cd netwerking.club
nix develop
cd website
hugo server

```

And there is an `.envrc` file, so you can also do

```bash

git clone git@github.com:jxlxx/netwerking.club.git
cd netwerking.club
direnv allow
cd website
hugo server

```

so that whenever you `cd` into `netwerking.club` the shell loads automatically.



# To edit 

All the content can be found in `website/content`















