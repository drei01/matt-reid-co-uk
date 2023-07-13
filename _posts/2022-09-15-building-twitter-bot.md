---
layout: post
title: Building A Twitter Growth Bot in 30 minutes
---

*In this post I build a Twitter growth bot using Node and Google Cloud Functions. This was originally a live twitter thread.*

---

The children are finally asleep. I have an idea for a Twitter growth tool. Follow along here as I [#buildinpublic](https://twitter.com/search?q=#buildinpublic) <img src="https://pbs.twimg.com/tweet_video_thumb/FZQjXOmWAAIj1fZ.jpg" alt="Man with comedy glasses hacking at a computer" height="480" width="480">

💡 Idea  
A bot that automatically tweets once a week as me and tags the 5 accounts with the most replies to my tweets in the last week.  
  
All you have to do to be tagged is to reply to my tweets.

We'll use Google Cloud Scheduler and Cloud Functions  
It took me a while to find a quickstart for cloud functions and typescript 👇🏻  
[github.com/GoogleCloudPla…](https://github.com/GoogleCloudPlatform/functions-framework-nodejs/blob/master/docs/typescript.md)

<img src="https://opengraph.githubassets.com/79138b4e733d2860ecdbdcf723ac488aa1bffcc609dd6cf52a640a4ca4ea8ab8/GoogleCloudPlatform/functions-framework-nodejs" alt="Google Cloud Platform Node Framework" height="300" width="600">
[functions-framework](https://github.com/GoogleCloudPlatform/functions-framework-nodejs/blob/master/docs/typescript.md)

Hello World 👍 
<img src="https://pbs.twimg.com/media/FZQk91vX0AE_j_h.jpg" alt="Web browser with a blank webpage showing Hello, World" height="134" width="539">

I don't have access to Twitter API v2 yet. But I have an old V1 app so let's use that for this experiment.  
  
I'm using this twitter API client  
<img src="https://static.npmjs.com/338e4905a2684ca96e08c7780fc68412.png" alt="NPM logo" height="300" width="600">

[twitter-api-client](https://www.npmjs.com/package/twitter-api-client)

Let's get the last 10 replies to my tweets. <img src="https://pbs.twimg.com/media/FZQwqzEX0AEiKpO.jpg" alt="Code snippet to get last X replies to a Tweet" height="338" width="600">

So we can get the last X replies.  
Now to:  
\- Make sure they aren't over a 7 days old  
\- Collect all the users and count them
<img src="https://pbs.twimg.com/media/FZQw5ZbXkAEypvR.jpg" alt="browser window showing a JSON array of tweets" height="274" width="600">

Well, that seemed to work well.  <img src="https://pbs.twimg.com/media/FZQ63tJWIAkflrJ.jpg" alt="A tweet saying 'My top five Twitter users this week are...'" height="90" width="600">

Now we use Cloud Scheduler to run our function every Friday.
<img src="https://pbs.twimg.com/media/FZRDwX7XgAAOO8M.jpg" alt="A Google Cloud Scheduler configuration form " height="424" width="349">

• • •

*That's the end of the Twitter thread. It was great fun to build this tool and I'm getting great engagement from it each week. If you want more like this, [follow me](https://twitter.com/matthew_reid) on Twitter.*

[Original Twitter Thread](https://twitter.com/Matthew_Reid/status/1554906664515649537)