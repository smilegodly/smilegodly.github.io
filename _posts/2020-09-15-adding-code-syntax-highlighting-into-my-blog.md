---
layout: post
title: "Adding Code Syntax Highlighting Into My Blog"
date: 2020-09-15
---

I wanted to make my blogging platform more responsive to the following things... Code, Gifs, Images, and Youtube videos. I decided to get started with implementing code syntax highlighting and code block responsiveness in my blog. Originally I mostly intended to use this platform for blogging about coding open source projects and to journal my experiences involved with open source in general. It was because of that fact that I figured this should be the first part of code written for my blog and I should start there.

I have been using a Ruby program called Jekyll which I have been using to build my blog and Jekyll has a built in syntax highlighter called Rouge. The highlighted code in green is the code I had to add to the Jekyll config file to explicitly setup the syntax highlighter in Jekyll. 

![Jekyll config file](https://cdn.discordapp.com/attachments/409198534949077024/755569914332446750/unknown.png "Syntax Highlighting Jekyll Configuration")

The syntax highlighting style that I used for the highlighter is called monokai. It looks very similiar to the style of sublime evidently... there could be a correlation. I'm definately going to be updating this css in the future, but as of today, this is the css stylesheet that I'm currently using in my blog for the code syntax highlighting.

{% highlight css %}
.highlight table td { padding: 5px; }
.highlight table pre { margin: 0; }
.highlight .c, .highlight .ch, .highlight .cd, .highlight .cpf {
  color: #75715e;
  font-style: italic;
}
.highlight .cm {
  color: #75715e;
  font-style: italic;
}
.highlight .c1 {
  color: #75715e;
  font-style: italic;
}
.highlight .cp {
  color: #75715e;
  font-weight: bold;
}
.highlight .cs {
  color: #75715e;
  font-weight: bold;
  font-style: italic;
}
.highlight .err {
  color: #960050;
  background-color: #1e0010;
}
.highlight .gi {
  color: #ffffff;
  background-color: #324932;
}
.highlight .gd {
  color: #ffffff;
  background-color: #493131;
}
.highlight .ge {
  color: #000000;
  font-style: italic;
}
.highlight .gr {
  color: #aa0000;
}
.highlight .gt {
  color: #aa0000;
}
.highlight .gh {
  color: #999999;
}
.highlight .go {
  color: #888888;
}
.highlight .gp {
  color: #555555;
}
.highlight .gs {
  font-weight: bold;
}
.highlight .gu {
  color: #aaaaaa;
}
.highlight .k, .highlight .kv {
  color: #66d9ef;
  font-weight: bold;
}
.highlight .kc {
  color: #66d9ef;
  font-weight: bold;
}
.highlight .kd {
  color: #66d9ef;
  font-weight: bold;
}
.highlight .kp {
  color: #66d9ef;
  font-weight: bold;
}
.highlight .kr {
  color: #66d9ef;
  font-weight: bold;
}
.highlight .kt {
  color: #66d9ef;
  font-weight: bold;
}
.highlight .kn {
  color: #f92672;
  font-weight: bold;
}
.highlight .ow {
  color: #f92672;
  font-weight: bold;
}
.highlight .o {
  color: #f92672;
  font-weight: bold;
}
.highlight .mf {
  color: #ae81ff;
}
.highlight .mh {
  color: #ae81ff;
}
.highlight .il {
  color: #ae81ff;
}
.highlight .mi {
  color: #ae81ff;
}
.highlight .mo {
  color: #ae81ff;
}
.highlight .m, .highlight .mb, .highlight .mx {
  color: #ae81ff;
}
.highlight .se {
  color: #ae81ff;
}
.highlight .sb {
  color: #e6db74;
}
.highlight .sc {
  color: #e6db74;
}
.highlight .sd {
  color: #e6db74;
}
.highlight .s2 {
  color: #e6db74;
}
.highlight .sh {
  color: #e6db74;
}
.highlight .si {
  color: #e6db74;
}
.highlight .sx {
  color: #e6db74;
}
.highlight .sr {
  color: #e6db74;
}
.highlight .s1 {
  color: #e6db74;
}
.highlight .ss {
  color: #e6db74;
}
.highlight .s, .highlight .sa, .highlight .dl {
  color: #e6db74;
}
.highlight .na {
  color: #a6e22e;
}
.highlight .nc {
  color: #a6e22e;
  font-weight: bold;
}
.highlight .nd {
  color: #a6e22e;
  font-weight: bold;
}
.highlight .ne {
  color: #a6e22e;
  font-weight: bold;
}
.highlight .nf, .highlight .fm {
  color: #a6e22e;
  font-weight: bold;
}
.highlight .no {
  color: #66d9ef;
}
.highlight .bp {
  color: #f8f8f2;
}
.highlight .nb {
  color: #f8f8f2;
}
.highlight .ni {
  color: #f8f8f2;
}
.highlight .nn {
  color: #f8f8f2;
}
.highlight .vc {
  color: #f8f8f2;
}
.highlight .vg {
  color: #f8f8f2;
}
.highlight .vi {
  color: #f8f8f2;
}
.highlight .nv, .highlight .vm {
  color: #f8f8f2;
}
.highlight .w {
  color: #f8f8f2;
}
.highlight .nl {
  color: #f8f8f2;
  font-weight: bold;
}
.highlight .nt {
  color: #f92672;
}
.highlight {
  color: #f8f8f2;
  background-color: #49483e;
  padding: 1px 10px 1px 10px;
  width: max-content;
  margin: auto;
}
{% endhighlight %}

