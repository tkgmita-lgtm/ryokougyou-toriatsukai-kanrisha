// --- 1. 学習データの定義 ---
const textbookData = [
  {
    unit: "単元1：旅行業の登録",
    content: "・旅行業を営むには、観光庁長官または都道府県知事の「登録」が必要。\n・有効期間は「5年」。更新は有効期間満了の「2ヶ月前」までに申請。\n★ポイント：有効期間を3年と引っ掛けてくる問題が多いので注意！"
  },
  {
    unit: "単元2：旅行業務取扱管理者",
    content: "・営業所ごとに、1名以上の旅行業務取扱管理者を選任しなければならない。\n・従業員が10名以上の営業所では、複数の選任が必要。\n★ポイント：試験合格＝管理者になれるわけではない。営業所で「選任」されて初めて管理者となる。"
  }
];

const practiceData = [
  {
    question: "旅行業の登録の有効期間は3年であり、期間満了後も引き続き事業を営む場合は更新登録が必要である。",
    answer: false,
    explanation: "×です。有効期間は「5年」です。引っかけの定番なので注意しましょう。"
  },
  {
    question: "旅行業者は、1つの営業所につき、従業員10人ごとに1名以上の旅行業務取扱管理者を選任しなければならない。",
    answer: false,
    explanation: "×です。「10人ごとに1人」ではなく、「従業員が10人以上の営業所においては、複数人」選任すれば足ります。"
  }
];

const pastExamData = [
  {
    question: "[過去問] 企画旅行に参加する旅行者が提供を受けるサービスは、運送等サービスのみである。",
    answer: false,
    explanation: "×です。運送や宿泊だけでなく、それらに付随するサービスも含まれます。"
  },
  {
    question: "[過去問] 旅行業協会に加入している旅行業者は、営業保証金を供託する必要はない。",
    answer: true,
    explanation: "〇です。旅行業協会（JATAやANTA）の保証社員になれば、「弁済業務保証金分担金」を納付することで、営業保証金の供託は免除されます。"
  }
];

// --- 2. アプリの制御ロジック ---
let currentQuizData = [];
let currentQuestionIndex = 0;

function showScreen(screenId) {
  document.querySelectorAll('.screen').forEach(screen => {
    screen.classList.remove('active');
  });
  const targetScreen = document.getElementById(screenId);
  if (targetScreen) {
    targetScreen.classList.add('active');
  }
}

function goHome() {
  showScreen('home-screen');
}

function renderTextbook() {
  const container = document.getElementById('textbook-content');
  if (!container) return;
  container.innerHTML = '';
  textbookData.forEach(item => {
    const box = document.createElement('div');
    box.className = 'unit-box';
    box.innerHTML = `<h3>${item.unit}</h3><p>${item.content}</p>`;
    container.appendChild(box);
  });
}

function startQuiz(type) {
  const resultContainer = document.getElementById('result-container');
  const answerButtons = document.querySelector('.answer-buttons');
  if (resultContainer) resultContainer.classList.add('hidden');
  if (answerButtons) answerButtons.classList.remove('hidden');

  if (type === 'practice') {
    document.getElementById('quiz-title').innerText = "練習問題 (引っかけ注意)";
    currentQuizData = [...practiceData].sort(() => Math.random() - 0.5);
  } else if (type === 'past') {
    document.getElementById('quiz-title').innerText = "過去問題 (一問一答)";
    currentQuizData = [...pastExamData].sort(() => Math.random() - 0.5);
  }
  
  currentQuestionIndex = 0;
  showQuestion();
}

function showQuestion() {
  if (currentQuestionIndex >= currentQuizData.length) {
    document.getElementById('question-text').innerText = "すべての問題が終了しました！お疲れ様でした！";
    const answerButtons = document.querySelector('.answer-buttons');
    const resultContainer = document.getElementById('result-container');
    if (answerButtons) answerButtons.classList.add('hidden');
    if (resultContainer) resultContainer.classList.add('hidden');
    return;
  }
  document.getElementById('question-text').innerText = currentQuizData[currentQuestionIndex].question;
  const resultContainer = document.getElementById('result-container');
  const answerButtons = document.querySelector('.answer-buttons');
  if (resultContainer) resultContainer.classList.add('hidden');
  if (answerButtons) answerButtons.classList.remove('hidden');
}

function answer(userAnswer) {
  const currentQ = currentQuizData[currentQuestionIndex];
  const isCorrect = (userAnswer === currentQ.answer);
  
  const resultText = document.getElementById('result-text');
  if (isCorrect) {
    resultText.innerText = "⭕ 正解！";
    resultText.style.color = "#5cb85c";
  } else {
    resultText.innerText = "❌ 不正解...";
    resultText.style.color = "#d9534f";
  }
  
  document.getElementById('explanation-text').innerText = currentQ.explanation;
  
  const answerButtons = document.querySelector('.answer-buttons');
  const resultContainer = document.getElementById('result-container');
  if (answerButtons) answerButtons.classList.add('hidden');
  if (resultContainer) resultContainer.classList.remove('hidden');
}

function nextQuestion() {
  currentQuestionIndex++;
  showQuestion();
}

// ページが読み込まれたら実行
window.onload = function() {
  renderTextbook();
};
