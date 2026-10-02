---
layout: single
title: "ホーム"
permalink: /
author_profile: true
---

<!-- ▼ ここから下に、先ほどのレトロRPG風カード一覧のコードを配置します -->

<!-- 冒険のエリア（カテゴリー）選択コマンド -->
<div class="ff-category-menu">
  <span class="ff-cmd-label">▼ 探索エリア選択：</span>
  <a href="/adventure-log/" class="ff-cmd-btn active">すべて</a>
  <a href="/popomomoblog/categories/#その他" class="ff-cmd-btn">その他</a>
  <a href="/popomomoblog/categories/#other" class="ff-cmd-btn">✈️ 国内旅行</a>
</div>

<!-- 記事カードのグリッドコンテナ -->
<div class="ff-card-grid">
  {% for post in site.posts %}
  <article class="ff-card">
    {% if post.header.image %}
    <div class="ff-card-image-wrap">
      <a href="{{ post.url | relative_url }}">
        <img src="{{ post.header.image | relative_url }}" alt="{{ post.title }}" class="ff-card-image">
      </a>
    </div>
    {% endif %}

    <div class="ff-card-body">
      <div class="ff-card-header">
        <span class="ff-card-date">{{ post.date | date: "%Y.%m.%d" }}</span>
        {% if post.categories[0] %}
        <span class="ff-card-category">📁 {{ post.categories[0] }}</span>
        {% endif %}
      </div>

      <h3 class="ff-card-title">
        <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
      </h3>

      <p class="ff-card-excerpt">
        {% if post.excerpt %}
          {{ post.excerpt | strip_html | truncate: 70 }}
        {% else %}
          {{ post.content | strip_html | truncate: 70 }}
        {% endif %}
      </p>

      <div class="ff-card-tags">
        {% for tag in post.tags %}
          <span class="ff-tag">#{{ tag }}</span>
        {% endfor %}
      </div>
    </div>
  </article>
  {% endfor %}
</div>

<!-- タグ（属性・ステータス風） -->
      <div class="ff-card-tags">
        <span class="ff-tag-label">タグ：</span>
        {% for tag in post.tags %}
          <span class="ff-tag">#{{ tag }}</span>
        {% endfor %}
      </div>

<style>
/* スタイルはそのまま適用できます */
.ff-category-menu {
  margin-bottom: 25px;
  font-family: 'Courier New', Courier, Monaco, monospace;
}
.ff-cmd-label {
  color: #ffdd00;
  font-weight: bold;
  margin-right: 10px;
}
.ff-cmd-btn {
  display: inline-block;
  background: #111;
  color: #ccc;
  border: 1px solid #444;
  padding: 5px 12px;
  margin: 4px 6px 4px 0;
  text-decoration: none;
  font-size: 0.9rem;
  border-radius: 2px;
  transition: all 0.2s;
}
.ff-cmd-btn:hover, .ff-cmd-btn.active {
  background: #222;
  color: #ffdd00;
  border-color: #ffdd00;
}
.ff-card-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
  gap: 20px;
}
.ff-card {
  background-color: #0b0b0b;
  border: 2px solid #ffffff;
  box-shadow: 0 0 8px rgba(0, 0, 0, 0.8), inset 0 0 10px rgba(255, 255, 255, 0.02);
  display: flex;
  flex-direction: column;
  font-family: 'Courier New', Courier, Monaco, monospace;
  transition: transform 0.2s, border-color 0.2s;
  border-radius: 2px;
  overflow: hidden;
}
.ff-card:hover {
  border-color: #ffdd00;
  transform: translateY(-3px);
}
.ff-card-image-wrap {
  width: 100%;
  height: 160px;
  overflow: hidden;
  border-bottom: 1px solid #333;
}
.ff-card-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.3s ease;
}
.ff-card:hover .ff-card-image {
  transform: scale(1.05);
}
.ff-card-body {
  padding: 15px;
  display: flex;
  flex-direction: column;
  flex-grow: 1;
  justify-content: space-between;
}
.ff-card-header {
  display: flex;
  justify-content: space-between;
  font-size: 0.75rem;
  color: #888;
  margin-bottom: 8px;
  border-bottom: 1px dashed #333;
  padding-bottom: 4px;
}
.ff-card-category {
  color: #00ffcc;
}
.ff-card-title a {
  color: #ffffff;
  text-decoration: none;
  font-size: 1rem;
  line-height: 1.4;
  font-weight: bold;
}
.ff-card-title a:hover {
  color: #ffdd00;
}
.ff-card-excerpt {
  font-size: 0.85rem;
  color: #aaaaaa;
  margin: 10px 0;
  line-height: 1.5;
  flex-grow: 1;
}
.ff-card-tags {
  display: flex;
  gap: 6px;
  flex-wrap: wrap;
  margin-top: 10px;
  border-top: 1px dashed #222;
  padding-top: 8px;
}
.ff-tag {
  font-size: 0.7rem;
  color: #ffcc00;
  background: #151515;
  border: 1px solid #333;
  padding: 2px 5px;
  border-radius: 2px;
}
@media screen and (max-width: 600px) {
  .ff-card-grid {
    grid-template-columns: 1fr;
  }
}
</style>
