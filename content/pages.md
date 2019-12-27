Pages
=====

The Pages API can be used to [create a new entry](https://feedbin.com/blog/2019/08/20/save-webpages-to-read-later/) from the URL of an article.

### `POST /v2/pages.json`

Create a new page.

```bash
curl --request POST \
--user "example@example.com:password" \
--header "Content-Type: application/json; charset=utf-8" \
--data-ascii '{"url": "https://feedbin.com/blog/2018/09/11/private-by-default/", "title": "Private by Default"}' \
https://api.feedbin.com/v2/pages.json
```

**Request Body**

```json
{
    "url": "https://feedbin.com/blog/2018/09/11/private-by-default/",
    "title": "Private by Default"
}
```

The title is optional and will only be used if Feedbin cannot find the title of the content.

**Response**

If successful, the response will be the full [entry](entries.md).

```json
{
    "author": null,
    "content": "<div>\n<p class=\"page-meta\"> <time> September 11, 2018 </time> <em>by</em> Ben Ubois </p>\n<main> <p>I want Feedbin to be the opposite of Big Social. I think people should have the right not to be tracked on the Internet and Feedbin can help facilitate that.</p> <p>Since Feedbin is 100% funded by paying customers, I can focus solely on making the best product possible without compromises. Therefore, Feedbin can be private by default.</p> <p>To me this means eliminating all potential points of leaking user data while using Feedbin.</p> <p>Since Feedbin displays web content, this isn\u2019t the easiest thing to do. Here are the leaks I\u2019ve identified and eliminated.</p> <h2 id=\"iframes\">iFrames</h2> <p>The biggest visual and functional change is how iFrames work.</p> <p>Feedbin previously whitelisted a number of iFrame sources like YouTube and Vimeo so you could see embedded content. iFrames embed full web-pages from a 3rd-party source. They\u2019re usually resource intensive to load and they enable cross-site tracking.</p> <p>Feedbin now replaces all iFrames with a custom new module. The new module still includes the poster frame from videos (where available) and will fetch the title and other metadata.</p> <p>Clicking on the module will swap in the original iFrame. For YouTube and Vimeo, clicking will also start playing the video.</p> <p>I prefer the look of this module to the original iFrame. It loads faster, has a clearer, consistent look with richer meta-data, and uses fewer resources doing it.</p> <p><a href=\"https://assets.feedbin.com/assets-site/blog/2018-09-11/embed-3f43088538ae5ed7e585c00013adc13a915fd35de31990b3081a085b963ed7dd.png\"><img class=\"wide\" src=\"https://assets.feedbin.com/assets-site/blog/2018-09-11/embed-3f43088538ae5ed7e585c00013adc13a915fd35de31990b3081a085b963ed7dd.png\"></a></p> <h2 id=\"third-party-javascript\">Third-party JavaScript</h2> <p><strong>Google Analytics</strong> is probably the number-one tracker. It\u2019s ubiquitous on the web. For a long time it was a no-brainer to install on any website because you get a lot of functionality for free.</p> <p>Feedbin used Google Analytics up until April, 2018. It was useful to see some of the stats it provided. The browser stats were good to get a sense of when it would be appropriate to drop support for older browsers. It was also useful to see referrer information to see where customers were coming from.</p> <p>There are good private alternatives to Google Analytics out there. <a href=\"https://matomo.org\">Matomo</a> is one that I came across. They have a great <a href=\"https://matomo.org/privacy-policy/\">privacy policy</a> for their hosted product and you can choose to run it yourself for even more control.</p> <p>I thought about replacing Google Analytics with Matomo, but I came to the same conclusion that it didn\u2019t provide anything I <em>need</em> in order to run Feedbin. Better to not collect that data at all.</p> <p><strong>Twitter &amp; Instagram</strong> embeds were another source of third-party JavaScript I identified. I would bet that the second largest contributor to tracking you across the web, comes from sites that embed social widgets. Feedbin previously used the Twitter and Instagram widgets to render embedded tweets and images that appeared in blog posts. This provided a richer experience by showing the full embed as intended by the author.</p> <p>However there is an alternative. Both Twitter and Instagram offer public <a href=\"https://oembed.com/\">oEmbed</a> endpoints. oEmbed can give you much of the data needed to properly render this content. Feedbin takes this a step further by making the oEmbed requests from the server. If your browser made the requests client-side, this would give the publishers the opportunity to read and set tracking cookies. The end result is that you see pretty much the same content as you did before.</p> <p><strong>JavaScript in blog posts</strong> is worth mentioning. RSS uses HTML for rendering content. All HTML is allowed including <code class=\"highlighter-rouge\">&lt;script&gt;</code> tags. Feedbin has always used an <a href=\"https://github.com/rgrove/sanitize\">HTML sanitizer</a> to strip dangerous content out of posts, including scripts, since that would be the definition of an <a href=\"https://www.owasp.org/index.php/Cross-site_Scripting_(XSS)\">XSS vulnerability</a>.</p> <h2 id=\"images\">Images</h2> <p>Images are another potential source of leaking data. Feedbin has used an <a href=\"https://github.com/atmos/camo\">image proxy</a> since launch to prevent <a href=\"https://developer.mozilla.org/en-US/docs/Security/MixedContent\">mixed content warnings</a>. A side benefit of the image proxy, is that your browser only makes requests to the proxy and the proxy gets the image data, preventing your request from reaching the origin.</p> <h2 id=\"fonts\">Fonts</h2> <p>Feedbin has the option to use fonts from <a href=\"http://www.typography.com/\">Hoefler &amp; Co.</a>. This requires a single request to their service, which means that they have the opportunity to track you if they wish. To eliminate this source, the default article font is now a system font. Custom fonts will only be loaded if they\u2019re chosen.</p> <h2 id=\"exceptions\">Exceptions</h2> <p><strong>Stripe</strong> is the only third-party exception I can think of. Stripe provides the invaluable functionality of billing and subscriptions. Using Stripe means Feedbin does not have to collect, store or ever see any sensitive payment data. However, since Stripe makes their money from paying customers, I think they are incentivized to be careful with this data. Their <a href=\"https://stripe.com/us/privacy\">privacy policy</a> has more details on how they store and use data.</p> <p>I think with these changes in place, the only external requests that should ever be made by your browser, with the exception of Stripe, are ones initiated by you.</p> </main>\n</div>",
    "created_at": "2019-12-27T18:16:19.986803Z",
    "extracted_content_url": "https://extract.feedbin.com/parser/feedbin/04a050a680b063a1f5033927fdd665eb472f5ee0?base64_url=aHR0cHM6Ly9mZWVkYmluLmNvbS9ibG9nLzIwMTgvMDkvMTEvcHJpdmF0ZS1ieS1kZWZhdWx0Lw==",
    "feed_id": 6,
    "id": 109,
    "published": "2018-09-11T00:00:00.000000Z",
    "summary": "September 11, 2018 by Ben Ubois I want Feedbin to be the opposite of Big Social. I think people should have the right not to be tracked on the Internet and Feedbin can help facilitate that. Since Feedbin is 100% funded by paying customers, I can focus",
    "title": "Private by Default",
    "url": "https://feedbin.com/blog/2018/09/11/private-by-default/"
}
```
