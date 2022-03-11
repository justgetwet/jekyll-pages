---
layout: default
title: Top Page
---

<main>
  <div class="caption">
    <div class="book">{% include icons/book-open.svg %}</div>
    <h3>ARTICLE</h3>
  </div>
    <aside>
      {% for post in site.posts %}
      <h3>
        <div class="post-items">
          <div class="post-date">{{ post.date | date: "%b %d, %Y"}}</div>
          <a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a>
        </div>
      </h3>
      {% endfor %}
    </aside>  

</main>
