---
layout: page
title: Home
permalink: /
subtitle:


---

<style>
.page-heading {
  display: none !important;
}
h1.post-title {
  display: none !important;
}
.image-grid {
  display: flex;
  justify-content: center;
  max-width: 800px;
  margin: 2rem auto;
}
.main-image {
  width: 100%;
  max-width: 600px;
  height: 400px;
  background-color: #f0f0f0;
  overflow: hidden;
}
.main-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}
/* .side-image {
  width: 100%;
  height: 200px;
  background-color: #f0f0f0;
  overflow: hidden;
}
.side-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
} */

.welcome-title {
  text-align: center;
  margin-bottom: 2rem;
}
.post-content {
  display: flex;
  flex-direction: column;
}
.post-content > h2:has(+ .publications) {
  order: -2;
}
.post-content > .publications {
  order: -2;
}
.post-content > .news {
  order: -1;
  border-bottom: 1px solid #e0e0e0;
  padding-bottom: 2rem;
  margin-bottom: 2rem;
}
.publications .paper {
  display: flex;
  margin-bottom: 2rem;
  gap: 1.5rem;
}
.publications .paper-preview {
  flex-shrink: 0;
  width: 150px;
}
.publications .paper-preview img {
  width: 100%;
  height: auto;
  object-fit: cover;
}
.publications .paper-content {
  flex: 1;
}
.publications .paper-title {
  font-size: 1.1rem;
  font-weight: 500;
  margin-bottom: 0.5rem;
  color: #000;
}
.publications .paper-authors {
  color: #888;
  margin-bottom: 0.3rem;
}
.publications .paper-authors .emphasized {
  color: #000;
  font-weight: 600;
}
.publications .paper-venue {
  font-style: italic;
  color: #666;
  margin-bottom: 0.5rem;
}
.publications .paper-links {
  display: flex;
  gap: 0.5rem;
  flex-wrap: wrap;
  align-items: center;
}
.publications .paper-btn {
  display: inline-flex;
  align-items: center;
  gap: 0.4rem;
  padding: 0.25rem 0.75rem;
  background-color: #f0f0f0;
  color: #333;
  text-decoration: none;
  border-radius: 4px;
  font-size: 0.9rem;
  transition: background-color 0.2s;
}
.publications .paper-btn:hover {
  background-color: #e0e0e0;
}
.publications .paper-btn img {
  width: 16px;
  height: 16px;
  object-fit: contain;
}
.publications .paper-btn.website {
  display: inline-flex;
  align-items: center;
  gap: 0.4rem;
}
.publications .paper-btn.website .fa-link {
  font-size: 0.9rem;
}
.publications .paper-award {
  display: inline-flex;
  align-items: center;
  padding: 0.25rem 0.75rem;
  background-color: #d4af37;
  color: #fff;
  border-radius: 4px;
  font-size: 0.9rem;
  font-weight: 500;
}
.publications .paper-topic {
  display: inline-flex;
  align-items: center;
  padding: 0.25rem 0.75rem;
  background-color: #e8f4f8;
  color: #0066cc;
  border-radius: 4px;
  font-size: 0.9rem;
}
.news {
  border-bottom: 1px solid #e0e0e0;
  padding-bottom: 2rem;
  margin-bottom: 2rem;
  margin-top: 1.5rem;
}
.news-item {
  display: flex;
  gap: 2rem;
  margin-bottom: 0.5rem;
  align-items: baseline;
}
.news-date {
  font-weight: 600;
  min-width: 120px;
  flex-shrink: 0;
}
.news-content {
  flex: 1;
}
.news-content a {
  color: #a64dff;
  text-decoration: none;
}
.news-content a:hover {
  text-decoration: underline;
}
</style>

<h1 class="welcome-title">WELCOME TO <strong>IDEA TEAM</strong>!</h1>

<div class="image-grid">
  <div class="main-image">
    <img src="/assets/img/main_pic1.jpg" alt="Main image">
  </div>
  <!-- <div class="side-image">
    <img src="/assets/img/main_pic2.jpg" alt="Image 2">
  </div>
  <div class="side-image">
    <img src="/assets/img/main_pic3.jpg" alt="Image 3">
  </div> -->
</div>


LAB Introducing text LAB Introducing text LAB Introducing text LAB Introducing text LAB Introducing text LAB Introducing text LAB Introducing text LAB Introducing text LAB Introducing text

---

## News

<div class="news">
{% assign sorted_news = site.news | sort: "date" | reverse %}
{% for item in sorted_news limit: 5 %}
  <div class="news-item">
    <div class="news-date">{{ item.date | date: "%b %d, %Y" }}</div>
    <div class="news-content">
      {% if item.inline %}
        {{ item.content | remove: '<p>' | remove: '</p>' }}
      {% else %}
        <a href="{{ item.url }}">{{ item.title }}</a>
      {% endif %}
    </div>
  </div>
{% endfor %}
</div>


## Selected publications

<div class="publications">
{% assign selected_papers = site.data.publications.papers | where: "selected", true %}
{% for paper in selected_papers %}
  <div class="paper">
    {% if paper.preview %}
    <div class="paper-preview">
      <img src="/assets/img/publication_preview/{{ paper.preview }}" alt="{{ paper.title }}">
    </div>
    {% endif %}
    <div class="paper-content">
      <div class="paper-title">
        {{ paper.title }}
      </div>
      <div class="paper-authors">
        {% assign author_parts = paper.author | split: '_' %}
        {% for part in author_parts %}
          {% assign index = forloop.index0 | modulo: 2 %}
          {% if index == 0 %}
            {{ part }}
          {% else %}
            <span class="emphasized">{{ part }}</span>
          {% endif %}
        {% endfor %}
      </div>
      <div class="paper-venue">
        {{ paper.venue }}, {{ paper.year }}
      </div>
      <div class="paper-links">
        {% if paper.links %}
          {% for link in paper.links %}
            {% if link.type == "acm" %}
              <a href="{{ link.url }}" target="_blank" class="paper-btn">
                <img src="/assets/img/acm_dl_logo.png" alt="ACM">
                ACM DL
              </a>
            {% elsif link.type == "arxiv" %}
              <a href="{{ link.url }}" target="_blank" class="paper-btn">
                <img src="/assets/img/arxiv_logo.png" alt="arXiv">
                arXiv
              </a>
            {% elsif link.type == "website" %}
              <a href="{{ link.url }}" target="_blank" class="paper-btn website">
                <i class="fas fa-link"></i>
                Website
              </a>
            {% else %}
              <a href="{{ link.url }}" target="_blank" class="paper-btn">
                {{ link.name }}
              </a>
            {% endif %}
          {% endfor %}
        {% endif %}
        {% if paper.award and paper.award != "" %}
          <span class="paper-award">{{ paper.award }}</span>
        {% endif %}
        {% if paper.topics %}
          {% for topic in paper.topics %}
            <span class="paper-topic">#{{ topic }}</span>
          {% endfor %}
        {% endif %}
      </div>
    </div>
  </div>
{% endfor %}
</div>

