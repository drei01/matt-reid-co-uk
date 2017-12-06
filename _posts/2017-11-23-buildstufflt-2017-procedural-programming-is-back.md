---
layout: post
title: BuildStuff Lithuania 2017
---
I recently attended [BuildStuff](http://buildstuff.lt/) for the first time thanks to my company [Small Improvements](https://www.small-improvements.com). I can't remember the last time I came back from a conference so invigorated and full of learning. I wrote a post about it over on the Small Improvements [tech blog](https://tech.small-improvements.com/2017/12/05/5-lessons-from-build-stuff-2017/) but here's something that didn't make it into that post.

#### Procedural programming is making a comeback

This is what [Kevlin Henney](https://twitter.com/KevlinHenney) argued during his well received talk. Kevlin is a fantastically clever guy and his talks are always entertaining as well as thought provoking. Although the talk was mostly a history of procedural programming languages (everyone in the audience was geeking out over Algol68), there were a couple of takeaways that stuck in my mind.

Guard clauses can be misused, the procedural if-else block is actually more readable.

Take a look at this

```
public Integer add(Integer a, Integer b){
    if(a==null && b==null) {
        return null;
    }

    if(a==null) {
        return b;
    }

    if(b==null) {
        return a;
    }

    return a + b;
}
```

Now collapse the if statements

```
    if(a==null && b==null)...

    if(a==null)...

    if(b==null)...

    return a + b;
```
It's hard to surmise the logic from here as we don't know whether the `if` statements will mutate the state of `a` or `b`.

Consider the alternative

```
public Integer add(Integer a, Integer b){
    if(a==null && b==null) {
        return null;
    } else if(a==null) {
        return b;
    } else if(b==null) {
        return a;
    } else {
        return a + b;
    }
}
```

This is a lot easier to reason about even when we collapse the if-else blocks

```
    if(a==null && b==null)...
    else if(a==null)...
    else if(b==null)...
    else ...
```

By adding the `else` clauses we tell the reader that we only fall into the logic if none of the other clauses are met.