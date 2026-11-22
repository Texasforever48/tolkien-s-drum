<!DOCTYPE html>
<html lang="zh-CN">
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <meta name="theme-color" content="#151515">
    <title>Tolkien 的鼓</title>
    <style>
      :root {
        color-scheme: dark;
        --background: #151515;
        --surface: #202020;
        --text: #f5efdf;
        --muted: #b7b1a6;
        --accent: #ff934f;
      }

      * { box-sizing: border-box; }

      body {
        margin: 0;
        background: var(--background);
        color: var(--text);
        font: 16px/1.6 system-ui, -apple-system, "PingFang SC", sans-serif;
      }

      main {
        max-width: 1100px;
        margin: auto;
        padding: 32px 24px 64px;
      }

      header { font-size: 14px; letter-spacing: 2px; }

      .hero {
        display: grid;
        grid-template-columns: 1.4fr 1fr;
        align-items: center;
        gap: 24px;
        padding: 48px 0;
      }

      h1 {
        margin: 0;
        font-size: clamp(36px, 6vw, 70px);
        line-height: 1.2;
        letter-spacing: -2px;
      }

      h1 em { color: var(--accent); font-style: normal; }
      .drum { width: 100%; max-width: 320px; justify-self: center; }
      h2 { margin: 0 0 20px; font-size: 22px; }

      .cards {
        display: grid;
        grid-template-columns: repeat(3, minmax(0, 1fr));
        gap: 18px;
      }

      .card {
        display: flex;
        flex-direction: column;
        padding: 24px;
        border-radius: 16px;
        background: var(--surface);
      }

      h3 { margin: 0; font-size: 22px; }
      .card p { flex: 1; margin: 12px 0 24px; color: var(--muted); font-size: 14px; }
      .clock { margin-bottom: 20px; font-size: 36px; font-variant-numeric: tabular-nums; }

      button {
        min-height: 44px;
        padding: 10px 16px;
        border: 0;
        border-radius: 8px;
        background: var(--accent);
        color: #21160e;
        font: inherit;
        font-weight: 600;
        cursor: pointer;
      }

      button:hover { background: #ffac75; }
      button:focus-visible { outline: 2px solid var(--text); outline-offset: 4px; }
      .reset { margin-top: 8px; background: transparent; color: var(--muted); font-size: 13px; }
      .reset:hover { background: #303030; }
      .status { min-height: 24px; margin-top: 8px; color: var(--accent); font-size: 13px; }

      @media (max-width: 700px) {
        .hero { grid-template-columns: 1fr; padding: 40px 0; }
        .drum { max-width: 200px; }
        .cards { grid-template-columns: 1fr; }
      }
    </style>
    <link rel="stylesheet" href="background.css">
  </head>
  <body>
    <main>
      <header>TOLKIEN / DRUMS</header>

      <section class="hero" aria-label="架子鼓练习室">
        <h1>每天一点，<br>打出你的<em>节奏。</em></h1>
        <svg class="drum" viewBox="0 0 360 320" role="img" aria-label="架子鼓线条插画">
          <g fill="none" stroke="#766553" stroke-width="2">
            <path d="M70 90v184m0-30-30 42m30-42 30 42M287 78v190m0-25-28 40m28-40 28 40M180 225v60m0-12-25 22m25-22 25 22"/>
            <ellipse cx="70" cy="88" rx="58" ry="12" stroke="#ff934f"/>
            <ellipse cx="287" cy="75" rx="57" ry="12" stroke="#ff934f"/>
            <path d="m122 117-17 59m131-61 16 61"/>
            <ellipse cx="131" cy="124" rx="38" ry="18"/>
            <path d="M93 124v38c0 24 76 24 76 0v-38"/>
            <ellipse cx="226" cy="124" rx="38" ry="18"/>
            <path d="M188 124v38c0 24 76 24 76 0v-38"/>
          </g>
          <circle cx="179" cy="218" r="72" fill="#24211e" stroke="#ff934f" stroke-width="3"/>
          <circle cx="179" cy="218" r="61" fill="none" stroke="#66513e"/>
          <text x="179" y="225" text-anchor="middle" fill="#f5efdf" font-size="14" font-family="sans-serif" letter-spacing="3">TOLKIEN</text>
          <path d="m136 54 76 52m11-65-60 69" stroke="#f5efdf" stroke-width="5" stroke-linecap="round"/>
        </svg>
      </section>

      <h2>今天，练这三项</h2>
      <section class="cards" aria-label="今日练习计划">
        <article class="card" data-seconds="300">
          <h3>单击练习</h3>
          <p>左右手交替，保持力度和间隔均匀。</p>
          <div class="clock" role="timer" aria-label="单击练习剩余时间">05:00</div>
          <button class="start" type="button">开始练习</button>
          <button class="reset" type="button">重置</button>
          <div class="status" role="status"></div>
        </article>

        <article class="card" data-seconds="600">
          <h3>基本摇滚节奏</h3>
          <p>稳住底鼓与军鼓，先求准确，再提速。</p>
          <div class="clock" role="timer" aria-label="基本摇滚节奏剩余时间">10:00</div>
          <button class="start" type="button">开始练习</button>
          <button class="reset" type="button">重置</button>
          <div class="status" role="status"></div>
        </article>

        <article class="card" data-seconds="600">
          <h3>跟着一首歌练习</h3>
          <p>选一首喜欢的歌，把节奏连起来。</p>
          <div class="clock" role="timer" aria-label="跟着一首歌练习剩余时间">10:00</div>
          <button class="start" type="button">开始练习</button>
          <button class="reset" type="button">重置</button>
          <div class="status" role="status"></div>
        </article>
      </section>
    </main>

    <script>
      document.querySelectorAll(".card").forEach((card) => {
        const duration = Number(card.dataset.seconds);
        const clock = card.querySelector(".clock");
        const start = card.querySelector(".start");
        const status = card.querySelector(".status");
        let remaining = duration;
        let deadline = 0;
        let timer = null;

        function render() {
          const minutes = String(Math.floor(remaining / 60)).padStart(2, "0");
          const seconds = String(remaining % 60).padStart(2, "0");
          clock.textContent = `${minutes}:${seconds}`;
          start.textContent = timer !== null ? "暂停" : remaining === 0 ? "再练一次" : "开始练习";
          status.textContent = remaining === 0 ? "练习完成" : "";
        }

        function stop() {
          clearInterval(timer);
          timer = null;
        }

        function tick() {
          remaining = Math.max(0, Math.ceil((deadline - Date.now()) / 1000));
          if (remaining === 0) stop();
          render();
        }

        start.addEventListener("click", () => {
          if (timer !== null) {
            tick();
            stop();
            render();
            if (remaining > 0) {
              start.textContent = "继续练习";
              status.textContent = "已暂停";
            }
            return;
          }

          if (remaining === 0) remaining = duration;
          deadline = Date.now() + remaining * 1000;
          timer = setInterval(tick, 250);
          render();
        });

        card.querySelector(".reset").addEventListener("click", () => {
          stop();
          remaining = duration;
          render();
        });
      });
    </script>
  </body>
</html>
