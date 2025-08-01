# Web programming

<br>![web image](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/resources/web.jpg)

## Table of Contents
+ [The Internet](#the-internet)
  + [History of the Web](#history-of-the-web)
  + [How the web works](#how-the-web-works)
  + [The web standards model (HTML, CSS, JavaScript)](#the-web-standards-model-(html,-css,-javascript))
  + [Internet and the World Wide Web](#internet-and-the-world-wide-web)
  + [Validation](#validation)
  + [Web accessibility and W3C standards](#web-accessibility-and-w3c-standards)
+ [Introduction to HTML](#introduction-to-html)
+ [Advanced HTML](#advanced-html)
+ [CSS: Cascading Styling Sheets](#css:-cascading-styling-sheets)
+ [JavaScript](#javascript)
+ [XML](#xml)
+ [Server side programming with PHP](#server-side-programming-with-php)
+ [Introduction to Mobile Web](#introduction-to-mobile-web)


## The Internet

**References:**

- Francis, M.N. (2012, March 4). **_History of the Web_**. Retrieved from [here](https://www.w3.org/wiki/The_history_of_the_Web).
- MDM Developers. (2019, May 18). **_How the Web Works_**. Retrieved from [here](https://developer.mozilla.org/en-US/docs/Learn/Getting_started_with_the_web/How_the_Web_works).
- W3C. (2016, December 3). **_The Web standards model—HTML, CSS and JavaScript_**. Retrieved from [here](https://www.w3.org/wiki/The_web_standards_model_-_HTML_CSS_and_JavaScript).
- Toothman, J. (2019, March 12). **_What's the difference between the Internet and the World Wide Web?_**. Retrieved from [here](https://computer.howstuffworks.com/internet/basics/internet-versus-world-wide-web.htm).
- W3C. (n.d.). **_Why Validate?_**. Retrieved from [here](http://validator.w3.org/docs/why.html).
- W3C. (n.d.). **_Web Validation Service_**. Retrieved from [here](https://validator.w3.org/).
- W3C Web Accessibility Initiative (WAI) (2017, December 4). **_Introduction to web accessibility and W3C standards_** [Video]. YouTube. Retrieved from [here](https://www.youtube.com/watch?v=20SHvU2PKsM).
- Khan Academy Computing. (2014, December 9). **_HTML validation | Computer programming | Khan Academy**_ [Video]. YouTube. Retrieved from [here](https://www.youtube.com/watch?v=qrU3ghYJjEw).

### History of the Web

**1957**: Soviet Union successfully launches the first satellite (Sputnik 1) into orbit. This event lead to the creation of ARPA (US Department of Defence) for researching and develop advanced ideas and technologies.

**1960**: Joseph Licklider (ARPA) publishes a paper (*Man-Computer Symbiosis*) articulating the idea of networked computers providing advanced information storage and retrieval.

**1967**: The plan for this computer network (ARPANET) is presented.

**1969**: The first four-computer network was up and running. The core problem was how to connect separate physical networks without tying up network resources for constant links. This was solved the packet switching technique (data requests are split into small chunks, called packets, which can be processed quickly without blocking communication from other parties).

Other (private) networks using packet switching appeared: X.25 (by the International Telecommunication Union), JANET (based on X.25, for UK universities), CompuServe (American commercial enterprise), etc. However, the proliferation of different networking protocols complicated communication between separated networks.

**1972**: ARPA was renamed to DARPA.

**1974**: Robert Kahn (ARPA) and Vinton Cerf (Stanford University) created a standard for masking the differences between networking protocols (Internet Transmission Control Program). This specification made the host computer (not the network) responsible of maintaining transmission integrity. This made easy to join almost all networks together. ARPA funded development of this software.

**1977**: Successful demonstration of 3 different networks communicating using this specification.

**1981**: The specification was finalised, published, and adopted.

**1982**: ARPANET connections outside US were converted to use the new TCP/IP protocol.

**1991**: University of Minnesota released Gopher, an information retrieval system for delivering menus of links to files, computer resources, and other menus. These menus could even use the Internet to fetch menus from other systems. Popular with universities and large organisations.

**1991**: Tim Berners-Lee (CERN) had been working on an information management system, in which text could contain links and references to other works, allowing the reader to jump from document to document (hypertext). He created a server for publishing hypertext and a program for reading them (WorldWideWeb). This software was released in 1991.

**1993**: Three main events:

- Licence fees were applied to Gopher, so many organisations started to look for alternatives (the CERN had such alternative).
- CERN released the source code of WorldWideWeb into the public domain.
- NCSA released Mosaic (program that was a combined web browser and Gopher client), available for Unix, Macintosh, and Windows. 

Mosaic increased in popularity, and with it the Web. Soon, the number of available web browsers increased dramatically, many created by research projects at universities and corporations.

**1994**: Telenor (Norwegian communications company) created the Opera browser. Netscape Communications Corporation, founded by Marc Andreessen (who left NCSA) and Jim Clark, released the Netscape Navigator.

**1995**: Microsoft released Internet Explorer based on the Mosaic technology, licensed to him by Spyglass Inc. (commercial arm of NCSA).

**Browser wars**: Netscape and Microsoft tried to support as much features as possible in order to attract developers. However, there were problems: they didn't focus on fixing problems with such features, they added proprietary features, and some features were incompatible with the other browser. This made developing web sites complicated and confusing, sometimes forcing to build two websites, one for each browser, or not supporting one of them.

Opera maintained a small but steady presence throughout this period, trying to innovate and support web standards as well as possible.

**1994**: Tim Berners-Lee founded W3C (World Wide Web Consortium) at MIT, with support from CERN, DARPA, and the European Commission. It's purpose was to standardize the protocols and technologies used to build the web. W3C publishes specifications as recommendations, which are not enforced. Manufacturers only had to conform to them if the wished to label their products as W3C-compliant.

**1998**: Internet Explorer 4 and Netscape Navigator 4 dominated the market, but web developers were required to know too many ways of writing code. The WaSP (Web Standards Project) was created by a group of web developers. They called the W3C documents standards rather than recommendations. They made a call to action to web developers, ridiculed companies involved with the W3C that didn't support the standards correctly, and helped to identify problems in some browsers and web developing tools.

**2000**: Microsoft released Internet Explorer 5 Macintosh Edition (Mac OS default browser at the time) with a reasonable level of support of W3C recommendations. Opera had decent support too. WaSP persuaded Netscape to postpone release of Netscape Navigator 5 until it was much more compliant. This contributed to make web developers and designers feel comfortable working.

**2000**: New practices had appeared, with many web sites being more like desktop applications than static pages. W3C decided that the future (of markup languages) was XML and XHTML, not HTML, and published the XHTML 1.0 specification. XHTML was like HTML 4.01, but using the stricter markup syntax rules of XML. XHTML 2.0 soon followed with features but without backwards compatibility with the markup already on the Web. XHTML didn't work properly in Internet Explorer, and the developer tools were not ready to work with it.

**2004**: Some developers and implemented formed the WHATWG group, aiming to write better HTML markup spec that could handle authoring the new breed of web applications without breaking backwards compatibility. This resulted on the Web Applications 1.0 specification.

**2007**: W3C adopted the Web Applications 1.0 specification and called it HTML5. It was backwards compatible, better suited for dynamic applications, included powerful new features, and has a clearly defined parsing algorithm (so all browsers will create the same DOM from the same markup).

### How the web works

#### Definitions

**Computers connected** to the Internet are called:

- **Clients**: Makes requests. Typical web user's internet-connected devices (computer, phone...) and web-accessing software on those devices (usually a web browser).
- **Servers**: Makes responses. Computers storing webpages, sites, or apps. When a client wants to access a webpage, a copy of it is downloaded from the server onto the client machine to be displayed in his browser.

**Internet connection**: It allows to send and receive data on the web.

**TCP/IP** (Transmission Control Protocol and Internet Protocol): Communication protocols that define how data should travel across the Internet.

**DNS** (Domain Name System): It's like an address book for websites. When you enter a web address in the browser, it looks at the DNS to find the website's IP address.

**HTTP** (Hypertext Transfer Protocol): Application protocol that defines a language for clients and servers to speak to each other. 

**Component files**: Files that make up a website. Two main types:

- **Code files**: Websites are built primarily from HTML, CSS, and JavaScript.
- **Assets**: Images, music, video, text documents, PDFs, etc.

#### Process

1. You enter a web address (of a website) into your browser.
2. The browser goes to the DNS server and finds the real address where the website lives on.
3. The browser sends an HTTP request message to the server asking it to send a copy of the website. All messages between client and server are send across your Internet connection using TCP/IP.
4. If the server approves the client's request, it sends a "200 OK" message, meaning that you can look the website, and starts sending the website's files to the browser in small chunks (data packets).
5. The browser assembles the small chunks into a complete web page and displays it to you.

#### Parsing

Web browsers send requests to server for HTML files, which often contain `<link>` elements referencing external CSS stylesheets, and `<script>` elements referencing external JavaScript scripts. Order in which these files are parsed by the browser:

1. The HTML file is parsed first. As the browser parses it, it sends requests back to the server for any CSS file from `<link>` elements, and any JavaScript file from `<script>` elements. 
2. The browser generates an in-memory DOM tree from the parsed HTML, generates an in-memory CSSOM structure from the parsed CSS, and compiles and executes the parsed JavaScript.
3. Building the DOM tree, applying the styles from the CSSOM tree, and executing the JavaScript results in a visual representation of the page that is painted to the screen.

#### DNS

Web addresses (IP addresses) are a set of numbers (like `192.0.2.172`) representing a unique location on the web. They aren't easy to remember, so the DNS system was invented. I t uses special servers that match up a web address you type into your browser (like `google.com`) to the website's real IP address. Websites can be reaches directly via their IP addresses (check it out using a [DNS lookup tool](https://www.nslookup.io/website-to-ip-lookup/)).

#### Packets

Data is sent across the web in thousands of small chunks. Some reasons for this are:

- Sometimes they're dropped or corrupted, and it's easier to replace small chunks.
- Packets can be routed along different paths, making the exchange faster and allowing different users to download the same website at the same time.

### The web standards model (HTML, CSS, JavaScript)

#### Separation

HTML files can contain layout and style, but it's recommended to use HTML just for layout, and use CSS for styling. Reasons:

- __More efficient code__: The larger the files, the longer to download and the more bandwidth they take. Including styling just once in a separate CSS file keeps the HTML file cleaner.
- __Easier to maintain__: Changing your site's appearance will only require to modify one file, not many.
- __Accessibility__: A web page with a proper semantic structure makes it easier for visually impaired users to use "screen reader" software. Using best practices make keyboard controls on web pages (for mobility impaired users) work better.
- __Device compatibility__: A plain markup HTML page, with no style information, can be reformatted for different devices. CSS natively allows to specify different style sheets for different presentation methods/media types.
- __Web crawlers/search engines__: A search engine use a "crawler" (software that reads through your pages). If it has trouble finding your content or mis-interprets it, your ranking in relevant search results may suffer.
- __Good practice__: Separating content (HTML), style (CSS), and behaviour (JavaScript) is the best way to develop web applications. 

#### Markup

**HTML** and **XHTML** are markup languages. They're composed of **elements**, which contain **attributes** (some optional, some mandatory). Elements define the content type. Attributes define extra information about those elements (ID, where a link points...). Markup describes the function of the content. Typical element:

```
<div id="footer"></div>
```

- `<div id="footer">`: Start tag
- `<id="footer">`: Attribute
- `</div>`: End tag

**HTML**: Oldest and most common web language. Elements and attributes are case insensitive (`<h1>` == `<H1>`). Some elements doesn't need a closing tag (`<p>`), and others shouldn't have (`<img>`). Attributes may be written without being enclosed in quotes. Shorthand can be used for certain attributes (`<input required>`).

**XHTML**: Reformulation of XML as an XML vocabulary, which has much stricter syntax rules. In XTML5 you're free to use HTML or XHTML syntax. Elements and attributes and case sensitive (all lowercase). All elements must be explicitly closed (`<p>...</p>`). Elements without content should be closed using a slash in the start tag (`<hr>` == `</hr>` == `<hr>`). Attribute values must be enclosed by quotes. The full attribute form must be used for all attributes (`<input required="required">`).

**Validators**: Tools created by the W3C to automatically check your pages for you, and point out any problems/errors your code might have (missing closing tags, missing quotes around attributes...).

#### CSS

**CSS** (Cascading Style Sheets): It gives fine control over the formatting and layout of your document. It works on a system of rules, which select the elements you want to style and set values for some of their properties (set color, background, font size, style, position...). CSS rule example:

```
p {
    line-height: 2;
    color: green;
}
```

This makes any content enclosed within `<p></p>` tags to have double the line height and be colored green.

#### JavaScript

**JavaScript**: Scripting language use to add behaviour to web pages (validate data you enter, provide drag and drop functionality, change styles on the fly, animate page elements...). Usually, it finds a target HTML element and does something to it (similar to CSS).

#### HTML example

```
<!DOCTYPE html>

<head>
  <meta charset="utf-8">

  <title>References</title>
  <style type="text/css">
    @import url("styles.css");
  </style>
</head>

<body>
  <div id="bggraphic"></div>
  <div id="header">
    <h1>References</h1>
  </div>
  <div id="references">
    <cite class="article">Adams, J. R. (2008). The Benefits of Valid Markup: A Post-Modernistic Approach to Developing
    Web Sites. <em>The Journal of Awesome Web Standards, 15:7,</em> 57-62.</cite>
    <cite class="book">Baker, S. (2006). <em>Validate Your Pages.... Or Else!.</em> Detroit, MI: Are you out
    of your mind publishers.</cite>
    <cite class="article">Lane, J. C. (2007). Dude, HTML 4, that's like so 2000. <em>The Journal that Publishes Genius,
    1:2, </em> 12-34.</cite>
    <cite class="website">Smith, J. Q. (2005). <em>Web Standards and You.</em> Retrieved May 3, 2007 from
    Web standards and you.</cite>
  </div>
  <div id="footer">
    <p>The content of this page is copyright © 2007 <a href="mailto:jonathan.lane@gmail.com">J. Lane</a></p>
  </div>
</body>
</html>
```

- Line 1 (`<!DOCTYPE html>`): Document type declaration (or doctype). It makes the browser render the page properly in "standards mode". [Choose the right doctype for your HTML documents](https://www.w3.org/wiki/Choosing_the_right_doctype_for_your_HTML_documents).
- Lines 5-7`: Import a CSS file into the page. The styles it contains will be applied to the various elements on the page.

<br>![Example image without CSS](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/resources/examplewithoutCSS.png)

#### CSS example

```
body {
  background: #fff url('images/gradbg.jpg') top left repeat-x;
  color: #000;
  margin: 0;
  padding:0;
  border: 0;
  font-family: Verdana, Arial, sans-serif; font-size: 1em;
}

div {
  width: 800px;
  margin: 0 auto;
}

#bggraphic {
  background: url('images/pen.png') top left no-repeat;
  height: 278px;
  width: 362px;
  position: absolute;
  left: 50%;
  z-index: 100;
}

h1 {
  text-align: center;
  text-transform: uppercase;
  font-size: 1.5em;
  margin-bottom: 30px;
  background: url('images/headbg.png') top left repeat;
  padding: 10px 0;
}

#references cite {
  margin: 1em 0 0 3em;
  text-indent: -3em;
  display: block;
  font-style: normal;
  padding-right: 3px;
}

.website {
  border-right: 5px solid blue;
}

.book {
  border-right: 5px solid red;
}

.article {
  border-right: 5px solid green;
}

#footer {
  font-size: 0.5em;
  border-top: 1px solid #000;
  margin-top: 20px;
}

#footer a {
  color: #000;
  text-decoration: none;
}

#footer a:hover {
  text-decoration: underline;
}
```

- `body {…}`: It sets some defaults for the document (text and background color, width of border around the text...). Modern browsers will apply their own defaults, but specifying this you can control how your website looks on different browsers.
- `div {…}`: Page is set to 800 pixels width (a percentage can be used, which depends on the browser window size). The margin setting ensures the page content stays centered.
- `background: url;`: Background image used. Three images were used (gradient, semi-transparent pen, semi-transparent heading).

<br>![Example image with CSS](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/resources/examplewithCSS.jpg)

#### Use modern web standards and best practices

Web designers and developers should use modern web standards and best practices, and all browsers should support web standards perfectly. However, this doesn't always happen. Using modern standards and best practices makes it easier to create cross browser web sites and maintaining their code, and provides better accessibility and SEO. Modern browsers support HTML, CSS, and JavaScript really well.

### Internet and the World Wide Web

After the Sputnik's launch (1957), president Dwight D. Eisenhower started ARPA (Advanced Research Projects Agency) in 1958 to increase U.S. technological advancements. It created the first ARPANET network (1969), and Internet was born. More and more computers were added to this network, beginning to form the Internet we know today. By 1990, more than 300.000 computer were connected to the network.

In 1990, Tim Berners-Lee developed HTTP (Hypertext Transfer Protocol), a set of rules for how files and other information are transferred between computers. People quickly developed browsers supporting HTTP. By 1992, more than a million computers were connected.

**Internet** is a network of networks (work, school, home, company...). It's composed of machines, hardware, and data. These networks are of all kinds and sizes (LANs: local area networks, regional networks...). Your phone is on a network that is part of Internet. Even satellites are connected to the Internet.

**World Wide Web** (WWW) is a system we use to access the Internet. It brings the Internet to life. There're different systems (web, e-mail, instant messaging...), but the Web is the most popular. The WWW uses hypertext to access information on different networks. We typically access the Web through browsers (Chrome, Brave...).

**W3C** (World Wide Web Consortium): Organization run by Tim Berners-Lee that aims to develop standards and guidelines for the Web. 

**Internet Society** (1992): Provides leadership in many aspects of Internet-related information, initiatives, and activities.

### Validation

#### Validators

They're tools created by the W3C to automatically check your pages for you, and point out any problems/errors your code might have (missing closing tags, missing quotes around attributes...). Useful links:

- [W3C HTML validator](https://validator.w3.org/)
- [W3C CSS validation](https://jigsaw.w3.org/css-validator/)
- [HTML5 validator](https://html5.validator.nu/): It tends to be more up to data about HTML5 than the W3C one. 
- [Debuggin HTML](https://developer.mozilla.org/en-US/docs/Learn/HTML/Introduction_to_HTML/Debugging_HTML)
- [Choosing the right doctype for your HTML documents](https://www.w3.org/wiki/Choosing_the_right_doctype_for_your_HTML_documents)

#### HTML validation

You should make webpages that are valid HTML because it gives more confidence that the browsers will interpret them exactly as you expect. You may not follow HTML specification correctly, but browsers can be really forgiving and let you get away with it, not letting you know that something is wrong with your webpage. Thus, your should run your webpage through the [W3 validation service](https://validator.w3.org/). It checks and tells you if your page is valid and if there's something wrong. It lets you enter an URL, upload a file, or copy and paste code.

#### Why validate?

- **Validation as a debugging tool**: Web browsers are good at parsing HTML code, but some error are not always caught gracefully. Often, different software on different platforms won't handle error in a similar fashion. Using standard, interoperable markup and stylesheets helps to have our page handled consistently across platforms and user-agents. Most developers ensure that their markup and CSS is validated before creating a rich interactive layer. Most web professionals running into web styling or scripting bugs check validation errors first.

- **Validation as a future-proof quality check**: Checking that a page "displays fine" in several browsers may ensure that it "works" today, but doesn't guarantee that it will work tomorrow. Validation checks whether a page is built in accordance with Web standards, and may guarantee that future web platforms will handle it as designed.

- **Validation eases maintenance**: Using Standards (such as HTML and CSS) according to a widely accepted coding style makes applications easier to maintain, even by someone else.

- **Validation helps teach good practices**: Many professionals know these technologies. Beginners find automated checking tools invaluable in spotting mistakes. Teachers consider it good introduction to broader, more complex quality concepts such as accessibility.

- **Validation is a sign of professionalism**: There is little certification and courses for web professionals. Professionals are proud of creating web content using semantic and well-formed markup, separation of style and content, etc. Validation quickly checks whether the code is a professional work. 

Any debugging process, including validation, is sometimes difficult, and modern browsers include an automatic error correction system that cope very well with errors in HTML or CSS. This makes validation seem useless or costly, widespreading the following statements:

- _My site looks right and works fine - isn't that enough?_: Markup languages are just data formats. A website doesn't look like anything at all. It only takes on a visual appearance when it presented by your browser. In practice, different browsers display the same page very differently (this is deliberate, it's not a browser bug). This is WYSINWOG (What You See Is Not What Others Get), unless by coincidence. This is one of the main strengths of the web (example: a blind user can select very large print or text-to-speech without a publisher having to prepare a separate edition).

- _Lots of websites out there don't validate - including household-name companies_: Such companies have visits because of the name and despite of dreadful websites, which is a luxury you may not afford. Also, accessibility is lay in many countries (example: you may risk a lawsuit if your site is inaccessible to a disabled person who cannot use "conventional" browsers). Whilst validation doesn't guarantee accessibility, it's important for exercising "due diligence".

- _Validation means boring websites, and stifles creativity_: That might have been the case in the 2000's, but today most of the stunning, content and design-rich Web sites are built with standard (X)HTML, CSS and scripting.

### Web accessibility and W3C standards

**Web accessibility**: People with disabilities should be able to use the Web equally ([read more](w3.org/wai)). Examples:

- People that cannot use arms, may use a stick.
- Deaf people could use captions to watch videos.
- Blind people could use a screen reader (it reads aloud what is on screen).

Accessibility has many benefits. Examples:

- Captions benefit anyone in a loud/quiet environment.
- Good color contrast works better when there's glare.
- Improved layout and design provide better user experience.

A lot of accessibility can be built into the underlying code of websites and applications. Web technologies from W3C, such as HTML, support many accessibility features. Examples:

- Features to provide text alternatives for images, which are read aloud by screen readers and also used by search engines.
- Headings
- Labels

Good authoring tools (wikis, content management systems, code editors...) help create accessible code, automatically or with input from the author.

Web browsers, media players, and apps also need to support accessibility features. 

W3C provides standards to help make the Web accessible, which are internationally recognized by governments and businesses. Examples:

- **WCAG** (Web Content Accessibility Guidelines): Most well-known W3C accessibility standard. It's the ISO standard 40500, and adopted in the European standard EN 301 549. It's built around 4 core principles:

  - **First perceivable**: For example, so people can see or hear the content.
  - **Operable**: For example, so people can use the computer by typing or by voice.
  - **Understandable**: For example, so people can get clear and simple languages.
  - **Robust**: For example, so people can use different assistive technologies.

- **ATAG** (Authoring Tool Accessibility Guidelines): It defines requirements for content management systems, code editors, and other software.

- **UAAG** (User Agent Accessibility Guidelines): It defines requirements for web browsers and media players.

Around 15-20% of the population has disabilities. The UN convention of the Rights of Persons with Disabilities defines the access to information (including the Web) as a human right. Most countries around the world ratified this UN convention, and several adopted binding policies too.


## Introduction to HTML

**References:**

- MDN Contributors (2020, February 13). _**Information Architecture—Planning a simple website**_. Retrieved from [here](http://www.w3.org/community/webed/wiki/Information_Architecture_-_planning_out_a_web_site).
- W3C (2017, November 11). _**What does a good web page need?**_. Retrieved from [here](http://www.w3.org/community/webed/wiki/What_does_a_good_web_page_need).
- Raggett, D. (2005, May 25). _**Getting Started with HTML**_. Retrieved from [here](http://www.w3.org/MarkUp/Guide/).
- _**Getting Started**_. (n.d.) Retrieved from [here](http://www.htmldog.com/guides/html/beginner/gettingstarted/).
- _**Lesson 3: Elements and tags**_. (n.d.). Retrieved from [here](http://html.net/tutorials/html/lesson3.php).
- Krossing, D. (2017, June 22). _**1: How to get started with HTML & CSS | HTML tutorial for beginners | Learn HTML and CSS | mmtuts**_. [Video]. YouTube. Retrieved from [here](https://youtu.be/pm5OVxpul48).
- Wright, J. (2010, November 10). _**Learn HTML in 12 minutes**_. [Video]. YouTube. Retrieved from [here](https://youtu.be/bWPMSSsVdPk).
- Web Dev Simplified. (2018, August 22). _**Learn CSS in 20 minutes**_ [Video]. YouTube. Retrieved from [here](https://youtu.be/1PnVor36_40).
- Locke, M. (2010, January 22). _**Website Design Tips: The Standard Website Layout**_ [Video]. Retrieved from [here](https://youtu.be/3meSOXY9uGA).
- Locke, M. (2010, February 5). Color Selection and Web Design [Video]. Retrieved from [here](https://youtu.be/Ukl9yecLxIQ).

### Planning a simple website

**Information architecture**: Work out what content you want to put on a whole website, what pages you need, and how they should be arranged and link to one another for the best possible user experience. Steps for a simple website:

1. Consider the elements common to most, or all, pages (navigation menu, footer content...).
2. Draw a rough sketch of what you want the structure of each page to look like. Annotate what each part is going to be.
3. Brainstorm all the other, not common to every page, content you want to have on your website.
4. Sort all these content items into groups, to give an idea of what parts might live together on different pages (similar to the [card sorting](https://developer.mozilla.org/en-US/docs/Glossary/Card_sorting) technique).
5. Sketch a rough sitemap. Draw a bubble for each page on your site, and lines to show the typical workflow between pages. The homepage could be in the center and link to most/all the others. You might include notes about how things might be presented.

### What a good web page needs

Issues to consider: consistency, usability, and accessibility.

#### Homepage

Misconceptions:

- _The homepage is the best place to start_: It often tries to summarise everything in the site, and be everything for everyone, making it a bloated mess that overwhelms the user.
- _The homepage is the first page your site visitors will see_: Most visitors may end up on your site based upon a search.

Use the homepage to highlight the areas of content within the site and drive your traffic to them. Treat it as any other page on the site and give it a defined purpose (to show what's new, to provide an overview, to introduce to a topic and lead people further into the site...). 

#### Navigation

Identify the common destinations and put them into your main navigation. Navigation appears on other parts of the site repeatedly. It must be **consistent**. Example: a set of tabs at the top of the page provide links, it remains there as you move through the site, and change to indicate where you currently are.

Misconception: _Any page should be at most 3 clicks away_. This can lead to complex navigation by cramming in as many links as possible. This leads to too much information for the user to take in and use effectively. Too much or too little choice can paralyze. Users will continue through the site if they feel progress from one link to another and that they are on track to their goal.

#### Other common elements

Like navigation, other parts of a site can appear on pages repeatedly:

- Show ownership: Branding, logo, masthead. 
- Header: It may contain (or be attached to) the logo, the main navigation, or a search box.
- Footer: Last area of the page. It should contain extra information such as a copyright notice, or links to useful ancillary pages on your site ("About this site", "Terms & conditions", "Contact us"...).

**Consistency** is key. Color, layout, shapes and icons, typography and imagery, all combine to create an overall impression of a page as "belonging" to the site. Consistent appearances and placement help to keep you oriented through the site and provides familiarity. 

#### Context

Each page, despite the common elements, should be unique. It should do one thing, or a small number of things, and do them well.

**Content** should be relevant and separate. It should be uniquely addressable (i.e., live at a unique URL) and logically ordered (both within the site and the page) so that it can be easily found.

Each section of content on a page should be introduced by a **heading**, indicating its relative importance within the page (similar to a newspaper).

#### Usability

Usability makes a site behave in a rational and expected way. Bad usability stems from not considering the needs of the site's users. Focus on them when designing and creating the experience in order to create a satisfying and rewarding site. Creating usable sites is not easy, and much of the knowledge comes from experience. Learn what things from other sites annoy you and avoid them. Test your site on real people and watch as they use it.

#### Accessibility

Accessibility affects many people, not only those with disabilities. Assistive technology is any extra piece of computer equipment or hardware that helps a person interact with their computer more successfully.







- W3C (2017, November 11). _**What does a good web page need?**_. Retrieved from [here](https://www.w3.org/wiki/What_does_a_good_web_page_need).
- Raggett, D. (2005, May 25). _**Getting Started with HTML**_. Retrieved from [here](http://www.w3.org/MarkUp/Guide/).
- _**Getting Started**_. (n.d.) Retrieved from [here](http://www.htmldog.com/guides/html/beginner/gettingstarted/).
- _**Lesson 3: Elements and tags**_. (n.d.). Retrieved from [here](http://html.net/tutorials/html/lesson3.php).
- Krossing, D. (2017, June 22). _**1: How to get started with HTML & CSS | HTML tutorial for beginners | Learn HTML and CSS | mmtuts**_. [Video]. YouTube. Retrieved from [here](https://youtu.be/pm5OVxpul48).
- Wright, J. (2010, November 10). _**Learn HTML in 12 minutes**_. [Video]. YouTube. Retrieved from [here](https://youtu.be/bWPMSSsVdPk).
- Web Dev Simplified. (2018, August 22). _**Learn CSS in 20 minutes**_ [Video]. YouTube. Retrieved from [here](https://youtu.be/1PnVor36_40).
- Locke, M. (2010, January 22). _**Website Design Tips: The Standard Website Layout**_ [Video]. Retrieved from [here](https://youtu.be/3meSOXY9uGA).
- Locke, M. (2010, February 5). Color Selection and Web Design [Video]. Retrieved from [here](https://youtu.be/Ukl9yecLxIQ).









## Advanced HTML

**References:**

- w3schools. (n.d.). _**HTML Tutorial**_. Retrieved from [here](https://www.w3schools.com/html/default.asp).
- Morris, J. (2018, July 30). HTML tags, attributes and elements [Video]. YouTube. Retrieved from [here](https://youtu.be/vNOyRZIkC7o).
- LearnCode.academy. (2013, October 21). Web development tutorial for beginners (#1) - How to build webpages with HTML, CSS, Javascript. YouTube. Retrieved from [here](https://youtu.be/3JluqTojuME).


## CSS: Cascading Styling Sheets

**References:**

- MDN Contributors. (2019, December 4). _**CSS basics**_. Retrieved from [here](https://developer.mozilla.org/en-US/docs/Learn/Getting_started_with_the_web/CSS_basics).
- MDN Contributors. (2020. January 9). _**Inheritance and Cascade**_. Retrieved from [here](https://developer.mozilla.org/en-US/docs/Learn/CSS).
- MDN Contributors. (2021, April 23). _**Fundamental text and font styling**_. Retrieved from [here](https://developer.mozilla.org/en-US/docs/Learn/CSS/Styling_text/Fundamentals).
- MDN Contributors. (2020, February 20). _**CSS Building Blocks**_. Retrieved from [here](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks).
- Khan Academy. (2014, November 25). _**CSS inheritance | Intro to HTML/CSS: Making webpages | Computer Programming | Khan Academy**_ [Video]. YouTube. Retrieved from [here](https://youtu.be/PhyF-HdbV8M).
- Codeacademy. _**Learn HTML**_. Retrieved from [here](https://www.codecademy.com/learn/learn-html).
- Codeacademy. _**Learn CSS**_. Retrieved from [here](https://www.codecademy.com/learn/learn-css).


## JavaScript

**References:**

- MDN Contributors. (2024, February 4). Learn web development, Retrieved from [here](https://developer.mozilla.org/en-US/docs/Learn).
- MDN Contributors. (2024, January 24). What is JavaScript? Retrieved from [here](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/First_steps/What_is_JavaScript).
- Hack Reactor. (2016, March 11). Say what? Introduction to Javascript [Video]. YouTube. Retrieved from [here](https://youtu.be/Osrjn8FGKMM).
- Codeacademy. _**Learn JavaScript: Introduction**_. Retrieved from [here](https://www.codecademy.com/learn/introduction-to-javascript).
- Codeacademy. _**Learn JavaScript: Functions**_. Retrieved from [here](https://www.codecademy.com/learn/introduction-to-javascript).
- w3schools. _**JavaScript functions**_. Retrieved from [here](https://www.w3schools.com/js/js_functions.asp).

## XML

**References:**

- w3schools. (n.d.). _**XML tutorial**_. Retrieved from [here](http://www.w3schools.com/xml/default.asp).
- Banas, D. (2010, May 9). _**Learn XML tutorial**_ [Video]. Retrieved from [here](https://youtu.be/qgZVAznwX38).

## Server side programming with PHP

**References:**

- Achour, M., Betz, F., et. al. (2020, February 2). _**PHP Manuel: Getting started - Introduction**_. Retrieved from [here](http://php.net/manual/en/introduction.php).
- W3Schools. (n.d.). _**PHP introduction**_. Retrieved from [here](http://www.w3schools.com/php/php_intro.asp) (complete the introductory tutorial on PHP).
- LinkedIn Learning. (2014, July 29). _**Web technology tutorial: Server-side scripting | lynda.com**_ [Video]. YouTube. Retrieved from [here](https://youtu.be/JnCLmLO9LhA).
- W3Schools. (n.d.) _**PHP tutorial**. Retrieved from [here](https://www.w3schools.com/php/) (complete the PHP tutorial).

## Introduction to Mobile Web

**References:**

- W3C. (2016). _**Mobile Web**_. Retrieved from [here](http://www.w3.org/standards/webdesign/mobilweb).
- Smashing Magazine (2012, July 2). _**Guidelines For Mobile Web development**_. Retrieved from [here](https://www.smashingmagazine.com/2012/07/guidelines-for-mobile-web-development/).
- W3Schools. (n.d.). _**JQuery tutorial**_. Retrieved from [here](http://www.w3schools.com/jquerymobile/default.asp).
- Digital Garage. (2019, January 14). _**Understanding mobile web and mobile apps**_ [Video]. YouTube. Retrieved from [here](https://youtu.be/w4_iBMnFKk4).




