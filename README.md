## Technical Summary

Note: All this is liable to change once I get a block of free time to optimize the backend further. Things planned:

- Changing the origin file text markup language from [Markdown](http://daringfireball.net/projects/markdown/) to [Org](http://orgmode.org/org.html#Markup)
- Changing the static site generator from [Jekyll](https://jekyllrb.com/) to [Hugo](https://gohugo.io/)
- Incorporating [Pandoc](http://pandoc.org/) into the build process, or an Org parser for [Go](https://golang.org/)
- Using [Netlify](https://www.netlify.com/) instead of [Github Pages](https://pages.github.com/) for hosting
- Using [Netlify](https://www.netlify.com/) instead of [Cloudflare](https://www.cloudflare.com/) for CDN services, minification, SSL, and max-age headers
- Using [Zopfli Encoding](https://en.wikipedia.org/wiki/Zopfli) for seldom changed assets and pictures (rather than a less size-efficient DEFLATE encoder).

### Jekyll
Pages (located in the ["pages" subdirectory](https://github.com/StevenTammen/steventammen.github.io/tree/master/pages)) are written in GitHub flavored markdown, which [Jekyll](https://jekyllrb.com/) then converts to HTML and inserts into the template in the ["_layouts" subdirectory](https://github.com/StevenTammen/steventammen.github.io/tree/master/_layouts).

### Hosting
This site is hosted on GitHub Pages in this repository. Because this is a so called "User Pages site" (rather than a project site), it is hosted at steventammen.github.io (rather than steventammen.github.io/project-name).

### Custom Domain
I have opted to use steventammen.com as a custom domain instead of sticking with steventammen.github.io. Because I'm using Cloudflare as my DNS, I have acces to [CNAME flattening](https://blog.cloudflare.com/introducing-cname-flattening-rfc-compliant-cnames-at-a-domains-root/), which basically means I can use this apex domain bare without worrying about changes in GitHub Pages' server IP addresses. I've opted to go the non-www route because I think it looks cleaner and because I have no need of cookie separation on subdomains.

### Content Delivery Network (CDN)
Rather than sticking with Github Pages' CDN ([Fastly](https://www.fastly.com/)), this site uses [Cloudflare's CDN](https://www.cloudflare.com/features-cdn/). One of the main reasons for this is that Cloudflare offers a way to purge the CDN cache when you update pages, while GitHub's implementation of Fastly does not, as far as I can tell. Since I'm careful to individually purge files from the cache when I update them (there's [an API](https://www.cloudflare.com/docs/next/#zone-purge-individual-files-by-url-and-cache-tags)), Cloudflare lets me ensure that the CDN will never send outdated files. This is important because the files on this site tend to get updated a lot. (As to why this is, please see the Continuous Improvement, Open Source Content, and Open Source Design sections of the site's [About Page](https://steventammen.com/about/)).

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

## Pull Requests

I encourage you to submit pull requests for any improvements you can make to content (such as correcting typos or improving phrasing) or the site's design (such as improving the mobile UX). You can also check the [open issues](https://github.com/StevenTammen/steventammen.github.io/issues) for things that I'd like to get implemented eventually. I'm not a web developer by profession, so many of the things that I want done are out of my present knowledge range.

## Copyright and Terms of Use

The contents of this site are licensed under the <a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/">Creative Commons Attribution-ShareAlike 4.0 International License</a>. Any code associated with subprojects is licensed under the <a rel="license" href="http://www.gnu.org/licenses/gpl.html">GNU General Public License v3</a>, and will be located elsewhere (i.e., in project repositories separate from this one).
  
<br/>
<a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/">![Creative Commons License](https://i.creativecommons.org/l/by-sa/4.0/88x31.png "Creative Commons License")</a> &nbsp; &nbsp; &nbsp; <a rel="license", href="http://www.gnu.org/licenses/gpl.html">![GNU GPLv3 License](http://www.gnu.org/graphics/gplv3-88x31.png "GNU GPLv3 License")</a>
