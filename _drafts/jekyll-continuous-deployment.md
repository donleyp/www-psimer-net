---
layout: post
title:  "Jekyll, S3, and Continuous Deployment"
date:   2015-02-22 22:00:00
categories: AWS
tags: jekyll AWS S3
---
I would like to get to something like this in the future (but that's another blog post):

{% mermaid %}
graph LR
	GIT[GIT Repo]
	clone(Local Clone)
	s3((S3))
	GIT-->clone
	clone-->GIT
	GIT-->|s3_website|s3
{% endmermaid %}