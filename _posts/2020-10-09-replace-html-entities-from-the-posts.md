---
layout: post
title: "Fixing Telescopes Code Blocks"
date: 2020-10-09
---

<!-- Discussion on the issue & thinking it through -->
For my first PR of Hacktoberfest 2020 I wanted to give myself a challenge I hadn't done before in the Telescope repository. I was reading some of the Telescope posts and noticed raw entities within the code blocks. This frustrated me seeing as I was trying to read & copy paste code content within one of the posts, and the raw HTML entities `&lt;` `&gt;` `&amp;` were in the code blocks still, rendering the code unreadable and uncopy & paste-able ! I noticed there was an [issue](https://github.com/Seneca-CDOT/telescope/issues/1091) that addressed this. To be honest, I was a little bit intimidated to start this as I've never done anything like it before, and I knew it would probably take me **atleast** a few days to complete. I let this issue sit in my head and after thinking it through and looking at existing code in the already existing project, I found some code in another function that did something similiar to what I needed, and, I realized that I could use this existing code I had found in Telescope to build my own code from it and fix the issue at hand.

<!-- Starting my journey --> 
I needed code that would decode an encoded html entity into its decoded character entity. I wanted to apply this idea to the code content on telescope by decoding the entire code block at project runtime, and then, replace the old encoded version of the code block with the newly decoded one. I found an entity decoder in the `entities` package that was already installed in the Telescope project, I threw some strings that contained the encoded html entities into `entities.decoder()`, and... it worked! I had decoded character entities as a result. SUCCESS! This was a great starting place to begin my journey. 

<!-- Discuss the code fix & the tests around the fix -->
<!-- Discuss the need for double decoding -->
<!-- Include image example of the fix & also the code that fixed it -->
I knew that the code would be something that would query all the `<code>` elements on the page, decode it, and replace it on the page **before** any of the posts were loaded. I'd definately also need tests to see if the function I was writing was actually working the way I expected it to. After a few days of trial and error and suffering, I finally came up with some code that actually fixed the problem! Here is the code that does the magical fix.

The code below accepts the dom tree of Telescope, checks if the dom tree is okay, queries up all of the `<code>` elements, decodes any html entities within the dom, and then replaces the old code block with the fixed up code. 

```js
const entities = require('entities');

function decode(codeElement) {
  // decode twice for double encoded html entities
  const result = entities.decodeHTML(codeElement.innerHTML);
  return entities.decodeHTML(result);
}

module.exports = function (dom) {
  if (!(dom && dom.window && dom.window.document)) {
    return null;
  }

  let fixedCodeElement = {};

  dom.window.document.querySelectorAll('code').forEach((code) => {
    fixedCodeElement = decode(code);
    code.innerHTML = fixedCodeElement;
  });
  return `<code>${fixedCodeElement}</code>`; // return decoded string to the tests
};
```

I added some tests to make sure that the result I was getting back was what I expected. The test below makes sure that double encoded arrow functions within the code are being decoded properly. I always check for double encoded entities because some of the entities were double encoded and if you decode it twice, you get the correct result out of that entity. Some weren't double encoded but it didn't matter because when I double decoded a singly encoded entitity, nothing bad happened and I got the correct result anyway. I'm not sure how some of the entities got double encoded and some didn't though, it might have been from all the different types of blogging platforms that people are using (medium, wordpress, etc...) but this is just some speculation & some food for thought. 

```js
test('Encoded string with arrow function should be decoded', () => {
  const htmlData = `<code>
    <span class="hljs-string">', ...].map((number) =&gt;;
      twilio.messages.create({
        body: '...'
    </span>
  </code>`;
  const decoded = `<code>
    <span class="hljs-string">', ...].map((number) =>;
      twilio.messages.create({
        body: '...'
    </span>
  </code>`;
  const data = decodeHTML(htmlData);
  expect(data).toBe(decoded);
});
```

<!-- Before and after picture of the fix -->
After a few days of testing and trial & error and also excessive coffee consumption, I was *finally* succesful in my journey to fixing the code blocks on Telescope! I pushed the fix and made a [Pull Request](https://github.com/Seneca-CDOT/telescope/pull/1157) to get the changes reviewed and *hopefully* pushed to upstream so that I finally could read the code on Telescope and copy & paste it as it was meant to be :) 

Here is a before and after photo of the fix in action! Notice the encoded HTML entities within the code `&lt;` , `&gt;`, `&amp;`.

![](https://user-images.githubusercontent.com/35276477/95153209-e973d400-075c-11eb-804a-8d7d9d666282.PNG "Before")

After the fix.

![](https://user-images.githubusercontent.com/35276477/95153231-fb557700-075c-11eb-9db0-c5a82dfbb6cc.PNG "After")
