---
layout: post
title:  "Hosting a Blog on Amazon S3"
date:   2015-02-22 22:00:00
categories: AWS
tags: jekyll
excerpt: >
  Hosting a blog on tublr or blogger seemed boring while hosting a blog using my own WordPress site seemed like overkill. I was looking for a way to host a blog using just Amazon S3 static website hosting and simple text-based tools. I found Jekyll and this is my blog post about it.
---
# Why not WordPress?

I've wanted to setup a blog for a long time. The main thing that's been stopping me is that I didn't think I would have the time to keep it up and figured it would be worse to start one and then let it peter off. The other reason was that I wanted something that I had complete control of (e.g. not blogger, or tumblr) but without a lot of maintenance headaches. The first reason is just an issue of committment and the second reason is just an excuse. If I wanted a blog I would have to find a simple way to put it together that met my architectural needs.

I thought about bringing up a WordPress blog using [Elastic Beanstalk](http://aws.amazon.com/elasticbeanstalk) or a small EC2 instance with the LAMP stack installed. It bothered me from an architectural perspective that I needed a relational database and an application server to back a blog. A blog, after all, is just a set of articles and other content put together to create a website. The articles don't change over time or gather data from a database. They simply sit there in the database waiting to be served up. It doesn't make a lot of sense that I need a multi-tiered application architecture for this simple task. One thing that blogging servers do very well though is article management and page generation based on templates. I needed that functionality but I did not want the content to be generated at request time.

I wanted a solution that would give me the DRY-ness of CMS systems, be easy to use (for an engineer), and did not require a server. I wondered whether anyone had solved the problem of building and deploying a blog to Amazon S3 so I [googled "host a blog on s3"][host-blog-on-s3] and clicked on one of the top articles, ["No Server Required - Jekyll & Amazon S3"][no-server-required], by Werner Vogels. Werner is the CTO of Amazon so I knew I had struck proverbial Internet gold here. Werner's thoughts on creating a blog jived well with my own so I took a look at the technologies he mentioned. Within two hours I had moved my domain away from pointing at a Google Site page and had a fully working blog on Amazon S3.

# Jekyll in a Nutshell

[Jekyll][jekyll] is a tool that enables you to "Transform your plain text into static websites and blogs". You install it using the Ruby gem command: `gem install jekyll`. To create a Jekyll blog you run the `jekyll new` command. To edit the blog and add content you simply create simple text files containing markdown, html, or other convertible text. The placement and naming of the files is important and gives Jekyll the hints it needs to generate your site. You also prepend what is called "Front matter" to the files. This config gets processed by Jekyll for any hints or meta-data that it can't glean from the location and name of the file. To build your site you use the `jekyll build` command which will generate your site into the '_site' directory of the project. During development you can use the `jekyll serve` command to run a small web server at <http://localhost:4000> that serves up your site. This command will also watch for changes and rebuild your site when they occur.

# Jekyll in a Bucket

[s3_website](https://github.com/laurilehmijoki/s3_website) is another Ruby gem that makes it easy to create a website hosted using S3 static website hosting with just a couple of parameters. It will also support [CloudFront](http://aws.amazon.com/cloudfront) distributions and other advanced features. The setup is fairly easy and it will create the necessary bucket for you if it does not already exist so it is a great way to bootstrap the whole process especially for those of us who are not S3 experts yet.

# Blogging Like a Hacker

Once we have a site built out and everything customized the way we want it is time to figure out our workflow so that we can quickly add and edit content to the site. Werner mentioned using DropBox for storing his site in the cloud and syncing the content to all of his computers so that he can edit it at any time. I like this idea but I wanted the power of a source control system as well so I chose [GitHub](http://github.com). s3_website works on local files, not Git repos so my workflow looks like this:

{% mermaid %}
graph LR
	GIT[GIT Repo]
	clone(Local Clone)
	s3((S3))
	GIT-->clone
	clone-->GIT
	clone-->|s3_website|s3
{% endmermaid %}

Now my basic workflow is this:

1. Startup a shell and cd into my project directory.
2. Run `jekyll serve`.
3. Open a browser to <http://localhost:4000>
4. Make my edits.
5. Refresh the browser to see my changes. Rince, Repeat.
6. When I want to publish execute the command `s3_website push`.
7. Periodically push to GitHub to backup my changes.

# Next Steps

In a future article I plan to detail the steps taken to setup this website and cover some of the nuances of the nuances of setting this up correctly including how to setup [Amazon Route 53](http://aws.amazon.com/route53) to point your custom domain at your newly minted website.

[no-server-required]:http://www.allthingsdistributed.com/2011/08/Jekyll-amazon-s3.html
[host-blog-on-s3]:https://www.google.com/webhp?sourceid=chrome-instant&ion=1&espv=2&ie=UTF-8#q=hosting%20a%20blog%20on%20s3
[jekyll]:http://jekyllrb.com
