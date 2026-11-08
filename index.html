<!DOCTYPE html>
<html lang="ko">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>경안 분실물 센터</title>

<script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs@4.22.0/dist/tf.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/@teachablemachine/image@0.8.5/dist/teachablemachine-image.min.js"></script>

<style>
*{box-sizing:border-box}
body{margin:0;font-family:Arial,"Malgun Gothic",sans-serif;background:#f2f9ff;color:#243746}
header{background:linear-gradient(135deg,#8ed8ff,#d8f2ff);padding:24px;text-align:center;border-bottom:3px solid #ffdf70}
header h1{margin:0 0 8px;color:#174d70}
header p{margin:0;color:#38647d}
main{max-width:1000px;margin:24px auto;padding:0 16px}
.panel{background:white;border:1px solid #d5eaf5;border-radius:16px;padding:20px;margin-bottom:18px;box-shadow:0 4px 12px #28648c14}
h2{margin-top:0;color:#22658c}
input,select,button{font:inherit}
input[type=text],input[type=file],select{width:100%;padding:11px;border:1px solid #c7dce8;border-radius:9px;margin:7px 0 12px;background:#fbfdff}
button{border:0;border-radius:9px;padding:11px 16px;background:#318bc0;color:white;font-weight:bold;cursor:pointer;margin:4px 3px 4px 0}
button:hover{background:#236f9e}
button.secondary{background:#f2c94c;color:#574400}
button:disabled{opacity:.5;cursor:not-allowed}
.status{padding:12px;border-radius:9px;background:#eef8ff;color:#285c7b;margin-top:10px;white-space:pre-wrap}
.status.error{background:#fff0f0;color:#a83232}
.status.success{background:#effaf0;color:#276b35}
.preview-wrap{text-align:center;margin:12px 0}
#preview{display:none;max-width:100%;max-height:300px;border-radius:12px;border:1px solid #d7e5ed}
.result-grid,.items-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(220px,1fr));gap:12px}
.result-card,.item-card{background:#f7fbfe;border:1px solid #d8eaf4;border-radius:12px;padding:14px}
.item-card h3{margin:0 0 8px;color:#23658a}
.item-card p{margin:5px 0;font-size:14px}
.item-card .match{color:#16803c;font-weight:bold}
@media(max-width:600px){header{padding:18px 12px}.panel{padding:15px}}
</style>
</head>

<body>
<header>
  <h1>🔎 경안 분실물 센터</h1>
  <p>AI가 물품을 인식하고 분실물과 습득물을 연결합니다</p>
</header>

<main>
  <section class="panel">
    <h2>① AI 모델 연결</h2>
    <label for="modelUrl">Teachable Machine 모델 주소</label>
    <input id="modelUrl" type="text"
      value="https://teachablemachine.withgoogle.com/models/o4RSk5MB-/">
    <button id="loadModelBtn">AI 모델 연결하기</button>
    <div id="modelStatus" class="status">모델 연결 전입니다.</div>
  </section>

  <section class="panel">
    <h2>② 물품 사진 분석</h2>
    <label for="imageInput">물품 사진 선택</label>
    <input id="imageInput" type="file" accept="image/*">

    <div class="preview-wrap">
      <img id="preview" alt="선택한 물품 사진">
    </div>

    <button id="analyzeBtn" disabled>사진 AI 분석하기</button>
    <div id="analysisStatus" class="status">먼저 AI 모델을 연결해 주세요.</div>
    <div id="predictionResults" class="result-grid"></div>
  </section>

  <section class="panel">
    <h2>③ 분실물 / 습득물 등록</h2>

    <label for="recordType">등록 유형</label>
    <select id="recordType">
      <option value="분실">분실 신고</option>
      <option value="습득">습득 등록</option>
    </select>

    <label for="zone">위치 구역</label>
    <select id="zone">
      <option value="">위치를 선택하세요</option>
      <option value="교실">교실</option>
      <option value="복도">복도</option>
      <option value="체육관">체육관</option>
      <option value="도서관">도서관</option>
      <option value="운동장">운동장</option>
      <option value="급식실">급식실</option>
      <option value="컴퓨터실">컴퓨터실</option>
    </select>

    <button id="registerBtn" disabled>분실물 등록하기</button>
    <div id="registerStatus" class="status">사진 분석 후 등록할 수 있습니다.</div>
  </section>

  <section class="panel">
    <h2>④ 자동 매칭 결과</h2>
    <div id="matches" class="items-grid">
      분실 신고와 습득 등록이 쌓이면 자동으로 비교합니다.
    </div>
  </section>

  <section class="panel">
    <h2>⑤ 등록된 물품</h2>
    <div id="items" class="items-grid"></div>
  </section>

  <section class="panel">
    <h2>⑥ 마이크로비트 연결</h2>
    <p>마이크로비트를 USB로 연결한 뒤 버튼을 눌러 연결하세요.</p>
    <button id="connectMicrobitBtn" class="secondary">마이크로비트 연결</button>
    <div id="microbitStatus" class="status">연결되지 않았습니다.</div>
  </section>
</main>

<script>
const MODEL_URL_DEFAULT =
  "https://teachablemachine.withgoogle.com/models/o4RSk5MB-/";

let model = null;
let currentPrediction = null;
let currentColor = null;
let currentImage = null;
let items = [];
let serialPort = null;
let serialWriter = null;

const $ = id => document.getElementById(id);

function setStatus(id, message, type = "") {
  const element = $(id);
  element.textContent = message;
  element.className = "status" + (type ? " " + type : "");
}

function normalizeModelUrl(url) {
  url = url.trim();

  if (!url) {
    throw new Error("모델 주소를 입력해 주세요.");
  }

  if (!url.endsWith("/")) url += "/";

  if (!url.startsWith("https://teachablemachine.withgoogle.com/models/")) {
    throw new Error("티처블 머신의 모델 주소를 확인해 주세요.");
  }

  return url;
}

async function loadModel() {
  const button = $("loadModelBtn");
  button.disabled = true;

  try {
    if (typeof tmImage === "undefined") {
      throw new Error("AI 라이브러리를 불러오지 못했습니다. 인터넷 연결을 확인해 주세요.");
    }

    setStatus("modelStatus", "AI 모델을 불러오는 중입니다...");

    const baseUrl = normalizeModelUrl($("modelUrl").value);

    model = await tmImage.load(
      baseUrl + "model.json",
      baseUrl + "metadata.json"
    );

    setStatus(
      "modelStatus",
      "AI 모델 연결 성공! 학습 클래스: " + model.getTotalClasses(),
      "success"
    );

    $("analyzeBtn").disabled = !currentImage;

  } catch (error) {
    model = null;
    $("analyzeBtn").disabled = true;

    setStatus(
      "modelStatus",
      "모델 연결 실패: " + error.message +
      "\n모델 주소와 티처블 머신 업로드 상태를 확인해 주세요.",
      "error"
    );

  } finally {
    button.disabled = false;
  }
}

function loadImageFile(file) {
  if (!file) return;

  if (!file.type.startsWith("image/")) {
    setStatus("analysisStatus", "이미지 파일을 선택해 주세요.", "error");
    return;
  }

  const reader = new FileReader();

  reader.onload = () => {
    const img = $("preview");

    img.onload = () => {
      currentImage = img;
      currentPrediction = null;
      currentColor = null;

      img.style.display = "inline-block";
      $("analyzeBtn").disabled = !model;
      $("registerBtn").disabled = true;
      $("predictionResults").innerHTML = "";

      setStatus(
        "analysisStatus",
        model
          ? "사진이 준비되었습니다. AI 분석을 눌러 주세요."
          : "사진이 준비되었습니다. 먼저 AI 모델을 연결해 주세요."
      );
    };

    img.onerror = () => {
      currentImage = null;
      setStatus("analysisStatus", "사진을 불러오지 못했습니다.", "error");
    };

    img.src = reader.result;
  };

  reader.onerror = () => {
    setStatus("analysisStatus", "파일을 읽을 수 없습니다.", "error");
  };

  reader.readAsDataURL(file);
}

function estimateColor(img) {
  const canvas = document.createElement("canvas");
  const ctx = canvas.getContext("2d", { willReadFrequently: true });

  canvas.width = 80;
  canvas.height = 80;
  ctx.drawImage(img, 0, 0, 80, 80);

  const data = ctx.getImageData(0, 0, 80, 80).data;

  let rTotal = 0, gTotal = 0, bTotal = 0, count = 0;

  for (let i = 0; i < data.length; i += 4) {
    const r = data[i], g = data[i + 1], b = data[i + 2];
    const brightness = (r + g + b) / 3;

    if (brightness < 18 || brightness > 245) continue;

    rTotal += r;
    gTotal += g;
    bTotal += b;
    count++;
  }

  if (!count) return "혼합색";

  const r = rTotal / count;
  const g = gTotal / count;
  const b = bTotal / count;

  const max = Math.max(r, g, b);
  const min = Math.min(r, g, b);
  const diff = max - min;

  if (max < 65) return "검은색";
  if (min > 205) return "흰색";

  if (diff < 25) {
    return max < 130 ? "회색" : "밝은 회색";
  }

  if (r > 170 && g > 130 && b < 110) return "노란색";

  if (r > g * 1.35 && r > b * 1.25) {
    return g > 100 ? "주황색" : "빨간색";
  }

  if (g > r * 1.2 && g > b * 1.1) return "초록색";
  if (b > r * 1.15 && b > g * 1.1) return "파란색";
  if (r > 150 && b > 130 && g < 150) return "분홍색";
  if (r > g && g > b && r < 180) return "갈색";

  return "혼합색";
}

async function analyzeImage() {
  if (!model) {
    setStatus("analysisStatus", "먼저 AI 모델을 연결해 주세요.", "error");
    return;
  }

  if (!currentImage || !currentImage.complete) {
    setStatus("analysisStatus", "먼저 사진을 선택해 주세요.", "error");
    return;
  }

  $("analyzeBtn").disabled = true;
  $("registerBtn").disabled = true;

  try {
    setStatus("analysisStatus", "AI가 사진을 분석하고 있습니다...");

    const predictions = await model.predict(currentImage);
    predictions.sort((a, b) => b.probability - a.probability);

    currentPrediction = predictions[0];
    currentColor = estimateColor(currentImage);

    const confidence = Math.round(currentPrediction.probability * 100);
    const results = $("predictionResults");
    results.innerHTML = "";

    predictions.forEach(prediction => {
      const card = document.createElement("div");
      card.className = "result-card";

      const name = document.createElement("strong");
      name.textContent = prediction.className;

      const percentage = document.createElement("p");
      percentage.textContent =
        Math.round(prediction.probability * 100) + "%";

      card.append(name, percentage);
      results.appendChild(card);
    });

    if (confidence < 60) {
      setStatus(
        "analysisStatus",
        "AI 확신도가 낮습니다 (" + confidence +
        "%). 사진을 더 선명하게 찍어 다시 분석해 주세요.",
        "error"
      );
      return;
    }

    setStatus(
      "analysisStatus",
      "분석 완료: " + currentPrediction.className +
      "\n추정 색상: " + currentColor +
      "\nAI 확신도: " + confidence + "%",
      "success"
    );

    $("registerBtn").disabled = false;

  } catch (error) {
    setStatus("analysisStatus", "사진 분석 실패: " + error.message, "error");

  } finally {
    $("analyzeBtn").disabled = !model;
  }
}

function createItem() {
  if (!currentPrediction || !currentColor) {
    setStatus("registerStatus", "먼저 사진을 분석해 주세요.", "error");
    return;
  }

  const zone = $("zone").value;

  if (!zone) {
    setStatus("registerStatus", "위치 구역을 선택해 주세요.", "error");
    return;
  }

  const type = $("recordType").value;

  const item = {
    id: Date.now(),
    type: type,
    name: currentPrediction.className,
    color: currentColor,
    feature: currentColor + " " + currentPrediction.className,
    zone: zone,
    confidence: currentPrediction.probability,
    date: new Date().toLocaleString("ko-KR")
  };

  items.unshift(item);

  renderItems();
  renderMatches();

  setStatus(
    "registerStatus",
    item.feature + " 물품이 " + type + "으로 등록되었습니다.",
    "success"
  );

  $("registerBtn").disabled = true;
  currentPrediction = null;
}

function renderItems() {
  const container = $("items");
  container.innerHTML = "";

  if (items.length === 0) {
    container.textContent = "아직 등록된 물품이 없습니다.";
    return;
  }

  items.forEach(item => {
    const card = document.createElement("div");
    card.className = "item-card";

    const title = document.createElement("h3");
    title.textContent =
      (item.type === "분실" ? "🔍 분실" : "📦 습득") + " · " + item.name;

    const feature = document.createElement("p");
    feature.textContent = "AI 특징: " + item.feature;

    const location = document.createElement("p");
    location.textContent = "위치: " + item.zone;

    const date = document.createElement("p");
    date.textContent = "등록: " + item.date;

    const sendButton = document.createElement("button");
    sendButton.className = "secondary";
    sendButton.textContent = "마이크로비트로 전송";
    sendButton.addEventListener("click", () => sendToMicrobit(item));

    card.append(title, feature, location, date, sendButton);
    container.appendChild(card);
  });
}

function renderMatches() {
  const container = $("matches");
  container.innerHTML = "";

  const lostItems = items.filter(item => item.type === "분실");
  const foundItems = items.filter(item => item.type === "습득");
  const matches = [];

  lostItems.forEach(lost => {
    foundItems.forEach(found => {
      let score = 0;

      if (lost.name === found.name) score += 2;
      if (lost.color === found.color) score += 1;
      if (lost.zone === found.zone) score += 1;

      if (score >= 3) matches.push({ lost, found, score });
    });
  });

  if (matches.length === 0) {
    container.textContent = "현재 일치하는 분실물과 습득물이 없습니다.";
    return;
  }

  matches.forEach(match => {
    const card = document.createElement("div");
    card.className = "item-card";

    const title = document.createElement("h3");
    title.textContent = "🔗 유사 물품 발견";

    const lost = document.createElement("p");
    lost.textContent =
      "분실 신고: " + match.lost.feature + " · " + match.lost.zone;

    const found = document.createElement("p");
    found.textContent =
      "습득 등록: " + match.found.feature + " · " + match.found.zone;

    const score = document.createElement("p");
    score.className = "match";
    score.textContent = "일치 점수: " + match.score + "/4";

    card.append(title, lost, found, score);
    container.appendChild(card);
  });
}

function toEnglishItem(name) {
  const map = {
    "무선이어폰": "EARBUDS",
    "지갑": "WALLET",
    "볼펜": "PEN",
    "카드": "CARD"
  };

  return map[name] || name.toUpperCase();
}

function toEnglishColor(color) {
  const map = {
    "검은색": "BLACK",
    "흰색": "WHITE",
    "회색": "GRAY",
    "밝은 회색": "LIGHT GRAY",
    "빨간색": "RED",
    "주황색": "ORANGE",
    "노란색": "YELLOW",
    "초록색": "GREEN",
    "파란색": "BLUE",
    "분홍색": "PINK",
    "갈색": "BROWN",
    "혼합색": "MIXED"
  };

  return map[color] || color.toUpperCase();
}

function toEnglishZone(zone) {
  const map = {
    "교실": "CLASSROOM",
    "복도": "HALL",
    "체육관": "GYM",
    "도서관": "LIBRARY",
    "운동장": "FIELD",
    "급식실": "CAFETERIA",
    "컴퓨터실": "COMPUTER"
  };

  return map[zone] || zone.toUpperCase();
}

async function connectMicrobit() {
  if (!("serial" in navigator)) {
    setStatus(
      "microbitStatus",
      "이 브라우저는 Web Serial을 지원하지 않습니다. Chrome 또는 Edge를 사용해 주세요.",
      "error"
    );
    return;
  }

  try {
    serialPort = await navigator.serial.requestPort();
    await serialPort.open({ baudRate: 115200 });
    serialWriter = serialPort.writable.getWriter();

    setStatus("microbitStatus", "마이크로비트 연결 성공!", "success");

  } catch (error) {
    serialPort = null;
    serialWriter = null;

    setStatus("microbitStatus", "연결 실패: " + error.message, "error");
  }
}

async function sendToMicrobit(item) {
  if (!serialWriter) {
    setStatus("microbitStatus", "먼저 마이크로비트를 연결해 주세요.", "error");
    return;
  }

  try {
    const message =
      "ITEM|" + toEnglishItem(item.name) +
      "|" + toEnglishColor(item.color) +
      "|" + toEnglishZone(item.zone) + "\n";

    await serialWriter.write(new TextEncoder().encode(message));

    setStatus("microbitStatus", "마이크로비트 전송 완료!", "success");

  } catch (error) {
    setStatus("microbitStatus", "전송 실패: " + error.message, "error");
  }
}

$("loadModelBtn").addEventListener("click", loadModel);

$("imageInput").addEventListener("change", event => {
  loadImageFile(event.target.files[0]);
});

$("analyzeBtn").addEventListener("click", analyzeImage);
$("registerBtn").addEventListener("click", createItem);
$("connectMicrobitBtn").addEventListener("click", connectMicrobit);

$("modelUrl").value = MODEL_URL_DEFAULT;

renderItems();
renderMatches();
</script>
</body>
</html>
