* Course notes for: https://frontendmasters.com/courses/web-perf/
## Part 1
* Correlation != causation
* There is no one metric which causes the other
* Google says performance is important. As it owns a big portion of the internet we want our site to feature in their search results better.
* It will rank you on performance
* Angry and frustrated users do not stick around for too long.
* Perceived peformance/ Wait time feels subjective to the user
* How much time we spend depends on our expectation of how much time it should take and what we do while we are waiting
* This is called Perceived Performance
* Bored time feels slower
* Anxious wait time feels slower like a lab test/loan application
* Unexplained wait time feels slower.
* Uncertain waits also feel slower when we dont know how long it will take.
* People will wait for something valuable
* Older way to measure performance was Page Load, from start till the tim page has been completely loaded.
* To counter this some sites would have the load event fire right away and then do lazy loading for a longer amount of time. This gave them more performance rank but was not solving the issue.
* The new web vitals:
* FCP: Time between when user clicks the URL and when the first meaningful content enters the Page
* Not just a div but something meaningful
* Time until when the user sees an indication that the page is loading. 
* That the click registered
* **Respond quick**
* LCP: Largest Contentful Paint 
* This is measured in Pixels. the Length and breadth of the largest contentful area that was painted
* When does the user think that the site is almost ready
* Mostly it is the images that take the largest amount of time to paint
* **Get to the point**
* CLS: Cumulative Layout Shift
* CLS is the total number of times some content shifts through the entire time user is on the page as async loading of content is also ongoing.
* Say a top banner that pushes the whole page down
* **Dont move stuff after you have shown it**
* How does this affect a Client Side rendered app ? 
* If a click or a page load will move a whole lot of content again then that adds to CLS
* FID: First Input Delay
* More conceptual about what the browser needs to be doing and not so much about client interaction
* If there is a whole lot of deferes JS that the browser is running even when the user clicks on a button say then there will be a delay as the Browser is still busy
* Browser is too busy parsing and compiling the JS
* This is measured only when the user first interacts.
* User thought the page was ready and wanted to perform some action but the browser wasnt done.
* Time delay between user's first click and execution of the application code
* **dont load too much**
* for Lighthouse best to undock the developer options window in Chrome to maintain healthy Window Size
* Report is relative to your machine and dependent on Window size
* Keep Chrome in foreground and not in background. As that might result in Chrome stopping JS etc
* Where should we measure performance from ? There are services which peridically tell us about the performance of our application like NewRelic etc
* There is also something called Field Data, Capturing data from users who are using the site from the network they use it one. These are called RUM tools like RequestMetrics. These are much more accurate and very noisy as well. Because it will capture some data not very relevant
* Learn to differentiate Noise data from Signal data
* Chrome captures field data from all devices and pushes it to google. [here is how we can access it](https://crux-compare.netlify.app) has this data tabulated 
* Crux data isnt perfect either because it pulls data from users devices and averages them
* but field data is from user's device. how well the site tailors itself to that user on a limited slow device is what Field data tells us
* Field data depends on browser so only Chrome and Edge send this data right now
* Also chrome on iOS is a Chrome wrapper on Safari Engine so that will not send data either
* Hence the data might have a positive bias on desktop towards Chrome user
* It will have a negative bias for Phones as it wil be from Android, they are quite a bit slower on web applications than iOS users
* Mobile data will be skewed worse then
* Mac data will have Safari and will be underreported as well.
* Chrome extensions always impact the performance of a web page
  
## Part 2

* Speed of loading of a site will matter only when your site is 20% faster than your competitor only then will people notice it
* in order to capture live data we are going to use `window.performance` API
* An Entry in the performance API describes on Network event, one session etc
* performace data is based on events and is raw numbers on how a certain event start and stop
* `performanceObserver` is used to add a listener for specfic events
* ### How to improver performance?
* **Do Fewer things**
* Improving FCP means respond quick
* So a Quick Server delivering Small documents over a Short hop network connection
* On Server side ensure server is sized correctly, enough overhead, minimize processing that needs to be done to deliver the content, and the bandwidth to the service needs to be as Big as possible in order to handle all the requests coming in.
* On the Document side ensure the document is properly compressed and less size, small payload to be as effective on UI as possible
* On network side we can have CDN or Edge networks
* Improving LCP means getting the right bytes out the door first
* Defer resources only till the point it is needed
* Images are a big part so what can we do to crunch the image beyond just compression
* Cut as much of overhard out from the HTTP request
* Maybe a JS file or a lower image is not needed etc
* one way might be `<script async src=...></script>`
* async will tell browsert to download JS when you need it or get to it
* Just the order of download changes with `async`
* Other one can be `defer` Execute it later, it will not block this
* for images we can use `loading="lazy"`
* `InterectionObserver` is used to check whether an element is visible.
* We can use a lazyLoader script that inject `data` atrribute into a component when it becomes visible
* This is a dynamic injecting of attribute when needed
* Optimizing Images: We can use srcset for img which will have a set of images that can be used based on viewport sizes and then uses `sizes` attr to pick the right one.
* We can also have some image optimizer which crunches images during build time.
* Using responsive img attrs will help in understanding optimzations much better
* Now to reduce overhead:
* Normally a request consists of `DNS->TCP->SSL->REQ->RESP->PROCESSING`
* One of the best things is to use HTTP2 as it can reuse connections do we cut out the DNS TCP and SSL part from above.
* Not all servers work with HTTP/2 yet
* Caching is another way to be able to do it but it can only happen on second requests for the same resource.
* `cache-control`, `expires` and `etag` are the attrs we use for caching
* Some assets can be pre-fetched like css `rel="preconnect"` can help us with this
* The above will connect with google and fetch the resource later
* Some assets  can use `rel="preload"` which will pre load the asset
* We can also load a smaller quality image and then a high quality image. This is overall a slow approach as this means more data. the FCP and LCP works and user is able to see something on the site
* Reduce CLS: CLS before LCP is fine. A User can live with it thinking okay the site is still loading
* But if it happens after, LCP makes the user angry
* Improving CLS can be by giving layout hints say `height` or `width` to an element. So that much space is always reserved.
* If images or resources are asynch loading in the page they will keep moving and pushing components around which might impact CLS score again.
* Here is where adding layout hints like above will help
* First Input Delay: time delay between user's first click and execution of application code.
* Dont load too much
* This is also realted to LCP, if we have all these JS asynch defered before LCP then we are forgiven
* Mostly anxious users like for medical results will be less forgiving for a wait