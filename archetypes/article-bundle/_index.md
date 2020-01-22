---
type: "article" #don't change this line
title: {{ replace (delimit (last 1 (split .Name "_")) "") "-" " " | title }}
description: "A short description about the article"
images: ["image1-for-social-sharing.jpg", "image1-for-social-sharing.jpg"]
draft: false
date: "2019-12-31"
layout: "single" #corresponds to the html template file in /layouts/issue-X
myCustomVariable: "One can add more custom metadata / content like so"
---

# This is a post heading

And this is some content for the post body. One can put images in the assets directory of the post folder, and reference it like so:

{{< figure src="assets/myImage.jpg" >}}
