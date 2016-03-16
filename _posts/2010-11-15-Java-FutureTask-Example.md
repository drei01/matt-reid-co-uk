---
layout: post
title: Java FutureTask Example
---

I spent a while looking for a solid example of futuretask use in java
for my latest android app (more posts on that soon I hope) but I found a
great one
[here](http://stackoverflow.com/questions/536327/is-it-a-good-way-to-use-java-util-concurrent-futuretask)

Here is the code:

``` {.js name="code"}
public void startMyApplication() {
    ExecutorService executor = Executors.newFixedThreadPool(2);
    FuturTask futureOne = new FutureTask(myFirstProcess);
    FuturTask futureTwo = new FutureTask(mySecondProcess);
    executor.execute(futureOne);
    executor.execute(futureTwo);
    while (!(futureOne.isDone() && futureTwo.isDone())) {
        try {
            // I wait until both processes are finished.
            Thread.sleep(1000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
    logger.info("Processing finished");
    executor.shutdown();
    // Do some processing on results
    ...
}
```

 















[Back to top](blog_post.php-id=34.html#content)



-   Tags: [java](search.php-category=java.html),
    [futuretask](search.php-category=futuretask.html),
    [android](search.php-category=android.html),













##### Connect with me {#contact}

[![](images/icons/twitter.png)](http://twitter.com/Matthew_Reid "Twitter")
[![](images/icons/github.png)](http://github.com/drei01 "Github")
[![](images/icons/linkedin.png)](http://linkedin.com/e/fpf/70699506 "Linkedin")
©2016 [matt-reid.co.uk](index.html)


