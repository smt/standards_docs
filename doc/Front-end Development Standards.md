# Empathy Lab Front-end Development Standards

This document contains normative guidelines for web applications built by the UI Development practice of Empathy Lab. It is to be readily available to anyone who wishes to check the iterative progress of our best practices.

This document outlines our de-facto code standards. The primary motivation is two-fold: `1)` code consistency and `2)` best practices. By maintaining consistency in coding styles and conventions, we can ease the burden of legacy code maintenance, and mitigate risk of breakage in the future. By adhering to best practices, we ensure optimized page loading, performance and maintainable code.

## Pillars of Front-end Development

1. Separation of presentation, content, and behavior.
2. [Markup should be well-formed, semantically correct](http://www.bbc.co.uk/guidelines/futuremedia/technical/semantic_markup.shtml) and [generally valid](#validation).
3. [Javascript should progressively enhance the experience](http://icant.co.uk/articles/pragmatic-progressive-enhancement/)

## General Practices

### Indentation

For all code languages, we require indentation to be done via soft tabs (using the space character). Hitting *Tab* in your text editor shall be equivalent to **four spaces**.

### Readability vs Compression

We prefer readability over file-size savings when it comes to maintaining existing files. Plenty of whitespace is encouraged, along with ASCII art, where appropriate. There is no need for any developer to purposefully compress HTML or CSS, nor obfuscate JavaScript.

We will use server-side processes in place that automatically compress and gzip all static client-side files, such as CSS and JavaScript.

## Markup

### HTML5

HTML5 is a new version of HTML and XHTML. The [HTML5 draft](http://whatwg.org/specs/web-apps/current-work/) specification defines a single language that can be written in HTML and XML. It attempts to solve issues found in previous iterations of HTML and addresses the needs of Web Applications, an area previously not adequately covered by HTML. ([source](http://html5.org/))

Developers are encouraged to use parts of HTML5 when appropriate, while ensuring older browsers are handled fairly.

<p id="validation">We will test our markup against the <a href="http://validator.w3.org/">W3C validator</a>, to ensure that the markup is well formed. 100% valid code is not a goal, but validation certainly helps to write more maintainable sites as well as debugging code. <b>Empathy Lab does not guarantee code is 100% valid, but instead assures the cross-browser experience is fairly consistent.</b></p>

#### Template

The [HTML5 Boilerplate](http://html5boilerplate.com/) is an amazing resource with example code for starting a new HTML5 site. Read the comments and the code - it contains many standards and best practices.

#### Self-closing Comments

Though we are using [HTML5](http://dev.w3.org/html5/spec/Overview.html), which allows for either HTML or XHTML style syntax, we prefer the strictness of XHTML. Therefore, all tags must be properly closed. For tags that can wrap nodes such as text or other elements, termination is a trivial enough task. For tags that are self-closing, the forward slash should have exactly one space preceding it `<br />` vs. the compact but incorrect `<br/>`. The W3C specifies that a single space should precede the self-closing slash ([source](http://w3.org/TR/xhtml1/#C_2)).

#### Quotes

In keeping with the strictness of XHTML code conventions, according to the W3C, all attributes must have a value, and must use double-quotes ([source](http://w3.org/TR/xhtml1/#h-4.4)). The following are examples of proper and improper usage of quotes and attribute/value pairs.

##### Correct

    <input type="text" name="email" disabled="disabled" />

##### Incorrect

    <input type=text name=email disabled>

#### Doctype

A nice aspect of HTML5 is that it streamlines the amount of code that is required. Meaningless attributes have been dropped, and the `DOCTYPE` declaration has been simplified significantly. Additionally, there is no need to use `CDATA` to escape inline JavaScript, formerly a requirement to meet XML strictness in XHTML.

##### XHTML 1.0 Transitional Doctype

    <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
    "http://w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">

##### HTML 4.0 Strict DOCTYPE

    <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">

##### HTML 5 DOCTYPE:

    <!DOCTYPE html>

* All markup should be delivered as UTF-8, as its the most friendly for internationalization. It should be designated in both the HTTP header and the head of the document.

Setting the character set using tags.

    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />

In HTML5, just do:

* Make use of `DL` (definition lists) and `BLOCKQUOTE`, when appropriate.
* Items in list form should always be housed in a `UL`, `OL`, or `DL`, never a set of `DIV`s or `P`s.
* Use `label` fields to label each form field, the `for` attribute should associate itself with the input field, so users can click the labels. `cursor:pointer;` on the label is wise, as well. <sup>[note 1](http://www.accessifyforum.com/viewtopic.php?t=1926#14178) [note 2](http://www.accessifyforum.com/viewtopic.php?t=6738)</sup>
* Do not use the `size` attribute on your input fields. The `size` attribute is relative to the font-size of the text inside the input. Instead use CSS width.
* Place an HTML comment on some closing `DIV`s to indicate what element you&rsquo;re closing. It will help when there is lots of nesting and indentation.
* Tables shouldn&rsquo;t be used for page layout (duh), but can save you time, like in the case of form layout.
* Use [microformats](http://en.wikipedia.org/wiki/Microformat) where appropriate, specifically `hCard` and `adr`.
* Make use of `THEAD`, `TBODY`, and `TH` tags (and the `scope` attribute) when appropriate.

###### Table markup with proper syntax (THEAD,TBODY,TH [scope])

    <table summary="This is a chart of year-end returns for 2005.">
        <thead>
            <tr>
                <th scope="col">Table header 1</th>
                <th scope="col">Table header 2</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>Table data 1</td>
                <td>Table data 2</td>
            </tr>
        </tbody>
    </table>

* Always use title-case for headers and titles. Do not use all caps or all lowercase titles in markup, instead apply the CSS property text-transform:uppercase/lowercase.

## CSS

See the *3D CSS Box Model* diagram by [Jon Hicks](http://hicksdesign.co.uk/boxmodel/).

### Inline Styles

We strive to maintain proper separation of content and design, and therefore highly discourage the use of inline `style="..."` attributes. This not only makes maintenance a nightmare, but inextricably ties the presentation to the data it represents.

**Note:** An exception to this rule is `style="display:none"` for revealing hidden elements via JavaScript.

### CSS Validation

It&rsquo;s likely not a wise use of time to validate your CSS with the [W3C validator](http://jigsaw.w3.org/css-validator/), though it may identify a few problems.

### CSS Formatting

Some developers prefer CSS properties on their own line. Others prefer putting them next to each other and doing one rule per line. Both are good approaches; the important thing is consistency. At the outset of development, the project team should decide which they want to do.

### Pixels vs. Ems

We use the `px` unit of measurement to define `font-size`, because it offers absolute control over text. We realize that using the `em` unit for font sizing used to be popular, to accommodate for Internet Explorer 6 not resizing pixel based text. However, all major browsers (including <abbr title="Internet Explorer 7">IE7</abbr> and <abbr title="Internet Explorer 8">IE7</abbr>) now support text resizing of pixel units and/or full-page zooming. Since <abbr title="Internet Explorer 6">IE6</abbr> is largely considered deprecated, pixels sizing is preferred. Additionally, unit-less `line-height` is preferred because it does not inherit a percentage value of its parent element, but instead is based on a multiplier of the `font-size`.

#### Correct

    #selector {
        font-size: 13px;
        line-height: 1.5;
    }

#### Incorrect

    #selector {
        font-size: 0.813em;
        line-height: 1.25em;
    }

### Internet Explorer Bugs

Inevitably, when all other browsers appear to be working correctly, any and all versions of Internet Explorer will introduce a few nonsensical bugs, delaying time to deployment. While we encourage troubleshooting and building code that will work in all browsers without special modifications, sometimes it is necessary to use conditional `if IE` comments for [CSS hooks we can use in our stylesheets](http://paulirish.com/2008/conditional-stylesheets-vs-css-hacks-answer-neither/).

Stoyan Stefanov writes about how these conditional comments can [block downloads](http://www.phpied.com/conditional-comments-block-downloads/) in some browsers while interpreting these comments. He prescribes a successful method which involves the injection of an empty conditional comment before any substantive conditional comments. However, by applying conditional comments to the `html` tag as demonstrated below, this issue is remedied.

#### Fixing IE

    .box { float: left; margin-left: 20px; }
    .ie6 .box { margin-left: 10px; }

    <!--[if lt IE 7 ]> <html class="ie6"> <![endif]-->
    <!--[if IE 7 ]>    <html class="ie7"> <![endif]-->
    <!--[if IE 8 ]>    <html class="ie8"> <![endif]-->
    <!--[if IE 9 ]>    <html class="ie9"> <![endif]-->
    <!--[if (gt IE 9)|!(IE)]><!--> <html class=""> <!--<![endif]-->
    <head>
        <title>base page</title>
        <link type="text/css" rel="stylesheet" href="styles.css">
    </head>

### Shorthand

In general, CSS shorthand is preferred because of its terseness, and the ability to later go back and add in values that are already present, such as the case with margin and padding. Developers should be aware of the <abbr title="Top Right Bottom Left">TRBL</abbr> acronym, denoting the order in which the sides of an element are defined, in a clock-wise manner: Top, Right, Bottom, Left. If *bottom* is undefined, it inherits its value from top. Likewise, if *left* is undefined, it inherits its value from right. If only the top value is defined, all sides inherit from that one declaration.

For more on reducing stylesheet code redundancy, and using CSS shorthand in general:

* [http://qrayg.com/journal/news/css-background-shorthand](http://qrayg.com/journal/news/css-background-shorthand)
* [http://sonspring.com/journal/css-redundancy](http://sonspring.com/journal/css-redundancy)
* [http://dustindiaz.com/css-shorthand](http://dustindiaz.com/css-shorthand)

#### General coding principles

* Add CSS through external files, minimizing the # of files, if possible. It should always be in the `HEAD` of the document.
* Use the `LINK` tag to include, [never the `@import`](http://blog.amodernfable.com/2008/01/21/thoughts-on-linking-to-stylesheets/).

##### Including a stylesheet

    <link rel="stylesheet" type="text/css" href="myStylesheet.css" />

##### Don&rsquo;t use inline styling

    <p style="font-size: 12px; color: #FFFFFF">This is poor form, I say</p>

* Don&rsquo;t include styles inline in the document, either in a style tag or on the elements. It&rsquo;s harder to track down style rules.
* Use a reset CSS file (like [Eric Meyer&rsquo;s reset](http://meyerweb.com/eric/tools/css/reset/)) to zero our cross-browser weirdness.
* Use a font-normalization file like [YUI fonts.css](http://developer.yahoo.com/yui/fonts/)
* Elements that occur only once inside a document should use IDs, otherwise, use classes.
* Understand [cascading and selector specificity](http://www.stuffandnonsense.co.uk/archives/css_specificity_wars.html) so you can write very terse and effective code.
* Write selectors that are optimized for speed. This means, where possible, avoiding expensive CSS selectors. Avoid the * wildcard selector. Don&rsquo;t qualify ID selectors (e.g. `div#myid`) or class selectors (e.g. `table.results`) unless its necessary for readability or for efficiency. More on [writing efficient CSS on the MDC](https://developer.mozilla.org/en/Writing_Efficient_CSS).

##### Reasonable use of qualifying class selectors

    .error {color:#ff0000;}

    input[type=text].error, textarea.error {background-color:#ffe6e6;}

    select.error {border:1px solid #ff0000;}

##### Multiple classes and IE6.

    p.disclosure.warning { text-align: center; color: red; }

IE6 will ignore the earlier class rule and treat that rule like:

    p.warning { text-align: center; color: red; }

#### Images

* For repeating images, use [something larger than 1x1 pixels](http://www.iandevlin.com/blog/2010/03/webdev/fading-issue-with-repeating-background-transparent-image-in-internet-explorer)
* You should never be using spacer images.
* Use [CSS sprites](#_leverage_css_sprites) generously. They make hover states easy, improve page load time, and reduce carbon dioxide emissions.
* Typically, all images should be sliced with a transparent background (PNG8). All should be cropped tightly to the image boundaries.
    * However, the logo should always have a background matte and have padding before the crop. (so other people can hotlink to the file)

## JavaScript

We primarily develop new applications in jQuery, though we have expertise in plain JavaScript as well as all major modern JavaScript libraries.

### General coding principles
* 99% of code should be housed in external JavaScript files. They should be included at the end of the `BODY` tag for maximum page performance.
* Don&rsquo;t rely on the user-agent string if you don&rsquo;t have to. Do proper feature detection. (More at [Dive Into HTML5: Detection](http://diveintohtml5.org/detect.html) & [jQuery.support](http://api.jquery.com/jQuery.support/) docs)
* Don&rsquo;t use document.write().

#### All Boolean variables should start with &ldquo;is&rdquo;. Test for positive conditions

    isValid = (test.value >= 4 && test.success);

* Name variables and functions logically: For example, `popUpWindowForAd` rather than `myWindow`.
* Documentation should follow [NaturalDocs](http://www.naturaldocs.org/documenting.html) structure.
* Large blocks of code should be separated by flowerbox comments to indicate chapters of the file.
* Constants or configuration variables (like animation durations, etc.) should be at the top of the file.
* Strive to create functions which can be generalized, take parameters, and return values. This allows for substantial code reuse and, when combined with includes or external scripts, can reduce the overhead when scripts need to change.
    * For example, instead of hard coding a pop-window with window size, options, and url, consider creating a function which takes size, url, and options as variables.
* Comment your code! It helps reduce time spent troubleshooting JavaScript functions.
* Don&rsquo;t waste your time with `<!-- -->` comments surrounding your inline JavaScript, unless you care about Netscape 4. :)
* Surround your inline JavaScript with `<![CDATA[ ]]>` if you&rsquo;re [working in XHTML](http://www.wdvl.com/Authoring/Languages/XML/XHTML/dif.html).
* It&rsquo;s preferred to have code organized in an Object Literal/Singleton, the Module Pattern, or Objects with constructors, where possible.
* Minimize global variables.

#### When specifying any global variable, clearly identify it

    window.globalVar = { ... }

### White-space

In general, the use of whitespace should follow longstanding English reading conventions. Such that, there will be one space after each comma and colon (and semi-colon where applicable), but no spaces immediately inside the right and left sides of parenthesis. In short, we advocate readability within reason. Additionally, braces should always appear on the same line as their preceding argument.

Consider the following examples of a JavaScript for-loop…

#### Correct

    for (var i = 0, j = arr.length; i < j; i++) {

    }

#### Incorrect

    for ( var i = 0, j = arr.length; i < j; i++ )
    {

    }

#### Also incorrect

    for(var i=0,j=arr.length;i<j;i++){

    }

### Variables, ID & Class

All JavaScript variables shall be written in either completely lowercase letter or camelCase. All `id` and `class` declarations in CSS shall be written in only lowercase. Neither dashes nor underscores shall be used.

### Event Delegation

When assigning unobtrusive event listeners, it is typically acceptable to assign the event listener directly to the element(s) which will trigger some resulting action. However, occasionally there may be multiple elements which match the criteria for which you are checking, and attaching event listeners to each one might negatively impact performance. In such cases you should use event delegation instead.

jQuery&rsquo;s [`delegate()`](http://api.jquery.com/delegate) is preferred over [`live()`](http://api.jquery.com/live) for performance reasons.

### Debugging

Even with the best of validators, inevitably browser quirks will cause issues. There are several invaluable tools which will help to refine code integrity and loading speed. It is important that you have all of these tools available to you, despite the browser you primarily use for development. We recommend developing for Firefox and Safari first, then Google Chrome and Opera, with additional tweaks via conditional comments just for Internet Explorer. The following is a list of helpful debuggers and speed analyzers&hellip;

* Firefox: [Firebug](http://getfirebug.com/), [Page Speed](http://code.google.com/speed/page-speed/), [YSlow](http://developer.yahoo.com/yslow/)
* Safari: [Web Inspector](http://developer.apple.com/safari/library/documentation/AppleApplications/Conceptual/Safari_Developer_Guide/UsingtheWebInspector/UsingtheWebInspector.html)
* Google Chrome: [Developer Tools](http://google.com/chrome/intl/en/webmasters-faq.html#tools)
* Opera: [Dragonfly](http://opera.com/dragonfly/)
* Internet Explorer 6-7: [Developer Toolbar](http://microsoft.com/downloads/details.aspx?familyid=E59C3964-672D-4511-BB3E-2D5E1DB91038)

## Accessibility

* [Section 508 Standards for intranet and internet information and applications](http://www.section508.gov/index.cfm?FuseAction=Content&amp;ID=12#Web). Interfaces developed by Empathy Lab should meet Section 508 standards.
* [W3C checklist of checkpoints for accessibility](http://www.w3.org/TR/WCAG10/full-checklist.html). Interfaces developed by Empathy Lab should meet Priority 1 guidelines.
* [The WCAG 1.0 Guidelines](http://www.w3.org/TR/1999/WAI-WEBCONTENT-19990505/#Guidelines).

## Performance

### Optimize Delivery of CSS and JavaScript

There are many optimizations that should be done for serving CSS and JavaScript in Production:

* Follow the [Yahoo Performance Guidelines](http://developer.yahoo.com/performance/)
* Smush images using [smush.it](http://developer.yahoo.com/yslow/smushit/). Also using [YSlow](http://developer.yahoo.com/yslow/) can autosmush all your images for you.
* Set caching headers appropriately.
* Consider a cookie-less subdomain for static assets
* Avoid inline `<script>` blocks.
* CSS should be located in the `<head>` of the document, Javascript should be right before the `</body>` tag.
* Both CSS and JavaScript should be served minified. Most people use the [YUI Compressor](http://developer.yahoo.com/yui/compressor/) for this.
* Both CSS and JavaScript should be served using gzip on the wire
* CSS should be concatenated together. Obviously this can only be done for files that share the same media type (e.g. screen or print). The general goal here is to reduce the number of HTTP connections to dependencies during the loading of the page.
* JavaScript should be concatenated. While a ajax script dependency manager would be ideal (similar to the YUI 3 Loader), it&rsquo;s rather complicated to implement. In its place I&rsquo;d recommend a singular download of most of the script used on the site. (Of course, proper caching should be used to retain the file as long as is reasonable)
* Concatenation and minification typically occur during an automated build process, when packaging the code for deployment on stage or production. Many use tools like [Ant](http://ant.apache.org/) or [Maven](http://maven.apache.org/) for this
* Avoid inline `<script>` blocks within the HTML. They block rendering and are quite devastating to page load time.

### Optimize JavaScript execution

During a page load, there is typically a lot of script waiting to execute, but you can prioritize it. This order prioritizes based on user response:

1. Script that changes the visible nature of the page needs to fire absolutely first. This includes any font adjustment, box layout, or IE6 pngfixes.
2. Page content initialization
3. Page header, primary nav, and footer initialization
4. Attaching event handlers
5. Omniture, Doubleclick, and other 3rd party scripts

### Leverage CSS Sprites

CSS Sprites basically take a number of image assets and merge them together into a singular image file. Each part of it is revealed using CSS background-position. Some typical CSS would look like:

    a.expandbox { display:block; width: 75px; height: 15px; text-indent: -999px; overflow:hidden;
                  background: url(../img/sprite.png) no-repeat -50px -5px; }

It&rsquo;s quite common to leverage sprites for :hover states. In that case you&rsquo;ll see something like:

    a.expandbox:hover { background-position: -50px -20px; }

Using sprites reduces total page weight and reduces HTTP connections which speeds up page load. [More on the general technique and overview at CSS-tricks.com](http://css-tricks.com/css-sprites/).

Many developers use a vertically-oriented sprite in addition to the primary sprite. This vertical sprite will be <=100px wide (and tall) and contain icons that are typically placed next to text, such as list item bullets. Yahoo [uses a few such as this one](http://l.yimg.com/a/i/ww/sp/pa-icons3.gif). The one consideration is to not make sprites too large, something over 1000px in either direction will end up using a sizeable amount of memory. [More detail about sprites and memory usage](http://blog.vlad1.com/2009/06/22/to-sprite-or-not-to-sprite/).

### Image formats

There are four main image formats that should be used, detailed here:

* **JPEG.** This will cover all photography-based images, such as homepage and category page promo images, or anything with a very high color count.
* **PNG24.** This format, easily accessible in Photoshop, outputs high-color count imagery and fully supports graded opacity by pixel. Relatively, it&rsquo;s quite a heavy format as far as kilobyte weight. It is the only format that IE6 needs to execute a pngfix on. In that case, Empathy Lab recommends the DD_belatedPNG script (A pngfix fixes the issue where PNG24&rsquo;s appear to have a grey or light-blue background in IE6. They are not always compatible with background-position.)
In many cases, you can use a GIF fallback for IE6, in place of a PNG24. This is especially true if any sprites need to be done in PNG24. All pngfixes are very slow and expensive, so it&rsquo;s best to avoid using them.
* **PNG8.** A surprising diversity of color can be captured inside 256 colors, so it&rsquo;s worth trying PNG before heading JPG. PNG also is a lot more compressible than GIF (using tools like pngcrush and pngquant). This format allows graded opacity in nearly all browsers, but in IE6, those semi-opaque pixels are just shown 100% transparent. In many cases this is sufficient. It also does not require a pngfix script to be run, so it&rsquo;s optimized for speed.
Photoshop cannot output these semi-opaque files correctly but [Fireworks can](http://www.sitepoint.com/blogs/2007/09/18/png8-the-clear-winner/).
* **Transparent GIF 89a.** GIF 89a offers the flexibility of transparency and wide browser support, but the constraints of no graded opacity nor a color depth above 256. In our experience, color depths of 64 still provide very good quality thumbnails, and keep the file size comparably very small.
All low-color count imagery such as icons or thematic graphics should be done in PNG8, as it&rsquo;s the most size-efficient of these four. PNG8 is our primary recommendation for most site graphics.

For further optimization all of these formats, taking them through Yahoo&rsquo;s [Smush.It](http://developer.yahoo.com/yslow/smushit/) will reveal how they can be smaller.

### Caching

For static content, the browser should cache the file locally as long as is reasonable. Content that should have far future caching includes:

* CSS and JavaScript
* product images
* thematic graphics
* `favicon.ico`
* Flash `.swf`
* promo images (lighter caching likely)

For the best caching, leverage the `Expires` http header. This is a far future `Expires` header, telling the browser that this response won&rsquo;t be stale until April 15, 2015.

    Expires: Thu, 15 Apr 2015 20:00:00 GMT

If your server is Apache, use the `ExpiresDefault` directive to set an expiration date relative to the current date. This example of the `ExpiresDefault` directive sets the `Expires` date 1 year out from the time of the request.

    ExpiresDefault "access plus 1 year"

`Expires` http header should be set to a value between one month from present to a year (far future) from present. Caching only applies to that exact URL, so a change in the filename of any asset will start a fresh copy. Many developers use a build process to add a version number or timestamp to their assets. Each subsequent build will start a brand new cached version, allowing you to use far future cache dates without worry. [Google has a lot more detail on browser caching](http://code.google.com/speed/page-speed/docs/caching.html#LeverageBrowserCaching)

### Shard resources across domains

Static content should certainly be served from a domain different than the one that serves HTML. This is optimal so that there are [no extra cookies headers on all static content requests](http://developer.yahoo.com/performance/rules.html#cookie_free). It&rsquo;s also much easier to write caching rules for the entire domain. In addition, any subdomains of the current domain will inherit domain cookies, so it&rsquo;s worth using a completely new domain.

However, with enough assets (especially images) the number of requests grows enough to slow down the load of the page. Many browsers have a low constraint of how many assets they will download simultaneously per domain. (In IE6 and 7, it&rsquo;s only two) In this case, we can serve the assets from multiple subdomains such as:

* static1.otherdomain.com
* static2.otherdomain.com
* static3.otherdomain.com

[More information on domain sharding on Google Speed](http://code.google.com/speed/page-speed/docs/rtt.html#ParallelizeDownloads)

### Avoid IFRAMEs

Iframes are the most costly element to add to a given page. They block the page from firing the `onload` event until they are complete. Sometimes they are useful to let another agency handle tracking scripts. For example, the Doubleclick floodlight tag is an `iframe`, and the admin can add tracking pixels into it from their dashboard. In any case where an `iframe` is added, it should be appended to the DOM dynamically after window `onload` has fired. [More detail at Yahoo&rsquo;s Performance site](http://developer.yahoo.com/performance/rules.html#iframes).

### 3rd Party Integration

#### Omniture

We recommend to add the Omniture JavaScript code to the DOM using JavaScript after the page has loaded (either a DOM ready event or window&rsquo;s `load` event). Using this technique, there is no external domain script dependency, which can slow down (and potentially hang) a page load.

#### Flash

Backup HTML content should be in place of the Flash in all cases to maximize SEO value. For XML-driven Flash, the backup HTML content should be leveraging the exact same XML file, to ensure data consistency.

All replacements should be done using `SWFObject` but without inline script tags. `SWFObject` initialization should fire after the DOM Ready event. Minimum player version should be set to minimum v9, to ensure AS3 compatibility.

## Search Engine Optimization

### Be aware of SEO best practices

* [Print css best practices](http://24ways.org/2007/back-to-the-future-of-print)
* Site/app will fit according to [Browser Resolution guidelines](#_browser_resolution).
* Site/app will be compatible with browser requirements described in [Browser Testing and Support](#_browser_testing_and_support)
* Be aware of Accessibility best practices, such as the 508 and WCAG standards: [http://www.section508.gov](http://www.section508.gov) [http://www.w3.org/TR/WCAG20/](http://www.w3.org/TR/WCAG20/)

#### Indexability

We must use semantic markup that&rsquo;s readable and logical when JavaScript and CSS are off. All page content must be in HTML; we don&rsquo;t want to use `iframes` or JavaScript for loading initial indexable content. All links should be to HTML destinations. For example:

    <a href="/shelf/jordan/page/2">

instead of

    <a href="javascript:loadPage(2);">

This lets the page get indexed correctly by search engines as well as allows users to open in new tabs and windows.

#### Optimization

The title tag should feature target keywords for the unique page. The titles should be unique to each page. Headings (h1,h2,etc) should form an outline of the document and represent the most important keywords for that page. URLs should be human-readable with primary target keywords present in them:

    http://domain.com/mens-shoes/basketball/jordan/jordan-mens-ajf-6-basketball-shoe/

vs

    http:// domain.com/ecomm.cfm?view=prod&prodId=23425

#### Flash and Image Replacement

Always use backup HTML content for Flash. All promo images should use CSS-based image replacement instead of alt tags. For example:

    <a href="/nike/morethanagame/" id="morethan">
        <h4>Nike: More Than A Game</h4>
        <h5>Experience the movement and view apparel</h5>
    </a>

    a#morethan { background:url(/promos/nikegame.jpg) no-repeat; width: 200px; height: 100px;
                 text-indent: -999px; overflow:hidden; display:block; }

### Google&rsquo;s SEO Report Card

[Google&rsquo;s SEO Report Card](http://googlewebmastercentral.blogspot.com/2010/03/googles-seo-report-card.html) is an effort to provide Google&rsquo;s product teams with ideas on how they can improve their products&rsquo; pages using simple and accepted optimizations. These optimizations are intended to not only help search engines understand the content of their pages better, but also to improve their our users&rsquo; experience when visiting their sites. Simple steps such as fixing 404s and broken links, simplifying URL choice, and providing easier-to-understand titles and snippets for their pages can benefit both users and search engines.

## Code Reviews

### What is a code review?

A code review is the cornerstone of the formal process for ensuring the quality of user experiences developed by the Front-end Development team. This involves a meeting among authors of markup, reviewers and other stakeholders, with expected input and subsequent code revisions.

### Why should I have a code review?

Code reviews are a strategic investment of time to mitigate risk on a project.

Oftentimes, interface developers are asked to author markup from wire frames or visual compositions. However, its possible that screens that are designed cannot be translated to markup easily, or without compromising quality. Code reviews provide an opportunity for this risk to be addressed and resolved before full production of pages begins.

### Code reviews increase the overall level of knowledge across projects

Since code reviews involve members from within and outside a project team, techniques and best practices are easily shared throughout the entire Front-end Development team.

### Code reviews eliminate bugs before they are reproduced from a few templates into multiple pages

Ideally, code reviews are conducted early in the development process, before full production of pages begins. When templates are reviewed by the team and run through multiple validation tools and browsers, bugs can and will appear. This is the ideal time for bugs to be fixed.

### Code reviews give a set of fresh eyes an opportunity to spot issues with code

Reviewers from outside a project team can spot issues with code more easily than authors of markup, who have been working with code for a longer amount of time.

### Who should participate in a code review?

Ultimately, the Front-end Development Lead on a project is required to ensure that proper code review procedures are followed.

Ideally, a practice lead should act as facilitator for a code review session, unless the practice lead is also the interface developer whose code is under review. In this situation, a project manager can be brought in as a facilitator.

The review team should include at least two senior members of the Interface Technology team versed in development and best practices.

### What is required for a code review?

Before a code review is conducted, templates to be reviewed must be fully developed, validated, and tested against the browsers and platforms required by the project.

A practice lead and/or interface developer must distribute the following 48 hours prior to the date of the code review:

* Code for all pages, associated server-side includes, CSS, and JavaScripts. These should be fully commented, printed out with line numbers along the left side, and the file/page name in the footer of each printed page.
* Screenshots of each template
* URLs of the templates, if applicable
* A list of browsers and platforms supported by the project
* A list of known issues/areas of concern

It is typical for code to be changed constantly until the code review is to take place. Unfortunately, this does not leave enough time for validation and testing. If this is the case, it is recommended that the code review be rescheduled to a date that ensures a proper code review.

In addition, a practice lead and/or interface developer should book a conference room and call-in number for all attendees, since it is possible that members of either the project or code review team are off-site. An hour should provide enough time for review of two or three templates; however, time will vary depending on the volume and complexity of the templates.

During the code review, a practice lead and/or interface developer should facilitate the meeting, while the practice lead or project manager takes notes and assigns action items. Reviewers should have reviewed the code and come prepared to ask questions or provide feedback.

Notes and action items (including owners) should be distributed to all attendees after the code review. If substantial changes come out of a code review, or all code is not reviewed, it may be necessary to schedule a second code review. However, this should be discussed amongst the project team to determine feasibility.

## Browser Testing and Support

### What we support

Empathy Lab supports any browser with an A-Grade in [Yahoo&rsquo;s Graded Browser Support](http://developer.yahoo.com/yui/articles/gbs/), with the exception of Opera. There may be exceptions to this, given regional markets and their particular metrics.

We will strive to support any other mission critical browsers mandated by the client (IE 5.5, Opera, Konqueror, Safari 3 on PC, etc), though we cannot guarantee all functionality is possible.

### How we test

IE Testing

* Have IE6 installed natively (added benefit of using IE developer toolbar, DebugBar and CompanionJS) and [Spoon.net IE7 and IE8](http://spoon.net/browsers)
* Alternatively, have IE7 installed natively on your machine, and install IE6/8 via [Spoon.net](http://spoon.net/browsers)
* Many developers recommend using the [spoon.net browser sandboxes](http://spoon.net/browsers) over [IETester](http://www.my-debugbar.com/wiki/IETester/HomePage), which is still better than [Multiple_IE](http://tredosoft.com/Multiple_IE) and [IE7 standalone](http://tredosoft.com/IE7_standalone).

Firefox

* [Firefox 3.5+](http://www.mozilla.com/en-US/firefox/all-older.html) should be installed natively as well - with version 3.0 available through a [portable apps](http://portableapps.com/) version.
* If you're up to it, Install Firefox 3 side-by-side with FF2 - keep your Firefox 2 profiles and settings.

Safari

* Use the[ newest release of Safari for the PC](http://www.apple.com/safari/). It is 98% consistent with Safari on OS X, but not completely, so test there if its a required platform.

Opera

* You can download [old versions from their archive](http://arc.opera.com/pub/opera/win/). Install in different folders to run multiple versions

#### Bugs in standalone versions

Note: The IE6 standalone has a buggy implementation of opacity in some cases. This will result in any opacity applied with a CSS filter, like alpha opacity or a 24-bit PNG, to fail. In the case that opacity must be tested, you will need a native IE6 installation.

It has been noticed that IE 7 using the Vista platform does have differences from IE 7 on Windows XP, therefore, you might want to make sure that someone on your team has this configuration as well. [IETester](http://www.my-debugbar.com/wiki/IETester/HomePage) is known to fix a number of these issues, as do the Xenocode browsers.

#### Browser testing

* [Multiple_IE](http://tredosoft.com/Multiple_IE)
* [IE7 standalone](http://tredosoft.com/IE7_standalone) (if IE6 is installed natively)
* [How to revert from IE7 back to native IE6](http://www.tech-recipes.com/rx/1163/internet-explorer-7-how-to-uninstall-ie7-beta-versions-and-above/) (does not always work)
* [Prevent IE 7 Install](http://www.microsoft.com/downloads/details.aspx?familyid=4516A6F7-5D44-482B-9DBD-869B4A90159C&displaylang=en)
* [Install IE on OS X](http://winebottler.kronenberg.org/)
* [VNC information at Wikipedia](http://en.wikipedia.org/wiki/VNC) ... including links to clients and downloads.

## Browser Resolution

##### 1024px resolution

* Fold estimated at 570px.
* Optimal width: 960px - Has comfortable padding on both sides, is divisible by many numbers, and also plays well with [IAB ad standard widths](http://www.iab.net/iab_products_and_industry_services/1421/1443/1452)
* Larger width: 970px - Still has some padding on both sides in most browsers. The math plays well with the [Golden Ratio](http://en.wikipedia.org/wiki/Golden_ratio)
* Maximum width: 996px - Without incurring any horizontal scrollbars in the major browsers. [Based on the research here](http://www.nealgrosskopf.com/tech/thread.php?pid=43) the maximum is 1003 px wide if you don&rsquo;t want a horizontal scrollbar.

##### Current stats on window sizes

* [Authentic Boredom - Optimal width for 1024px resolution?](http://www.cameronmoll.com/archives/001220.html)
* [http://marketshare.hitslink.com/report.aspx?qprid=17&qpmr=100&qpdt=1&qpct=3&qptimeframe=M](http://marketshare.hitslink.com/report.aspx?qprid=17&qpmr=100&qpdt=1&qpct=3&qptimeframe=M)
* [http://modernl.com/article/screen-resolutions-and-aspect-ratios-worldwide](http://modernl.com/article/screen-resolutions-and-aspect-ratios-worldwide)
* [http://www.w3counter.com/globalstats.php](http://www.w3counter.com/globalstats.php)
* [http://960.gs/](http://960.gs/) - "The 960 Grid System is an effort to streamline web development workflow by providing commonly used dimensions. The premise of the system is ideally suited to rapid prototyping, but it would work equally well when integrated into a production environment. There are printable sketch sheets, design layouts, and a CSS file that have identical measurements.

##### System resolution is not, however, the same as browser size

* [Browser size does matter - Actual numbers | mentalized](http://mentalized.net/journal/2006/10/24/browser_size_does_matter_actual_numbers/)
* [What size do i need to support | baekdal](http://www.baekdal.com/reports/actual-browser-sizes/abs-sizes/)
* [http://www.456bereastreet.com/archive/200704/poll_results_504_of_respondents_maximise_windows/](http://www.456bereastreet.com/archive/200704/poll_results_504_of_respondents_maximise_windows/)
* [http://www.useit.com/alertbox/screen_resolution.html](http://www.useit.com/alertbox/screen_resolution.html)

## Cross-Browser Performance Strategy

### There are two major truths when it comes to in-browser experience:

1. Both we and the client want the most responsive experience possible.
2. Everything added to the page slows it down.

So with these two facts of life, what steps do we need to take so everyone is happy?

#### Create success metrics with the client

These should be customized to your client and project and done before the wireframing phase. These goals should be reasonable from a technical POV, as well as testable.

Some goals that would be appropriate:

1. The slowest browser supported must go from an empty cache to fully loaded and initialized within 10 seconds.
2. Hover states (and other &ldquo;instant&rdquo; changes) should respond within 300ms.
3. Animations should appear smooth, with jumpiness occurring < 15% of the time (across all browsers).

For load-time based goals, it&rsquo;s important to define who&rsquo;s computer and connection this must be done on (e.g. the clients). Additionally, the goal may be defined for multiple pages, for example: the two most popular landing pages (e.g. homepage and support).

If the client has more wants more aggressive goals than are reasonable with the intended design, expectations need to be set with visual and interactive design to keep things more minimal.

### Communicating the performance impact during design phase

#### Internally

During IA, IxD, and visual design, it is the interface developer&rsquo;s role to communicate the performance impact of interactive features or certain visual techniques on the target browsers. Give the designers concrete constraints: &ldquo;If we&rsquo;re using Cuf&oacute;n, we cannot have more than 10 elements of custom font per page.&rdquo;

#### Externally

Expectations need to be set that all browsers will not have the same experience. They won&rsquo;t perform as well as each other, nor may it make sense to have feature parity. It may be sensible to drop a few features from the IE6 and IE7 experience. Features that could be considered to be dropped are: *shadows, transitions, rounded corners, opacity, gradients*.

##### When communicating the impact of something:

* Clarify the impact with as much detail as possible: &ldquo;it will hurt page load&rdquo; vs. &ldquo;it will add 2 seconds to page load in IE&rdquo;
* Provide a quick POC (proof of concept) if it&rsquo;s reasonable: &ldquo;This similar-looking page without siFR loads in 4 seconds, with siFR it loads in 8 and has a delay to show during scrolling&rdquo;

### Develop according to best practices

Choose libraries and plugins that are performance optimized. Make wise architecture decisions based on performance goals. Also minimize DOM manipulation when possible, and write styles to [avoid visual changes](http://paulirish.com/2009/avoiding-the-fouc-v3/) to the page as it loads and initializes.

### Measure performance during QA

QA teams should also prioritize performance related tickets alongside visual, functional, and usability issues. Developers and QA should determine how that priority will be assigned. During QA, the success metrics should be tested regularly.

Tools to test with

#### When performance goals aren&rsquo;t met, there are three options:

* *Redevelop the code* - profile, discover bottlenecks, refactor code, optimize to target faster execution in the browser
* *Drop the feature* - turn it off for slower browsers only
* *Redesign approach of the UI* - perhaps the design could use a tweak which would bypass the issue entirely

With this approach, we think all parties have  a better chance of having aligned expectations heading in as well as a more sensible workflow in dealing with performance challenges.

## Appendix A: Validators

* <a href="http://jigsaw.w3.org/css-validator/">W3C CSS Validation Service</a>
* <a href="https://addons.mozilla.org/en-US/firefox/addon/249">HTML Validation firefox extension</a>
* <a href="http://jigsaw.w3.org/css-validator/">CSS validator</a>
* Accessibility - <a href="http://bobby.watchfire.com/">Bobby Validation Service</a>
    * Tests individual pages for accessibility against either the W3C or Section 508 standards.
* Accessibility - <a href="http://www.cynthiasays.com/">Cynthia Says Portal</a>
    * Similar to Bobby, tests individual pages for accessibility against either the W3C or Section 508 standards.

## Appendix B: Tools

* [BrowserCam](http://www.browsercam.com/) - Displays how a web site will appear in most browsers (including versions) and operating systems.
* Accessibility - [Evaluation, Repair, and Transformation Tools for Web Content Accessibility](http://www.w3.org/WAI/ER/existingtools.html) - lists validation tools for validating, testing and fixing web content to make it more accessible.

### Code Editors

<dl>
    <dt>Vim</dt>
    <dd>Vim is Vi, Improved. It is a highly configurable, immensely powerful open source editor, but with a fairly steep learning curve for newcomers. Those who use Vim successfully tend to be evangelists on its behalf, and there are many scripts and plugins available for it. <a href="http://vim.org/">Vim</a></dd>
    <dt>TextMate</dt>
    <dd>TextMate is a very popular text editor for Mac OS X. Its primary advantage over other editors is its snippets framework and gigantic bundle library. It utilizes tab-triggers and keyboard shortcuts moreso than IntelliSense autocompletion. TextMate is extremely suitable for rapid HTML, CSS, and JavaScript development, but it can support far more than that besides. <a href="http://macromates.com/">TextMate</a></dd>
    <dt>Netbeans</dt>
    <dd>For JSP development on Tomcat, Netbeans is often the easiest IDE to get up and running. It's open source and Java-based. <a href="http://netbeans.org/">Netbeans</a></dd>
    <dt>Aptana</dt>
    <dd>Aptana Studio is a powerful, free and open source Ajax development environment which runs stand-alone or within Eclipse. Aptana Studio offers tooling for Ajax including HTML, CSS, DOM, and JavaScript editing and debugging, plus support via additional free plugins for PHP, Ruby on Rails, Adobe AIR, Apple iPhone development. It also features full SVN repository integration for committing, branching, tagging, merging and repository browsing. <a href="http://aptana.com/">Aptana</a></dd>
    <dt>Geany</dt>
    <dd>Geany is a text editor using the GTK2 toolkit with basic features of an integrated development environment. It was developed to provide a small and fast IDE, which has only a few dependencies from other packages. It supports many filetypes and has some nice features. <a href="http://www.geany.org/">Geany</a></dd>
    <dt>Notepad ++</dt>
    <dd>Notepad++ is a free (free as in &ldquo;free speech&rdquo;, but also as in &ldquo;free beer&rdquo;) source code editor and Notepad replacement, which supports several programming languages, running under the MS Windows environment. <a href="http://notepad-plus.sourceforge.net/uk/about.php">Notepad ++</a></dd>
    <dt>e TextEditor</dt>
    <dd>E is a new text editor for Windows, with powerful editing features and quite a few unique abilities. It makes manipulating text fast and easy, and lets you focus on your writing by automating all the manual work. You can extend it in any language, and by supporting TextMate bundles, it allows you to tap into a huge and active community. <a href="http://www.e-texteditor.com/">e TextEditor</a></dd>
    <dt>Edit Plus</dt>
    <dd>EditPlus is a text editor, HTML editor and programmers editor for Windows. While it can serve as a good Notepad replacement, it also offers many powerful features for Web page authors and programmers. <a href="http://www.editplus.com/">EditPlus</a></dd>
</dl>

### Firefox Plugins

<dl>
<dt>FireFTP</dt>
<dd>FireFTP is a free, secure, cross-platform FTP client for Mozilla Firefox which provides easy and intuitive access to FTP servers. <a href="http://fireftp.mozdev.org/">FireFTP</a></dd>
<dt>Firebug</dt>
<dd>Firebug integrates with Firefox to put a wealth of development tools at your fingertips while you browse. You can edit, debug, and monitor CSS, HTML, and JavaScript live in any web page. <a href="https://addons.mozilla.org/en-US/firefox/addon/1843">Firebug</a></dd>
<dt>Web Developer Toolbar</dt>
<dd>Adds a menu and a toolbar with various web developer tools. <a href="https://addons.mozilla.org/en-US/firefox/addon/60">Web Developer Toolbar</a></dd>
<dt>JSView</dt>
<dd>Adds an item in the status bar that displays all external JavaScript and CSS files loaded on a given page. Allows you to click on and view the files and things like their URLs. Great way to pull file URLs to put into Charles for remote debugging. <a href="https://addons.mozilla.org/en-US/firefox/addon/2076">JSView</a></dd>
<dt>Live HTTP headers</dt>
<dd>When running, captures all HTTP traffic from the browser, which enables you to see what files are being requested as well as information about the requests and server responses. <a href="https://addons.mozilla.org/en-US/firefox/addon/3829">Live HTTP Headers</a></dd>
<dt>Quick Locale Switcher</dt>
<dd>A tremendous help when doing internationalization, Quick Locale Switcher allows you to change the locale sent along in the browser&rsquo;s user-agent HTTP header, telling servers to display content for you in other locales.</dd>
<dt>Screengrab</dt>
<dd>Screengrab sits in the Firefox status bar, allowing you to capture and copy or save screen shots of everything from selections of a web page to the entire page, even parts displayed &ldquo;below the fold.&rdquo; <a href="https://addons.mozilla.org/en-US/firefox/addon/1146">Screengrab</a></dd>
<dt>Total Validator</dt>
<dd>Enables one-click access to sending your page through a markup validator. No better way to quickly check for missing or mismatched tags! Also available as a standalone application. <a href="http://www.totalvalidator.com/tool/extension.html">Total Validator</a></dd>
</dl>

#### Charles Proxy

Charles watches all requests and can tell you a lot of information about them. Also supremely useful is Map Local which lets you use a local file in place of a given URL (good for replacing a minified JS with a full one).

#### IE Plugins

**CompanionJS, DebugBar, IE8 Dev tools**

##### IE Developer Toolbar:

The Microsoft Internet Explorer Developer Toolbar provides a variety of tools for quickly creating, understanding, and troubleshooting Web pages. [IE Developer Toolbar](http://www.microsoft.com/downloads/details.aspx?familyid=e59c3964-672d-4511-bb3e-2d5e1db91038&amp;displaylang=en)

### JavaScript Libraries

* [jQuery](http://jquery.com/) - popular, chainable, performance-optimized, and well-documented.
* [Mootools](http://mootools.net/) - small footprint, known for its visual effects.
* [Prototype](http://prototypejs.org/) - large footprint, huge developer community, integrated into Rails.
* [Scriptaculous](http://script.aculo.us/) - sits on top of prototype, big, slider, draggables.
* [Dojo](http://dojotoolkit.org/) - large, for big applications.
* [YUI](http://developer.yahoo.com/yui/) - well-documented, best practices javascript coding.
* [Ext](http://extjs.org/) - sits on YUI, jQuery, and Prototype. More dojo-like functionality.

### Tutorials & Tools:

* [CSS Cheatsheet](http://lesliefranke.com/files/reference/csscheatsheet.html)
* [CSS Links](http://www.dezwozhere.com/links.html)
* [Clean CSS](http://www.cleancss.com/)

### Icons

* [Famfamfam silk icons](http://www.famfamfam.com/lab/icons/silk/)
* [Sweetie](http://sublink.ca/icons/)
* [Paul's bookmarks for more icons](http://delicious.com/paul.irish/icons)

## Appendix C: Resources

* [Opera's The Web Standards Curriculum](http://dev.opera.com/articles/view/1-introduction-to-the-web-standards-cur/#toc) - basic articles about building with web standards
* [Google Doctype](http://code.google.com/p/doctype/wiki/Welcome?tm=6) - more advanced tutorials on javascript and CSS
* [10 Principles of the CSS Masters](http://nettuts.com/html-css-techniques/10-principles-of-the-css-masters/) - all of this is smart advice.
* [Google](http://www.google.com/) - when in doubt, google it.
* [Yahoo's Exceptional Performance](http://developer.yahoo.com/performance/) team has maintained one of the best summaries of performance advice
* [Google now has a Speed site](http://code.google.com/speed/page-speed/docs/rules_intro.html) with excellent detail. (Click All best practices)
* There are many more excellent resources on [page optimization](http://delicious.com/paul.irish/optimization) and [javascript performance](http://delicious.com/paul.irish/performance).
* [Mozilla's coding standards](http://wiki.mozilla.org/WebDev:FrontendCodeStandards)
* [Delicious `moluedev` tag](http://delicious.com/tag/moluedev).
* [Nokia's JavaScript Performance Best Practices](http://wiki.forum.nokia.com/index.php/JavaScript_Performance_Best_Practices)

## Revision History

*Authors: Stephen Tudor*

- 2010 March: Minor changes to license/attribution.
- 2010 February: Initial porting to Markdown, with some reorganization.

By the Empathy Lab Front-end Development practice. &nbsp; | &nbsp; Thx to [Isobar](http://na.isobar.com/standards/) and [Fellowship Technologies](http://developer.fellowshipone.com/patterns/code.php). &nbsp; | &nbsp; Steal &amp; modify plz, [CC-BY](http://creativecommons.org/licenses/by/3.0/) license.