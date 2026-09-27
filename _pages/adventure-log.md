---
layout: single
title: "クエスト達成数と総ポイントの推移"
permalink: /adventure-log/
author_profile: true
---

<!-- Chart.jsの読み込み -->
<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>

<div class="ff-status-window">
  <div class="ff-title">▼ ぼうけんのきろく ―― 年次戦果レポート ――</div>
  <p class="ff-text">旅の足あと：<br>クエスト達成数、および総ポイント数の年ごとの推移</p>

  <!-- グラフ表示エリア -->
  <div class="ff-chart-container">
    <canvas id="adventureChart"></canvas>
  </div>
</div>

<style>
/* スーファミFF風ダークウィンドウのスタイル */
.ff-status-window {
  background-color: #0b0b0b; /* 漆黒の背景 */
  border: 2px solid #ffffff; /* シャープな白い枠線 */
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.8), inset 0 0 15px rgba(255, 255, 255, 0.03);
  color: #ffffff;
  padding: 20px;
  margin: 20px 0;
  font-family: 'Courier New', Courier, Monaco, monospace;
  border-radius: 2px;
}

.ff-title {
  font-size: 1.2rem;
  font-weight: bold;
  margin-bottom: 15px;
  border-bottom: 1px solid #333333;
  padding-bottom: 8px;
  letter-spacing: 1px;
  color: #f0f0f0;
}

.ff-text {
  font-size: 0.95rem;
  line-height: 1.6;
  margin-bottom: 20px;
  color: #cccccc;
}

.ff-chart-container {
  background-color: #15152b;
  padding: 15px;
  border: 1px solid #222222;
  border-radius: 2px;
  position: relative;
  height: 350px;
  width: 100%;
}
</style>

<script>
// 2026年以降、毎年1月にこちらの数値を書き換えてください
const adventureData = {
  labels: ['2026', '2027', '2028', '2029', '2030'], // 年ごとのラベル
  points: [180000, 200000, , ],          // 総ポイント数
  quests: [5, 10, , ]                    // クエスト達成数
};

document.addEventListener("DOMContentLoaded", function() {
  const ctxReal = document.getElementById('adventureChart').getContext('2d');
  
  new Chart(ctxReal, {
    type: 'line',
    data: {
      labels: adventureData.labels,
      datasets: [
        {
          label: '総ポイント数 (P)',
          data: adventureData.points,
          borderColor: '#ffdd00', // FF風の引き締まったゴールド
          backgroundColor: '#ffdd00',
          borderWidth: 2,
          pointRadius: 4,
          pointHoverRadius: 6,
          yAxisID: 'y',
        },
        {
          label: 'クエスト達成数 (件)',
          data: adventureData.quests,
          borderColor: '#00ffcc', // FF風のサイバーシアン
          backgroundColor: '#00ffcc',
          borderWidth: 2,
          pointRadius: 4,
          pointHoverRadius: 6,
          yAxisID: 'y1',
        }
      ]
    },
    options: {
      responsive: true,
      maintainAspectRatio: false,
      interaction: {
        mode: 'index',
        intersect: false,
      },
      plugins: {
        legend: {
          labels: {
            color: '#ffffff',
            font: {
              family: 'Courier New, monospace',
              size: 12,
              weight: 'bold'
            }
          }
        },
        tooltip: {
          backgroundColor: 'rgba(10, 10, 10, 0.95)',
          titleColor: '#ffdd00',
          bodyColor: '#ffffff',
          borderColor: '#ffffff',
          borderWidth: 1,
          padding: 10,
          boxPadding: 4,
          callbacks: {
            label: function(context) {
              let label = context.dataset.label || '';
              if (label) {
                label += ': ';
              }
              if (context.parsed.y !== null) {
                label += context.parsed.y;
              }
              return label;
            }
          }
        }
      },
      scales: {
        x: {
          grid: {
            color: 'rgba(255, 255, 255, 0.08)'
          },
          ticks: {
            color: '#cccccc',
            font: {
              family: 'Courier New, monospace',
              weight: 'bold'
            }
          }
        },
        y: {
          type: 'linear',
          display: true,
          position: 'left',
          suggestedMin: 0,
          suggestedMax: 500000, // ★ポイントの最大値に合わせて上限を設定
          title: {
            display: true,
            text: 'ポイント (P)',
            color: '#ffdd00',
            font: { weight: 'bold' }
          },
          grid: {
            color: 'rgba(255, 255, 255, 0.08)'
          },
          ticks: {
            color: '#ffdd00'
          }
        },
        y1: {
          type: 'linear',
          display: true,
          position: 'right',
          suggestedMin: 0,
          suggestedMax: 50,     // ★クエスト数の最大値に合わせて上限を設定
          title: {
            display: true,
            text: 'クエスト数 (件)',
            color: '#00ffcc',
            font: { weight: 'bold' }
          },
          grid: {
            drawOnChartArea: false,
            color: 'rgba(255, 255, 255, 0.08)'
          },
          ticks: {
            color: '#00ffcc'
          }
        }
      }
    }
  });
});
</script>
