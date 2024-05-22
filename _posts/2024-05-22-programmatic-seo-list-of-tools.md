---
layout: post
title: "Programmatic SEO: How to create a list of tools for your niche"
---

Programmatic SEO is all the rage but what is it and can it really bring that delicious SEO juice with minimal effort?

## What is programmatic SEO?

If you haven't heard of programmatic SEO or pSEO then you've probably been living under a rock. If you haven't been living under a rock and you've ever googled `how to connect gmail with google sheets` (or something similar), then you'll see Zapier appears top of the search results with a page seems to match your query perfectly. That's programmatic SEO in action.

![zapier programmatically generated page about gmail and google sheets](/assets/images/pseo/zapier-gmail.png)

Zapier has thousands upon thousands of these pages. Did they write them all by hand, maybe hiring a team of small children from south east asia? No, of course not. They generated them with code using a template.

## Generating a one webpage for each tool in your niche

The following technique will work for a list of anything. It could be a list of products, people, apps etc. If you can list it in a spreadsheet, you can use pSEO on it.

## Step 1: Scrape a list of tools

Here's a list of No-Code website builders I scraped for my site [PriceWell](https://pricewell.com/). I used the [Simplescraper](https://simplescraper.io/) browser extension which makes it easy to point and click on the relevant items a get a CSV of the results. In my case I only had around 25 items so their free plan was enough.

**Note:** You need to scrape all the fields you are going to need for your pSEO page. Have a look at the Zapier example they have `Create integrations between TOOL_1 and TOOL_2 to automate any workflow.` as their title. They need the tool name and a logo for that tool at the minimum.

![1 scrape list of tools](/assets/images/pseo/1-scrape-list-of-tools.png)

## Step 2: Bung it in an Airtable

I exported the results of my scrape as a CSV and imported them into an airtable. Here I have the tool name and a url for their logo. Next I need to actually download the logo to use it in my template

![2 basic airtable](/assets/images/pseo/2-basic-airtable.png)

## Step 3: Download the logo

I used an airtable script here to loop through each row and make a connection to the url to download the image into a new cell. At the time scripts were a free feature of airtable but they may have become a paid feature since. If you want to do this for free you might need to do it manually (depending on how many results you have) or run a script on your machine to use the airtable API to upload each image to a cell.

![3 airtable script dl logo](/assets/images/pseo/3-airtable-script-dl-logo.png)

and here are the results

![4 airtable logo downloaded](/assets/images/pseo/4-airtable-logo-downloaded.png)

## Step 4: Generate a unique header image

Using the wonderful Bannerbear we can generate a unique image for each tool. I created a template that takes the tool logo and name and generates a nice looking header image. I then used the Bannerbear airtable integration to apply this to each row in the airtable and upload the result back to airtable.

![5 bannerbear apply template](/assets/images/pseo/5-bannerbear-apply-template.png)

Running the automation is as simple as clicking "run".

![6 bannerbear complete](/assets/images/pseo/6-bannerbear-complete.png)

And here are the results in the airtable (I actually have two programmatic pages for each tool so I've got two image columns and two different Bannerbear templates).

![7 airtable bannerbear result](/assets/images/pseo/7-airtable-bannerbear-result.png)

## Step 5: Generate the webpages

The [PriceWell](https://pricewell.com) website uses markdown so I wrote a template for the webpage for each tool in markdown and found [Pandoc](https://pandoc.org/) and a nice Python script that would read the CSV (exported from airtable) and merge the variables into the template.

![8 pandoc merge](/assets/images/pseo/8-pandoc-merge.png)

Here's what my Python script ended up looking like.

![9 python script](/assets/images/pseo/9-python-script.png)

Generating 25+ webpages is now as simple as running the script.

![10 python script run](/assets/images/pseo/10-python-script-run.png)

## Step 6: Publish the results

Now all we need to do is publish the [result](https://www.pricewell.com/versoly-stripe-subscription/). A lot of each page is the same because the solution works the same way for each tool.

![11 result](/assets/images/pseo/11-result.png)

**Note:** Google won't automatically index your pages so you might want to head to the Google Search Console and submit each page (or [this script](https://github.com/goenning/google-indexing-script) will do this for you).
