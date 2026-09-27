---
layout: single
title: "ステータス"
permalink: /status/
author_profile: true
---

<div class="rpg-party-container">
  <div class="board-header-title">
    <span><i class="fas fa-users" style="color: #ffcc00;"></i> パーティ<i class="fas fa-users" style="color: #ffcc00;"></i></span>
  </div>

  <!-- 2人分を並べるグリッド枠 -->
  <div class="rpg-party-grid">

    <!-- ================= 1人目：自分 ================= -->
    <div class="rpg-status-card">
      <div class="rpg-header">
        <h3>ぽぽ</h3>
        <span class="rpg-level">Lv. 永遠の18歳</span>
      </div>
      
      <div class="rpg-body">
        <!-- 基本ステータス -->
        <ul class="rpg-stats-list">
          <li><span>職業:</span> <strong style="flex: 1; text-align: center;">ポイ活士</strong></li>
          <li><span>HP:</span> <strong style="flex: 1; text-align: center;">1200 / 1200</strong></li>
          <li><span>MP（総保有ポイント）:</span> <strong id="total-magic" style="color: #0077cc; flex: 1; text-align: center;">0Pt</strong></li>
          <li><span>攻撃力 (ATK):</span> <strong style="flex: 1; text-align: center;">120</strong></li>
          <li><span>防御力 (DEF):</span> <strong style="flex: 1; text-align: center;">95</strong></li>
          <li><span>素早さ (AGI):</span> <strong style="flex: 1; text-align: center;">150</strong></li>
        </ul>

        <!-- 7大魔石グリッド -->
        <h4 class="rpg-section-title"><i class="fas fa-gem"></i> 7大魔石（保有ポイント収蔵庫）</h4>
        <div class="rpg-stone-grid">
          <div class="rpg-stone-card" data-points="41000">
            <div class="stone-icon">💎</div>
            <div class="stone-info">
              <div class="stone-name">Vポイント</div>
              <div class="stone-value">41,000 Pt</div>
            </div>
          </div>
          <div class="rpg-stone-card" data-points="49000">
            <div class="stone-icon">🔥</div>
            <div class="stone-info">
              <div class="stone-name">PayPayポイント</div>
              <div class="stone-value">49,000 Pt</div>
            </div>
          </div>
          <div class="rpg-stone-card" data-points="184000">
            <div class="stone-icon">✨</div>
            <div class="stone-info">
              <div class="stone-name">Pontaポイント</div>
              <div class="stone-value">184,000 Pt</div>
            </div>
          </div>
          <div class="rpg-stone-card" data-points="500">
            <div class="stone-icon">🌟</div>
            <div class="stone-info">
              <div class="stone-name">楽天ポイント</div>
              <div class="stone-value">500 Pt</div>
            </div>
          </div>
          <div class="rpg-stone-card" data-points="100">
            <div class="stone-icon">🌀</div>
            <div class="stone-info">
              <div class="stone-name">dポイント</div>
              <div class="stone-value">100 Pt</div>
            </div>
          </div>
          <div class="rpg-stone-card" data-points="1000">
            <div class="stone-icon">🔮</div>
            <div class="stone-info">
              <div class="stone-name">Microsoftポイント（1/10）</div>
              <div class="stone-value">1,000 Pt</div>
            </div>
          </div>
          </div>
          <div class="rpg-stone-card" data-points="3000">
            <div class="stone-icon">🍃</div>
            <div class="stone-info">
              <div class="stone-name">WESTERポイント（期限：2028/3）</div>
              <div class="stone-value">3,000 Pt</div>
            </div>
          </div>
        

        <!-- 装備品セクション -->
        <h4 class="rpg-section-title"><i class="fas fa-shield-alt"></i> 装備品 & アイテム</h4>
        <table class="rpg-equipment-table">
          <tr>
            <th><i class="fas fa-magic"></i> 武器（メインクレカ）</th>
            <td>某ゴールドカード <span>(ATK +50)</span></td>
          </tr>
          <tr>
            <th><i class="fas fa-tshirt"></i> 防具（メインバンク）</th>
            <td>ドコモSMTBネット銀行 <span>(DEF +40 / 手数料軽減)</span></td>
          </tr>
          <tr>
            <th><i class="fas fa-shield-alt"></i> 盾（携帯電話）</th>
            <td>楽天モバイル <span>(DEF +40 / 通信料軽減)</span></td>
          </tr>
          <tr>
            <th><i class="fas fa-ring"></i> 装飾品（サブスク）</th>
            <td>Amazonプライム <span>(LUCK +99 / 送料無料！)</span></td>
          </tr>
          <tr>
            <th><i class="fas fa-box"></i> 所持品</th>
            <td>世帯主の大葉（家庭菜園） <span>(HP回復・栽培中)</span><br>
            シャトレーゼ会員カード<span>(無料宿泊の可能性が秘められている)</span></td>
          </tr>
        </table>
      </div>
    </div><!-- /.rpg-status-card (1人目終了) -->


    <!-- ================= 2人目：パートナー ================= -->
    <div class="rpg-status-card">
      <div class="rpg-header" style="background: #2d2340;">
        <h3>もも</h3>
        <span class="rpg-level" style="background: #4a90e2;">Lv. 草むしり検定3級</span>
      </div>
      
      <div class="rpg-body">
        <ul class="rpg-stats-list">
          <li><span>職業:</span> <strong style="flex: 1; text-align: center;">羊飼い</strong></li>
          <li><span>HP:</span> <strong style="flex: 1; text-align: center;">1200 / 1200</strong></li>
          <li><span>MP:</span> <strong style="color: #0077cc; flex: 1; text-align: center;">-- Pt</strong></li>
          <li><span>攻撃力 (ATK):</span> <strong style="flex: 1; text-align: center;"> 110</strong></li>
          <li><span>防御力 (DEF):</span> <strong style="flex: 1; text-align: center;">100</strong></li>
          <li><span>素早さ (AGI):</span> <strong style="flex: 1; text-align: center;">140</strong></li>
        </ul>

        <h4 class="rpg-section-title"><i class="fas fa-shield-alt"></i> 装備品 & アイテム</h4>
        <table class="rpg-equipment-table">
          <tr>
            <th><i class="fas fa-magic"></i> 武器</th>
            <td>フライパンブレード <span>(ATK +30)</span></td>
          </tr>
          <tr>
            <th><i class="fas fa-tshirt"></i> 防具</th>
            <td>ホーリーエプロン <span>(AGI +50)</span></td>
          </tr>
          <tr>
            <th><i class="fas fa-shield-alt"></i> 盾</th>
            <td>まな板の盾 <span>(DEF +40)</span></td>
          </tr>
          <tr>
            <th><i class="fas fa-ring"></i> 装飾品</th>
            <td>家庭円満のペンダント <span>(LUCK +80)</span></td>
          </tr>
          <tr>
            <th><i class="fas fa-box"></i> 所持品</th>
            <td>みょうがの芽（家庭菜園） <span>(MP回復・栽培中)</span></td>
          </tr>
        </table>
      </div>
    </div><!-- /.rpg-status-card (2人目終了) -->

  </div> <!-- /.rpg-party-grid -->
</div>

<style>
  .initial-content, .page {
    max-width: 3000px !important;
  }
  /* パーティ全体コンテナ */
  .rpg-party-container {
    font-family: 'Courier New', Courier, monospace;
    background-color: #0d0d1a;
    border: 4px solid #ffffff;
    box-shadow: 6px 6px 0px #000000;
    padding: 20px;
    margin: 20px 0;
    color: #f3f3f3;
    image-rendering: pixelated;
  }

  .board-header-title {
    text-align: center;
    font-size: 1.1rem;
    font-weight: bold;
    color: #ffcc00;
    border-bottom: 2px dashed #444466;
    padding-bottom: 12px;
    margin-bottom: 20px;
    letter-spacing: 1px;
  }

  /* 2人分を左右に並べるグリッド */
　.rpg-party-grid {
    display: grid;
    grid-template-columns: 1fr; /* 1列に変更 */
    gap: 20px; /* カード同士の上下の隙間 */
  }

  /* RPG風ステータスカードのデザイン */
  .rpg-status-card {
    border: 2px solid #444466;
    border-radius: 4px;
    background: #15152b;
    overflow: hidden;
    margin-bottom: 50px;
  }
  .rpg-header {
    background: #33334d;
    color: #fff;
    padding: 10px 14px;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  .rpg-header h3 {
    margin: 0;
    font-size: 15px;
    color: #fff;
    border: none;
    padding: 0;
  }
  .rpg-level {
    background: #ff4d4f;
    color: #fff;
    padding: 2px 8px;
    border-radius: 3px;
    font-size: 12px;
    font-weight: bold;
  }
  .rpg-body {
    padding: 15px;
  }
  .rpg-stats-list {
    list-style: none;
    padding: 0;
    margin: 0 0 15px 0;
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 8px;
  }
  .rpg-stats-list li {
    font-size: 13px;
    border-bottom: 1px dashed #22233b;
    padding-bottom: 4px;
    display: flex;
    justify-content: space-between;
  }
  .rpg-stats-list li span {
    color: #aaaaaa;
  }
  .rpg-section-title {
    font-size: 13px;
    border-bottom: 2px solid #444466;
    padding-bottom: 3px;
    margin-top: 15px;
    margin-bottom: 8px;
    color: #00ffcc;
  }

  /* 6大魔石グリッド */
  .rpg-stone-grid {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 8px;
    margin-bottom: 15px;
  }
  .rpg-stone-card {
    background-color: #0d0d1a;
    border: 2px solid #33334d;
    color: #fff;
    padding: 6px 8px;
    display: flex;
    align-items: center;
    gap: 8px;
    border-radius: 4px;
  }
  .stone-icon {
    font-size: 1.1rem;
    background: #15152b;
    padding: 2px 4px;
    border: 1px solid #444466;
  }
  .stone-info {
    display: flex;
    flex-direction: column;
  }
  .stone-name {
    font-size: 0.65rem;
    color: #aaaaaa;
  }
  .stone-value {
    font-size: 0.8rem;
    font-weight: bold;
    color: #ffeb3b;
    font-family: 'Courier New', Courier, monospace;
  }

  .rpg-equipment-table {
    width: 100%;
    border-collapse: collapse;
    font-size: 12px;
  }
  .rpg-equipment-table th, .rpg-equipment-table td {
    padding: 6px 8px;
    border-bottom: 1px solid #22233b;
    text-align: left;
  }
  .rpg-equipment-table th {
    width: 35%;
    color: #8888aa;
    font-weight: normal;
  }
  .rpg-equipment-table td {
    color: #d1d5db;
  }
  .rpg-equipment-table td span {
    color: #888;
    font-size: 11px;
    margin-left: 4px;
  }

  /* スマホ対応（画面が狭いときは1列にする） */
  @media screen and (max-width: 768px) {
    .rpg-party-grid {
      grid-template-columns: 1fr;
    }
    .rpg-stats-list {
      grid-template-columns: 1fr;
    }
  }
</style>

<script>
/* 各魔石のポイントを自動合算して「総魔力値」に反映するスクリプト */
document.addEventListener("DOMContentLoaded", function() {
  const cards = document.querySelectorAll('.rpg-stone-card');
  let total = 0;
  cards.forEach(card => {
    const pts = parseInt(card.getAttribute('data-points')) || 0;
    total += pts;
  });
  const totalEl = document.getElementById('total-magic');
  if (totalEl) {
    totalEl.textContent = total.toLocaleString();
  }
});
</script>
