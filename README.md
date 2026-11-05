<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Grade 10 – Term 1: Interactive Decision Webpage (C10)</title>
  <style>
    :root {
      --primary: #2563eb;
      --primary-hover: #1d4ed8;
      --bg: #f8fafc;
      --card-bg: #ffffff;
      --text: #0f172a;
      --text-muted: #64748b;
      --border: #e2e8f0;
      --accent-success: #10b981;
      --accent-warning: #f59e0b;
      --accent-danger: #ef4444;
      --chip-bg: #eff6ff;
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen, Ubuntu, Cantarell, sans-serif;
    }

    body {
      background-color: var(--bg);
      color: var(--text);
      padding: 24px;
      line-height: 1.5;
    }

    .container {
      max-width: 1280px;
      margin: 0 auto;
      display: flex;
      flex-direction: column;
      gap: 24px;
    }

    header {
      background: var(--card-bg);
      padding: 20px 24px;
      border-radius: 12px;
      border: 1px solid var(--border);
      display: flex;
      justify-content: space-between;
      align-items: center;
      flex-wrap: wrap;
      gap: 16px;
      box-shadow: 0 1px 3px rgba(0,0,0,0.05);
    }

    .header-title h1 {
      font-size: 1.5rem;
      font-weight: 700;
      color: var(--text);
    }

    .header-title p {
      font-size: 0.875rem;
      color: var(--text-muted);
    }

    .ai-record-btn {
      display: inline-flex;
      align-items: center;
      gap: 8px;
      background: #f1f5f9;
      color: var(--primary);
      text-decoration: none;
      padding: 8px 16px;
      border-radius: 8px;
      font-weight: 600;
      font-size: 0.875rem;
      border: 1px solid #cbd5e1;
      transition: all 0.2s;
    }

    .ai-record-btn:hover {
      background: var(--chip-bg);
      border-color: var(--primary);
    }

    .grid {
      display: grid;
      grid-template-columns: 1fr;
      gap: 24px;
    }

    @media (min-width: 1024px) {
      .grid {
        grid-template-columns: 320px 1fr;
      }
    }

    .card {
      background: var(--card-bg);
      border-radius: 12px;
      border: 1px solid var(--border);
      padding: 20px;
      box-shadow: 0 1px 3px rgba(0,0,0,0.05);
    }

    .card-header {
      font-size: 1.1rem;
      font-weight: 600;
      margin-bottom: 16px;
      display: flex;
      justify-content: space-between;
      align-items: center;
    }

    .control-group {
      display: flex;
      flex-direction: column;
      gap: 12px;
      margin-bottom: 20px;
    }

    label {
      font-size: 0.875rem;
      font-weight: 600;
      color: var(--text-muted);
    }

    select, input, button {
      padding: 8px 12px;
      border-radius: 6px;
      border: 1px solid var(--border);
      font-size: 0.9rem;
      outline: none;
    }

    select, input {
      width: 100%;
    }

    button {
      background: var(--primary);
      color: white;
      border: none;
      font-weight: 600;
      cursor: pointer;
      transition: background 0.2s;
    }

    button:hover {
      background: var(--primary-hover);
    }

    .btn-secondary {
      background: #f1f5f9;
      color: var(--text);
      border: 1px solid var(--border);
    }

    .btn-secondary:hover {
      background: #e2e8f0;
    }

    .btn-danger {
      background: #fee2e2;
      color: var(--accent-danger);
      border: 1px solid #fca5a5;
    }

    .btn-danger:hover {
      background: #fecaca;
    }

    .btn-group {
      display: flex;
      gap: 8px;
    }

    /* Table Styles */
    .table-container {
      overflow-x: auto;
      margin-bottom: 16px;
    }

    table {
      width: 100%;
      border-collapse: collapse;
      text-align: left;
    }

    th, td {
      padding: 10px 12px;
      border: 1px solid var(--border);
      font-size: 0.875rem;
    }

    th {
      background: #f8fafc;
      font-weight: 600;
    }

    td input {
      width: 80px;
      padding: 4px 8px;
      text-align: right;
    }

    .prob-warning {
      font-size: 0.8rem;
      color: var(--accent-danger);
      margin-top: 4px;
      display: none;
    }

    /* Results Grid */
    .results-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
      gap: 16px;
      margin-top: 16px;
    }

    .result-card {
      background: #f8fafc;
      border: 1px solid var(--border);
      border-left: 4px solid var(--primary);
      padding: 16px;
      border-radius: 8px;
    }

    .result-card.maximax { border-left-color: #10b981; }
    .result-card.maximin { border-left-color: #f59e0b; }
    .result-card.regret { border-left-color: #8b5cf6; }
    .result-card.emv { border-left-color: #2563eb; }

    .result-title {
      font-size: 0.85rem;
      font-weight: 600;
      color: var(--text-muted);
      text-transform: uppercase;
      letter-spacing: 0.05em;
    }

    .result-value {
      font-size: 1.25rem;
      font-weight: 700;
      margin: 4px 0;
    }

    .result-alt {
      font-size: 0.9rem;
      color: var(--text);
      font-weight: 600;
    }

    /* Flow Diagram */
    .flow-container {
      width: 100%;
      overflow-x: auto;
      padding: 16px 0;
    }

    svg {
      width: 100%;
      min-width: 600px;
      height: 220px;
    }

    .stage-box {
      fill: #ffffff;
      stroke: var(--border);
      stroke-width: 2;
      rx: 8;
    }

    .stage-box.active {
      stroke: var(--primary);
    }

    .stage-text-title {
      font-weight: 600;
      font-size: 14px;
      fill: var(--text);
    }

    .stage-text-detail {
      font-size: 12px;
      fill: var(--text-muted);
    }

    .connector-line {
      stroke: #cbd5e1;
      stroke-width: 2;
      stroke-dasharray: 4;
    }

    footer {
      margin-top: 32px;
      text-align: center;
      font-size: 0.85rem;
      color: var(--text-muted);
      border-top: 1px solid var(--border);
      padding-top: 16px;
    }
  </style>
</head>
<body>

  <div class="container">
    <!-- Header -->
    <header>
      <div class="header-title">
        <h1>Grade 10 – Term 1: Decision Webpage</h1>
        <p>Interactive Decision Analysis under Uncertainty &amp; Staged Filtering (C10 Practice)</p>
      </div>
      <a href="https://github.com" target="_blank" class="ai-record-btn">
        <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M18 13v6a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V8a2 2 0 0 1 2-2h6"></path><polyline points="15 3 21 3 21 9"></polyline><line x1="10" y1="14" x2="21" y2="3"></line></svg>
        AI Development Record
      </a>
    </header>

    <div class="grid">
      <!-- Controls Sidebar -->
      <div class="card">
        <div class="card-header">
          <span>Configuration</span>
        </div>

        <div class="control-group">
          <label for="exampleSelect">Preloaded Examples</label>
          <select id="exampleSelect" onchange="loadExample()">
            <option value="1">1. Business Expansion</option>
            <option value="2">2. Crop Selection</option>
          </select>
        </div>

        <hr style="margin: 16px 0; border: none; border-top: 1px solid var(--border);">

        <div class="control-group">
          <label>Manage Alternatives</label>
          <div class="btn-group">
            <button onclick="addAlternative()">+ Add</button>
            <button class="btn-danger" onclick="removeAlternative()">- Remove</button>
          </div>
        </div>

        <div class="control-group">
          <label>Manage States of Nature</label>
          <div class="btn-group">
            <button onclick="addState()">+ Add</button>
            <button class="btn-danger" onclick="removeState()">- Remove</button>
          </div>
        </div>

        <hr style="margin: 16px 0; border: none; border-top: 1px solid var(--border);">

        <div class="control-group">
          <label for="stage1Criteria">Filter Stage 1</label>
          <select id="stage1Criteria" onchange="calculateAll()">
            <option value="none">None</option>
            <option value="maximax">Maximax</option>
            <option value="maximin" selected>Maximin (Conservative)</option>
            <option value="emv">EMV / Bayes</option>
          </select>
        </div>

        <div class="control-group">
          <label for="stage2Criteria">Filter Stage 2</label>
          <select id="stage2Criteria" onchange="calculateAll()">
            <option value="none">None</option>
            <option value="regret" selected>Minimax Regret</option>
            <option value="emv">EMV / Bayes</option>
          </select>
        </div>
      </div>

      <!-- Main Content Area -->
      <div style="display: flex; flex-direction: column; gap: 24px;">
        <!-- Payoff & Probabilities Table -->
        <div class="card">
          <div class="card-header">
            <span>Payoff Matrix &amp; State Probabilities</span>
          </div>
          
          <div class="table-container">
            <table id="payoffTable">
              <!-- Dynamically Generated -->
            </table>
          </div>
          <div id="probWarning" class="prob-warning">Warning: Probabilities must sum to exactly 1.00</div>
        </div>

        <!-- Decision Criteria Results -->
        <div class="card">
          <div class="card-header">
            <span>Decision Criteria Evaluation</span>
          </div>
          
          <div class="results-grid">
            <div class="result-card maximax">
              <div class="result-title">Maximax (Optimistic)</div>
              <div class="result-value" id="valMaximax">-</div>
              <div class="result-alt" id="altMaximax">-</div>
            </div>

            <div class="result-card maximin">
              <div class="result-title">Maximin (Pessimistic)</div>
              <div class="result-value" id="valMaximin">-</div>
              <div class="result-alt" id="altMaximin">-</div>
            </div>

            <div class="result-card regret">
              <div class="result-title">Minimax Regret</div>
              <div class="result-value" id="valRegret">-</div>
              <div class="result-alt" id="altRegret">-</div>
            </div>

            <div class="result-card emv">
              <div class="result-title">EMV / Bayes</div>
              <div class="result-value" id="valEMV">-</div>
              <div class="result-alt" id="altEMV">-</div>
            </div>
          </div>
        </div>

        <!-- Staged Filtering Flow Diagram -->
        <div class="card">
          <div class="card-header">
            <span>Staged Elimination Pipeline &amp; Flow Diagram</span>
          </div>
          
          <div class="flow-container">
            <svg id="flowDiagram" viewBox="0 0 750 200">
              <!-- Dynamically Generated SVG Elements -->
            </svg>
          </div>
        </div>
      </div>
    </div>

    <!-- Footer -->
    <footer>
      Grade 10 – Term 1 Decision Analysis Framework | 
      <a href="https://github.com" target="_blank" style="color: var(--primary); text-decoration: none;">AI Conversation Record Link</a>
    </footer>
  </div>

  <script>
    // State Data
    let alternatives = ["Expand Capacity", "Subcontract Production", "Status Quo"];
    let states = ["High Demand", "Moderate Demand", "Low Demand"];
    let probabilities = [0.35, 0.45, 0.20];
    let payoffs = [
      [250, 120, -50],
      [140, 90, 10],
      [50, 40, 30]
    ];

    const examples = {
      1: {
        alternatives: ["Expand Capacity", "Subcontract Production", "Status Quo"],
        states: ["High Demand", "Moderate Demand", "Low Demand"],
        probabilities: [0.35, 0.45, 0.20],
        payoffs: [
          [250, 120, -50],
          [140, 90, 10],
          [50, 40, 30]
        ]
      },
      2: {
        alternatives: ["Plant Corn", "Plant Wheat", "Plant Soybeans"],
        states: ["Favorable Weather", "Normal Weather", "Drought"],
        probabilities: [0.30, 0.50, 0.20],
        payoffs: [
          [180, 110, -30],
          [120, 95, 20],
          [100, 80, 40]
        ]
      }
    };

    function loadExample() {
      const id = document.getElementById("exampleSelect").value;
      const ex = examples[id];
      alternatives = [...ex.alternatives];
      states = [...ex.states];
      probabilities = [...ex.probabilities];
      payoffs = ex.payoffs.map(row => [...row]);
      renderTable();
      calculateAll();
    }

    function renderTable() {
      const table = document.getElementById("payoffTable");
      let html = "<thead><tr><th>Alternative / State</th>";
      
      states.forEach((st, idx) => {
        html += `<th><input type="text" value="${st}" onchange="updateStateName(${idx}, this.value)"></th>`;
      });
      html += "</tr><tr><th>State Probabilities</th>";

      probabilities.forEach((p, idx) => {
        html += `<th><input type="number" step="0.05" min="0" max="1" value="${p}" onchange="updateProb(${idx}, this.value)"></th>`;
      });
      html += "</tr></thead><tbody>";

      alternatives.forEach((alt, rIdx) => {
        html += `<tr><td><input type="text" value="${alt}" onchange="updateAltName(${rIdx}, this.value)"></td>`;
        states.forEach((_, cIdx) => {
          const val = payoffs[rIdx] && payoffs[rIdx][cIdx] !== undefined ? payoffs[rIdx][cIdx] : 0;
          html += `<td><input type="number" value="${val}" onchange="updatePayoff(${rIdx}, ${cIdx}, this.value)"></td>`;
        });
        html += "</tr>";
      });

      html += "</tbody>";
      table.innerHTML = html;

      // Probability check
      const sum = probabilities.reduce((a, b) => a + b, 0);
      const warn = document.getElementById("probWarning");
      if (Math.abs(sum - 1.0) > 0.01) {
        warn.style.display = "block";
        warn.innerText = `Warning: Probabilities sum to ${sum.toFixed(2)} (must equal 1.00)`;
      } else {
        warn.style.display = "none";
      }
    }

    function updateStateName(idx, val) { states[idx] = val; }
    function updateAltName(idx, val) { alternatives[idx] = val; }
    function updateProb(idx, val) { probabilities[idx] = parseFloat(val) || 0; calculateAll(); }
    function updatePayoff(r, c, val) { payoffs[r][c] = parseFloat(val) || 0; calculateAll(); }

    function addAlternative() {
      alternatives.push(`Alternative ${alternatives.length + 1}`);
      payoffs.push(new Array(states.length).fill(0));
      renderTable();
      calculateAll();
    }

    function removeAlternative() {
      if (alternatives.length > 1) {
        alternatives.pop();
        payoffs.pop();
        renderTable();
        calculateAll();
      }
    }

    function addState() {
      states.push(`State ${states.length + 1}`);
      probabilities.push(0);
      payoffs.forEach(row => row.push(0));
      renderTable();
      calculateAll();
    }

    function removeState() {
      if (states.length > 1) {
        states.pop();
        probabilities.pop();
        payoffs.forEach(row => row.pop());
        renderTable();
        calculateAll();
      }
    }

    function calculateAll() {
      if (!payoffs.length || !payoffs[0].length) return;

      // 1. Maximax
      const maxes = payoffs.map(row => Math.max(...row));
      const maxVal = Math.max(...maxes);
      const maximaxAlts = alternatives.filter((_, i) => maxes[i] === maxVal);
      document.getElementById("valMaximax").innerText = maxVal;
      document.getElementById("altMaximax").innerText = maximaxAlts.join(", ");

      // 2. Maximin
      const mins = payoffs.map(row => Math.min(...row));
      const minVal = Math.max(...mins);
      const maximinAlts = alternatives.filter((_, i) => mins[i] === minVal);
      document.getElementById("valMaximin").innerText = minVal;
      document.getElementById("altMaximin").innerText = maximinAlts.join(", ");

      // 3. Minimax Regret
      const maxColValues = states.map((_, cIdx) => Math.max(...payoffs.map(r => r[cIdx])));
      const regretTable = payoffs.map(row => row.map((val, cIdx) => maxColValues[cIdx] - val));
      const maxRegrets = regretTable.map(row => Math.max(...row));
      const minRegretVal = Math.min(...maxRegrets);
      const regretAlts = alternatives.filter((_, i) => maxRegrets[i] === minRegretVal);
      document.getElementById("valRegret").innerText = minRegretVal;
      document.getElementById("altRegret").innerText = regretAlts.join(", ");

      // 4. EMV / Bayes
      const emvs = payoffs.map(row => row.reduce((sum, val, cIdx) => sum + val * (probabilities[cIdx] || 0), 0));
      const maxEMVVal = Math.max(...emvs);
      const emvAlts = alternatives.filter((_, i) => Math.abs(emvs[i] - maxEMVVal) < 0.001);
      document.getElementById("valEMV").innerText = maxEMVVal.toFixed(2);
      document.getElementById("altEMV").innerText = emvAlts.join(", ");

      // Staged Filtering
      renderFlowDiagram({
        maximax: maximaxAlts,
        maximin: maximinAlts,
        regret: regretAlts,
        emv: emvAlts
      });
    }

    function renderFlowDiagram(criteriaResults) {
      const s1Type = document.getElementById("stage1Criteria").value;
      const s2Type = document.getElementById("stage2Criteria").value;

      let stage0Alts = [...alternatives];
      let stage1Alts = s1Type !== "none" ? criteriaResults[s1Type] : stage0Alts;
      let stage2Alts = s2Type !== "none" ? stage1Alts.filter(alt => criteriaResults[s2Type].includes(alt)) : stage1Alts;
      
      // If stage 2 filter removes everything, fallback to stage 1 remaining
      if (stage2Alts.length === 0) stage2Alts = stage1Alts;

      const svg = document.getElementById("flowDiagram");
      svg.innerHTML = `
        <!-- Connectors -->
        <line x1="200" y1="100" x2="270" y2="100" class="connector-line" />
        <line x1="470" y1="100" x2="540" y2="100" class="connector-line" />

        <!-- Stage 0 -->
        <g transform="translate(10, 30)">
          <rect class="stage-box" width="190" height="140" />
          <text x="15" y="30" class="stage-text-title">Initial Pool</text>
          <text x="15" y="55" class="stage-text-detail">${stage0Alts.length} Alternatives</text>
          <text x="15" y="85" class="stage-text-detail">${stage0Alts.slice(0, 2).join(", ")}${stage0Alts.length > 2 ? '...' : ''}</text>
        </g>

        <!-- Stage 1 -->
        <g transform="translate(270, 30)">
          <rect class="stage-box active" width="200" height="140" />
          <text x="15" y="30" class="stage-text-title">Stage 1 Filter</text>
          <text x="15" y="50" class="stage-text-detail">Criterion: ${s1Type.toUpperCase()}</text>
          <text x="15" y="75" class="stage-text-detail">Passed: ${stage1Alts.length}</text>
          <text x="15" y="100" class="stage-text-detail" fill="#2563eb">${stage1Alts.join(", ")}</text>
        </g>

        <!-- Stage 2 / Final -->
        <g transform="translate(540, 30)">
          <rect class="stage-box active" width="200" height="140" stroke="#10b981" />
          <text x="15" y="30" class="stage-text-title">Stage 2 / Selected</text>
          <text x="15" y="50" class="stage-text-detail">Criterion: ${s2Type.toUpperCase()}</text>
          <text x="15" y="75" class="stage-text-detail">Optimal Choice:</text>
          <text x="15" y="100" font-weight="bold" fill="#10b981">${stage2Alts.join(", ")}</text>
        </g>
      `;
    }

    // Initial Load
    renderTable();
    calculateAll();
  </script>
</body>
</html>
