---
layout: layouts/base.njk
eleventyNavigation:
  key: About Me
  order: 3
numberOfLatestPostsToShow: 5
---
# About Me

Robert Kingett is a blind and gay writer that wears a lot of hats, but mostly writes fiction and nonfiction featuring disabled characters.

# Recent posts.

{% set postsCount = collections.posts | length %}
{% set latestPostsCount = postsCount | min(numberOfLatestPostsToShow) %}
<h1>Latest {{ latestPostsCount }} Post{% if latestPostsCount != 1 %}s{% endif %}</h1>

{% set postslist = collections.posts | head(-1 * numberOfLatestPostsToShow) %}
{% set postslistCounter = postsCount %}
{% include "postslist.njk" %}