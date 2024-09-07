+++
title = "My Site's Performance"
date = 2024-09-07
updated = 2024-09-07

description = "My reasons for the changes to the tabi theme and hosting for better performance"

[taxonomies]
tags = ["web dev", "performance", "software"]

[extra]
giscus = true
quick_navigation_buttons = true
toc = true
+++

Recently I have been trying to prepare my site for the 2025 summer internship season. One of my goals was to improve my websites performance. The tabi theme I use already gets a [100 on Google Lighthouse](https://pagespeed.web.dev/analysis/https-www-traudt-dev/mp1q56nnpm?form_factor=mobile), but I did notice some issues when running it through the likes of [WebPageTest](https://www.webpagetest.org/result/240906_BiDcYQ_9TB/). It mentioned that I had no fetch priority on my head shot, lacked passive event listeners, and was loading images that were blocking the webpage render. I also had some CLS from my head shot. I resolved all of these issues on [my fork of tabi](https://github.com/blaine-t/site). I would consider pushing them up to the main project but I believe that depending on the site some of these could be detrimental to other people's sites so I will just keep these changes on my fork. I do want to talk about a couple things that I learned about during this processes when it comes to website development, more specifically static site development.

## Static Sites

### Cloudflare Pages

I currently have this site deployed using Cloudflare pages, so I have my data across the world using Cloudflare's CDN. This means that my files are closer to people than they would be if I self hosted this site like I do with my other services. The main reason I decided to do this is because since this is a static site I can use [Cloudflare pages free tier](https://pages.cloudflare.com/). Their free tier is extremely generous and there is no way I will go over the limits imposed by it. This was the first performance improvement I made to my site.

### Browser Cache

One of the great things about a static site is how easy to cache the whole site is. The only items that aren't reused between different pages is the HTML (duh) and new images. The rest of the site's CSS and JS is able to be cached between page loads leading to fast redirects on the site. I would have liked to inline some of the CSS and JS to reduce the time for a cold start but I think it is worth losing some performance there to have snappier page redirects.

### Repeatability

The best part about optimizing a static site is the fact that there is no dynamic content that you have to work around. You know what is going to be on the page every time you load it. This makes testing using tools like Google Lighthouse and WebPageTest a lot more consistent between runs meaning you can know if the performance difference is from your changes and not some other reason.

## General Improvements

### Fetch Priority

[Fetch priority](https://web.dev/articles/fetch-priority) is a technology I have had no previous experience in so it was interesting to explore what it had to offer. The first issue I wanted to tackle was that my head shot had a "low" fetch priority. This was leading to the first render of my site not having my head shot and making it look a little off. My first attempt at solving this was adding `fetchpriority="high"` to the head shot img tag but this only did so much. I decided on adding a `rel=preload` in a link at the top of the head to make sure that the head shot was available before page render and that did the trick! In order to make sure that I didn't slow down the site doing this though I ensured that my head shot image was compressed down. I currently have my 270x270px headshot only weighing 8KB in webp format so I would say that is adequate enough. While on the topic of fetch priority I also added `preconnect` to the navbar to make any of those redirects even snappier. I am still on the fence on this one because Firefox seems to ignore them and Chrome loads them before it loads my lazy images leading to a possible slow down on rendering my "Featured projects" images. I will update here if I decide not to keep them.

### Passive Event Listeners

[Passive event listeners](https://developer.chrome.com/docs/lighthouse/best-practices/uses-passive-event-listeners) are also new to me. They make sense in that they stop scroll and touch down events from affecting the users scrolling experience by telling the browser that they don't block them and are just listening to see if they happen. This makes it so the browser doesn't have to wait for JS to execute in order to actually scroll the page. There was only one JS file that had this issue and it was `searchElasticlunr.js` which had 3 `addEventListener`s that got this treatment. It didn't appear to have any adverse effect on using the search functionality on the site so I am keeping it around!

### Lazy Loading Images

A [recent tabi commit](https://github.com/blaine-t/tabi/commit/9e7b845e544758792831da520379e04089909b78) actually introduced lazy loading the footer svgs which was a great improvement in this regard but one thing that still wasn't lazy loaded was the "Featured projects" images. I added lazy loading to these images and it is a very minute change and only realistically effects mobile users or people with very wonky aspect ratios. I still implemented it as it didn't hurt the site's load times.

## Image Optimization

### File Format

One of the issues I struggled with was deciding on a file format for images on this site. I originally settled on webp because it was the format I was used to for performant images with transparent backgrounds but then I came to find out that avif finally got major browser support with [Can I Use giving it Baseline 2024 status](https://caniuse.com/avif). I am currently in the process of porting over all of my images to avif. One thing I have noticed with avif is that it is a lot harder to encode to a good size than webp because of the massive amount of variables at your disposal. When I was converting my pngs to webps all I did was `cwebp -q 100 input.png -o output.webp` and that would normally produce good results but with avif there are so many more tunables. I am currently using `avifenc --min 0 --max 63 -a end-usage=q -a cq-level=30 -a color:enable-chroma-deltaq=1 -a color:enable-qm=1 -a color:deltaq-mode=3 input.png ouput.avif` and it works pretty well but sometimes webp comes out better.

I really wish that as a web dev community we could decide on one format instead of having to deal with all these different ones. JPEG-XL looks promising but Google doesn't want to implement it so it is off the table (we love monopolies). Avif seems pretty good but just recently got support so there will be some old browsers that won't support this image format sadly. Webp has been around for a lot longer but at this point it is getting old. I really have a love/hate relationship with webp. It has a great lossless and nearly lossless compression mode which makes it great for storing images, the problem is that noone supports it in non-HTML scenarios, [NOT EVEN GOOGLE THEMSELVES](https://groups.google.com/a/webmproject.org/g/webp-discuss/c/mmMVhoWqqUw). This really sucks as it is the closest we have to an adopted lossy transparent supporting image format. Webp brings together the good of jpeg and png but with no support it is hard to use. Finally there is png and jpeg, both widely supported as they have been around forever but both have pretty big weaknesses. With my theme having both a light and dark theme I need transparency on most images which jpeg doesn't support. The problem is when I move to png my file sizes balloon with it as png is a lossless format, and a not amazingly optimized one at that. It is consistently larger than newer formats' lossless.

So what am I, a lowly web dev, going to do about it? I am planning on using avif or webp images across the website and providing pngs (possibly lower resolution to counter size issues) as a fallback for transparent content and jpeg as a fallback for non-transparent content. While I wish I could go to avif only, and given this blogs audience I probably could without affecting many people's experience, but it is not something I want to chance.

### Resolution

I love the tabi theme but one of the things I struggled initially was sizing of my images. I originally sized them to have good resolution for desktop but then realized that mobile has almost 2x the resolution requirement for project card images. Since I was already having to re-encode to avif this wasn't a big deal but I do wish the tabi documentation had something stating the recommended resolution for each type of image (and maybe it does and I just missed it). For anyone curious 600px width is the go to for project images and 760px width for inline article images.

## Closing

Overall, optimizing this website has been a fun experience but it has shown me the pains of the modern web. I'm still old enough to remember parts of the old internet and the simplicity that came with it. I sometimes wish for that old internet back but I think a lot of that is nostalgia at this point. I really wish it wasn't a requirement to have an ad-blocker in this day and age but here we are where everything has to be monetized. I will never apply any trackers or advertisements to this website for that reason. I want to provide a modern take on the old web experience through having a nice to navigate static web site like I have now!
