---
layout: post
title: android - fade out button
---

I got this tip from a wonderful
[presentation](http://www.youtube.com/watch?v=jF6Ad4GYjRU) by Eric Burke
of square but it works so well I needed to share it.








Android has no standard depressed animation for
[ImageButton](http://developer.android.com/reference/android/widget/ImageButton.html)'s
so it requires a bit of hacking around to get a similar effect. This can
also be used to disable a button (in conjunction with
setClickable(false))










First we need to create an
[AlphaAnimation](http://developer.android.com/reference/android/view/animation/AlphaAnimation.html) for
our prefered opacity (there is no setAlpha on a view on android versions
below 2.3)










    /**
         * create a 1 second alpha animation to disable a button
         * @return
         */
        private Animation disabledAnimation() {
            Animation disabledAnim = new AlphaAnimation(0.5f, 0.5f);
            disabledAnim.setDuration(1);
            disabledAnim.setFillEnabled(true);
            disabledAnim.setFillAfter(true);
            return disabledAnim;
        }

Then on the view you want to fade out (either in an OnClickListener or
other) start the animation.










    v.startAnimation(disabledAnimation());

The reason this works is because we have set the animation duration to 





one second and set fill after to true (keeping the last frame of the
animation active after it has finished).















Enjoy :)



 









