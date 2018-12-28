title: Moving House
tags:
  - Meta
date: 2017-12-19 23:32:45
---
Previously I had this blog hosted on RedHat's OpenShift PaaS using WordPress. I haven't been blogging frequently for about 2 years, and I missed RedHat's memo about the migration because I registered using an obscure email from a shell account without webmail. [https://blog.openshift.com/migrate-to-v3-v2-eol/](https://blog.openshift.com/migrate-to-v3-v2-eol/) Lo and behold my blog has vanished, although thankfully I have the entire SQL dump (and most of the crucial media) from the beginning of this year. To minimize the chance of this happening ever again (and to minimize the effort of getting my site up and running again, knock on wood) SSGs seem like the best solution since they have the content in a portable, versionable format, although I would have preferred a Ghost blog.

Hexo caught my eye over other static site generators due to:
* Complete compatibility with Octopress plugins
* `hexo server -d` watches the filesystem and automatically generates new content upon reload
* Prebuilt themes like the one I'm using now have the basics of what a nerdy blog needs OOTB:
	* $\textbf{MathJax}$
	* Instant {% fab font-awesome-flag %} support with an `npm install hexo-tag-fontawesome`
	* SEO basics like a configurable sitemap and newfangled generator plugins for stuff like Google AMP which will close the gap between CMSes
* One line deploy to Git, (S)FTP, among other targets