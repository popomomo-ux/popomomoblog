---
layout: single
title: "行きたい・行った場所マップ"
permalink: /map/
author_profile: true
---

<div class="rpg-party-container">
  <!-- マップのタイトルヘッダー -->
  <div class="board-header-title">
    <span><i class="fas fa-map-marked-alt" style="color: #ffcc00;"></i> WORLD MAP - 冒険の足跡 - <i class="fas fa-map-marked-alt" style="color: #ffcc00;"></i></span>
  </div>

  <!-- フィルターグループ1：カテゴリ -->
  <div class="filter-section">
    <span class="filter-label">カテゴリ:</span>
    <div class="filter-buttons" id="category-filters">
      <button class="filter-btn category-btn active" data-category="all">すべて</button>
      <button class="filter-btn category-btn" data-category="spot">観光</button>
      <button class="filter-btn category-btn" data-category="cafe">カフェ</button>
      <button class="filter-btn category-btn" data-category="hotel">宿</button>
      <button class="filter-btn category-btn" data-category="gourmet">グルメ</button>
      <button class="filter-btn category-btn" data-category="spa">温泉</button>
      <button class="filter-btn category-btn" data-category="temple">神社・お寺</button>
      <button class="filter-btn category-btn" data-category="festival">お祭り</button>
    </div>
  </div>

  <!-- フィルターグループ2：ステータス（行きたい / 行った） -->
  <div class="filter-section" style="margin-top: 10px;">
    <span class="filter-label">状態:</span>
    <div class="filter-buttons" id="status-filters">
      <button class="filter-btn status-btn active" data-status="all">すべて</button>
      <button class="filter-btn status-btn" data-status="want">行きたい</button>
      <button class="filter-btn status-btn" data-status="visited">行った</button>
    </div>
  </div>

  <div id="blog-map"></div>
</div>

<!-- Leaflet CSS & JS の読み込み -->
<link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css" />
<script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>

<style>
  /* 共通のレトロRPG風コンテナ（ステータス画面と同一世界観） */
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

  /* フィルターのレイアウト（レトロ風ウインドウ調） */
  .filter-section {
    display: flex;
    align-items: center;
    gap: 10px;
    flex-wrap: wrap;
    background: #15152b;
    border: 2px solid #444466;
    padding: 10px;
    border-radius: 4px;
  }
  .filter-label {
    font-weight: bold;
    font-size: 12px;
    color: #00ffcc;
    min-width: 60px;
    letter-spacing: 1px;
  }
  .filter-buttons {
    display: flex;
    gap: 6px;
    flex-wrap: wrap;
  }
  .filter-btn {
    padding: 4px 10px;
    border: 2px solid #444466;
    background: #0d0d1a;
    color: #d1d5db;
    border-radius: 3px;
    cursor: pointer;
    font-size: 12px;
    font-family: 'Courier New', Courier, monospace;
    transition: all 0.1s;
  }
  .filter-btn:hover {
    border-color: #ffcc00;
    color: #ffcc00;
  }
  .filter-btn.active {
    background: #ffcc00;
    color: #0d0d1a;
    border-color: #ffcc00;
    font-weight: bold;
  }

  /* 地図のスタイル */
  #blog-map {
    width: 100%;
    height: 600px;
    border: 2px solid #444466;
    border-radius: 4px;
    margin-top: 15px;
    margin-bottom: 0px;
    z-index: 1;
  }
  .custom-pin {
    background: transparent;
    border: none;
  }
  .pin-circle {
    width: 34px;
    height: 34px;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    color: white;
    font-size: 14px;
    box-shadow: 0 3px 8px rgba(0,0,0,0.5);
    border: 2px solid #ffffff;
  }

  /* LeafletポップアップのダークRPG風デザイン調整 */
  .leaflet-popup-content-wrapper, .leaflet-popup-tip {
    background: #15152b !important;
    color: #f3f3f3 !important;
    border: 2px solid #444466 !important;
    border-radius: 4px !important;
    font-family: 'Courier New', Courier, monospace !important;
  }
  .leaflet-popup-content {
    color: #f3f3f3 !important;
    font-size: 13px;
  }
  .leaflet-container a.leaflet-popup-close-button {
    color: #ffcc00 !important;
  }
</style>

<script>
document.addEventListener("DOMContentLoaded", () => {
  const map = L.map('blog-map').setView([34.577613, 135.195469], 8);

  L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
    maxZoom: 15,
    attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors'
  }).addTo(map);

// --- アイコンを自動生成する関数 ---
  function createPinIcon(category, status, popup) { // ← ここに popup を追加
    const color = (status === 'want') ? '#ff4d4f' : '#52c41a'; // 行きたい: 赤, 行った: 緑
      
    let iconClass = 'fas fa-map-marker-alt';
    if (category === 'spot') {
      // popupの中身に「ジャンボフェリー」という文字が含まれていれば船アイコンにする
      if (popup && popup.includes('ジャンボフェリー')) {
        iconClass = 'fas fa-ferry';
      } else {
        iconClass = 'fas fa-camera';
      }
    }
    else if (category === 'cafe') iconClass = 'fas fa-coffee';
    else if (category === 'hotel') iconClass = 'fas fa-bed';
    else if (category === 'gourmet') iconClass = 'fas fa-utensils';
    else if (category === 'spa') iconClass = 'fas fa-bath';
    else if (category === 'temple') iconClass = 'fas fa-torii-gate';
    else if (category === 'festival') iconClass = 'fas fa-drum';

    return L.divIcon({
      className: 'custom-pin',
      html: `<div class="pin-circle" style="background-color: ${color};"><i class="${iconClass}"></i></div>`,
      iconSize: [34, 34],
      iconAnchor: [17, 17]
    });
  }

  // //////////////////////////////// --- スポットデータ一覧 --- ////////////////////////////////
  const locations = [
    /////// 観光地（spot）///////
    { 
      lat: 34.528658, lng: 134.658774,
      category: 'spot', status: 'visited', 
      popup: '<b>ジャンボフェリー</b><br><span style="color:#52c41a;">神戸から高松への船旅</span>' 
    },
    { 
      lat: 34.48173281861081, lng: 136.84561749514268,
      category: 'spot', status: 'visited', 
      popup: '<b>鳥羽水族館</b><br><span style="color:#52c41a;">念願のラッコとの邂逅</span>' 
    },
    { 
      lat: 26.445519309491356, lng: 127.7455738340109, 
      category: 'spot', status: 'want', 
      popup: '<b>やちむんの里</b><br><span style="color:#ff4d4f;">器好きの妻の憧れの地</span><br><a href="https://www.yomitan-kankou.jp/tourist/watch/1611319504/" target="_blank">▶ 参考サイト</a>' 
    },

    { 
      lat: 34.33000989198189, lng: 134.04572668164545, 
      category: 'spot', status: 'visited', 
      popup: '<b>栗林公園</b><br><span style="color:#52c41a;">スケールが規格外な日本庭園</span>' 
    },
    /////// カフェ（cafe）///////
    { 
      lat: 34.67720586538338, lng: 135.83435945467428, 
      category: 'cafe', status: 'visited', 
      popup: '<b>今西清兵衛商店</b><br><span style="color:#52c41a;">5種類の利き酒を楽しみ、おちょこもGET</span>' 
    },
    /////// 宿（hotel）///////
    { 
      lat: 34.26270992262492, lng: 132.76163093325016, 
      category: 'hotel', status: 'want', 
      popup: '<b>シャトレーゼ ガトーキングダム せとうち</b><br><span style="color:#ff4d4f;">シャトレーゼポイントで宿泊したい！</span><br><a href="https://setouchi.gateauxkingdom.com/" target="_blank">▶ 公式ホームページ</a>' 
    },
    { 
      lat: 36.34717436720957, lng: 136.36480203753936,
      category: 'hotel', status: 'want', 
      popup: '<b>大江戸温泉物語Premium 加賀まるや</b><br><span style="color:#ff4d4f;">直通往復バスで意外と近そう</span><br><a href="https://www.ooedoonsen.jp/kagamaruya/" target="_blank">▶ 公式ホームページ</a>' 
    },
    { 
      lat: 34.79807765578565, lng: 135.25105887734713, 
      category: 'hotel', status: 'want', 
      popup: '<b>有馬きらり</b><br><span style="color:#ff4d4f;">豊臣秀吉も愛した日本三古湯の一つでくつろぎたい</span><br><a href="https://www.arima-view.com/" target="_blank">▶ 公式ホームページ</a>' 
    },
    /////// グルメ（gourmet）///////
    ////大阪旅行////
     { 
       lat: 34.7009683276561, lng: 135.49893544092137,
       category: 'gourmet', status: 'visited', 
       popup: '<b>焼きスパゲッティ×ワイン ローマ軒 大阪駅前第3ビル店</b><br><span style="color:#52c41a;">ここでしか食べられない味。30分飲み放題もギルティ</span>' 
    },
    ////滋賀旅行////
     { 
       lat: 35.116698686806814, lng: 136.18397076421496,
       category: 'gourmet', status: 'visited', 
       popup: '<b>近江牛専門店 万葉 太郎坊亭</b><br><span style="color:#52c41a;">近江牛の焼肉ランチ</span>' 
    },
    { 
       lat: 35.38052398005815, lng: 136.26722772771663, 
       category: 'gourmet', status: 'visited', 
       popup: '<b>翼果楼（よかろう）</b><br><span style="color:#52c41a;">鯖の旨味で何度でも食べたくなる味。</span>' 
    },
    ////京都旅行////
    { 
       lat: 34.98667666257747, lng: 135.76128515468568, 
       category: 'gourmet', status: 'visited', 
       popup: '<b>KIZAHASHI</b><br><span style="color:#52c41a;">味も器も天下一品</span>' 
    },
    { 
       lat: 35.030846536661066, lng: 135.75794097981836,
       category: 'gourmet', status: 'visited', 
       popup: '<b>松乃家</b><br><span style="color:#52c41a;">味も量も昔懐かしい良い食堂</span>' 
    },
    { 
       lat: 35.05568798940034, lng: 135.74850561236036,
       category: 'gourmet', status: 'visited', 
       popup: '<b>中華料理 紅華 大宮本店</b><br><span style="color:#52c41a;">味もコスパも最高の町中華</span>' 
    },

    ////香川旅行////
    { 
       lat: 34.349957544828925, lng: 134.04730055466248, 
       category: 'gourmet', status: 'visited', 
       popup: '<b>めりけんや 高松駅前店</b><br><span style="color:#52c41a;">本場は違うぜ！</span>' 
    },
    { 
       lat: 34.34120738894437, lng: 134.04998443931802, 
       category: 'gourmet', status: 'visited', 
       popup: '<b>海鮮問屋 仲見世</b><br><span style="color:#52c41a;">さわらのお刺身には仰天</span>' 
    },
    ////三重旅行////
    { 
       lat: 34.48921240667204, lng: 136.71041894302834,
       category: 'gourmet', status: 'visited', 
       popup: '<b>さかな屋くにちゃん</b><br><span style="color:#52c41a;">とんぼマグロのてこね寿司</span>' 
    },
  　{ 
       lat: 34.48753748116291, lng: 136.8437741835035,
       category: 'gourmet', status: 'visited', 
       popup: '<b>漁師直営店浜幸</b><br><span style="color:#52c41a;">漁師さん直営の新鮮な海鮮丼が絶品！</span><br><a href="https://tabelog.com/mie/A2403/A240302/24008096/?msockid=292d4690b08d6ef838a45037b11d6f40" target="_blank">▶ 食べログ</a>' 
    },
    { 
       lat: 34.49447327832972, lng: 136.6985271123398,
       category: 'gourmet', status: 'visited', 
       popup: '<b>ぎょうざの美鈴</b><br><span style="color:#52c41a;">餃子はもちろん女将さんの握ったおにぎりがまた食べたい。</span><br><a href="https://www.gyouzanomisuzu.com/" target="_blank">▶ 公式ホームページ</a>' 
    },
    ////静岡旅行////
    { 
       lat: 34.70586385200359, lng: 137.73413920129764,
       category: 'gourmet', status: 'want', 
       popup: '<b>さわやか 浜松遠鉄店</b><br><span style="color:#ff4d4f;">噂に名高いハンバーグ食べたいね</span><br><a href="https://www.genkotsu-hb.com/" target="_blank">▶ 公式ホームページ</a>' 
    },  
    /////// 温泉（spa）///////
    { 
       lat: 35.17874811246188, lng: 136.97932715284028,
       category: 'spa', status: 'want', 
       popup: '<b>RAKU SPA GARDEN 名古屋</b><br><span style="color:#ff4d4f;">名古屋周辺の大型スーパー銭湯</span><br><a href="https://rakuspa.com/nagoya/" target="_blank">▶ 公式ホームページ</a>' 
     },
     { 
       lat: 33.852149147516016, lng: 132.78640614461185, 
       category: 'spa', status: 'want', 
       popup: '<b>道後温泉</b><br><span style="color:#ff4d4f;">約3,000年の歴史を持つ、日本最古級の温泉</span><br><a href="https://dogo.jp/about" target="_blank">▶ 公式ホームページ</a>' 
     },
   /////// 神社・お寺（temple）///////
    { 
       lat: 34.68166881964122, lng: 135.8484718796952, 
       category: 'temple', status: 'visited', 
       popup: '<b>春日大社</b><br><span style="color:#52c41a;">大雨の中で鹿を鑑賞☂</span>' 
     },
    { 
       lat: 34.45520145314381, lng: 136.72515291048603, 
       category: 'temple', status: 'visited', 
       popup: '<b>伊勢神宮</b><br><span style="color:#52c41a;">2人のゆかりの地</span>' 
     },
   /////// お祭り（festival）///////
    { 
       lat: 36.57737102425911, lng: 137.13575114865438, 
       category: 'festival', status: 'want', 
       popup: '<b>おわら風の盆</b><br><span style="color:#ff4d4f;">WESTERポイントで行けるかな？</span><br><a href="https://owara-gyoujiunei.com/" target="_blank">▶ 公式ホームページ</a>' 
    }
    
  ];

  let currentCategory = 'all';
  let currentStatus = 'all';
  let currentMarkers = [];

  // マップのピンを更新する関数（AND条件でフィルタリング）
  function updateMarkers() {
    currentMarkers.forEach(marker => map.removeLayer(marker));
    currentMarkers = [];

    locations.forEach(loc => {
      const matchCategory = (currentCategory === 'all' || loc.category === currentCategory);
      const matchStatus = (currentStatus === 'all' || loc.status === currentStatus);

      if (matchCategory && matchStatus) {
        const icon = createPinIcon(loc.category, loc.status, loc.popup);
        const marker = L.marker([loc.lat, loc.lng], { icon: icon })
          .addTo(map)
          .bindPopup(loc.popup);
        currentMarkers.push(marker);
      }
    });
  }

  // 初期表示
  updateMarkers();

  // カテゴリボタンのイベント
  document.querySelectorAll('.category-btn').forEach(button => {
    button.addEventListener('click', (e) => {
      document.querySelectorAll('.category-btn').forEach(b => b.classList.remove('active'));
      e.target.classList.add('active');
      currentCategory = e.target.getAttribute('data-category');
      updateMarkers();
    });
  });

  // ステータスボタンのイベント
  document.querySelectorAll('.status-btn').forEach(button => {
    button.addEventListener('click', (e) => {
      document.querySelectorAll('.status-btn').forEach(b => b.classList.remove('active'));
      e.target.classList.add('active');
      currentStatus = e.target.getAttribute('data-status');
      updateMarkers();
    });
  });
});
</script>
