
# INF 100 - Information in the 21st Century - Data Exploration Exercise using Twitter APIs

> This data exploration exercise has been converted to a IPython Notebook format
so that you can interactively run the example code as you read through the steps
in the exercise. The purpose of this exercise is to show the real power of the
Python programming language to interact with Twitter APIs.

> This exercise has been build using references from the awesome book [Mining
the Social Web (2nd Edition)](http://bit.ly/135dHfs) written by Matthew A.
Russell.

> How can you tap into the wealth of social web data that exists in various
streams such as Twitter, Facebook, Tumblr, Instagram, Pinterest, Reddit and so
on? This exercise would help you discover who's making connections with whom,
what they are talking about, and where they are located?

> By the end of the exercise, you would learn how to acquire, analyze and
summarize data from Twitter for your assigned country.

> This notebook assumes that you are reading along with the book and have the
context of having fun running sample code

## Copyright and Licensing

> This notebook has been build using the [Simplified BSD
License](https://github.com/ptwobrussell/Mining-the-Social-Web-2nd-
Edition/blob/master/LICENSE.txt) that has been provided by the author of the
book. You are free to reference or adapt this notebook like we did as long you
follow the governance for the license terms.

## Overview

In this exercise, we will learn in a fun way the process of getting started with
a minimal development environment using simple python commands, survey Twitter's
API and gather some analytical insights from tweets. Topics that you would gain
from this data exploration exercise include:

* How to make request to Twitter using APIs
* Find trending tweet topics for World and US
* Find unique Where on Earth Identifier for your assigned country
* Find trending tweet topics for your assigned country

### What is Twitter?

Twitter is as a microblogging service that allows people to communicate with
short, 140-character messages that roughly correspond to thoughts or ideas.
Think twitter as a high-speed global text-messaging service. It allows
communication at light speed.

If you are curious about how many of us over the world using twitter, then over
[640 million curious people are registered, with over 115 million of them
actively engaging](http://bit.ly/1a1kNXR).

Wow, that's a lot of people generating messages all over the world!



### Exploring Twitter's API

Twitter is described as a real-time, highly social microblogging service that
allows users to post short status updates, called **tweets**, that appear on
timelines.

Tweets may include one or more **entities** in their **140 characters** of
**content and reference** one or more places that map to **locations** in the
real world.

An understanding of **users**, **tweets**, and **timelines** is required to
effectively use Twitter API.

#### What are Tweets?

Tweets are the essence of Twitter. They are 140 characters of text content
associated with a user's status update. In addition to the textual content of a
tweet itself, two additional pieces of metadata come along with it: **entities**
and **places**.

> Tweet entities are essentially the user mentions, hashtags, URLs, and media
that may be associated with a tweet

> places are locations in the real world that may be attached to a tweet.

**Note**: A place may be the actual location in which a tweet was authored, but
it might also be a reference to the place described in a tweet.

##### Sample Tweet

> @ptwobrussell is writing @SocialWebMining, 2nd Ed. from his home office in
Franklin, TN. Be #social: http://on.fb.me/16WJAf9

In the sample tweet from the author of the referenced book used for this
exercise, we see that the tweet is 124 characters long.

Let's identify how many **entities** exist in the above tweet.

We see the following entities:

* @ptwobrussell and @SocialWebMining (user mentions)
* hashtag social (hashtag is known by having a pound sign in front of the
metadata or keyword)
* http://on.fb.me/16WJAf9 (URL)

**Note**: Although there is a place called Franklin, Tennessee that's explicitly
mentioned in the tweet, the **places** metadata associated with the tweet might
include the location in which the tweet was authored, which may or may not be
Franklin, Tennessee.



### Let's start playing

Since Twitter provides API's (Application Programming Interfaces) in order to
interact with its data, we need to follow twitter's strict instructions to make
a connection in order to query data.

We need a Twitter account, which is required for API access. Twitter provides
liberal [terms of service](http://bit.ly/1a1kWKB), [API
Documentation](http://bit.ly/1a1kSKQ), and [Developer Rules of the
Road](http://bit.ly/1a1kX1a).



####Step 1: Create a Twitter account

In order to create a twitter account, we would go to **www.twitter.com** and
sign-up for a new account. For this exercise, a pre-defined twitter account has
been created.

####Step 2: Create an application on Twitter

Before you make any API requests to Twitter, we would need to create/register an
application at [Twitter Apps](http://bit.ly/1a1kYlS). Creating an application is
the standard way for developers or anyone querying data to gain API access and
for Twitter to monitor and interact with us. We would only need read-access to
the APIs.

We have used the newly created account to register an application with Twitter
and in return Twitter provides a standardized means to access their API.

After successful registration, Twitter provides with 4 key pieces of information
that you would need to gain access to the API. They are:

1. Consumer Key
2. Consumer Secret
3. Access Token
4. Access Secret

The below four credential values are provided when we successfully register the
application. Do not forget to write it down, since we will be soon using it in
our data exploration exercise.

| Key          | Value                     |
| -------------|:-------------------------:|
| Consumer Key | 8QC4PwQMNffBkFmt6NrvzroEZ |
| Consumer Secret|s4CBIlsPegpCd5KB1YTpiiBxZnXIFKbsY4ntkXYlbURtC5i86K|
| Access Token | 2806182539-PvJSJoPPrKzmkv8oRQJcLmES7kFxCidrYiAYieE |
| Access Token Secret | 2DCajCymQSETPskrA7cYd1fyX9LnlQxbegRVf0T6YAnYD |

####Step 3: Authorizing an application to access Twitter account data


    import twitter
    
    # Provide values from the table above and replace the 
    # empty string values that are defined as placeholders.
    
    
    CONSUMER_KEY = ''
    CONSUMER_SECRET = ''
    OAUTH_TOKEN = ''
    OAUTH_TOKEN_SECRET = ''
    
    auth = twitter.oauth.OAuth(OAUTH_TOKEN, OAUTH_TOKEN_SECRET,
                               CONSUMER_KEY, CONSUMER_SECRET)
    
    twitter_api = twitter.Twitter(auth=auth)
    
    # Nothing to see by displaying twitter_api except that it's now a
    # defined variable
    
    print twitter_api

> What is this In [n]:?

>> Anytime in this notebook, you see a cell with In [n] where 'n' is a
sequential number, it is the placeholder where you will run python code in this
notebook. The above code snippet required you to fill in the 4 placeholder
variables with the values that were posted in a table.

>> * CONSUMER_KEY = '8QC4PwQMNffBkFmt6NrvzroEZ'
>> * CONSUMER_SECRET = 's4CBIlsPegpCd5KB1YTpiiBxZnXIFKbsY4ntkXYlbURtC5i86K'
>> * OAUTH_TOKEN = '2806182539-PvJSJoPPrKzmkv8oRQJcLmES7kFxCidrYiAYieE'
>> * OAUTH_TOKEN_SECRET = '2DCajCymQSETPskrA7cYd1fyX9LnlQxbegRVf0T6YAnYD'

>>>After filling in the placeholder values, to execute the python code, (select
the cell by highlighting it) and then either:

>>> 1. Press SHIFT + ENTER simultaneously OR
>>> 2. Click the "Run Cell" icon (looks above for something like this > ) OR
>>> 3. Select from the top menu "Cell" and then from the drop list select "Run"

**Note**:

If we successfully connected to Twitter API, then we should get back a message
in the following format:

<code><code class="literal">&lt;twitter.api.Twitter object at
0x39d9b50&gt;</code></code>

####Step 4: Exploring Trending Topics

With an authorized connection in place, we can now issue a request to Twitter to
retrieve data. The next step demonstrates how to ask Twitter for the topics that
are currently trending worldwide. The API can be easily modified to restrict the
topics to specific locales. The means for constraining queries is via [Yahoo!
GeoPlanet's](https://developer.yahoo.com/geo/geoplanet/) Where On Earth (WOE) ID
system, which is an API unto itself that aims to provide a way to map a unique
identifier to any named place on Earth (or even in a virtual world).

* The Yahoo! Where On Earth ID for the entire world is **1**.
* The Yahoo! Where On Earth ID for US is **23424977**

#####Exercise 1.1 Retrieving Trends


    # The Yahoo! Where On Earth ID for the entire world is 1.
    # See https://dev.twitter.com/docs/api/1.1/get/trends/place and
    # http://developer.yahoo.com/geo/geoplanet/
    
    WORLD_WOE_ID = 1
    US_WOE_ID = 23424977
    
    # Prefix ID with the underscore for query string parameterization.
    # Without the underscore, the twitter package appends the ID value
    # to the URL itself as a special case keyword argument.
    
    world_trends = twitter_api.trends.place(_id=WORLD_WOE_ID)
    us_trends = twitter_api.trends.place(_id=US_WOE_ID)
    
    print world_trends
    print
    print us_trends

You should see a semireadable response that is a list of Python
      dictionaries or collections from the API (as opposed to any kind of error
message),
      such as the following truncated results, before proceeding further. (In
      just a moment, we'll reformat the response to be more easily
      readable.) **Don't worry if it is not understandable as long as it is not
an error message!**

<code>[{u'created\_at': u'2013-03-27T11:50:40Z', u'trends': [{u'url':
u'http://twitter.com/search?q=%23MentionSomeoneImportantForYou'...</code>

<blockquote><div><strong>Note:</strong></div><p>The developer documentation
states that the results of a Trends
        API query are updated only once every five minutes, so it's not a
        judicious use of your efforts or API requests to ask for results more
        often than that.</p></blockquote>

As we saw earlier, the semi-readable output from Exercise 1.1 is printed out in
native Python data format. Unless we write Python code to beautify the printed
output, this notebook will not, so in order to force the notebook to a nicer
display, we will use the built-in JSON format.

<blockquote><div><strong>Note:</strong></div><p><a class="ulink"
href="http://bit.ly/1a1l2lJ" target="\_top">JSON</a> is a data
        exchange format that you will encounter on a regular
        basis. In a nutshell, JSON provides a way to arbitrarily store maps,
        lists, primitives such as numbers and strings, and combinations
        thereof. In other words, you can theoretically model just about
        anything with JSON should you desire to do so.</p></blockquote>

In short, ignore the data jargon and remember the term **JSON**. It will make
the exercise 1.1 output look more meaningful and prettier!

#####Exercise 1.2 Displaying API Responses as pretty-printed JSON


    import json
    
    print json.dumps(world_trends, indent=1)
    print
    print json.dumps(us_trends, indent=1)

An abbreviated sample response from the Trends API produced with
      <code class="literal">json.dumps</code> would look like the
      following:

<pre>[
 {
  "created\_at": "2013-03-27T11:50:40Z",
  "trends": [
   {
    "url": "http://twitter.com/search?q=%23MentionSomeoneImportantForYou",
    "query": "%23MentionSomeoneImportantForYou",
    "name": "\#MentionSomeoneImportantForYou",
    "promoted\_content": null,
    "events": null
   },
   ...
  ]
 }
]</pre>

#####Exercise 1.3 Explore Trends for your assigned country

Now that you have seen how to run trending tweets for the World and the US,
printed them in a pretty format using JSON data format, it is time for you to do
the following:

#####Step 1.3.1

Go to [Yahoo! GeoPlanet's](https://developer.yahoo.com/geo/geoplanet/) and
follow the instructions as listed below:

1. Get an Application ID.
2. Fire up a web browser and explore the API.
3. Get your unique Where On Earth ID based on your assigned country.

> You would need to create an yahoo account, then create a new application by
providing details such as Application Name, a brief description of the
application and a home page URL. When asked for Access Scopes, choose **"This
app will only access public APIs, Web Services, or RSS feeds"**. Provide
Application Owner Name and Email address (**your name and yahoo account id** you
just created)

Your Application Name and brief description could be specific to the INF 100
exercise you are doing to data mine twitter. Provide your public page (Facebook,
LinkedIn, Twitter or any other web page that you have as a web presence) for the
Application URL since you are not creating a specific application, but using it
for this exercise.

Once you have successfully created the application, you would be asked to agree
to the Terms of Condition and provided with a unique application ID.

[Yahoo Application Id Screenshot
Sample](https://s3.amazonaws.com/sunycci/Images/YahooGeoPlanetReg.png "GeoPlanet
Application ID")

The Application ID is a long 68 character string which you see under **Consumer
Key**. Make sure to highlight it and then copy it for the next step.

Open up a web browser of your choice and type the following API request URL:

http://where.yahooapis.com/v1/countries/NA?appid=[yourappidhere]

Replace [yourappidhere] with your unique Yahoo Application Id

Sample ID: dj8yJmk9UFhzTVVBUjFlRDF1JmQ9WVdrOVVrOWhSM3B0TkhNbWNHblzNQS0tJnM9Y29uc
3VtZXJzZWNyZXQmeD1iZQ--

In order to retrieve the WOE (Where On Earth), now paste the url

http://where.yahooapis.com/v1/countries/NA?appid=dj8yJmk9UFhzTVVBUjFlRDF1JmQ9WVd
rOVVrOWhSM3B0TkhNbWNHblzNQS0tJnM9Y29uc3VtZXJzZWNyZXQmeD1iZQ--

**Note**: For security reasons, I have modified the unique application id, but
it would return results for your application Id.

Note down your assigned country unique WOE Id



####Exercise 1.4: Repeat exercises 1.1 and 1.2 with your assigned country

Now that you have your assigned country **Where On Earth Unique Id**, follow
these instructions to generate new output:

#####Step 1.4.1

Go to Exercise 1.1 and Replace the US_WOE_ID = 23424977 to US_WOE_ID = [your
assigned country WOE ID].

**Note** Don't worry that the placeholder variable is called US_WOE_ID. It is
irrelevent, we can call it anything, hence no effort to change the placeholder
name.

After filling in the placeholder values, to execute the python code, (select the
cell by highlighting it) and then either:

1. Press SHIFT + ENTER simultaneously OR
2. Click the "Run Cell" icon (looks above for something like this > ) OR
3. Select from the top menu "Cell" and then from the drop list select "Run"

#####Step 1.4.2

Copy the output from the IPython notebook into a Word Document with the document
title named: **"FirstName_LastName-INF100X-MiningTwitterTrendsfor[assigned
country]**. Reference the Exercise 1.4 and the step 1.4.1 before pasting output
from this notebook.

e.g. John_Doe-INF100X-MiningTwitterTrendsforSingapore.docx


#####Step 1.4.3

Go to Exercise 1.2 and Replace the US_WOE_ID = 23424977 to US_WOE_ID = [your
assigned country WOE ID].

**Note** Don't worry that the placeholder variable is called US_WOE_ID. It is
irrelevent, we can call it anything, hence no effort to change the placeholder
name.

After filling in the placeholder values, to execute the python code, (select the
cell by highlighting it) and then either:

1. Press SHIFT + ENTER simultaneously OR
2. Click the "Run Cell" icon (looks above for something like this > ) OR
3. Select from the top menu "Cell" and then from the drop list select "Run"

#####Step 1.4.4
Copy the output from the IPython notebook in JSON format into the same Word
document. Reference the Exercise step 1.4.3 before pasting output from this
notebook.

## Final Step

Convert the word document into pdf and upload it to Blackboard.


    
