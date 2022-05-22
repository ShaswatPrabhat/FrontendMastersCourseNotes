https://learn-a11y.netlify.app/
* When we do things right folks across a varied range of spectrum can use and make full use of that site.
* Not just for the disabled but the benefits are for the power users, the testers and code quality as well...
* We are trying to make robust apps which are accesible to all users not a site which detects if a user is disabled and gives them a summary of the site
* More specifically, Web accessibility means that people with disabilities can perceive, understand, navigate, and interact with the Web, and that they can contribute to the Web. 
* Think of different disabilities and internalize them and think how can the app be accessed by each of those and web in general
* Providing a lot of CSS and JS adds a lot of  code that kind of reduces the accessibility of the site
* So its like as we have spent some time in making the web inaccessible so now is the time to make it accessible back
* When you become a senior dev then having a specialization in a particular field might make you more valuable to your company. A11y is one of those fields. It is not that a specialization is always needed but having it helps adding value
* One of the modes of input is keyboard only so thing to note is if my site can achieve say a Form submission with minimum number of Keystrokes.
* Screen Reader just reads out the elements on a page and maps actions then
* ### Curb cut effect:
    Often when we give effort to make our site more accessible to people with disabilities we end up making it more accessible and enjoyable to a whole group of folks beyond the intended audience
* In SDLC best way to integrate A11y is to think of different aspects at different times, sometimes design sometimes development like using the right HTML content use ARIA labels etc
* Screen readers normally are integrated on the OS level
* Aim is to get on par with a mouse user
* There might be some issues specific to a version of the screen reader version but usually folks do not want to upgrade their screen reader software because they might be very comfortable with them
* Alt text is one of the easiest approach to a11y. By default a screen reader will only read an image file's src name but if given an alt text it will read that
* But for a web app where a user can upload photos it can get really tricky. Like IG asks you for alt text to be displayed with the image.
* In cases like above some sites use hasing and it can get pretty rough with that approach.
* In cases where we have say a background image or pattern, then having an empty alt attr will help the screen reader to skip that image while screen reading.
* SEO want keywords in the alt text. Stufing keywords in the alt text is good for SEO but bad for a11y
* We can also have like an image that is hidden from screen readers or an alt text in a div that is hidden from non scren readers with the descriptive text
* Similarly for Aud Vid we need captions. We need captions for any audio video media that is uploaded on a site
* using `<div>` for everything might make it a bit more problematic as we might end up not using sematic HTML which allows us proper a11y feature set
* So say proper user of `<h1>` or `<h2>` tags for headings and nesting as well.
* dont mix CSS with this level of nesting as this will mess up with the screen readers
* So `labels` for form fields are needed as well for example and a simple CSS will work but not work with screen reader
* but the `label` tag can only work with labelable elements not all elements
* In such cases we use `aria-label` property
* We can use a class like this
    ``` css    
          .visuallyhidden {
            position: absolute;
            left: 0;
            top: -500px;
            width: 1px;
            height: 1px;
            overflow: hidden;
          }
    ```
    and then use the same class across a lot of our elements to make the screen reader only visible classes
* ### [Aria on MDN](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA) and [the Aria spec](https://www.w3.org/TR/html-aria/#aria-table)
* `aria-label` and `aria-labelledby` do the exact same thing, they add a label to something. `aria-label` just adds it to inline to the HTML element whereas `aria-labelledby` can be used to externally reference a div tag say.
* Also we can use i10n libs to internationalize these labels and descriptions as well
* ### [Aria role reference](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/ARIA_Techniques)
* Adding roles will help us define the role and ARIA also helps us to define the state like checked autocomplete etc
* Mostly it is setting and removing attrs with JavaScript
* As these are data selectors they can be used in css selectors as well
* `aria-live` is like a state change for the nested HTML element the screen reader will re read it out to the user
* Keyboard shortcuts are like event listeners in your app and trigerring event when some buttons are hit.
* Skip to content will help remove repeating repitions of say nav bar elements to always get to the main content
* We can prepend it to the top of the site and visually hidden
* one thing to remember is to know what kind of tags are tabable and what kind of HTML elements are not tabable
* Sometimes when we need to make a non tabable element tababale we can use `tabindex` attr to do so.
* `document.activeElement` can be used to say cache and element from which a user came from and then focus back on it on action back or action close so that tab order and focus order are also maintained
* Tab trapping means say for a modal we keep track of the first and last tababale element and then add listeners for tab and shift+tab events. Then we can cycle across these elements in order withouth returning the tab to the main content.
* ### Color contrasts and Visually challenged users
* Check contrast in design phase, Chrome has an inbuilt dev tool as well.
* So in case of forms if we are using Red for a failing field and Green for a passing field then it might be challenging for folks with disabilities to fully understand what the error might be. So color should not be the only indicator of information.
* Some label or icon should be used to convey more details
* [NoCoffee](https://addons.mozilla.org/en-US/firefox/addon/nocoffee/) is a nice plugin to be able to check the perception of your site for folks with visual impairments
* Setting language will help with conformance and telling upfront the language of the site as with i10n
* We can also have prefers reduced motion to check our CSS
* Same for prefers color scheme as well
* [Some Tools](https://learn-a11y.netlify.app/tooling/index.html) and [Some accessibility resources](https://learn-a11y.netlify.app/resources/index.html)