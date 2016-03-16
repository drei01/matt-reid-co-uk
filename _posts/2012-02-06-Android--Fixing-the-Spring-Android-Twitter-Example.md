---
layout: post
title: Android- Fixing the Spring Android Twitter Example
---

getWebView().setWebViewClient(new TwitterOAuthWebViewClient());I have
been using the excellent Spring Android for interaction with an api for
an app I am developing at work. The
[spring-android-showcase](https://github.com/SpringSource/spring-android-samples) project
has been excellent in helping me breeze through development.








I easily implemented Facebook connections using the
[FacebookWebOAuthActivity](https://github.com/SpringSource/spring-android-samples/blob/master/spring-android-showcase/client/src/org/springframework/android/showcase/social/facebook/FacebookWebOAuthActivity.java)










One issue I found when implementing the
[TwitterWebOAuthActivity](https://github.com/SpringSource/spring-android-samples/blob/master/spring-android-showcase/client/src/org/springframework/android/showcase/social/twitter/TwitterWebOAuthActivity.java) was
that it wasn"t finding the access token at the end of the OAuth process.










Using the facebook example I could see that it was using a webclient to
detect the access token when a new page was loaded in the webview, so I
implemented a similar process for twitter.










Simply add the following to TwitterWebOAuthActivity








    private class TwitterOAuthWebViewClient extends WebViewClient {
            @Override
            public void onPageStarted(WebView view, String url, Bitmap favicon) {
                Uri uri = Uri.parse(url);
                String oauthVerifier = uri.getQueryParameter("oauth_verifier");

                if (oauthVerifier != null) {
                    getWebView().clearView();
                    new TwitterPostConnectTask().execute(oauthVerifier);
                }
            }
        }



and the following to the onStart method



    getWebView().setWebViewClient(new TwitterOAuthWebViewClient());



I will endeavour to submit a pull request to the project to fix this
issue



 









