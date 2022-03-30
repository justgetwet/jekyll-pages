---
layout: default
title: Top Page
---

<main>
  <div class="caption">
    <!-- <div class="book">{% include icons/book-open.svg %}</div> -->
    <div class="newspaper">{% include icons/pencil.svg %}</div>
    <h2>Articles</h2>
  </div>
    <aside>
      {% for post in site.posts %}
      <h3>
        <div class="post-items">
          <div class="post-date">{{ post.date | date: "%b %d,"}}</div>
          <div class="post-year">{{post.date | date: "%Y"}}</div>
          <a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a>
        </div>
      </h3>
      {% endfor %}
    </aside>  

</main>
