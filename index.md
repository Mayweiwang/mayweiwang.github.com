---
layout: page
title: Love data and hope to explore the world of data.
tagline: Supporting tagline
---
{% include JB/setup %}

I am a data scientist in the field of High-Frequency surface wave radar remote sensing. More info. about me are provided on [Linkedin](https://ca.linkedin.com/in/wei-may-wang-96364315)


## About this blog

In `Archieve` menu I post some of the notes of my learning and working with data:
    
    Content : anything about data scicence 
    
    Including :
      Statistics 
      Python
      R
      Matlab
      Data analysis
      Machine learning
      Big Data

The blog should reference these categories whenever needed.
    
## Here's a sample "posts list".

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>




