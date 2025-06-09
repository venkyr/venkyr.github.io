---
layout: home
---

<div class="home-intro">
    <h1>Welcome to My Blog</h1>
    <p class="lead">A space for sharing thoughts, experiences, and knowledge.</p>
</div>

<section class="featured-posts">
    <h2>Latest Posts</h2>
    <ul class="post-list">
        {% for post in site.posts %}
            <li>
                <h2><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h2>
                <div class="post-meta">
                    {{ post.date | date: "%B %-d, %Y" }}
                </div>
                <div class="post-excerpt">
                    {{ post.excerpt | strip_html | truncatewords: 50 }}
                </div>
                <a href="{{ post.url | relative_url }}" class="read-more">Read more →</a>
            </li>
        {% endfor %}
    </ul>
</section> 