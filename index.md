---
layout: single
title: ""
permalink: /
author_profile: true
---

<!-- ▼ 冒険のエリア（カテゴリー）選択コマンド -->
<div class="ff-category-menu">
  <span class="ff-cmd-label">▼ 探索エリア選択：</span>
  <a href="/" class="ff-cmd-btn active">すべて</a>
  <a href="/popomomoblog/categories/#cat-ポイ活" class="ff-cmd-btn">ポイ活</a>  
  <a href="{{ '/popomomoblog/categories/#cat-' | append: ('ポイ活' | slugify) }}" class="ff-cmd-btn">ポイ活</a>
  <a href="/popomomoblog/categories/#cat-その他" class="ff-cmd-btn">その他</a>
</div>

<!-- 記事カードのグリッドコンテナ -->
<div class="ff-card-grid">
  {% for post in site.posts %}
  <article class="ff-card">
    <!-- teaser または image の設定を自動で判定して取得 -->
    {% assign post_image = post.header.teaser | default: post.teaser | default: post.header.image %}
    {% if post_image %}
    <div class="ff-card-image-wrap">
      <a href="{{ post.url | relative_url }}">
        <img src="{{ post_image | relative_url }}" alt="{{ post.title }}" class="ff-card-image">
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

      <div class="ff-card-title">
        <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
      </div>



      <div class="ff-card-tags">
        <span class="ff-tag-label">タグ：</span>
        {% for tag in post.tags %}
          <span class="ff-tag">#{{ tag }}</span>
        {% endfor %}
      </div>
    </div>
  </article>
  {% endfor %}
</div>


<style>
/* ==========================================
   レトロRPG風 ホーム画面・カードスタイル
   ========================================== */

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

/* グリッドレイアウト */
.ff-card-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
  gap: 20px;
}

/* カード本体 */
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

/* 画像エリア（縦幅コンパクト・背景黒） */
.ff-card-image-wrap {
  width: 100%;
  height: 130px; 
  overflow: hidden;
  border-bottom: 1px solid #333;
  background-color: #0b0b0b;
}

/* 写真をすべて表示（切れないように contain 指定） */
.ff-card-image {
  width: 100%;
  height: 100%;
  object-fit: contain; 
  transition: transform 0.3s ease;
}
.ff-card:hover .ff-card-image {
  transform: scale(1.05);
}

/* カード内部の余白を詰めて縦幅を短くする */
.ff-card-body {
  padding: 10px 12px !important;
  display: flex;
  flex-direction: column;
  flex-grow: 1;
  justify-content: space-between;
}

/* 日付やカテゴリ名ヘッダー */
.ff-card-header {
  display: flex;
  justify-content: space-between;
  font-size: 0.75rem;
  color: #888;
  margin-bottom: 4px;
  border-bottom: 1px dashed #333;
  padding-bottom: 3px;
}
.ff-card-category {
  color: #00ffcc;
}

/* 記事のタイトル */
.ff-card-title {
  margin: 4px 0;
}
.ff-card-title a {
  color: #ffffff;
  text-decoration: none;
  font-size: 0.9rem;
  line-height: 1.3;
  font-weight: bold;
}
.ff-card-title a:hover {
  color: #ffdd00;
}


/* タグエリア */
.ff-card-tags {
  display: flex;
  gap: 5px;
  flex-wrap: wrap;
  align-items: center;
  margin-top: 6px;
  border-top: 1px dashed #222;
  padding-top: 6px;
}
.ff-tag-label {
  font-size: 0.6rem !important;
  color: #888888;
  margin-right: 2px;
}
.ff-tag {
  font-size: 0.6rem;
  color: #ffcc00;
  background: #151515;
  border: 1px solid #333;
  padding: 2px 5px;
  border-radius: 2px;
}

/* スマホ表示対応 */
@media screen and (max-width: 600px) {
  .ff-card-grid {
    grid-template-columns: 1fr;
  }
}
</style>
