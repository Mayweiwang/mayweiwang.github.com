---
layout: post
title: "Data mining on Twitter"
description: ""
category: 
tags: []
---
{% include JB/setup %}
<link href="data:text/css,body%20%7B%0A%20%20background%2Dcolor%3A%20%23fff%3B%0A%20%20margin%3A%201em%20auto%3B%0A%20%20max%2Dwidth%3A%20700px%3B%0A%20%20overflow%3A%20visible%3B%0A%20%20padding%2Dleft%3A%202em%3B%0A%20%20padding%2Dright%3A%202em%3B%0A%20%20font%2Dfamily%3A%20%22Open%20Sans%22%2C%20%22Helvetica%20Neue%22%2C%20Helvetica%2C%20Arial%2C%20sans%2Dserif%3B%0A%20%20font%2Dsize%3A%2014px%3B%0A%20%20line%2Dheight%3A%201%2E35%3B%0A%7D%0A%0A%23header%20%7B%0A%20%20text%2Dalign%3A%20center%3B%0A%7D%0A%0A%23TOC%20%7B%0A%20%20clear%3A%20both%3B%0A%20%20margin%3A%200%200%2010px%2010px%3B%0A%20%20padding%3A%204px%3B%0A%20%20width%3A%20400px%3B%0A%20%20border%3A%201px%20solid%20%23CCCCCC%3B%0A%20%20border%2Dradius%3A%205px%3B%0A%0A%20%20background%2Dcolor%3A%20%23f6f6f6%3B%0A%20%20font%2Dsize%3A%2013px%3B%0A%20%20line%2Dheight%3A%201%2E3%3B%0A%7D%0A%20%20%23TOC%20%2Etoctitle%20%7B%0A%20%20%20%20font%2Dweight%3A%20bold%3B%0A%20%20%20%20font%2Dsize%3A%2015px%3B%0A%20%20%20%20margin%2Dleft%3A%205px%3B%0A%20%20%7D%0A%0A%20%20%23TOC%20ul%20%7B%0A%20%20%20%20padding%2Dleft%3A%2040px%3B%0A%20%20%20%20margin%2Dleft%3A%20%2D1%2E5em%3B%0A%20%20%20%20margin%2Dtop%3A%205px%3B%0A%20%20%20%20margin%2Dbottom%3A%205px%3B%0A%20%20%7D%0A%20%20%23TOC%20ul%20ul%20%7B%0A%20%20%20%20margin%2Dleft%3A%20%2D2em%3B%0A%20%20%7D%0A%20%20%23TOC%20li%20%7B%0A%20%20%20%20line%2Dheight%3A%2016px%3B%0A%20%20%7D%0A%0Atable%20%7B%0A%20%20margin%3A%201em%20auto%3B%0A%20%20border%2Dwidth%3A%201px%3B%0A%20%20border%2Dcolor%3A%20%23DDDDDD%3B%0A%20%20border%2Dstyle%3A%20outset%3B%0A%20%20border%2Dcollapse%3A%20collapse%3B%0A%7D%0Atable%20th%20%7B%0A%20%20border%2Dwidth%3A%202px%3B%0A%20%20padding%3A%205px%3B%0A%20%20border%2Dstyle%3A%20inset%3B%0A%7D%0Atable%20td%20%7B%0A%20%20border%2Dwidth%3A%201px%3B%0A%20%20border%2Dstyle%3A%20inset%3B%0A%20%20line%2Dheight%3A%2018px%3B%0A%20%20padding%3A%205px%205px%3B%0A%7D%0Atable%2C%20table%20th%2C%20table%20td%20%7B%0A%20%20border%2Dleft%2Dstyle%3A%20none%3B%0A%20%20border%2Dright%2Dstyle%3A%20none%3B%0A%7D%0Atable%20thead%2C%20table%20tr%2Eeven%20%7B%0A%20%20background%2Dcolor%3A%20%23f7f7f7%3B%0A%7D%0A%0Ap%20%7B%0A%20%20margin%3A%200%2E5em%200%3B%0A%7D%0A%0Ablockquote%20%7B%0A%20%20background%2Dcolor%3A%20%23f6f6f6%3B%0A%20%20padding%3A%200%2E25em%200%2E75em%3B%0A%7D%0A%0Ahr%20%7B%0A%20%20border%2Dstyle%3A%20solid%3B%0A%20%20border%3A%20none%3B%0A%20%20border%2Dtop%3A%201px%20solid%20%23777%3B%0A%20%20margin%3A%2028px%200%3B%0A%7D%0A%0Adl%20%7B%0A%20%20margin%2Dleft%3A%200%3B%0A%7D%0A%20%20dl%20dd%20%7B%0A%20%20%20%20margin%2Dbottom%3A%2013px%3B%0A%20%20%20%20margin%2Dleft%3A%2013px%3B%0A%20%20%7D%0A%20%20dl%20dt%20%7B%0A%20%20%20%20font%2Dweight%3A%20bold%3B%0A%20%20%7D%0A%0Aul%20%7B%0A%20%20margin%2Dtop%3A%200%3B%0A%7D%0A%20%20ul%20li%20%7B%0A%20%20%20%20list%2Dstyle%3A%20circle%20outside%3B%0A%20%20%7D%0A%20%20ul%20ul%20%7B%0A%20%20%20%20margin%2Dbottom%3A%200%3B%0A%20%20%7D%0A%0Apre%2C%20code%20%7B%0A%20%20background%2Dcolor%3A%20%23f7f7f7%3B%0A%20%20border%2Dradius%3A%203px%3B%0A%20%20color%3A%20%23333%3B%0A%7D%0Apre%20%7B%0A%20%20white%2Dspace%3A%20pre%2Dwrap%3B%20%20%20%20%2F%2A%20Wrap%20long%20lines%20%2A%2F%0A%20%20border%2Dradius%3A%203px%3B%0A%20%20margin%3A%205px%200px%2010px%200px%3B%0A%20%20padding%3A%2010px%3B%0A%7D%0Apre%3Anot%28%5Bclass%5D%29%20%7B%0A%20%20background%2Dcolor%3A%20%23f7f7f7%3B%0A%7D%0A%0Acode%20%7B%0A%20%20font%2Dfamily%3A%20Consolas%2C%20Monaco%2C%20%27Courier%20New%27%2C%20monospace%3B%0A%20%20font%2Dsize%3A%2085%25%3B%0A%7D%0Ap%20%3E%20code%2C%20li%20%3E%20code%20%7B%0A%20%20padding%3A%202px%200px%3B%0A%7D%0A%0Adiv%2Efigure%20%7B%0A%20%20text%2Dalign%3A%20center%3B%0A%7D%0Aimg%20%7B%0A%20%20background%2Dcolor%3A%20%23FFFFFF%3B%0A%20%20padding%3A%202px%3B%0A%20%20border%3A%201px%20solid%20%23DDDDDD%3B%0A%20%20border%2Dradius%3A%203px%3B%0A%20%20border%3A%201px%20solid%20%23CCCCCC%3B%0A%20%20margin%3A%200%205px%3B%0A%7D%0A%0Ah1%20%7B%0A%20%20margin%2Dtop%3A%200%3B%0A%20%20font%2Dsize%3A%2035px%3B%0A%20%20line%2Dheight%3A%2040px%3B%0A%7D%0A%0Ah2%20%7B%0A%20%20border%2Dbottom%3A%204px%20solid%20%23f7f7f7%3B%0A%20%20padding%2Dtop%3A%2010px%3B%0A%20%20padding%2Dbottom%3A%202px%3B%0A%20%20font%2Dsize%3A%20145%25%3B%0A%7D%0A%0Ah3%20%7B%0A%20%20border%2Dbottom%3A%202px%20solid%20%23f7f7f7%3B%0A%20%20padding%2Dtop%3A%2010px%3B%0A%20%20font%2Dsize%3A%20120%25%3B%0A%7D%0A%0Ah4%20%7B%0A%20%20border%2Dbottom%3A%201px%20solid%20%23f7f7f7%3B%0A%20%20margin%2Dleft%3A%208px%3B%0A%20%20font%2Dsize%3A%20105%25%3B%0A%7D%0A%0Ah5%2C%20h6%20%7B%0A%20%20border%2Dbottom%3A%201px%20solid%20%23ccc%3B%0A%20%20font%2Dsize%3A%20105%25%3B%0A%7D%0A%0Aa%20%7B%0A%20%20color%3A%20%230033dd%3B%0A%20%20text%2Ddecoration%3A%20none%3B%0A%7D%0A%20%20a%3Ahover%20%7B%0A%20%20%20%20color%3A%20%236666ff%3B%20%7D%0A%20%20a%3Avisited%20%7B%0A%20%20%20%20color%3A%20%23800080%3B%20%7D%0A%20%20a%3Avisited%3Ahover%20%7B%0A%20%20%20%20color%3A%20%23BB00BB%3B%20%7D%0A%20%20a%5Bhref%5E%3D%22http%3A%22%5D%20%7B%0A%20%20%20%20text%2Ddecoration%3A%20underline%3B%20%7D%0A%20%20a%5Bhref%5E%3D%22https%3A%22%5D%20%7B%0A%20%20%20%20text%2Ddecoration%3A%20underline%3B%20%7D%0A%0A%2F%2A%20Class%20described%20in%20https%3A%2F%2Fbenjeffrey%2Ecom%2Fposts%2Fpandoc%2Dsyntax%2Dhighlighting%2Dcss%0A%20%20%20Colours%20from%20https%3A%2F%2Fgist%2Egithub%2Ecom%2Frobsimmons%2F1172277%20%2A%2F%0A%0Acode%20%3E%20span%2Ekw%20%7B%20color%3A%20%23555%3B%20font%2Dweight%3A%20bold%3B%20%7D%20%2F%2A%20Keyword%20%2A%2F%0Acode%20%3E%20span%2Edt%20%7B%20color%3A%20%23902000%3B%20%7D%20%2F%2A%20DataType%20%2A%2F%0Acode%20%3E%20span%2Edv%20%7B%20color%3A%20%2340a070%3B%20%7D%20%2F%2A%20DecVal%20%28decimal%20values%29%20%2A%2F%0Acode%20%3E%20span%2Ebn%20%7B%20color%3A%20%23d14%3B%20%7D%20%2F%2A%20BaseN%20%2A%2F%0Acode%20%3E%20span%2Efl%20%7B%20color%3A%20%23d14%3B%20%7D%20%2F%2A%20Float%20%2A%2F%0Acode%20%3E%20span%2Ech%20%7B%20color%3A%20%23d14%3B%20%7D%20%2F%2A%20Char%20%2A%2F%0Acode%20%3E%20span%2Est%20%7B%20color%3A%20%23d14%3B%20%7D%20%2F%2A%20String%20%2A%2F%0Acode%20%3E%20span%2Eco%20%7B%20color%3A%20%23888888%3B%20font%2Dstyle%3A%20italic%3B%20%7D%20%2F%2A%20Comment%20%2A%2F%0Acode%20%3E%20span%2Eot%20%7B%20color%3A%20%23007020%3B%20%7D%20%2F%2A%20OtherToken%20%2A%2F%0Acode%20%3E%20span%2Eal%20%7B%20color%3A%20%23ff0000%3B%20font%2Dweight%3A%20bold%3B%20%7D%20%2F%2A%20AlertToken%20%2A%2F%0Acode%20%3E%20span%2Efu%20%7B%20color%3A%20%23900%3B%20font%2Dweight%3A%20bold%3B%20%7D%20%2F%2A%20Function%20calls%20%2A%2F%20%0Acode%20%3E%20span%2Eer%20%7B%20color%3A%20%23a61717%3B%20background%2Dcolor%3A%20%23e3d2d2%3B%20%7D%20%2F%2A%20ErrorTok%20%2A%2F%0A%0A" rel="stylesheet" type="text/css" />





<div id="header">
<h1 class="title">Data mining in twitter</h1>
<h4 class="author"><em>Wei Wang</em></h4>
<h4 class="date"><em>2015-03-25</em></h4>
</div>


<p>As we all know, the most popular social websites like <strong>Facebook</strong> and <strong>LinkedIn</strong> require the mutual acceptance of a connection between users (which usually implies a real-world connection of some kind), Twitter’s <strong>relationship model</strong> allows you to keep up with the latest happenings of any other user. Twitter’s following model is simple. It is the <strong>asymmetric following model</strong> that casts Twitter as more of an <strong>interest graph</strong> than a social network.</p>
<p>Think of an <strong>interest graph</strong> as a way of modeling connections between people and their arbitrary interests. Interest graphs provide a profound number of possibilities in the data mining realm that primarily involve <strong>measuring correlations between things</strong> for the objective of making intelligent recommendations and other applications in machine learning.</p>
<p>For example, you could use an interest graph to measure correlations and make recommendations ranging from whom to follow on Twitter to what to purchase online to whom you should date. To illustrate the notion of Twitter as an interest graph, consider that a Twitter user need not be a real person; it very well could be a person, but it could also be just about anything else.</p>
<div id="data-of-interests" class="section level2">
<h2>Data of interests</h2>
<p>The public firehose of all tweets has been known to peak at <strong>hundreds of thousands of tweets per minute</strong> during events with particularly wide interest, such as presidential debates. Twitter’s public firehose emits far too much data to consider for the scope of this book and presents interesting engineering challenges, which is at least one of the reasons that various third-party commercial vendors have partnered with Twitter to bring the firehose to the masses in a more consumable fashion. That said, a small random sample of the public timeline is available that provides filterable access to enough public data for API developers to develop powerful applications.</p>
</div>
<div id="creating-a-twitter-api-connection" class="section level2">
<h2>Creating a Twitter API connection</h2>
<p>Before you can make any API requests to Twitter, you’ll need to create an application at <a href="https://dev.twitter.com/apps" class="uri">https://dev.twitter.com/apps</a>. Creating an application is the standard way for developers to gain API access and for Twitter to monitor and interact with third-party platform developers as needed. The process for creating an application is just read-only access to the API.</p>
<p>For simplicity of development, the key pieces of information that you’ll need to take away from your newly created application’s settings are its</p>
<ul>
<li>consumer key</li>
<li>consumer secret</li>
<li>access token</li>
<li>access token secret</li>
</ul>
<p>The four OAuth (a means of allowing users to authorize third-party applications to access their account data without needing to share sensitive informatio) fields are what you’ll use to make API calls to Twitter’s API.</p>
</div>
<div id="finding-out-what-people-are-talking-about" class="section level2">
<h2>Finding out what people are talking about</h2>
<p>Inspecting the trends available to us through the <a href="https://dev.twitter.com/rest/reference/get/trends/place">GET trends/place resource</a>. While you’re at it, go ahead and bookmark the official API <a href="https://dev.twitter.com/overview/documentation">documentation</a> as well as the <a href="https://dev.twitter.com/rest/public">REST API v1.1 resources</a>, because you’ll be referencing them regularly as you learn the ropes of the developer-facing side of the Twitterverse.</p>
</div>
<div id="install-twitter-package-in-python" class="section level2">
<h2>Install twitter package in python</h2>
<p>Suppose we have created a folder ipython, open an terminal go to the directory</p>
<p><code>sudo pip install twitter</code></p>
</div>
<div id="launch-the-ipython-notebook" class="section level2">
<h2>Launch the ipython notebook</h2>
<p>Stay in the terminal, launch the notebook webconsole.</p>
<p><code>ipython notebook --pylab inline</code></p>
</div>
<div id="fire-up-python" class="section level2">
<h2>Fire up Python</h2>
<p>Let’s try to give our credentials to twitter and start a search</p>
<pre><code>import twitter

% XXX: Go to http://dev.twitter.com/apps/new to create an app and get values  
% for these credentials, which you'll need to provide in place of these  
% empty string values that are defined as placeholders.  
% See https://dev.twitter.com/docs/auth/oauth for more information  
% on Twitter's OAuth implementation.

CONSUMER_KEY = ''  
CONSUMER_SECRET = ''  
OAUTH_TOKEN = ''  
OAUTH_TOKEN_SECRET = ''

auth = twitter.oauth.OAuth(OAUTH_TOKEN, OAUTH_TOKEN_SECRET,
                           CONSUMER_KEY, CONSUMER_SECRET)

twitter_api = twitter.Twitter(auth=auth)

% Nothing to see by displaying twitter_api except that it's now a  
% defined variable

print twitter_api</code></pre>
<p>The results of this example should simply display an unambiguous representation of the twitter_api object that we’ve constructed, such as:</p>
<p><code>&lt;twitter.api.Twitter object at 0x111270c50&gt;</code></p>
</div>
<div id="exploring-trending-topics" class="section level2">
<h2>Exploring Trending Topics</h2>
<p>Ipython notebook code is given below # The Yahoo! Where On Earth ID for the entire world is 1. # See <a href="https://dev.twitter.com/docs/api/1.1/get/trends/place" class="uri">https://dev.twitter.com/docs/api/1.1/get/trends/place</a> and # <a href="http://developer.yahoo.com/geo/geoplanet/" class="uri">http://developer.yahoo.com/geo/geoplanet/</a></p>
<pre><code>WORLD_WOE_ID = 1
US_WOE_ID = 23424977

# Prefix ID with the underscore for query string parameterization.
# Without the underscore, the twitter package appends the ID value
# to the URL itself as a special case keyword argument.

world_trends = twitter_api.trends.place(_id=WORLD_WOE_ID)
us_trends = twitter_api.trends.place(_id=US_WOE_ID)

print world_trends
print
print us_trends</code></pre>
<p>You should see a semireadable response that is a list of <code>Python dictionaries</code> from the <code>API</code> (as opposed to any kind of error message), such as the following truncated results, before proceeding further.</p>
<p><code>[{u'created_at': u'2013-03-27T11:50:40Z', u'trends': [{u'url': u'http://twitter.com/search?q=%23MentionSomeoneImportantForYou'...</code></p>
<p>Notice that the sample result contains a URL for a trend represented as a search query that corresponds to the hashtag #MentionSomeoneImportantForYou, where <code>%23</code> is the <code>URL encoding</code> for the <code>hashtag symbol</code>. We’ll use this rather benign hashtag throughout the remainder of the chapter as a unifying theme for examples that follow.</p>
</div>
<div id="the-pattern-for-using-the-twitter-module" class="section level2">
<h2>The pattern for using the twitter module</h2>
<p>Simple and predictable:</p>
<ul>
<li>instantiate the Twitter class with an object chain corresponding to a base URL</li>
<li>invoke methods on the object that correspond to URL contexts.</li>
</ul>
<div id="for-example" class="section level3">
<h3>For example</h3>
<p>twitter_api._trends.place(WORLD_WOE_ID) initiates an HTTP call to GET <a href="https://api.twitter.com/1.1/trends/place.json?id=1" class="uri">https://api.twitter.com/1.1/trends/place.json?id=1</a>.</p>
<blockquote>
<p>“Note the URL mapping to the object chain that’s constructed with the twitter package to make the request and how query string parameters are passed in as keyword arguments. To use the twitter package for arbitrary API requests, you generally construct the request in that kind of straightforward manner, with just a couple of minor caveats that we’ll encounter soon enough.”</p>
</blockquote>
</div>
</div>
<div id="reformat-the-response-to-be-more-easily-readable" class="section level2">
<h2>Reformat the response to be more easily readable</h2>
<p>Displaying API responses as pretty-printed JSON</p>
<blockquote>
<p>“<strong>JSON</strong> is a data exchange format that you will encounter on a regular basis. In a nutshell, JSON provides a way to arbitrarily store maps, lists, primitives such as numbers and strings, and combinations thereof. In other words, you can theoretically model just about anything with JSON should you desire to do so.”</p>
</blockquote>
<pre><code>import json

print json.dumps(world_trends, indent=1)
print
print json.dumps(us_trends, indent=1)</code></pre>
<p>An abbreviated sample response from the Trends API produced with json.dumps would look like the following:</p>
<pre><code>[
 {
  &quot;created\_at&quot;: &quot;2013-03-27T11:50:40Z&quot;, 
  &quot;trends&quot;: [
   {
    &quot;url&quot;: &quot;http://twitter.com/search?q=%23MentionSomeoneImportantForYou&quot;, 
    &quot;query&quot;: &quot;%23MentionSomeoneImportantForYou&quot;, 
    &quot;name&quot;: &quot;\#MentionSomeoneImportantForYou&quot;, 
    &quot;promoted\_content&quot;: null, 
    &quot;events&quot;: null
   },
   ...
  ]
 }
]</code></pre>
<p>let’s use Python’s <code>set</code> data structure to automatically compute this for us. In this instance, a set refers to the mathematical notion of a data structure that stores an unordered collection of unique items and can be computed upon with other sets of items and setwise operations.</p>
</div>
<div id="computing-the-intersection-of-two-sets-of-trends" class="section level2">
<h2>Computing the intersection of two sets of trends</h2>
<p>How to use a Python list comprehension to parse out the names of the trending topics from the results that were previously queried, cast those lists to sets, and compute the setwise intersection to reveal the common items between them. Keep in mind that there may or may not be significant overlap between any given sets of trends, all depending on what’s actually happening when you query for the trends. In other words, the results of your analysis will be entirely dependent upon your query and the data that is returned from it.</p>
<pre><code>world_trends_set = set([trend['name'] 
                        for trend in world_trends[0]['trends']])

us_trends_set = set([trend['name'] 
                     for trend in us_trends[0]['trends']]) 

common_trends = world_trends_set.intersection(us_trends_set)

print common_trends</code></pre>
</div>



<!-- dynamically load mathjax for compatibility with self-contained -->
<script>
  (function () {
    var script = document.createElement("script");
    script.type = "text/javascript";
    script.src  = "https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML";
    document.getElementsByTagName("head")[0].appendChild(script);
  })();
</script>

<h4>
<a href="http://mayweiwang.github.io/" class="Return">Return to homepage</a>
</h4>
