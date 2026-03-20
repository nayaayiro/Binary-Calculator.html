# Binary-Calculator.html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">
  <title>Binary Master | Arithmetic & Conversions</title>
  <style>
    * {
      box-sizing: border-box;
      font-family: 'Segoe UI', 'Inter', system-ui, monospace;
    }
    body {
      background: linear-gradient(145deg, #10141e 0%, #0b0f17 100%);
      margin: 0;
      min-height: 100vh;
      display: flex;
      justify-content: center;
      align-items: center;
      padding: 24px;
    }
    .calculator {
      max-width: 1300px;
      width: 100%;
      background: rgba(18, 25, 40, 0.85);
      backdrop-filter: blur(10px);
      border-radius: 48px;
      padding: 28px;
      box-shadow: 0 25px 45px -12px rgba(0,0,0,0.5);
      border: 1px solid rgba(255,255,255,0.1);
    }
    h1 {
      font-size: 2rem;
      font-weight: 600;
      margin: 0 0 6px 0;
      background: linear-gradient(135deg, #c084fc, #60a5fa);
      -webkit-background-clip: text;
      background-clip: text;
      color: transparent;
      letter-spacing: -0.5px;
    }
    .sub {
      color: #94a3b8;
      margin-bottom: 32px;
      border-left: 3px solid #3b82f6;
      padding-left: 16px;
    }
    .grid-2col {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(400px, 1fr));
      gap: 28px;
    }
    .card {
      background: #0f172ad9;
      border-radius: 32px;
      padding: 1.8rem;
      border: 1px solid #334155;
      transition: all 0.2s;
    }
    .card-title {
      font-size: 1.5rem;
      font-weight: 600;
      margin-top: 0;
      margin-bottom: 1.2rem;
      display: flex;
      align-items: center;
      gap: 12px;
      color: #e2e8f0;
    }
    .input-group {
      margin-bottom: 1.2rem;
    }
    label {
      display: block;
      font-size: 0.8rem;
      text-transform: uppercase;
      letter-spacing: 1px;
      font-weight: 500;
      color: #94a3b8;
      margin-bottom: 6px;
    }
    input, select, button {
      width: 100%;
      padding: 12px 16px;
      background: #1e293b;
      border: 1px solid #334155;
      border-radius: 20px;
      color: #f1f5f9;
      font-size: 1rem;
      font-family: 'JetBrains Mono', monospace;
      outline: none;
      transition: 0.2s;
    }
    input:focus, select:focus {
      border-color: #60a5fa;
      box-shadow: 0 0 0 2px rgba(96,165,250,0.3);
    }
    .row-buttons {
      display: flex;
      gap: 14px;
      flex-wrap: wrap;
      margin: 20px 0 16px;
    }
    button {
      background: #3b82f6;
      border: none;
      font-weight: 600;
      cursor: pointer;
      width: auto;
      padding: 10px 24px;
      font-family: inherit;
    }
    button:hover {
      background: #2563eb;
      transform: translateY(-1px);
    }
    .secondary {
      background: #334155;
    }
    .secondary:hover {
      background: #475569;
    }
    .result-area {
      background: #0a0f1c;
      border-radius: 24px;
      padding: 16px;
      margin-top: 20px;
      border-left: 4px solid #3b82f6;
    }
    .result-label {
      font-size: 0.7rem;
      color: #60a5fa;
      letter-spacing: 1px;
    }
    .result-value {
      font-size: 1.5rem;
      font-weight: 700;
      font-family: monospace;
      word-break: break-word;
      color: #facc15;
    }
    .steps-box {
      background: #111827;
      border-radius: 16px;
      padding: 12px;
      margin-top: 12px;
      font-family: monospace;
      font-size: 0.8rem;
      white-space: pre-wrap;
      border-left: 3px solid #facc15;
      max-height: 200px;
      overflow-y: auto;
    }
    .toggle-switch {
      display: flex;
      align-items: center;
      gap: 12px;
      cursor: pointer;
      margin: 10px 0;
    }
    .error-text {
      color: #f87171;
      font-size: 0.75rem;
    }
    hr {
      border-color: #334155;
      margin: 20px 0;
    }
    @media (max-width: 860px) {
      .calculator { padding: 18px; }
      .grid-2col { gap: 20px; }
    }
  </style>
</head>
<body>
<div class="calculator">
  <h1>⚡ BINARY CALCULATOR</h1>
  <div class="sub">Precision arithmetic · fractional support · step-by-step logic</div>

  <div class="grid-2col">
    <!-- ARITHMETIC SECTION -->
    <div class="card">
      <div class="card-title">🔢 Binary Operations</div>
      <div class="input-group">
        <label>📥 First binary number (A)</label>
        <input type="text" id="binA" placeholder="e.g., 1011.01" value="1011">
      </div>
      <div class="input-group">
        <label>📥 Second binary number (B)</label>
        <input type="text" id="binB" placeholder="e.g., 11.1" value="11">
      </div>
      <div class="input-group">
        <label>⚙️ Operation</label>
        <select id="operation">
          <option value="add">➕ Addition (A + B)</option>
          <option value="sub">➖ Subtraction (A − B)</option>
          <option value="mul">✖️ Multiplication (A × B)</option>
          <option value="div">➗ Division (A ÷ B)</option>
        </select>
      </div>
      <div class="toggle-switch">
        <input type="checkbox" id="showSteps">
        <label style="margin:0;">🔍 Show calculation steps</label>
      </div>
      <div class="row-buttons">
        <button id="computeBtn">🧮 Calculate</button>
        <button id="testCaseBtn" class="secondary">🧪 Test: 101 + 11</button>
      </div>
      <div class="result-area">
        <div class="result-label">BINARY RESULT</div>
        <div class="result-value" id="binaryRes">—</div>
        <div class="result-label" style="margin-top: 12px;">DECIMAL EQUIVALENT</div>
        <div class="result-value" id="decimalRes" style="font-size:1rem;">—</div>
        <div id="stepsContainer" class="steps-box" style="display: none;"></div>
      </div>
    </div>

    <!-- CONVERSIONS SECTION -->
    <div class="card">
      <div class="card-title">🔄 Conversions</div>
      <div class="input-group">
        <label>Binary → Decimal (fractional)</label>
        <div style="display: flex; gap: 8px;">
          <input type="text" id="binToDecInput" value="1001.0101">
          <button id="binToDecBtn" style="width: auto;">→ Dec</button>
        </div>
        <div class="result-area" style="margin-top: 10px;">
          <span style="font-weight:500;">Decimal: </span><span id="decResult">—</span>
          <div id="decBreakdown" style="font-size:0.7rem; color:#cbd5e1; margin-top: 6px;"></div>
        </div>
      </div>
      <hr>
      <div class="input-group">
        <label>Decimal → Binary</label>
        <div style="display: flex; gap: 8px;">
          <input type="text" id="decToBinInput" value="9.3125">
          <button id="decToBinBtn" style="width: auto;">→ Bin</button>
        </div>
        <div class="result-area" style="margin-top: 10px;">
          Binary: <span id="binFromDec">—</span>
        </div>
      </div>
      <hr>
      <div class="input-group">
        <label>Binary → Hexadecimal</label>
        <div style="display: flex; gap: 8px;">
          <input type="text" id="binHexInput" value="1101.1011">
          <button id="binToHexBtn" style="width: auto;">→ Hex</button>
        </div>
        <div class="result-area">Hex: <span id="hexVal">—</span></div>
      </div>
      <div class="input-group">
        <label>Binary → Octal</label>
        <div style="display: flex; gap: 8px;">
          <input type="text" id="binOctInput" value="1011.01">
          <button id="binToOctBtn" style="width: auto;">→ Octal</button>
        </div>
        <div class="result-area">Octal: <span id="octVal">—</span></div>
      </div>
    </div>
  </div>
</div>

<script>
  // ---------- UTILITIES ----------
  function isValidBinary(str) {
    if (!str || str.trim() === "") return false;
    const trimmed = str.trim();
    const dotCount = (trimmed.match(/\./g) || []).length;
    if (dotCount > 1) return false;
    return /^[01]+(\.[01]+)?$/.test(trimmed);
  }

  // Binary string → decimal (exact with Number)
  function binaryToDecimal(binStr) {
    if (!isValidBinary(binStr)) throw new Error("Invalid binary format");
    const parts = binStr.trim().split('.');
    let intPart = parts[0] || "0";
    let fracPart = parts[1] || "";
    let decimal = 0;
    for (let i = 0; i < intPart.length; i++) {
      if (intPart[i] === '1') decimal += Math.pow(2, intPart.length - 1 - i);
    }
    for (let i = 0; i < fracPart.length; i++) {
      if (fracPart[i] === '1') decimal += Math.pow(2, -(i + 1));
    }
    return decimal;
  }

  // Decimal → binary (fractional with max bits)
  function decimalToBinary(decimalNum, maxFracBits = 12) {
    if (isNaN(decimalNum)) throw new Error("Invalid decimal");
    let num = decimalNum;
    let sign = num < 0 ? "-" : "";
    num = Math.abs(num);
    let intPart = Math.floor(num);
    let fracPart = num - intPart;
    let intBinary = intPart === 0 ? "0" : "";
    let temp = intPart;
    while (temp > 0) {
      intBinary = (temp % 2) + intBinary;
      temp = Math.floor(temp / 2);
    }
    if (intBinary === "") intBinary = "0";
    let fracBinary = "";
    let f = fracPart;
    let count = 0;
    while (f > 0 && count < maxFracBits) {
      f *= 2;
      if (f >= 1) {
        fracBinary += "1";
        f -= 1;
      } else {
        fracBinary += "0";
      }
      count++;
    }
    if (fracBinary.length === 0) return sign + intBinary;
    return sign + intBinary + "." + fracBinary;
  }

  // Binary arithmetic helpers with step generation
  function alignBinary(a, b) {
    let [intA, fracA] = a.split('.');
    let [intB, fracB] = b.split('.');
    intA = intA || "0"; intB = intB || "0";
    fracA = fracA || ""; fracB = fracB || "";
    const maxFrac = Math.max(fracA.length, fracB.length);
    fracA = fracA.padEnd(maxFrac, '0');
    fracB = fracB.padEnd(maxFrac, '0');
    const maxInt = Math.max(intA.length, intB.length);
    intA = intA.padStart(maxInt, '0');
    intB = intB.padStart(maxInt, '0');
    return { intA, intB, fracA, fracB, maxFrac, maxInt };
  }

  function addBinary(a, b) {
    if (!isValidBinary(a) || !isValidBinary(b)) throw new Error("Invalid binary input");
    const { intA, intB, fracA, fracB, maxFrac } = alignBinary(a, b);
    let carry = 0;
    let resFrac = "";
    for (let i = maxFrac - 1; i >= 0; i--) {
      let sum = carry + parseInt(fracA[i]) + parseInt(fracB[i]);
      resFrac = (sum % 2) + resFrac;
      carry = Math.floor(sum / 2);
    }
    let resInt = "";
    const maxInt = Math.max(intA.length, intB.length);
    for (let i = maxInt - 1; i >= 0; i--) {
      let sum = carry + parseInt(intA[i]) + parseInt(intB[i]);
      resInt = (sum % 2) + resInt;
      carry = Math.floor(sum / 2);
    }
    if (carry) resInt = "1" + resInt;
    let result = resInt.replace(/^0+/, '') || "0";
    if (resFrac.length) result += "." + resFrac.replace(/0+$/, '');
    return result;
  }

  function subtractBinary(a, b) {
    if (!isValidBinary(a) || !isValidBinary(b)) throw new Error("Invalid binary input");
    const aDec = binaryToDecimal(a);
    const bDec = binaryToDecimal(b);
    if (aDec < bDec) {
      // return negative result
      let pos = subtractBinary(b, a);
      return pos === "0" ? "0" : "-" + pos;
    }
    const { intA, intB, fracA, fracB, maxFrac } = alignBinary(a, b);
    let borrow = 0;
    let resFrac = "";
    for (let i = maxFrac - 1; i >= 0; i--) {
      let diff = parseInt(fracA[i]) - borrow - parseInt(fracB[i]);
      if (diff < 0) { diff += 2; borrow = 1; } else borrow = 0;
      resFrac = diff + resFrac;
    }
    let resInt = "";
    const maxInt = Math.max(intA.length, intB.length);
    for (let i = maxInt - 1; i >= 0; i--) {
      let diff = parseInt(intA[i]) - borrow - parseInt(intB[i]);
      if (diff < 0) { diff += 2; borrow = 1; } else borrow = 0;
      resInt = diff + resInt;
    }
    let result = resInt.replace(/^0+/, '') || "0";
    if (resFrac.length && !/^0+$/.test(resFrac)) result += "." + resFrac.replace(/0+$/, '');
    return result;
  }

  function multiplyBinary(a, b) {
    let aDec = binaryToDecimal(a);
    let bDec = binaryToDecimal(b);
    let prod = aDec * bDec;
    return decimalToBinary(prod, 12);
  }

  function divideBinary(a, b) {
    let bDec = binaryToDecimal(b);
    if (Math.abs(bDec) < 1e-12) throw new Error("Division by zero");
    let aDec = binaryToDecimal(a);
    let quot = aDec / bDec;
    return decimalToBinary(quot, 12);
  }

  // step descriptions
  function getOperationSteps(op, a, b, res) {
    if (op === 'add') return `➕ Addition: ${a} + ${b}\n➡️ Align binary points, column addition with carry.\n✅ Result = ${res}`;
    if (op === 'sub') return `➖ Subtraction: ${a} - ${b}\n➡️ Borrow method. Negative sign handled automatically.\n✅ Result = ${res}`;
    if (op === 'mul') {
      let aDec = binaryToDecimal(a), bDec = binaryToDecimal(b);
      return `✖️ Multiplication: ${a} × ${b}\n• Decimal: ${aDec} × ${bDec} = ${aDec*bDec}\n• Convert back to binary → ${res}`;
    }
    if (op === 'div') {
      let aDec = binaryToDecimal(a), bDec = binaryToDecimal(b);
      return `➗ Division: ${a} ÷ ${b}\n• Decimal: ${aDec} / ${bDec} = ${aDec/bDec}\n• Binary result (fractional trimmed) → ${res}`;
    }
    return "";
  }

  // ---------- UI Elements ----------
  const binA = document.getElementById('binA');
  const binB = document.getElementById('binB');
  const operation = document.getElementById('operation');
  const showSteps = document.getElementById('showSteps');
  const computeBtn = document.getElementById('computeBtn');
  const binaryResSpan = document.getElementById('binaryRes');
  const decimalResSpan = document.getElementById('decimalRes');
  const stepsContainer = document.getElementById('stepsContainer');
  const testCaseBtn = document.getElementById('testCaseBtn');

  function computeArithmetic() {
    try {
      let a = binA.value.trim();
      let b = binB.value.trim();
      if (!isValidBinary(a)) throw new Error("First binary invalid (only 0/1 and optional dot)");
      if (!isValidBinary(b)) throw new Error("Second binary invalid");
      let op = operation.value;
      let resultBin;
      switch(op) {
        case 'add': resultBin = addBinary(a, b); break;
        case 'sub': resultBin = subtractBinary(a, b); break;
        case 'mul': resultBin = multiplyBinary(a, b); break;
        case 'div': resultBin = divideBinary(a, b); break;
        default: throw new Error("Unknown operation");
      }
      // remove leading zeros for clean display
      if (resultBin && !resultBin.startsWith('-') && resultBin.includes('.')) {
        let [intPart, fracPart] = resultBin.split('.');
        intPart = intPart.replace(/^0+/, '') || "0";
        resultBin = intPart + (fracPart ? "." + fracPart : "");
      } else if (resultBin && !resultBin.startsWith('-')) {
        resultBin = resultBin.replace(/^0+/, '') || "0";
      }
      let resultDec = binaryToDecimal(resultBin.replace(/^-/, ''));
      if (resultBin.startsWith('-')) resultDec = -resultDec;
      binaryResSpan.innerText = resultBin;
      decimalResSpan.innerText = resultDec.toString();
      if (showSteps.checked) {
        stepsContainer.style.display = "block";
        stepsContainer.innerText = getOperationSteps(op, a, b, resultBin);
      } else {
        stepsContainer.style.display = "none";
      }
    } catch (err) {
      binaryResSpan.innerText = "⚠️ Error";
      decimalResSpan.innerText = err.message;
      if (showSteps.checked) {
        stepsContainer.style.display = "block";
        stepsContainer.innerText = `❌ ${err.message}`;
      } else stepsContainer.style.display = "none";
    }
  }

  computeBtn.addEventListener('click', computeArithmetic);
  testCaseBtn.addEventListener('click', () => {
    binA.value = "101";
    binB.value = "11";
    operation.value = "add";
    computeArithmetic();
  });

  // ---------- CONVERSIONS ----------
  // Binary -> Decimal detailed
  const binToDecInput = document.getElementById('binToDecInput');
  const binToDecBtn = document.getElementById('binToDecBtn');
  const decResultSpan = document.getElementById('decResult');
  const decBreakdown = document.getElementById('decBreakdown');
  binToDecBtn.addEventListener('click', () => {
    try {
      let bin = binToDecInput.value.trim();
      if (!isValidBinary(bin)) throw new Error("Invalid binary");
      const parts = bin.split('.');
      const intPart = parts[0];
      const fracPart = parts[1] || "";
      let intSum = 0, intSteps = [];
      for (let i = 0; i < intPart.length; i++) {
        if (intPart[i] === '1') {
          let val = Math.pow(2, intPart.length - 1 - i);
          intSum += val;
          intSteps.push(`1×2^${intPart.length-1-i}=${val}`);
        } else intSteps.push(`0×2^${intPart.length-1-i}=0`);
      }
      let fracSum = 0, fracSteps = [];
      for (let i = 0; i < fracPart.length; i++) {
        if (fracPart[i] === '1') {
          let val = Math.pow(2, -(i+1));
          fracSum += val;
          fracSteps.push(`1×2^-${i+1}=${val}`);
        } else fracSteps.push(`0×2^-${i+1}=0`);
      }
      let total = intSum + fracSum;
      decResultSpan.innerText = total;
      decBreakdown.innerText = `Integer: ${intSteps.join(' + ')} = ${intSum}\nFraction: ${fracSteps.join(' + ')} = ${fracSum}\nTotal = ${total}`;
    } catch(e) {
      decResultSpan.innerText = "Error";
      decBreakdown.innerText = e.message;
    }
  });

  // Decimal -> Binary
  const decToBinInput = document.getElementById('decToBinInput');
  const decToBinBtn = document.getElementById('decToBinBtn');
  const binFromDecSpan = document.getElementById('binFromDec');
  decToBinBtn.addEventListener('click', () => {
    try {
      let decVal = parseFloat(decToBinInput.value);
      if (isNaN(decVal)) throw new Error("Enter a valid decimal number");
      let binary = decimalToBinary(decVal, 12);
      binFromDecSpan.innerText = binary;
    } catch(e) {
      binFromDecSpan.innerText = "❌ " + e.message;
    }
  });

  // Binary to Hex
  const binHexInput = document.getElementById('binHexInput');
  const binToHexBtn = document.getElementById('binToHexBtn');
  const hexValSpan = document.getElementById('hexVal');
  binToHexBtn.addEventListener('click', () => {
    try {
      let bin = binHexInput.value.trim();
      if (!isValidBinary(bin)) throw new Error("Invalid binary");
      let dec = binaryToDecimal(bin);
      let hex = dec.toString(16).toUpperCase();
      hexValSpan.innerText = hex;
    } catch(e) { hexValSpan.innerText = "Error"; }
  });

  // Binary to Octal
  const binOctInput = document.getElementById('binOctInput');
  const binToOctBtn = document.getElementById('binToOctBtn');
  const octValSpan = document.getElementById('octVal');
  binToOctBtn.addEventListener('click', () => {
    try {
      let bin = binOctInput.value.trim();
      if (!isValidBinary(bin)) throw new Error("Invalid binary");
      let dec = binaryToDecimal(bin);
      let oct = dec.toString(8);
      octValSpan.innerText = oct;
    } catch(e) { octValSpan.innerText = "Error"; }
  });

  // Initial demo runs
  window.addEventListener('load', () => {
    computeArithmetic();
    binToDecBtn.click();
    decToBinBtn.click();
    binToHexBtn.click();
    binToOctBtn.click();
  });
</script>
</body>
</html>
