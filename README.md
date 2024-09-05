# html-notes


## Document Structure
https://web.dev/learn/html/document-structure

### <!DOCTYPE html>
The first thing in any HTML document is the preamble. For HTML, all you need is <!DOCTYPE html>. This may look like an HTML element, but it isn't. It's a special kind of node called "doctype". The doctype tells the browser to use standards mode. If omitted, browsers will use a different rendering mode known as quirks mode. Including the doctype helps prevent quirks mode.

#### Quirks Mode
> In the old days of the web, pages were typically written in two versions: One for Netscape Navigator, and one for Microsoft Internet Explorer. When the web standards were made at W3C, browsers could not just start using them, as doing so would break most existing sites on the web. Browsers therefore introduced two modes to treat new standards compliant sites differently from old legacy sites.

### lang attribute
The lang language attribute added to the <html> tag defines the main language of the document. The value of the lang attribute is a two- or three-letter ISO language code followed by the region. The region is optional, but recommended, as a language can vary greatly between regions. For example, French is very different in Canada `(fr-CA)` versus Burkina Faso `(fr-BF)`. This language declaration enables screen readers, search engines, and translation services to know the document language.

The lang attribute is not limited to the <html> tag. If there is text within the page that is in a language different from the main document language, the lang attribute should be used to identify exceptions to the main language within the document. Just like when it is included in the head, the lang attribute in the body has no visual effect. It only adds semantics, enabling assistive technologies and automated services to know the language of the impacted content.

In addition to setting the language for the document and exceptions to that base language, the attribute can be used in CSS selectors. `<span lang="fr-fr">Ceci n'est pas une pipe.</span>` can be targeted with the attribute and language selectors `[lang|="fr"]` and `:lang(fr)`.

### Inside `<head>: <meta charset="utf-8">`
The very first element in the <head> should be the charset character encoding declaration. It comes before the title to ensure the browser can render the characters in that title and all the characters in the rest of the document.

The default encoding in most browsers is windows-1252, depending on the locale. However, you should use UTF-8, as it enables the one- to four-byte encoding of all characters, even ones you didn't even know existed. Also, it's the encoding type required by HTML5.

### <script defer/async>
There are two attributes that can reduce the blocking nature of JavaScript download and execution: defer and async. With defer, HTML rendering is not blocked during the download, and the JavaScript only executes after the document has otherwise finished rendering. With async, rendering isn't blocked during the download either, but once the script has finished downloading, the rendering is paused while the JavaScript is executed.

### <link rel="stylesheet" href="styles.css">
`type="text/css"` is optional

## Metadata

https://web.dev/learn/html/metadata

### Pragma Directives

The http-equiv attribute has as its value a pragma directive. These directives describe how the page should be parsed. Supported http-equiv values enable setting directives when you are unable to set HTTP headers directly.

The specification defines seven pragma directives, most of which have other methods of being set. For example, while you can include a language directive with <meta http-equiv="content-language" content="en-us" />, we have already discussed using the lang attribute on the HTML element, which is what should be used instead.

The most common pragma directive is the refresh directive.

```html
<meta http-equiv="refresh" content="60; https://machinelearningworkshop.com/regTimeout" />
<meta http-equiv="content-security-policy" content="default-src https:" />
```

The most useful pragma directive is content-security-policy, which enables defining a content policy for the current document. Content policies mostly specify allowed server origins and script endpoints, which help guard against cross-site scripting attacks.


### Open Graph
* https://web.dev/learn/html/metadata

Create a Facebook media card:
```html
<meta property="og:title" content="Machine Learning Workshop" />
<meta property="og:description" content="School for Machines Who Can't Learn Good and Want to Do Other Stuff Good Too" />
<meta property="og:image" content="http://www.machinelearningworkshop.com/image/all.png" />
<meta property="og:image:alt" content="Black and white line drawing of refrigerator, french door refrigerator, range, washer, fan, microwave, vaccuum, space heater and air conditioner" />
```

### Description

The description value, however, is useful for SEO: the description content value is often what search engines display under the page's title in search results. Several browsers, like Firefox and Opera, use this as the default description of bookmarked pages. The description should be a short and accurate summary of the page's content.

```html
<meta name="description"
  content="Register for a machine learning workshop at our school for machines who can't learn good and want to do other stuff good too" />
```

## Semantic HTML

* Use `header,main,section,footer`
* Like DOM, CSSOM, there's AOM - Accessibility object model
* Assistive devices, such as screen readers, use the AOM to parse and interpret content. The DOM is a tree of all the nodes in the document. The AOM is like a semantic version of the DOM.
* While the role attribute can be used to add semantics to any element, you should instead use elements with the implicit role you need.
```html
<div role="banner">
  <span role="heading" aria-level="1">Three words</span>
  <div role="navigation">
    <a>one word</a>
    <a>one word</a>
    <a>one word</a>
    <a>one word</a>
  </div>
</div>
```

## Attributes
* Boolean attributes (eg: required)
* Enumberable attributes (contenteditable="false")
* tabindex
> The tabindex attribute takes as its value an integer. A negative value (the convention is to use -1) makes an element capable of receiving focus, such as via JavaScript, but does not add the element to the tabbing sequence. A tabindex value of 0 makes the element focusable and reachable via tabbing, adding it to the default tab order of the page in source code order. A value of 1 or more puts the element into a prioritized focus sequence and is not recommended.
* role
> The role attribute is part of the ARIA specification, rather than the WHATWG HMTL specification. The role attribute can be used to provide semantic meaning to content, enabling screen readers to inform site users of an object's expected user interaction.
* Custom attributes
> You can create any custom attribute you want by adding the data- prefix. You can name your attribute anything that starts with data- followed by any lowercase series of characters that don't start with xml and don't contain a colon (:).

`dataset` is used to iterate on these data-first-name as `domNode.dataset[firstName]`, yep, camelCase.