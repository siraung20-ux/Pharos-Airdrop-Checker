# Pharos-Airdrop-Checker
Have Fun For Sailors Community 
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>PHRS Airdrop Checker – Fun Demo</title>
  <meta name="viewport" content="width=device-width, initial-scale=1" />

  <!-- Optional Google Font -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Baloo+2:wght@500;700&display=swap" rel="stylesheet">

  <style>
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body {
      font-family: "Baloo 2", system-ui, -apple-system, sans-serif;
      min-height: 100vh;
      display: flex;
      align-items: center;
      justify-content: center;
      background: radial-gradient(circle at top, #2ef2ff 0, #0b1020 45%, #050611 100%);
      color: #f8f9ff;
      overflow: hidden;
    }

    /* Floating bubbles / tokens */
    .bg-bubble {
      position: fixed;
      border-radius: 999px;
      opacity: 0.35;
      filter: blur(2px);
      animation: float 14s infinite ease-in-out;
      pointer-events: none;
      z-index: 0;
    }

    .bubble-1 { width: 220px; height: 220px; background: #ff7fd9; top: 5%; left: 5%; animation-delay: 0s; }
    .bubble-2 { width: 180px; height: 180px; background: #2ef2ff; top: 60%; right: -60px; animation-delay: 3s; }
    .bubble-3 { width: 140px; height: 140px; background: #ffdd57; bottom: -60px; left: 50%; transform: translateX(-50%); animation-delay: 6s; }

    @keyframes float {
      0%, 100% { transform: translateY(0) scale(1); }
      50% { transform: translateY(-35px) scale(1.05); }
    }

    /* Main card */
    .card {
      position: relative;
      z-index: 1;
      width: 100%;
      max-width: 450px;
      background: radial-gradient(circle at top, #19223f 0, #0c1224 55%, #060814 100%);
      border-radius: 24px;
      padding: 24px 22px 20px;
      box-shadow:
        0 0 40px rgba(0, 255, 255, 0.2),
        0 20px 60px rgba(0, 0, 0, 0.85);
      border: 1px solid rgba(255, 255, 255, 0.08);
    }

    .card-header {
      display: flex;
      gap: 14px;
      align-items: center;
      margin-bottom: 12px;
    }

    .logo-badge {
      width: 52px;
      height: 52px;
      border-radius: 18px;
      background: radial-gradient(circle at 30% 15%, #ffffff 0, #ffe26e 14%, #ff8a3c 45%, #ff3c7f 100%);
      box-shadow: 0 0 20px rgba(255, 189, 74, 0.8);
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 24px;
      transform: rotate(-8deg);
    }

    .logo-badge span {
      text-shadow: 0 2px 4px rgba(0, 0, 0, 0.45);
    }

    .titles h1 {
      font-size: 1.4rem;
      line-height: 1.1;
      letter-spacing: 0.03em;
    }

    .titles h1 span {
      background: linear-gradient(120deg, #2ef2ff, #7af7ff, #fff5a8);
      -webkit-background-clip: text;
      color: transparent;
    }

    .titles p {
      font-size: 0.82rem;
      opacity: 0.8;
      margin-top: 2px;
    }

    .pill {
      display: inline-flex;
      align-items: center;
      gap: 6px;
      font-size: 0.7rem;
      background: rgba(46, 242, 255, 0.08);
      border-radius: 999px;
      padding: 4px 10px;
      border: 1px solid rgba(46, 242, 255, 0.3);
      margin-bottom: 10px;
    }

    .pill-dot {
      width: 8px;
      height: 8px;
      border-radius: 999px;
      background: radial-gradient(circle at 30% 20%, #ffffff 0, #2ef2ff 30%, #17c1cb 100%);
      box-shadow: 0 0 8px rgba(46, 242, 255, 0.8);
    }

    form {
      display: flex;
      flex-direction: column;
      gap: 10px;
      margin-top: 4px;
    }

    label {
      font-size: 0.78rem;
      opacity: 0.8;
    }

    .input-row {
      display: flex;
      gap: 8px;
    }

    input[type="text"] {
      flex: 1;
      background: rgba(7, 13, 31, 0.95);
      border-radius: 999px;
      border: 1px solid rgba(135, 153, 255, 0.35);
      padding: 9px 12px;
      font-size: 0.85rem;
      color: #f9fbff;
      outline: none;
      transition: border 0.18s ease, box-shadow 0.18s ease, background 0.18s ease;
    }

    input[type="text"]::placeholder {
      color: rgba(200, 205, 255, 0.55);
    }

    input[type="text"]:focus {
      border-color: #2ef2ff;
      box-shadow: 0 0 0 1px rgba(46, 242, 255, 0.6);
      background: rgba(7, 17, 40, 0.98);
    }

    button {
      border: none;
      border-radius: 999px;
      padding: 9px 16px;
      font-size: 0.86rem;
      font-weight: 700;
      cursor: pointer;
      background: linear-gradient(135deg, #ffdd57, #ff9b3d);
      color: #141219;
      box-shadow:
        0 0 16px rgba(255, 200, 80, 0.75),
        0 8px 28px rgba(0, 0, 0, 0.6);
      display: inline-flex;
      align-items: center;
      gap: 6px;
      transition: transform 0.1s ease, box-shadow 0.1s ease, filter 0.1s ease;
      white-space: nowrap;
    }

    button:hover {
      transform: translateY(-1px);
      filter: brightness(1.05);
      box-shadow:
        0 0 20px rgba(255, 210, 100, 0.85),
        0 10px 30px rgba(0, 0, 0, 0.75);
    }

    button:active {
      transform: translateY(1px) scale(0.98);
      box-shadow:
        0 0 10px rgba(255, 210, 100, 0.6),
        0 4px 16px rgba(0, 0, 0, 0.7);
    }

    .result {
      margin-top: 14px;
      padding: 12px 10px 10px;
      border-radius: 18px;
      background: radial-gradient(circle at top, rgba(46, 242, 255, 0.1), rgba(6, 10, 28, 0.95));
      border: 1px solid rgba(100, 130, 255, 0.4);
      min-height: 85px;
      display: none;
    }

    .result.show {
      display: block;
      animation: pop 0.35s ease-out;
    }

    @keyframes pop {
      0% { transform: scale(0.96); opacity: 0; }
      100% { transform: scale(1); opacity: 1; }
    }

    .result-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 6px;
    }

    .status-pill {
      display: inline-flex;
      align-items: center;
      gap: 6px;
      border-radius: 999px;
      padding: 4px 10px;
      font-size: 0.72rem;
    }

    .status-yes {
      background: rgba(46, 242, 110, 0.15);
      border: 1px solid rgba(46, 242, 110, 0.7);
      color: #a8ffcb;
    }

    .status-no {
      background: rgba(255, 102, 140, 0.12);
      border: 1px solid rgba(255, 102, 140, 0.7);
      color: #ffb6d1;
    }

    .result-main {
      font-size: 0.85rem;
      margin-bottom: 4px;
    }

    .result-main strong {
      color: #ffdd57;
    }

    .meta {
      font-size: 0.75rem;
      opacity: 0.75;
      display: flex;
      justify-content: space-between;
      flex-wrap: wrap;
      gap: 4px;
    }

    .tag {
      font-size: 0.7rem;
      opacity: 0.7;
    }

    .footer {
      margin-top: 10px;
      font-size: 0.7rem;
      opacity: 0.6;
      text-align: center;
    }

    .footer span {
      font-weight: 700;
      color: #ffd25b;
    }

    @media (max-width: 480px) {
      .card {
        margin: 12px;
        padding: 20px 16px 18px;
      }
      .input-row {
        flex-direction: column;
      }
      button {
        width: 100%;
        justify-content: center;
      }
    }
  </style>
</head>
<body>

  <!-- Fun background bubbles -->
  <div class="bg-bubble bubble-1"></div>
  <div class="bg-bubble bubble-2"></div>
  <div class="bg-bubble bubble-3"></div>

  <main class="card">
    <div class="card-header">
      <div class="logo-badge">
        <!-- Mini PHRS coin / lighthouse vibe -->
        <span>PH</span>
      </div>
      <div class="titles">
        <h1><span>PHRS</span> Airdrop Checker</h1>
        <p>Fun testnet-style demo for sailors & Gotchipus 🐙</p>
      </div>
    </div>

    <div class="pill">
      <div class="pill-dot"></div>
      <span>Demo mode · not an official checker</span>
    </div>

    <form id="checker-form">
      <label for="wallet-input">Paste your wallet address (EVM / Phantom / degen 🧪)</label>
      <div class="input-row">
        <input
          id="wallet-input"
          type="text"
          placeholder="0x... or your fun test wallet"
          autocomplete="off"
        />
        <button type="submit">
          ⚓ Check my drop
        </button>
      </div>
    </form>

    <section id="result" class="result">
      <div class="result-header">
        <div id="status-pill" class="status-pill status-yes">
          ✅ Eligible (demo)
        </div>
        <div class="tag">PHRS · Atlantic Season</div>
      </div>
      <div id="result-main" class="result-main">
        <!-- Filled by JS -->
      </div>
      <div class="meta">
        <div id="meta-left"></div>
        <div id="meta-right"></div>
      </div>
    </section>

    <div class="footer">
      <span>Heads up:</span> This is a playful mock checker for UI preview.<br/>
      For real PHRS airdrop info, always follow official Pharos channels only.
    </div>
  </main>

  <script>
    // Simple "fake checker" logic – fun only, no real API
    const form = document.getElementById("checker-form");
    const walletInput = document.getElementById("wallet-input");
    const resultBox = document.getElementById("result");
    const statusPill = document.getElementById("status-pill");
    const resultMain = document.getElementById("result-main");
    const metaLeft = document.getElementById("meta-left");
    const metaRight = document.getElementById("meta-right");

    const funMessagesYes = [
      "Congrats sailor, your Gotchipus has been farming non-stop in Atlantic season 🌊",
      "You’ve been touching testnet, not grass – PHRS gods approve 😈",
      "Your wallet smells like faucets, swaps & daily check-ins. Pure degen energy ⚡",
      "Pathfinder vibes detected – your XP radar is glowing neon 💫"
    ];

    const funMessagesNo = [
      "Hmm… this wallet looks sleepy. Maybe your Gotchipus is still level 0 😴",
      "No strong testnet waves detected yet. Time to farm missions, sailor 🌊",
      "PHRS lighthouse can’t find enough activity – try your most degen wallet 👀",
      "Zero-testnet aura… but it’s never too late to join the next wave ⚓"
    ];

    const tiers = [
      "Baby Sailor",
      "Testnet Explorer",
      "Atlantic Pathfinder",
      "OG Lighthouse Keeper"
    ];

    function hashString(str) {
      let h = 0;
      for (let i = 0; i < str.length; i++) {
        h = (h * 31 + str.charCodeAt(i)) >>> 0;
      }
      return h;
    }

    function fakeCheck(address) {
      const trimmed = address.trim();
      const hash = hashString(trimmed || "default");

      // random-ish demo logic
      const eligible = (hash % 5) !== 0;          // ~80% "eligible"
      const points = 200 + (hash % 4800);         // 200 – 4999
      const rank = 1 + (hash % 9999);            // 1 – 9999
      const tier = tiers[hash % tiers.length];
      const msgList = eligible ? funMessagesYes : funMessagesNo;
      const reason = msgList[hash % msgList.length];

      return { eligible, points, rank, tier, reason };
    }

    form.addEventListener("submit", (e) => {
      e.preventDefault();
      const addr = walletInput.value.trim();

      if (!addr) {
        walletInput.focus();
        walletInput.placeholder = "Paste something degen here first 😅";
        return;
      }

      const { eligible, points, rank, tier, reason } = fakeCheck(addr);

      // Update pill
      statusPill.textContent = eligible ? "✅ Eligible (demo)" : "❌ Not Eligible (demo)";
      statusPill.classList.toggle("status-yes", eligible);
      statusPill.classList.toggle("status-no", !eligible);

      // Main text
      resultMain.innerHTML = `
        <p>${reason}</p>
        <p style="margin-top:4px;">
          Estimated <strong>${points.toLocaleString()} PHRS points</strong> · Tier:
          <strong>${tier}</strong>
        </p>
      `;

      metaLeft.textContent = `Demo rank: #${rank.toLocaleString()}`;
      metaRight.textContent = "Mode: Testnet Fantasy 🧪";

      resultBox.classList.add("show");
    });
  </script>
</body>
</html>
