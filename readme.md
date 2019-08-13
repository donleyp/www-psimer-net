[![Build Status: live](https://travis-ci.org/donleyp/www-psimer-net.svg?branch=live)](https://travis-ci.org/donleyp/www-psimer-net)

[![Build Status: staging](https://travis-ci.org/donleyp/www-psimer-net.svg?branch=master)](https://travis-ci.org/donleyp/www-psimer-net)

*Please do not fork this repository. See acceptable use under license.*

# Build and Publishing

## Build

The blog is written using "wintersmith", a static site generator written in CoffeeScript on Node.js.

The only prerequisites are node, npm, and wintersmith.

1. Install Node.js
2. Install npm
3. install wintersmith `npm install wintersmith -g` (may need sudo based on your system config)

To preview the site:

 $ wintersmith preview

To build the site:

 $ wintersmith build

## Publishing

Copy the files in the `build` directory to your host.

Right now we are deploying this blog to "staging.psimer.net" and "www.psimer.net" using Amazon S3 Static Website Hosting. The deployment is performed by travis-ci.org at the end of the build for the "master" (staging) and "live" (www) branches. See .travis.yml for detailed config.

### Development Process

1. Make all changes on a local git clone of "master" or a branch off of "master".
2. Push to "master". travis-ci.org will build and deploy to staging.psimer.net
3. Test on staging.psimer.net
4. When testing passes merge "master" -> "live". travis-ci.org will build and deploy to www.psimer.net

# TODO

* write post about wintersmith
* Add source code link to menu

# License

## Intent

My intent is to share under the MIT license any and all code associated with this site so that others may feel free to repurpose such code for their own use with minimal restriction. The thoughts, ideas, and multi-media contained in this site, however, are mine and mine alone. You do not have the right to copy any of that without my express permission. You do have permission to link to, share, and otherwise disseminate excerpts and quotes of this site's content on social media networks and other avenues like email. 

Basically, feel free to copy the *how* but not the *what* and feel free to link to and quote the content on this site.

## Legaleze

All code in this project not otherwise marked as licensed by the original author is licensed under the following terms:

---

Copyright &copy; 2015 Donley R. P'Simer

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

---

The published site and all content files are:

Copyright &copy; 2015 Donley R. P'Simer. All rights reserved. Unauthorized re-publishing is prohibited. Content files are defined as markdown files (`**/*.md`) and any photo, video, or audio files included in the published content of the site.
