---
layout: post
title:  "Playing with Chalice"
date:   2016-11-04 12:20:25
categories: spotify data analysis serverless
featured: /assets/images/lambda.png
---

I've been really interested in serverless technology for the last few months.
Serverless computing is a cloud computing code execution model in which the
cloud provider fully manages starting and stopping virtual machines as necessary
to serve requests.

In Nnodes, we've tried out frameworks like
[Serverless](https://github.com/serverless/serverless), 
[Claudia](https://github.com/claudiajs/claudia) and
[Chalice](https://github.com/awslabs/chalice) for slackbots and small experiments. I really loved working
with Chalice because of how easy is to set up a fully functional micro service, 
and because I like Python a lot. This is why I've setup 
[musicdata.eduramirez.com](http://musicdata.eduramirez.com).

# The architecture

![Architecture diagram](/assets/images/architecture.png)

The backend is built over Chalice, using AWS's API Gateway, Lambda and DynamoDB.
It loads data for all songs of a given artist from Spotify's API, and stores it
in a DynamoDB table. It loads it directly from the table if it was previously
requested, preventing having to call the Spotify API each time (which implies
multiple, slow requests).

The frontend was built using Google's Web Starter Kit. It makes AJAX requests to
the backend to get a specific artist's data.


# The result

![musicdata.eduramirez.com](/assets/images/songsdata_screenshot.png)

In [musicdata.eduramirez.com](http://musicdata.eduramirez.com) you can 
look for any artist and display charts of the audio features of all of
his/her songs.
This features include duration, energy, and even danceability.

# The good things

* Python
* Really easy to set up and deploy.
* Really fast to set up and deploy. You can have a working endpoint in less 
than a minute.
* Very cheap, and even free if your API is not frequently called.

# The bad things

* All your code must be in just 1 file. This implies you can't even store
API keys in an external, untracked file in you repo. I'm loading my Spotify API
credentials from a DynamoDB table for now.
* Having to define different HTTP method's responses in the same function.

# The code

You can get the code at [git.io/vXClc](https://git.io/vXClc). There's a lot of 
room for improvement so any collaboration will be well received.

