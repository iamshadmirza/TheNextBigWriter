# Good practices in Web-Dev

To make sure quality user experience, your website must be displayed correctly across all the devices. To achieve this, we need to write scalable code and give the same output for all the devices.

## what will it change?
Following this will, of course, enhance the user experience once they visit your web platform. It will improve the readability of your code with the help of clear indentations, and depending upon the performance, it will also enhance the SEO rankings, pushing your platform to the top in search engines. It'll boost up the accessibility on the screen reader and other identical technologies.


## Tell me Some examples

Here you go...

1. ### **Don’t Use Divs for Everything**

 When creating elements, we tend to use the `div` element to wrap the header, footer, or navbar. When a screen reader or similar assistive technology is used to read web pages, it can not translate that `div` element to the header section, main section, or footer section. So instead of doing that, try writing semantic tags like `<main>`, `<nav>`, `<header>`, `<section>`, `<article>` etc.

 Below is an example code for how semantic websites should look.

 ```HTML
<html>
    <head>
        ...
    </head>
    <body>
        <nav>
            ...
        </nav>
        <main>
            <header>
                ...
            </header>
            <section>
                ...
            </section>
        </main>
        <footer>
            ...
        </footer>
    </body>
</html>
```

 ---

2. ### **Using The Right Doctype**

 Doctype defines which version of HTML you are using in your website. It helps web browsers to understand the Html version and render the web pages accordingly. A wrong declaration of doctype can lead to break the website in some browsers.

 Always use the suitable declaration for doctype. For html5, the correct doctype is mentioned below.

 _TIP: doctype declaration is not case sensitive._

 ```html
<!DOCTYPE html>
<html>
  <head>
    <title>Title of the document</title>
  </head>

  <body>
    The content of the document......
  </body>
</html>
```

 ---

3. ### **Mention the language attribute**

 Language attribute helps in the correct pronunciation of sentences when browsers are using screen readers. Screen readers generally load the language library in which they want to pronounce. However, insufficient language attributes can lead to selecting the default language as English and mispronouncing the word.

 Add lang attribute in `<html>` to use the power of screen readers.

 ```html
<html lang="en">
  ...
</html>
```

 ---

4. ### **Have an alt**

 What to do when you show your website and the image failed to load on your friend's phone? Have an alt, yes you read it right. Have an `alt` attribute in the `<img>` element. `alt` attributes are used as placeholders when your image is failed to load. So next time, don't forget to _have an alt_.

 Here is how you add an alt attribute.

 ```html
<img alt="Audits set-up in Chrome DevTools" src="..." />
```

 **Tips for writing alt**

 - `alt` text should give the intent, purpose, and meaning of the image.
 - Blind users should get as much information from alt text as a sighted user gets from the image.
 - Avoid non-specific words like "chart", "image", or "diagram".

 ---

5. ### **Incorrect aspect ratio**

 Remember when you are writing media queries for different screen sizes and trying combinations of different heights and widths? That when we sometimes mess up with the aspect ratio of images.

 To avoid the situation, change height and width in percentage or use CDN( content delivery network) to load images.

 ![comparision of correction and incorrect aspect ratio side by side](https://i.imgur.com/OEGEh8Z.png)

 ---

6. ### **Unsafe links to cross-origin destiantions**

 If your page uses `target="_blank"` to link other website to your page, you need to add `rel="noopener"` or `rel="noreferrer"` attribute in anchor element.
 If you use `target="_blank"` in your links, other pages can access your `window` object with `window.opener` property, which may lead to redirect page to malicious URL.

 Use the below-mentioned method to avoid this.

 ```html
<a href="https://examplepetstore.com" target="_blank" rel="noopener">
  Example Pet Store
</a>
```

 ---

7. ### **Front-end JavaScript libraries with known security vulnerabilities**

 Libraries are used to add prewritten code that can solve our tasks. However, the code in these libraries is sometimes vulnerable, which can inject vulnerability into your site. So if there are any known vulnerabilities in your javascript libraries, update them to the latest.

 You can use built-in tools like a lighthouse or [snyk database for known vaulnaribilities](https://snyk.io/vuln?packageManager=all).

 ---

8. ### **Use Meaningful Title Tags**

 Title tags help make a web page search engine friendly. Text inside title tags comes on google search results and web browser tabs.

 example :

 ```html
<title>Six Revisions - Web Development and Design Information</title>
```

 ---

9. ### **Use Descriptive Meta Tags**

 Meta tags give information about your web page to search engines and crawlers. More meaningful description means more hits on the search engine and leading more traffic to your website.

 For example, descriptive meta tags below will show info when searched on web pages.

 ```html
<meta
  name="description"
  content="Six Revisions is a blog that shares useful information about web development and design, dedicated to people who build websites."
/>
```

 ## ![Descriptive Meta Tags](https://i.imgur.com/VnIJDrU.png)

 ---

10. ### **Minify and Unify CSS,JS**

 CSS files or external libraries take time to load, making web pages slow to load. In order to make them a bit faster, use a single master CSS file and minify the CSS file removing unnecessary space and comments which web browsers don't need to understand.

 Also, make sure you are using trusted minified, some online service for Html editor was found to be injecting their own code to top rank them for SEO optimization.

 [here](https://casparwre.de/blog/seo-scam/) is a blog post about it.

 ---

11. ### **Use Lower Case Markup**

 Using a lower case to write HTML elements is standard practice. Capitalizing the Html won't affect your web page render, but it will definitely make your code less readable.

 #### Bad Practice

 ```html
<div>
  <img src="images/sample.jpg" alt="sample" />
  <a href="#" title="TEST">test</a>
  <p>some sample text</p>
</div>
```

 #### Good Practice

 ```html
<div id="test">
  <img src="images/sample.jpg" alt="sample" />
  <a href="#" title="test">test</a>
  <p>some sample text</p>
</div>
```

 ---

12. ### **Write Consistently Formatted Code(use preetier)**

 Writing a piece of code for software means tons of hours maintaining it. With this much time spending on maintaining the code, we need tools to improve readability and increase teamwork. That's where the code formatter, like prettier, comes in. They help us with readability, enhance collaboration and save our time and energy.

 These tools integrate with code editors easily and can work in the background without our involvement.
 One famous code formatter is [prettier](https://prettier.io/). It supports major code editors and connects with them seamlessly.

 ---

13. ### **Document your code**

 Writing an extended code includes months of maintenance with it. With many teammates doing the submodules, new team members can take a while to understand code. Even some of us forget what we wrote after some months. To avoid this situation, it is best to write comments in the section of the code.

 Here is a example of good code with comments,

 ```html
<!DOCTYPE html>
<html>
  <head>
    <!-- Document title -->
    <title>Title of the document</title>
  </head>

  <body>
    <!-- hero image -->
    <section>
      <img src="images/sample.jpg" alt="sample" />
    </section>

    <!-- Test link button -->
    <section>
      <a href="#" title="TEST">test</a>
    </section>
    <!-- Hero Content -->
    <section>
      <p>some sample text</p>
    </section>
  </body>
</html>
```

---

## Last but not the least
Following these web-dev practices will help you increase your client base and improve the inline presence on the web. Make sure you stick to these standards for all of your projects. What really matters is how you develop it, which will help you achieve and serve your goals.

## References

- https://www.w3schools.com/tags/tag_doctype.asp
- https://web.dev/image-aspect-ratio/
- https://www.webfx.com/blog/web-design/20-html-best-practices-you-should-follow/
