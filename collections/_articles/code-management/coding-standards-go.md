---
title: "Code Standards: Go"
date: 2017-06-30 00:00:00 -0400
last_modified_at: 
categories:
  - Code Management
tags: 
  - backend
  - go

author: Sudheer Dhurjati
author_profile: true
sidebar:
  title: ""
  nav: content-nav
toc: true
---

## Introduction
This page provides general standards of Go coding.  While this is quick reference, it is not a complete coding standards guide.  Go Beginners are encouraged to go through the <a href="https://golang.org/doc/effective_go.html" target="_blank">Effective Go Language Documentation</a> for a better understanding of Go language constructs and writing Idiomatic Go.  If you are just staring on Go, please do spend some time reading <a href="https://golang.org/ref/spec" target="_blank">Go language specification</a>, the <a href="https://tour.golang.org/" target="_blank">Tour of Go</a>, and <a href="https://golang.org/doc/code.html" target="_blank">How to Write Go Code</a>.

## Coding Guidelines
Effective Go Page has good content on coding guidelines for different Go constructs. Provided below is a list of shortcuts.  These can be accessed from https://golang.org/doc/effective_go.html as well. 

- <a href="https://golang.org/doc/effective_go.html#formatting" target="_blank">Formatting</a>
- <a href="https://golang.org/doc/effective_go.html#names" target="_blank">Names</a>
- <a href="https://golang.org/doc/effective_go.html#semicolons" target="_blank">Semicolons</a>
- <a href="https://golang.org/doc/effective_go.html#control-structures" target="_blank">Control structures</a>
- <a href="https://golang.org/doc/effective_go.html#functions" target="_blank">Functions</a>
  - <a href="https://golang.org/doc/effective_go.html#data" target="_blank">Data</a>
- <a href="https://golang.org/doc/effective_go.html#initialization" target="_blank">Initialization</a>
- <a href="https://golang.org/doc/effective_go.html#methods" target="_blank">Methods</a>
  - <a href="https://golang.org/doc/effective_go.html#interfaces_and_types" target="_blank">Interfaces and other types</a>
- <a href="https://golang.org/doc/effective_go.html#blank" target="_blank">The blank identifier</a>
- <a href="https://golang.org/doc/effective_go.html#embedding" target="_blank">Embedding</a>
- <a href="https://golang.org/doc/effective_go.html#concurrency" target="_blank">Concurrency</a>
- <a href="https://golang.org/doc/effective_go.html#errors" target="_blank">Errors</a>

## gofmt  
Run <a href="https://golang.org/cmd/gofmt/" target="_blank">gofmt</a> on your code to automatically fix the majority of mechanical style issues. Almost all Go code in the wild uses `gofmt`. The rest of this document addresses non-mechanical style points.  

All Go code in the standard packages has been formatted with gofmt.  As an example, there's no need to spend time lining up the comments on the fields of a structure. Gofmt will do that for you. Given the following declaration (Example 1), it will output the aligned columns (Example 2). 

###### [ Example 1 ]
{% highlight go linenos %}
type T struct {
    name string               // name of the object
    value int                                  // its value
}
{% endhighlight %}

###### [ Example 2 ]
{% highlight go linenos %}
type T struct {
    name    string    // name of the object
    value   int       // its value
}
{% endhighlight %}
All Go code in the standard packages has been formatted with gofmt.  You are encouraged to use gofmt as a routine post coding activity.

## Developer Resources
Here are some resources you should check out if you are learning / new to Go:
- <a href="http://tour.golang.org" target="_blank">Go Language Tour</a>
- Get better at Go:
  - <a href="https://golang.org/doc/code.html" target="_blank">Learn how to organize your Go workspace</a>
  - <a href="https://golang.org/doc/effective_go.html" target="_blank">Be more effective at writing Go</a>
  - <a href="https://golang.org/ref/spec" target="_blank">Learn more about the language itself</a>
  - <a href="https://golang.org/doc/#articles" target="_blank">More reading material</a>
- There are some awesome websites as well:
  - <a href="https://blog.gopheracademy.com" target="_blank">Resources for Gophers in general</a>
  - <a href="http://gotime.fm" target="_blank">Weekly podcast of Go awesomeness</a>
  - <a href="https://gobyexample.com" target="_blank">Examples of how to do things in Go</a>
  - <a href="http://go-database-sql.org" target="_blank">How to use SQL databases in Go</a>
  - <a href="https://dmitri.shuralyov.com/idiomatic-go" target="_blank">Tips on how to write more idiomatic Go code</a>
  - <a href="https://divan.github.io/posts/avoid_gotchas" target="_blank">Help you avoid gotchas in Go</a>
  - <a href="https://rakyll.org/style-packages/" target="_blank">Style guideline for Go packages</a>

There's also an exhaustive <a href="http://gophervids.appspot.com" target="_blank">list of videos</a> related to Go from various authors.

If you prefer books, you can try these:
- <a href="http://www.golangbootcamp.com/book" target="_blank">http://www.golangbootcamp.com/book</a>
- <a href="http://gopl.io" target="_blank">http://gopl.io</a>
- <a href="https://www.manning.com/books/go-in-action" target="_blank">https://www.manning.com/books/go-in-action</a>  (NOTE: if you e-mail @wkennedy at bill@ardanlabs.com,  you can get a free copy for being part of this Slack)

If you want to learn how to organize your Go project, make sure to read: <a href="https://medium.com/@benbjohnson/standard-package-layout-7cdbc8391fc1#.ds38va3pp" target="_blank">https://medium.com/@benbjohnson/standard-package-layout-7cdbc8391fc1#.ds38va3pp</a>.  Once you are accustomed to the language and syntax, you can read this series of articles for a walkthrough the various standard library packages: <a href="https://medium.com/go-walkthrough" target="_blank">https://medium.com/go-walkthrough</a>.

Finally, <a href="https://github.com/golang/go/wiki#learning-more-about-go" target="_blank">https://github.com/golang/go/wiki#learning-more-about-go</a>  will give a list of even more resources to learn Go.

## References
1. <a href="https://golang.org/doc/effective_go.htm" target="_blank">Effective Go: 
2. <a href="" target="_blank">Go Language Specification: language specification</a>
3. <a href="" target="_blank">Tour of Go: Tour of Go</a>
4. <a href="" target="_blank">Writing Go Code: How to Write Go Code</a>
5. <a href="" target="_blank">gofmt (Autoformat Go Code): gofmt</a>
6. <a href="" target="_blank">go import (Fix Go Imports): go import</a>
7. <a href="https://dmitri.shuralyov.com/idiomatic-go" target="_blank">Idiomatic Go</a>
8. <a href="https://divan.github.io/posts/avoid_gotchas" target="_blank">The traps</a>
9. <a href="https://github.com/golang/go/wiki/CodeReviewComments" target="_blank">Go Code Review Comments: Wiki</a>
10. <a href="https://fresh-air.aerobatic.io/post/debug-golang" target="_blank">Debugging Go Language</a>
11. <a href="https://spo-teamsite.ge.com/portals/hub/_layouts/15/PointPublishing.aspx?app=video&p=p&chid=b3596c6f-0fb1-45d3-addc-e571a30dc3e9&vid=cd50440c-4a80-4de8-afbb-265f9b9e5e22" target="_blank">Go Getting Started Video</a>
12. <a href="https://peter.bourgon.org/go-best-practices-2016" target="_blank">Go best-practices</a>
13. <a href="http://devs.cloudimmunity.com/gotchas-and-common-mistakes-in-go-golang/index.html#opening_braces" target="_blank">50 Shades of GO</a>