---
layout: page
title: Blog
permalink: /blog/
feature-img: "img/color.png"
---

<div>  
  <ul class="blog">
    {% for post in site.posts %}
    <li class="blogging">
      <header>
        <h1>
          {{ post.title }}
        </h1>
        <p class="meta">
          {{ post.date | date: "%-d %B %Y" }}
        </p>
      </header>
      <div class="content">
        {{ post.content }}
    </div>
    </li>
    {% endfor %}
  </ul>
</div>

<!-- <div class="posts">
    <h2 class="post-header">The latest from my blog</h2>
    <ul>
      {% for post in paginator.posts %}
      <li class="post-teaser">
        <header>
          <h3>
            <a class="post-link" href="{{ post.url | prepend: site.baseurl }}">
              {{ post.title }}
            </a>
          </h3>
          <p class="meta">
            {{ post.date | date: "%B %-d, %Y" }}
          </p>
        </header>
        <div class="excerpt">
          {{ post.excerpt | | strip_html | strip_newlines | truncate: 120 }}
        </div>
        <a href="{{ post.url | prepend: site.baseurl }}">
          {{ site.theme.str_continue_reading }}
        </a>
      </li>
      {% endfor %}
    </ul>
  </div>

  {% if paginator.total_pages > 1 %}
  <div class="pagination">
    {% if paginator.previous_page %}
    <a href="{{ paginator.previous_page_path | prepend: site.baseurl | replace: '//', '/' }}" class="button" >
      <i class="fa fa-chevron-left"></i>
      {{ site.theme.str_prev }}
    </a>
    {% endif %}
    {% if paginator.next_page %}
    <a href="{{ paginator.next_page_path | prepend: site.baseurl | replace: '//', '/' }}" class="button" >
      {{ site.theme.str_next }}
      <i class="fa fa-chevron-right"></i>
    </a>
    {% endif %}
  </div>
  {% endif %}
</div> -->