---
layout: post
title: "vscode & telescope PR’s"
date: 2019-12-11
---
This week my external and internal PR’s were in github.com/microsoft/vscode and github.com/SenecaCDOT/telescope.

In vscode I got rid of a duplicate ‘clear search’ text that was causing a bug inside of the settings-editor. While I doing this PR something in the build broke unexpectedly and while I was trying to fix the compilation errors, somebody else actually submitted a PR to my issue. I thought that this was kind of annoying as I was trying to fix my build so that I could have submitted it. Luckily Microsoft went with my bug fix as opposed to the other persons fix. I guess they have alot of experience with these situations and chose to do the right thing and take my work, which I was very pleased about. This gave me some hope in humanity, and also built up my confidence as a student getting involved in Open Source.

![duplicate code](https://awesomeresponsibility.files.wordpress.com/2019/12/image.png?w=1024)

In telescope I added tests for my previously written function that would extract URLs from a blog feed.
The tests I wrote for extractUrls() include: checking if the returned object remains an array, checking if the array contains URL’s, checking the length of the array matches the ammount of URL’s inside, checking that the array remains empty after passing no URL’s.

{% highlight js %}
const getUrls = require('../src/backend/utils/extract-urls');

test('The Array contains the URL from the blog feed data', () => {
  const htmlData =
    'Feel free to view all the changes <a href="https://github.com/FreezingMoon/AncientBeast/pull/1555">here</a>!</div>';
  const urlArray = getUrls.extract(htmlData);
  expect(urlArray[0]).toBe('https://github.com/FreezingMoon/AncientBeast/pull/1555');
});

test('The result returned from extract() is an Array', () => {
  const htmlData =
    'Feel free to view all the changes <a href="https://github.com/FreezingMoon/AncientBeast/pull/1555">here</a>!</div>';
  const urlArray = getUrls.extract(htmlData);
  const res = Array.isArray(urlArray);
  expect(res).toBe(true);
});

test('The length of the array matches the number of URLs in the string', () => {
  const htmlData =
    'Feel free to view all the changes <a href="https://github.com/FreezingMoon/AncientBeast/pull/1555">here</a>!</div>';
  const urlArray = getUrls.extract(htmlData);
  expect(urlArray.length).toBe(1);
  expect(urlArray[0]).toBe('https://github.com/FreezingMoon/AncientBeast/pull/1555');
});

test('The url array remains empty after given no URL from the blog feed data', () => {
  const htmlData =
    'Feel free to view all the changes <a href="Lorem ipsum dolor sit amet consectetur adipiscing elit">here</a>!</div>';
  const urlArray = getUrls.extract(htmlData);
  expect(urlArray[0]).toBe(undefined);
  expect(urlArray.length).toBe(0);
});

test('The result is still an array after given no URLs from the blog feed data', () => {
  const htmlData =
    'Feel free to view all the changes <a href="Lorem ipsum dolor sit amet consectetur adipiscing elit">here</a>!</div>';
  const urlArray = getUrls.extract(htmlData);
  const res = Array.isArray(urlArray);
  expect(res).toBe(true);
});

test('The length of the array is 0 given no URL in the html data', () => {
  const htmlData =
    'Feel free to view all the changes  <a href="Lorem ipsum dolor sit amet consectetur adipiscing elit">here</a>!</div>';
  const urlArray = getUrls.extract(htmlData);
  expect(urlArray.length).toBe(0);
});
{% endhighlight %}

In telescope I also got rid of some of the annoying console.log spams that would present themseleves whenever you tried to test the program. That had to go asap as it was difficult to see the tests. Currently there still is a console.log but it shows server info in the npm test , I am wondering if we could get rid of that aswell as it seems redundant to the tests…

![deleted console logs in feed worker](https://awesomeresponsibility.files.wordpress.com/2019/12/image-2.png)

External
Vscode Pull Request

- [https://github.com/microsoft/vscode/pull/86494](https://github.com/microsoft/vscode/pull/86494)

Internal
Telescope Pull Requests

- [https://github.com/Seneca-CDOT/telescope/pull/331](https://github.com/Seneca-CDOT/telescope/pull/331)
- [https://github.com/Seneca-CDOT/telescope/pull/337](https://github.com/Seneca-CDOT/telescope/pull/337)
- [https://github.com/Seneca-CDOT/telescope/pull/336](https://github.com/Seneca-CDOT/telescope/pull/336)
