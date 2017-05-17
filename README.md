# Technical Overview

Note: All this is liable to change once I get a block of free time to optimize the backend further. Things planned:

- Changing the origin file text markup language from [Markdown](http://daringfireball.net/projects/markdown/) to [Org](http://orgmode.org/org.html#Markup)
- Changing the static site generator from [Jekyll](https://jekyllrb.com/) to [Hugo](https://gohugo.io/)
- Incorporating [Pandoc](http://pandoc.org/) into the build process (or an Org parser for [Go](https://golang.org/) if someone gets around to writing one)
- Using [Netlify](https://www.netlify.com/) instead of [Github Pages](https://pages.github.com/) for hosting
- Using [Netlify](https://www.netlify.com/) instead of [Cloudflare](https://www.cloudflare.com/) for CDN services, minification, SSL, and max-age headers
- Using [Zopfli Encoding](https://en.wikipedia.org/wiki/Zopfli) for seldom changed assets and pictures (rather than a less size-efficient DEFLATE encoder).

### Jekyll
Pages (located in the ["pages" subdirectory](https://github.com/StevenTammen/steventammen.github.io/tree/master/pages)) are written in GitHub flavored markdown, which [Jekyll](https://jekyllrb.com/) then converts to HTML and inserts into the template in the ["_layouts" subdirectory](https://github.com/StevenTammen/steventammen.github.io/tree/master/_layouts).

### Hosting
This site is hosted on GitHub Pages in this repository. Because this is a so called "user pages site" (rather than a project site), it is hosted at steventammen.github.io (rather than steventammen.github.io/project-name).

### Custom Domain
I have opted to use steventammen.com as a custom domain instead of sticking with steventammen.github.io. Because I'm using Cloudflare as my DNS, I have acces to [CNAME flattening](https://blog.cloudflare.com/introducing-cname-flattening-rfc-compliant-cnames-at-a-domains-root/), which basically means I can use this apex domain bare without worrying about changes in GitHub Pages' server IP addresses. I've opted to go the non-www route because it means less typing over time, because it is more legible and speakable, and because I have no need of cookie separation on subdomains.

### Content Delivery Network (CDN)
Rather than sticking with Github Pages' CDN ([Fastly](https://www.fastly.com/)), this site uses [Cloudflare's CDN](https://www.cloudflare.com/features-cdn/). One of the main reasons for this is that Cloudflare offers a way to purge the CDN cache when you update pages, while GitHub's implementation of Fastly does not, as far as I can tell. Since I'm careful to individually purge files from the cache when I update them (there's [an API](https://www.cloudflare.com/docs/next/#zone-purge-individual-files-by-url-and-cache-tags)), Cloudflare lets me ensure that the CDN will never send outdated files. This is important because the files on this site tend to get updated a lot. (As to why this is, please see the "Open Source" and "Continuous Improvement" sections of the site's [About Page](https://steventammen.com/about/)).

### Caching Everything
Using a Cloudflare page rule, I have Cloudflare's ["cache everything" option](https://support.cloudflare.com/hc/en-us/articles/200172366-How-do-I-cache-everything-on-a-URL-) activated across all pages of the site with the Edge Cache TTL set to a month (the highest it can go). Basically, things will only need to get revalidated when I update individual files and purge them from the cache. Having practically everything cached on CDN edge nodes practically all the time means that the site should always load quickly.

### Max-Age Headers
I am also using Cloudflare to set max-age headers. Last time I checked, GitHub Pages' max-age headers were 600 seconds (non-configurable). Cloudflare lets you set them a lot higher -- I am currently using max-age headers of a day, which I think is a good compromise. Having them set too short (like 600 seconds) makes them not very useful because cached files will expire before getting used, but having them set too long can cause problems when you update pages, especially if different assets are at different aging points. For example, if you change the HTML of a page in a significant way, you are probably also going to change the CSS, so if the HTML is at a later aging point than the CSS, bad things will happen when only the HTML gets updated.

### Gzipping And Minification
GitHub Pages gzips HTML, CSS, and Javascript automatically, as does Cloudflare's CDN (which also compresses [additional file types](https://support.cloudflare.com/hc/en-us/articles/200168396-What-will-CloudFlare-gzip-)). I gzip pictures on my own, since neither service automatically compresses these. I have Cloudflare set to automatically minify HTML, CSS, and Javascript when they get sent to the CDN, and it does this even if the files it receives from GitHub Pages are gzipped.

### SSL
Connections from website visitors to Cloudflare are encrypted, as are connections from Cloudflare to GitHub's servers. Unfortunately, GitHub Pages doesn't offer proper TLS/SSL for custom domains, so until they get that operational, those of us with custom domains won't be able to achieve Strict Full SSL. Since security on this site is more for philosophical reasons than practical ones (i.e., I'm encrypting communications because everything should be encrypted in principle, not because I'm dealing with credit card numbers), I don't consider this much of a compromise, but it is important to note that this site does not have SSL in the same sense that your bank's site has SSL: back-end over TLS is not validated.

### Forcing HTTPS
HTTPS is forced with two page rules in Cloudflare: the first one changes http://steventammen.com/ requests to https://steventammen.com/ requests, and the second one ensures that redirects from https://www.steventammen.com/ to https://steventammen.com/ are done entirely over HTTPS. I don't need another page rule for http://www.steventammen.com/ to https://steventammen.com/ redirects because http://www.steventammen.com/ requests will always get redirected to http://steventammen.com/ requests, which will then get changed to https://steventammen.com/ requests because of the first page rule.

### HTTP Strict Transport Security (HSTS)
HSTS is enabled to prevent downgrade attacks, SSL stripping, and cookie hijacking. I'm not worried about HSTS taking my site down because I never plan to stop using HTTPS.

### Email
[Mailgun](https://mailgun.com) is used to handle all email through the site (rather than, say, Google Apps for Business).

# Contribution Guidelines

### Planned Contributions

I use a Kanban-esque [Waffle.io board](https://waffle.io/StevenTammen/steventammen.github.io) to track all of the things that I am currently working on, plan to work on soon, or plan to work on eventually -- both for content and design. Put simply, this is where you should start if you want to contribute to this site, because this is the roadmap for the future. If you see something you want to help with, go for it! (I'll explain how in a second).

Over time, if you take on an active role in development, I'll add you as a collaborator on GitHub, and you'll be able to edit pages and the Waffle.io board directly, with write permissions to the repository.

This is the side of contribution that is structured: groups of people work together to achieve planned goals in an orderly fashion.

### Ad Hoc Contributions

Things can also be improved over time without any sort of overarching plan to bind contributions together: "organic growth", if you will. If there is something about the content or design of the site that you think could be done better, that is valid grounds for contributing. Nothing on this site is off limits -- you are free to contribute, as you see fit, in whatever way you want, pending my approval. Below are some examples of what *ad hoc* contributions could look like.

Example Content Contributions:

- Eliminating typos
- Eliminating unecessary verbosity or denseness of prose
- Improving phrasing, flow, or pacing
- Adding visual aids, such as diagrams, to enhance comprehension
- Expanding vague sections or adding additional support for points 
- Anything else you think could make the content better

Example Design Contributions:

- Improving the desktop UX
- Improving the mobile UX
- Improving accessibility
- Adding customization options for various aspects of the site's appearance and functionality
- Anything else you think could make the site better

This is the side of contribution that is unstructured: individuals contribute over time to make the site better.

### How To Contribute With Respect To Content

At the top of every page I have included two buttons that link to its [markdown](https://daringfireball.net/projects/markdown/) source: one links to the page's location in this repository and the other links to the page's location on [Prose.io](http://prose.io/), an online markdown editor for GitHub.

You can help improve the site's content by submitting pull requests with editorial changes on Github, or by editing the pages on Prose.io and then pressing "Save" --> "Submit Change Request", which will automatically create the pull request for you. Prose.io is great if you don't have a lot of experience with Git and GitHub -- even though you need a GitHub account to propose changes through Prose.io, you need no other knowledge, so once you [set up a GitHub account](https://github.com/join), you can contribute freely without having to know all the complicated programmer stuff. If you aren't comfortable contributing through GitHub or Prose.io, you can also just email improvements to <a href="mailto:edits@steventammen.com">edits@steventammen.com</a>.

At the present time, I am not aware of any easy way for me to make content editable in a rich text environment, so if you want to contribute through GitHub or Prose.io, you are going to have to learn the basics of [markdown syntax](https://daringfireball.net/projects/markdown/syntax). You won't have to know anywhere near the whole specification to help -- if you skim the sections related to paragraphs, links, lists, and emphasis and you should have a good working knowledge in just a few minutes.

### How To Contribute With Respect To Design

You can help improve the site itself by submitting pull requests with design improvements. If you are comfortable with web development languages but not GitHub pull requests, you can send implementations to <a href="mailto:design@steventammen.com">design@steventammen.com</a> and I'll incorporate them into the repository myself. If you aren't comfortable with web development languages or GitHub pull requests, your ideas are still valuable, and you can send them to that same address.

For pull requests requiring significant amounts of work, it would be a good idea to check with me early on to make sure I approve of the changes or enhancements being considered. I don't want to put you in a situation where you put a lot of work into something that I wouldn't ultimately use.

### Benevolent Dictator For Life Powers

I enjoy working with other people -- and benefit immensely from constructive criticism and new perspectives -- but ultimately, decisions about the direction of this site come down to me. In particular, this means that I alone will choose:

1. what gets written about
2. which improvements find their way into the main repository, and 
3. how things are shared and licensed

I want to be transparent about this: all contributions to this site are subject to the three statements above. Now, I am perfectly happy to discuss my reasoning for any given decision I make. As a human being, I am subject to many [cognitive biases](https://en.wikipedia.org/wiki/List_of_cognitive_biases) that can lead to irrational decision-making, meaning that I am sometimes wrong (just like everybody is from time to time). If you think I am wrong, tell me *why*. I can't promise that I'll always change my mind to agree with you, but I can promise that I will give your view as fair a hearing as I can.

If it works out that there is a writing topic that you are really passionate about but I am not (for whatever reason), or something you think should be changed but I do not (for whatever reason), or work that you did that you don't want to be opensourced under copyleft (for whatever reason), it is better all the way around if you create a site of your own to do things your way (I'd be happy to help and contribute!).

What I envision, in the long run, is a community of people writing about the things they are passionate about, freely helping each other improve while at the same time maintaining their own autonomy. This encourages the collaboration that open source projects are known for without causing the conflicts of leadership that they are also known for.

# Copyright and Terms of Use

The contents of this site are licensed under the <a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/">Creative Commons Attribution-ShareAlike 4.0 International License</a>. Any code associated with subprojects is licensed under the <a rel="license" href="http://www.gnu.org/licenses/gpl.html">GNU General Public License v3</a>, and will be located elsewhere (i.e., in project repositories separate from this one).
  
<br/>
<a rel="license", href="http://creativecommons.org/licenses/by-sa/4.0/"><img src="https://i.creativecommons.org/l/by-sa/4.0/88x31.png", alt="Creative Commons License"></a> &nbsp; &nbsp; &nbsp; <a rel="license", href="http://www.gnu.org/licenses/gpl.html"><img src="http://www.gnu.org/graphics/gplv3-88x31.png", alt="GNU GPLv3 License")></a>
