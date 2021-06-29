# Web Scraping

*Web scraping* is the term for using a program to download and process content from the web

Modules in this Chapter:
* `webbrowser` -- comes with Python and opens a browser to a specific page
* `requests` -- downloads files and web pages from the internet
* `bs4` -- parses HTML, the format that web pages are written in
* `selenium` -- launches and controls (fill in forms/simulate mouse clicks) a web browser 


## The WebBrowser module

The `webbrowser` module's `open()` function can launch a new browser to a specified URL:
```python
import webbrowser
webbrowser.open('https://github.com/gestylinaga/')
```
...That's pretty much it, that's what the `webbrowser` does

### Ideas for Similar Programs

As long as you have a URL, the `webbrowser` module lets users cut out the step of opening the 
browser and directing themselves to a website

Try a Program To:
* Open all links on a page in separate browser tabs
* Open the browser to the URL for your local weather
* Open several social network sites that you regularly check


## Downloading Files from the Web with the Requests Module

The `requests` module lets you easily download files from the web without having to worry about 
complicated issues like:
* Network errors
* Connection problems
* Data compression

Note that `requests` must be installed with `pip`:
```bash
pip3 install requests
```
and to use it in scripts:
```python
import requests
```

### Downloading a Web Page with the requests.get() Function

### Checking for Errors


## Saving Downloaded Files to the Hard Drive

> Unicode Encodings


## HTML

### Resources for Learning HTML

### A Quick Refresher

### Viewing the Source HTML of a Web Page

### Opening Your Browser's Developer Tools

> Don't use Regular Expressions to Parse HTML

### Using the Developer Tools to Find HTML Elements


## Parsing HTML with the Bs4 Module

### Creating a BeautifulSoup Object from HTML

### Finding an Element with the select() Method

### Getting Data from an Element's Attributes


## Controlling the Browser with the Selenium Module

### Starting a selenium-Controlled Browser

### Finding Elements on the Page

### Clicking the Page

### Filling Out and Submitting Forms

### Sending Special Keys

### Clicking Browser Buttons

### More Information on Selenium


## Summary


## Practice Questions
1. Briefly describe the differences between the `webbrowser`, `requests`, `bs4`, and `selenium` modules.
2. What type of object is returned by `requests.get()`? How can you access the downloaded content as 
a string value?
3. What `requests` method checks that the download worked?
4. How can you get the HTTP status code of a `requests` response?
5. How do you save a `requests` response to a file?
6. What is the keyboard shortcut for opening a browser’s developer tools?
7. How can you view (in the developer tools) the HTML of a specific element on a web page?
8. What is the CSS selector string that would find the element with an `id` attribute of `main`?
9. What is the CSS selector string that would find the elements with a CSS class of `highlight`?
10. What is the CSS selector string that would find all the `<div>` elements inside another `<div>` element?
11. What is the CSS selector string that would find the `<button>` element with a value attribute 
set to favorite?
12. Say you have a Beautiful Soup `Tag` object stored in the variable spam for the element 
`<div>Hello, world!</div>`. How could you get a string `'Hello, world!'` from the `Tag` object?
13. How would you store all the attributes of a Beautiful Soup `Tag` object in a variable named 
`linkElem`?
14. Running `import selenium` doesn’t work. How do you properly import the `selenium` module?
15. What’s the difference between the `find_element_*` and `find_elements_*` methods?
16. What methods do Selenium’s `WebElement` objects have for simulating mouse clicks and keyboard keys?
17. You could call `send_keys(Keys.ENTER)` on the Submit button’s `WebElement` object, but what is 
an easier way to submit a form with `selenium`?
18. How can you simulate clicking a browser’s Forward, Back, and Refresh buttons with `selenium`?


---
[back to Automate the Boring Stuff with Python main page](atbswp.md)

[back to Index/Table of Contents](index.md)
