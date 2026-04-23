<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Mid-Term Chinese Exam</title>
<link href="https://fonts.googleapis.com/css2?family=Noto+Serif+SC:wght@400;700&family=DM+Sans:wght@400;500;600&display=swap" rel="stylesheet">
<style>
  :root {
    --primary: #2c5f8a;
    --accent: #e07b39;
    --success: #3a9a6e;
    --danger: #c0392b;
    --bg: #f5f0e8;
    --card-bg: #fffef9;
    --text: #1a1a2e;
    --muted: #6b6b7b;
    --border: #ddd5c0;
  }

  * { box-sizing: border-box; margin: 0; padding: 0; }

  body {
    font-family: 'DM Sans', sans-serif;
    background: var(--bg);
    color: var(--text);
    min-height: 100vh;
    padding: 20px;
    background-image: radial-gradient(circle at 20% 80%, rgba(44,95,138,0.08) 0%, transparent 50%),
                      radial-gradient(circle at 80% 20%, rgba(224,123,57,0.08) 0%, transparent 50%);
  }

  .wrapper { max-width: 680px; margin: 0 auto; }

  .card {
    display: none;
    background: var(--card-bg);
    border-radius: 16px;
    padding: 36px;
    box-shadow: 0 4px 24px rgba(0,0,0,0.08), 0 1px 4px rgba(0,0,0,0.04);
    border: 1px solid var(--border);
    animation: fadeIn 0.35s ease;
  }

  .card.active { display: block; }

  @keyframes fadeIn {
    from { opacity: 0; transform: translateY(12px); }
    to { opacity: 1; transform: translateY(0); }
  }

  .progress-wrap { margin-bottom: 24px; }
  .progress-label { display: flex; justify-content: space-between; font-size: 0.8rem; color: var(--muted); margin-bottom: 6px; }
  .progress-bar { background: #e8e0d0; height: 8px; border-radius: 99px; overflow: hidden; }
  .progress-fill { background: linear-gradient(90deg, var(--primary), var(--accent)); height: 100%; border-radius: 99px; transition: width 0.4s ease; }

  .timer-row { display: flex; justify-content: flex-end; margin-bottom: 16px; }
  .timer { background: #fff0e8; border: 1px solid #f0c8a0; border-radius: 8px; padding: 6px 14px; font-weight: 600; font-size: 0.9rem; color: var(--accent); }

  .section-tag { display: inline-block; background: var(--primary); color: white; font-size: 0.72rem; font-weight: 600; letter-spacing: 0.08em; text-transform: uppercase; padding: 4px 12px; border-radius: 99px; margin-bottom: 12px; }

  h1 { font-family: 'Noto Serif SC', serif; font-size: 1.8rem; margin-bottom: 14px; color: var(--primary); }
  h2 { font-family: 'Noto Serif SC', serif; font-size: 1.3rem; margin-bottom: 8px; color: var(--text); }
  p { color: var(--muted); line-height: 1.6; margin-bottom: 10px; }
  p strong { color: var(--text); }

  .vocab-big { font-family: 'Noto Serif SC', serif; font-size: 3.2rem; text-align: center; margin: 20px 0; color: var(--primary); letter-spacing: 0.05em; }

  .vocab-grid { display: grid; grid-template-columns: repeat(4, 1fr); gap: 12px; margin: 20px 0; }
  .vocab-tile { background: white; border: 2px solid var(--border); border-radius: 10px; padding: 16px 8px; text-align: center; cursor: pointer; transition: all 0.2s; font-family: 'Noto Serif SC', serif; font-size: 1.5rem; color: var(--primary); position: relative; }
  .vocab-tile:hover { border-color: var(--accent); transform: translateY(-2px); box-shadow: 0 4px 12px rgba(0,0,0,0.1); }
  .vocab-tile.revealed { border-color: var(--success); background: #f0faf5; }
  .vocab-tile .meaning { display: none; font-family: 'DM Sans', sans-serif; font-size: 0.72rem; color: var(--success); margin-top: 6px; font-weight: 600; }
  .vocab-tile.revealed .meaning { display: block; }
  .vocab-instruction { font-size: 0.85rem; color: var(--muted); text-align: center; margin-bottom: 16px; font-style: italic; }

  .option-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; margin: 16px 0; }
  .option-btn { padding: 14px 12px; border: 2px solid var(--border); border-radius: 10px; background: white; cursor: pointer; text-align: left; font-family: 'DM Sans', sans-serif; font-size: 0.92rem; color: var(--text); transition: all 0.2s; line-height: 1.4; }
  .option-btn:hover { border-color: var(--accent); background: #fff8f2; }
  .option-btn.selected { border-color: var(--primary); background: #f0f5ff; font-weight: 600; }

  /* Tone section */
  .tone-big { font-family: 'Noto Serif SC', serif; font-size: 4rem; text-align: center; margin: 16px 0; color: var(--primary); }
  .tone-grid { display: grid; grid-template-columns: repeat(4, 1fr); gap: 10px; margin: 16px 0; }
  .tone-btn { padding: 16px 8px; border: 2px solid var(--border); border-radius: 10px; background: white; cursor: pointer; text-align: center; font-family: 'Noto Serif SC', serif; font-size: 1.3rem; color: var(--primary); transition: all 0.2s; }
  .tone-btn:hover { border-color: var(--accent); background: #fff8f2; transform: translateY(-2px); }
  .tone-btn.selected { border-color: var(--primary); background: #f0f5ff; font-weight: 600; }
  .tone-label { font-family: 'DM Sans', sans-serif; font-size: 0.7rem; color: var(--muted); display: block; margin-top: 4px; }

  .listen-item { background: white; border: 2px solid var(--border); border-radius: 10px; padding: 14px 16px; margin-bottom: 10px; }
  .listen-item-top { display: flex; justify-content: space-between; align-items: center; margin-bottom: 10px; }
  .listen-item-text { font-family: 'Noto Serif SC', serif; font-size: 1.05rem; color: var(--primary); }

  #speech-msg { font-size: 0.88rem; color: var(--primary); margin-top: 10px; min-height: 20px; }

  .scramble-label { font-size: 0.8rem; font-weight: 600; text-transform: uppercase; letter-spacing: 0.06em; color: var(--muted); margin-bottom: 8px; }
  .scramble-zone { border: 2px dashed var(--border); min-height: 56px; display: flex; gap: 8px; padding: 10px; flex-wrap: wrap; margin-bottom: 12px; border-radius: 10px; background: white; align-items: center; }
  .scramble-zone.drop-area { border-color: var(--primary); background: #f5f8ff; }
  .chip { background: var(--primary); color: white; padding: 8px 16px; border-radius: 20px; cursor: pointer; font-family: 'Noto Serif SC', serif; font-size: 1rem; transition: all 0.2s; user-select: none; }
  .chip:hover { background: var(--accent); transform: scale(1.05); }
  [id^="bank"] .chip { background: #e8e0d0; color: var(--text); }
  [id^="bank"] .chip:hover { background: var(--accent); color: white; }

  .btn { display: inline-block; padding: 12px 26px; border: none; border-radius: 10px; cursor: pointer; font-size: 0.95rem; font-family: 'DM Sans', sans-serif; font-weight: 600; transition: all 0.2s; background: var(--primary); color: white; margin-top: 8px; }
  .btn:hover { background: var(--accent); transform: translateY(-1px); box-shadow: 0 4px 12px rgba(0,0,0,0.15); }
  .btn.secondary { background: white; color: var(--primary); border: 2px solid var(--primary); }
  .btn.secondary:hover { background: var(--primary); color: white; }
  .btn-row { display: flex; gap: 10px; flex-wrap: wrap; margin-top: 12px; }

  .welcome-meta { display: flex; gap: 16px; margin: 20px 0; flex-wrap: wrap; }
  .meta-pill { background: white; border: 1px solid var(--border); border-radius: 8px; padding: 10px 16px; font-size: 0.85rem; }
  .meta-pill span { font-weight: 700; color: var(--primary); display: block; font-size: 1.1rem; }

  .pronun-list { list-style: none; margin: 12px 0; }
  .pronun-list li { background: white; border: 2px solid var(--border); border-radius: 10px; padding: 14px 16px; margin-bottom: 8px; display: flex; justify-content: space-between; align-items: center; }
  .pronun-list li .btn { margin-top: 0; padding: 8px 16px; font-size: 0.85rem; flex-shrink: 0; }
  .pronun-char { font-family: 'Noto Serif SC', serif; font-size: 1.2rem; color: var(--primary); }
  .pronun-pinyin { font-size: 0.8rem; color: var(--muted); margin-top: 3px; font-style: italic; }

  .grammar-item { background: white; border: 2px solid var(--border); border-radius: 10px; padding: 16px; margin-bottom: 16px; }
  .grammar-prompt { font-size: 0.9rem; color: var(--muted); margin-bottom: 10px; }
  .grammar-prompt strong { color: var(--text); }

  #results { text-align: center; }
  .score-circle { width: 140px; height: 140px; border-radius: 50%; border: 6px solid var(--success); display: flex; align-items: center; justify-content: center; font-size: 2.4rem; font-weight: 700; color: var(--success); margin: 24px auto; font-family: 'Noto Serif SC', serif; background: #f0faf5; }
  .score-circle.mid { border-color: var(--accent); color: var(--accent); background: #fff8f0; }
  .score-circle.low { border-color: var(--danger); color: var(--danger); background: #fdf0ef; }

  .breakdown { background: #f9f6f0; border-radius: 12px; padding: 20px; margin: 16px 0; text-align: left; }
  .breakdown h3 { font-size: 0.9rem; text-transform: uppercase; letter-spacing: 0.06em; color: var(--muted); margin-bottom: 12px; }
  .breakdown-row { display: flex; justify-content: space-between; padding: 8px 0; border-bottom: 1px solid var(--border); font-size: 0.9rem; }
  .breakdown-row:last-child { border-bottom: none; }

  .feedback { font-size: 0.85rem; font-weight: 600; padding: 4px 12px; border-radius: 99px; display: inline-block; margin-top: 8px; }
  .feedback.ok { background: #edfaf4; color: var(--success); }
  .feedback.err { background: #fdf0ef; color: var(--danger); }

  /* Review table in results */
  .review-table { width: 100%; border-collapse: collapse; margin-top: 10px; font-size: 0.85rem; text-align: left; }
  .review-table th { background: #f0ece4; padding: 8px 10px; color: var(--muted); font-weight: 600; text-transform: uppercase; font-size: 0.75rem; letter-spacing: 0.05em; }
  .review-table td { padding: 8px 10px; border-bottom: 1px solid var(--border); }
  .review-table tr:last-child td { border-bottom: none; }
  .tag-correct { color: var(--success); font-weight: 700; }
  .tag-wrong { color: var(--danger); font-weight: 700; }
</style>
</head>
<body>
<div class="wrapper">

<div class="timer-row" id="timer-row" style="display:none">
  <div class="timer" id="global-timer">60:00</div>
</div>

<div class="progress-wrap" id="progress-wrap" style="display:none">
  <div class="progress-label">
    <span id="progress-text">Page 1</span>
    <span id="progress-pct">0%</span>
  </div>
  <div class="progress-bar"><div class="progress-fill" id="progress-fill"></div></div>
</div>

<!-- WELCOME -->
<div class="card active" id="page-start">
  <div class="section-tag">Mid-Term Exam</div>
  <h1>Chinese Language Exam</h1>
  <p>This exam covers <strong>Greetings, School Life,</strong> and <strong>Basic Verbs</strong>.</p>
  <div class="welcome-meta">
    <div class="meta-pill">⏱ Time Limit<span>60 Minutes</span></div>
    <div class="meta-pill">📋 Sections<span>5</span></div>
    <div class="meta-pill">🎤 Speaking<span>Required</span></div>
  </div>
  <p style="font-size:0.85rem;">Ensure your microphone is working before you begin.</p>
  <button class="btn" onclick="startExam()">Begin Exam →</button>
</div>

<!-- SECTION 1: VOCAB TILES -->
<div class="card" id="page-s1">
  <div class="section-tag">Section 1</div>
  <h2>Character Recognition</h2>
  <p class="vocab-instruction">Tap each character to reveal its meaning. Study them — questions follow.</p>
  <div class="vocab-grid">
    <div class="vocab-tile" onclick="reveal(this)">忙<div class="meaning">Busy</div></div>
    <div class="vocab-tile" onclick="reveal(this)">对不起<div class="meaning">Sorry</div></div>
    <div class="vocab-tile" onclick="reveal(this)">再见<div class="meaning">Goodbye</div></div>
    <div class="vocab-tile" onclick="reveal(this)">我<div class="meaning">I / Me</div></div>
    <div class="vocab-tile" onclick="reveal(this)">大<div class="meaning">Big</div></div>
    <div class="vocab-tile" onclick="reveal(this)">朋友<div class="meaning">Friend</div></div>
    <div class="vocab-tile" onclick="reveal(this)">问<div class="meaning">To ask</div></div>
    <div class="vocab-tile" onclick="reveal(this)">去<div class="meaning">To go</div></div>
    <div class="vocab-tile" onclick="reveal(this)">老师<div class="meaning">Teacher</div></div>
    <div class="vocab-tile" onclick="reveal(this)">学校<div class="meaning">School</div></div>
    <div class="vocab-tile" onclick="reveal(this)">明天<div class="meaning">Tomorrow</div></div>
    <div class="vocab-tile" onclick="reveal(this)">早上<div class="meaning">Morning</div></div>
    <div class="vocab-tile" onclick="reveal(this)">你好<div class="meaning">Hello</div></div>
    <div class="vocab-tile" onclick="reveal(this)">你<div class="meaning">You</div></div>
    <div class="vocab-tile" onclick="reveal(this)">多<div class="meaning">Many / Much</div></div>
    <div class="vocab-tile" onclick="reveal(this)">谢谢<div class="meaning">Thank you</div></div>
    <div class="vocab-tile" onclick="reveal(this)">上课<div class="meaning">Go to class</div></div>
    <div class="vocab-tile" onclick="reveal(this)">一<div class="meaning">One</div></div>
  </div>
  <div class="btn-row">
    <button class="btn secondary" onclick="revealAll()">Reveal All</button>
    <button class="btn" onclick="nextPage('s1q1')">Start Questions →</button>
  </div>
</div>

<!-- S1 Q1 -->
<div class="card" id="page-s1q1">
  <div class="section-tag">Section 1 · Q1</div>
  <h2>Character Recognition</h2>
  <p>What is the meaning of this word?</p>
  <div class="vocab-big">老师</div>
  <div class="option-grid" id="og-s1q1">
    <button class="option-btn" onclick="selectOption(this,'og-s1q1',false,'老师','Student')">A. Student</button>
    <button class="option-btn" onclick="selectOption(this,'og-s1q1',true,'老师','Teacher')">B. Teacher</button>
    <button class="option-btn" onclick="selectOption(this,'og-s1q1',false,'老师','School')">C. School</button>
    <button class="option-btn" onclick="selectOption(this,'og-s1q1',false,'老师','Person')">D. Person</button>
  </div>
  <button class="btn" onclick="nextPage('s1q2')">Next →</button>
</div>

<!-- S1 Q2 -->
<div class="card" id="page-s1q2">
  <div class="section-tag">Section 1 · Q2</div>
  <h2>Character Recognition</h2>
  <p>Which word means <strong>"Tomorrow"</strong>?</p>
  <div class="option-grid" id="og-s1q2">
    <button class="option-btn" onclick="selectOption(this,'og-s1q2',true,'明天 (Tomorrow)','明天')">A. 明天</button>
    <button class="option-btn" onclick="selectOption(this,'og-s1q2',false,'明天 (Tomorrow)','早上')">B. 早上</button>
    <button class="option-btn" onclick="selectOption(this,'og-s1q2',false,'明天 (Tomorrow)','再见')">C. 再见</button>
    <button class="option-btn" onclick="selectOption(this,'og-s1q2',false,'明天 (Tomorrow)','上课')">D. 上课</button>
  </div>
  <button class="btn" onclick="nextPage('s1q3')">Next →</button>
</div>

<!-- S1 Q3 -->
<div class="card" id="page-s1q3">
  <div class="section-tag">Section 1 · Q3</div>
  <h2>Character Recognition</h2>
  <p>What does <strong>对不起</strong> mean?</p>
  <div class="option-grid" id="og-s1q3">
    <button class="option-btn" onclick="selectOption(this,'og-s1q3',false,'对不起','You\'re welcome')">A. You're welcome</button>
    <button class="option-btn" onclick="selectOption(this,'og-s1q3',false,'对不起','Goodbye')">B. Goodbye</button>
    <button class="option-btn" onclick="selectOption(this,'og-s1q3',true,'对不起','Sorry / Excuse me')">C. Sorry / Excuse me</button>
    <button class="option-btn" onclick="selectOption(this,'og-s1q3',false,'对不起','Good morning')">D. Good morning</button>
  </div>
  <button class="btn" onclick="nextPage('s1q4')">Next →</button>
</div>

<!-- S1 Q4 -->
<div class="card" id="page-s1q4">
  <div class="section-tag">Section 1 · Q4</div>
  <h2>Character Recognition</h2>
  <p>Which character means <strong>"Big"</strong>?</p>
  <div class="option-grid" id="og-s1q4">
    <button class="option-btn" onclick="selectOption(this,'og-s1q4',false,'大 (Big)','问')">A. 问</button>
    <button class="option-btn" onclick="selectOption(this,'og-s1q4',false,'大 (Big)','去')">B. 去</button>
    <button class="option-btn" onclick="selectOption(this,'og-s1q4',true,'大 (Big)','大')">C. 大</button>
    <button class="option-btn" onclick="selectOption(this,'og-s1q4',false,'大 (Big)','忙')">D. 忙</button>
  </div>
  <button class="btn" onclick="nextPage('s1q5')">Next →</button>
</div>

<!-- S1 Q5 -->
<div class="card" id="page-s1q5">
  <div class="section-tag">Section 1 · Q5</div>
  <h2>Character Recognition</h2>
  <p>What does <strong>你好</strong> mean?</p>
  <div class="option-grid" id="og-s1q5">
    <button class="option-btn" onclick="selectOption(this,'og-s1q5',false,'你好','Goodbye')">A. Goodbye</button>
    <button class="option-btn" onclick="selectOption(this,'og-s1q5',true,'你好','Hello')">B. Hello</button>
    <button class="option-btn" onclick="selectOption(this,'og-s1q5',false,'你好','Thank you')">C. Thank you</button>
    <button class="option-btn" onclick="selectOption(this,'og-s1q5',false,'你好','Good morning')">D. Good morning</button>
  </div>
  <button class="btn" onclick="nextPage('s1q6')">Next →</button>
</div>

<!-- S1 Q6 -->
<div class="card" id="page-s1q6">
  <div class="section-tag">Section 1 · Q6</div>
  <h2>Character Recognition</h2>
  <p>What does <strong>学校</strong> mean?</p>
  <div class="option-grid" id="og-s1q6">
    <button class="option-btn" onclick="selectOption(this,'og-s1q6',false,'学校','Classroom')">A. Classroom</button>
    <button class="option-btn" onclick="selectOption(this,'og-s1q6',false,'学校','Teacher')">B. Teacher</button>
    <button class="option-btn" onclick="selectOption(this,'og-s1q6',true,'学校','School')">C. School</button>
    <button class="option-btn" onclick="selectOption(this,'og-s1q6',false,'学校','Library')">D. Library</button>
  </div>
  <button class="btn" onclick="nextPage('s1q7')">Next →</button>
</div>

<!-- S1 Q7 -->
<div class="card" id="page-s1q7">
  <div class="section-tag">Section 1 · Q7</div>
  <h2>Character Recognition</h2>
  <p>Which character means <strong>"You"</strong>?</p>
  <div class="option-grid" id="og-s1q7">
    <button class="option-btn" onclick="selectOption(this,'og-s1q7',false,'你 (You)','我')">A. 我</button>
    <button class="option-btn" onclick="selectOption(this,'og-s1q7',true,'你 (You)','你')">B. 你</button>
    <button class="option-btn" onclick="selectOption(this,'og-s1q7',false,'你 (You)','他')">C. 他</button>
    <button class="option-btn" onclick="selectOption(this,'og-s1q7',false,'你 (You)','她')">D. 她</button>
  </div>
  <button class="btn" onclick="nextPage('s1q8')">Next →</button>
</div>

<!-- S1 Q8 -->
<div class="card" id="page-s1q8">
  <div class="section-tag">Section 1 · Q8</div>
  <h2>Character Recognition</h2>
  <p>Which character means <strong>"I / Me"</strong>?</p>
  <div class="option-grid" id="og-s1q8">
    <button class="option-btn" onclick="selectOption(this,'og-s1q8',true,'我 (I/Me)','我')">A. 我</button>
    <button class="option-btn" onclick="selectOption(this,'og-s1q8',false,'我 (I/Me)','你')">B. 你</button>
    <button class="option-btn" onclick="selectOption(this,'og-s1q8',false,'我 (I/Me)','大')">C. 大</button>
    <button class="option-btn" onclick="selectOption(this,'og-s1q8',false,'我 (I/Me)','问')">D. 问</button>
  </div>
  <button class="btn" onclick="nextPage('s1q9')">Next →</button>
</div>

<!-- S1 Q9 -->
<div class="card" id="page-s1q9">
  <div class="section-tag">Section 1 · Q9</div>
  <h2>Character Recognition</h2>
  <p>What does <strong>早上</strong> mean?</p>
  <div class="option-grid" id="og-s1q9">
    <button class="option-btn" onclick="selectOption(this,'og-s1q9',false,'早上','Afternoon')">A. Afternoon</button>
    <button class="option-btn" onclick="selectOption(this,'og-s1q9',true,'早上','Morning')">B. Morning</button>
    <button class="option-btn" onclick="selectOption(this,'og-s1q9',false,'早上','Evening')">C. Evening</button>
    <button class="option-btn" onclick="selectOption(this,'og-s1q9',false,'早上','Night')">D. Night</button>
  </div>
  <button class="btn" onclick="nextPage('s1q10')">Next →</button>
</div>

<!-- S1 Q10 -->
<div class="card" id="page-s1q10">
  <div class="section-tag">Section 1 · Q10</div>
  <h2>Character Recognition</h2>
  <p>What does <strong>多</strong> mean?</p>
  <div class="option-grid" id="og-s1q10">
    <button class="option-btn" onclick="selectOption(this,'og-s1q10',false,'多','Few / Little')">A. Few / Little</button>
    <button class="option-btn" onclick="selectOption(this,'og-s1q10',true,'多','Many / Much')">B. Many / Much</button>
    <button class="option-btn" onclick="selectOption(this,'og-s1q10',false,'多','Big')">C. Big</button>
    <button class="option-btn" onclick="selectOption(this,'og-s1q10',false,'多','Small')">D. Small</button>
  </div>
  <button class="btn" onclick="nextPage('s1q11')">Next →</button>
</div>

<!-- S1 Q11 -->
<div class="card" id="page-s1q11">
  <div class="section-tag">Section 1 · Q11</div>
  <h2>Character Recognition</h2>
  <p>What does <strong>谢谢</strong> mean?</p>
  <div class="option-grid" id="og-s1q11">
    <button class="option-btn" onclick="selectOption(this,'og-s1q11',false,'谢谢','Sorry')">A. Sorry</button>
    <button class="option-btn" onclick="selectOption(this,'og-s1q11',false,'谢谢','Goodbye')">B. Goodbye</button>
    <button class="option-btn" onclick="selectOption(this,'og-s1q11',true,'谢谢','Thank you')">C. Thank you</button>
    <button class="option-btn" onclick="selectOption(this,'og-s1q11',false,'谢谢','Hello')">D. Hello</button>
  </div>
  <button class="btn" onclick="nextPage('s1q12')">Next →</button>
</div>

<!-- S1 Q12 -->
<div class="card" id="page-s1q12">
  <div class="section-tag">Section 1 · Q12</div>
  <h2>Character Recognition</h2>
  <p>What does <strong>再见</strong> mean?</p>
  <div class="option-grid" id="og-s1q12">
    <button class="option-btn" onclick="selectOption(this,'og-s1q12',false,'再见','Hello')">A. Hello</button>
    <button class="option-btn" onclick="selectOption(this,'og-s1q12',true,'再见','Goodbye')">B. Goodbye</button>
    <button class="option-btn" onclick="selectOption(this,'og-s1q12',false,'再见','See you tomorrow')">C. See you tomorrow</button>
    <button class="option-btn" onclick="selectOption(this,'og-s1q12',false,'再见','Good morning')">D. Good morning</button>
  </div>
  <button class="btn" onclick="nextPage('s1q13')">Next →</button>
</div>

<!-- S1 Q13 -->
<div class="card" id="page-s1q13">
  <div class="section-tag">Section 1 · Q13</div>
  <h2>Character Recognition</h2>
  <p>What does <strong>去</strong> mean?</p>
  <div class="option-grid" id="og-s1q13">
    <button class="option-btn" onclick="selectOption(this,'og-s1q13',false,'去','To come')">A. To come</button>
    <button class="option-btn" onclick="selectOption(this,'og-s1q13',false,'去','To ask')">B. To ask</button>
    <button class="option-btn" onclick="selectOption(this,'og-s1q13',true,'去','To go')">C. To go</button>
    <button class="option-btn" onclick="selectOption(this,'og-s1q13',false,'去','To see')">D. To see</button>
  </div>
  <button class="btn" onclick="nextPage('s1q14')">Next →</button>
</div>

<!-- S1 Q14 -->
<div class="card" id="page-s1q14">
  <div class="section-tag">Section 1 · Q14</div>
  <h2>Character Recognition</h2>
  <p>What does <strong>上课</strong> mean?</p>
  <div class="option-grid" id="og-s1q14">
    <button class="option-btn" onclick="selectOption(this,'og-s1q14',false,'上课','After school')">A. After school</button>
    <button class="option-btn" onclick="selectOption(this,'og-s1q14',true,'上课','Go to class')">B. Go to class</button>
    <button class="option-btn" onclick="selectOption(this,'og-s1q14',false,'上课','School is over')">C. School is over</button>
    <button class="option-btn" onclick="selectOption(this,'og-s1q14',false,'上课','Study at home')">D. Study at home</button>
  </div>
  <button class="btn" onclick="nextPage('s1q15')">Next →</button>
</div>

<!-- S1 Q15 -->
<div class="card" id="page-s1q15">
  <div class="section-tag">Section 1 · Q15</div>
  <h2>Character Recognition</h2>
  <p>What does <strong>一</strong> mean?</p>
  <div class="option-grid" id="og-s1q15">
    <button class="option-btn" onclick="selectOption(this,'og-s1q15',false,'一','Two')">A. Two</button>
    <button class="option-btn" onclick="selectOption(this,'og-s1q15',true,'一','One')">B. One</button>
    <button class="option-btn" onclick="selectOption(this,'og-s1q15',false,'一','Three')">C. Three</button>
    <button class="option-btn" onclick="selectOption(this,'og-s1q15',false,'一','Many')">D. Many</button>
  </div>
  <button class="btn" onclick="nextPage('s2')">Next Section →</button>
</div>

<!-- SECTION 2: TONES 声调 -->
<div class="card" id="page-s2">
  <div class="section-tag">Section 2 · 声调</div>
  <h2>Tone Recognition</h2>
  <p>Select the correct tone for each character. Tones: <strong>1st (ā)</strong> flat · <strong>2nd (á)</strong> rising · <strong>3rd (ǎ)</strong> dip · <strong>4th (à)</strong> falling</p>

  <!-- Tone Q1: 你 nǐ = 3rd -->
  <div class="listen-item" style="margin-bottom:16px">
    <div class="listen-item-top">
      <span style="font-size:0.85rem;color:var(--muted)">Q1</span>
      <button class="btn" style="padding:8px 16px;font-size:0.85rem;margin-top:0" onclick="playAudio('你')">▶ Listen</button>
    </div>
    <div class="tone-big">你</div>
    <div class="tone-grid" id="tg-s2q1">
      <button class="tone-btn" onclick="selectTone(this,'tg-s2q1',false,'你','1st Tone (nī)')">1st<span class="tone-label">nī (flat)</span></button>
      <button class="tone-btn" onclick="selectTone(this,'tg-s2q1',false,'你','2nd Tone (ní)')">2nd<span class="tone-label">ní (rising)</span></button>
      <button class="tone-btn" onclick="selectTone(this,'tg-s2q1',true,'你','3rd Tone (nǐ)')">3rd<span class="tone-label">nǐ (dip)</span></button>
      <button class="tone-btn" onclick="selectTone(this,'tg-s2q1',false,'你','4th Tone (nì)')">4th<span class="tone-label">nì (falling)</span></button>
    </div>
  </div>

  <!-- Tone Q2: 忙 máng = 2nd -->
  <div class="listen-item" style="margin-bottom:16px">
    <div class="listen-item-top">
      <span style="font-size:0.85rem;color:var(--muted)">Q2</span>
      <button class="btn" style="padding:8px 16px;font-size:0.85rem;margin-top:0" onclick="playAudio('忙')">▶ Listen</button>
    </div>
    <div class="tone-big">忙</div>
    <div class="tone-grid" id="tg-s2q2">
      <button class="tone-btn" onclick="selectTone(this,'tg-s2q2',false,'忙','1st Tone (māng)')">1st<span class="tone-label">māng (flat)</span></button>
      <button class="tone-btn" onclick="selectTone(this,'tg-s2q2',true,'忙','2nd Tone (máng)')">2nd<span class="tone-label">máng (rising)</span></button>
      <button class="tone-btn" onclick="selectTone(this,'tg-s2q2',false,'忙','3rd Tone (mǎng)')">3rd<span class="tone-label">mǎng (dip)</span></button>
      <button class="tone-btn" onclick="selectTone(this,'tg-s2q2',false,'忙','4th Tone (màng)')">4th<span class="tone-label">màng (falling)</span></button>
    </div>
  </div>

  <!-- Tone Q3: 多 duō = 1st -->
  <div class="listen-item" style="margin-bottom:16px">
    <div class="listen-item-top">
      <span style="font-size:0.85rem;color:var(--muted)">Q3</span>
      <button class="btn" style="padding:8px 16px;font-size:0.85rem;margin-top:0" onclick="playAudio('多')">▶ Listen</button>
    </div>
    <div class="tone-big">多</div>
    <div class="tone-grid" id="tg-s2q3">
      <button class="tone-btn" onclick="selectTone(this,'tg-s2q3',true,'多','1st Tone (duō)')">1st<span class="tone-label">duō (flat)</span></button>
      <button class="tone-btn" onclick="selectTone(this,'tg-s2q3',false,'多','2nd Tone (duó)')">2nd<span class="tone-label">duó (rising)</span></button>
      <button class="tone-btn" onclick="selectTone(this,'tg-s2q3',false,'多','3rd Tone (duǒ)')">3rd<span class="tone-label">duǒ (dip)</span></button>
      <button class="tone-btn" onclick="selectTone(this,'tg-s2q3',false,'多','4th Tone (duò)')">4th<span class="tone-label">duò (falling)</span></button>
    </div>
  </div>

  <!-- Tone Q4: 人 rén = 2nd -->
  <div class="listen-item" style="margin-bottom:16px">
    <div class="listen-item-top">
      <span style="font-size:0.85rem;color:var(--muted)">Q4</span>
      <button class="btn" style="padding:8px 16px;font-size:0.85rem;margin-top:0" onclick="playAudio('人')">▶ Listen</button>
    </div>
    <div class="tone-big">人</div>
    <div class="tone-grid" id="tg-s2q4">
      <button class="tone-btn" onclick="selectTone(this,'tg-s2q4',false,'人','1st Tone (rēn)')">1st<span class="tone-label">rēn (flat)</span></button>
      <button class="tone-btn" onclick="selectTone(this,'tg-s2q4',true,'人','2nd Tone (rén)')">2nd<span class="tone-label">rén (rising)</span></button>
      <button class="tone-btn" onclick="selectTone(this,'tg-s2q4',false,'人','3rd Tone (rěn)')">3rd<span class="tone-label">rěn (dip)</span></button>
      <button class="tone-btn" onclick="selectTone(this,'tg-s2q4',false,'人','4th Tone (rèn)')">4th<span class="tone-label">rèn (falling)</span></button>
    </div>
  </div>

  <!-- Tone Q5: 也 yě = 3rd -->
  <div class="listen-item" style="margin-bottom:16px">
    <div class="listen-item-top">
      <span style="font-size:0.85rem;color:var(--muted)">Q5</span>
      <button class="btn" style="padding:8px 16px;font-size:0.85rem;margin-top:0" onclick="playAudio('也')">▶ Listen</button>
    </div>
    <div class="tone-big">也</div>
    <div class="tone-grid" id="tg-s2q5">
      <button class="tone-btn" onclick="selectTone(this,'tg-s2q5',false,'也','1st Tone (yē)')">1st<span class="tone-label">yē (flat)</span></button>
      <button class="tone-btn" onclick="selectTone(this,'tg-s2q5',false,'也','2nd Tone (yé)')">2nd<span class="tone-label">yé (rising)</span></button>
      <button class="tone-btn" onclick="selectTone(this,'tg-s2q5',true,'也','3rd Tone (yě)')">3rd<span class="tone-label">yě (dip)</span></button>
      <button class="tone-btn" onclick="selectTone(this,'tg-s2q5',false,'也','4th Tone (yè)')">4th<span class="tone-label">yè (falling)</span></button>
    </div>
  </div>

  <!-- Tone Q6: 见 jiàn = 4th -->
  <div class="listen-item" style="margin-bottom:16px">
    <div class="listen-item-top">
      <span style="font-size:0.85rem;color:var(--muted)">Q6</span>
      <button class="btn" style="padding:8px 16px;font-size:0.85rem;margin-top:0" onclick="playAudio('见')">▶ Listen</button>
    </div>
    <div class="tone-big">见</div>
    <div class="tone-grid" id="tg-s2q6">
      <button class="tone-btn" onclick="selectTone(this,'tg-s2q6',false,'见','1st Tone (jiān)')">1st<span class="tone-label">jiān (flat)</span></button>
      <button class="tone-btn" onclick="selectTone(this,'tg-s2q6',false,'见','2nd Tone (jiǎn)')">2nd<span class="tone-label">jiǎn (rising)</span></button>
      <button class="tone-btn" onclick="selectTone(this,'tg-s2q6',false,'见','3rd Tone (jiǎn)')">3rd<span class="tone-label">jiǎn (dip)</span></button>
      <button class="tone-btn" onclick="selectTone(this,'tg-s2q6',true,'见','4th Tone (jiàn)')">4th<span class="tone-label">jiàn (falling)</span></button>
    </div>
  </div>

  <!-- Tone Q7: 很 hěn = 3rd -->
  <div class="listen-item" style="margin-bottom:16px">
    <div class="listen-item-top">
      <span style="font-size:0.85rem;color:var(--muted)">Q7</span>
      <button class="btn" style="padding:8px 16px;font-size:0.85rem;margin-top:0" onclick="playAudio('很')">▶ Listen</button>
    </div>
    <div class="tone-big">很</div>
    <div class="tone-grid" id="tg-s2q7">
      <button class="tone-btn" onclick="selectTone(this,'tg-s2q7',false,'很','1st Tone (hēn)')">1st<span class="tone-label">hēn (flat)</span></button>
      <button class="tone-btn" onclick="selectTone(this,'tg-s2q7',false,'很','2nd Tone (hén)')">2nd<span class="tone-label">hén (rising)</span></button>
      <button class="tone-btn" onclick="selectTone(this,'tg-s2q7',true,'很','3rd Tone (hěn)')">3rd<span class="tone-label">hěn (dip)</span></button>
      <button class="tone-btn" onclick="selectTone(this,'tg-s2q7',false,'很','4th Tone (hèn)')">4th<span class="tone-label">hèn (falling)</span></button>
    </div>
  </div>

  <!-- Tone Q8: 去 qù = 4th -->
  <div class="listen-item" style="margin-bottom:16px">
    <div class="listen-item-top">
      <span style="font-size:0.85rem;color:var(--muted)">Q8</span>
      <button class="btn" style="padding:8px 16px;font-size:0.85rem;margin-top:0" onclick="playAudio('去')">▶ Listen</button>
    </div>
    <div class="tone-big">去</div>
    <div class="tone-grid" id="tg-s2q8">
      <button class="tone-btn" onclick="selectTone(this,'tg-s2q8',false,'去','1st Tone (qū)')">1st<span class="tone-label">qū (flat)</span></button>
      <button class="tone-btn" onclick="selectTone(this,'tg-s2q8',false,'去','2nd Tone (qú)')">2nd<span class="tone-label">qú (rising)</span></button>
      <button class="tone-btn" onclick="selectTone(this,'tg-s2q8',false,'去','3rd Tone (qǔ)')">3rd<span class="tone-label">qǔ (dip)</span></button>
      <button class="tone-btn" onclick="selectTone(this,'tg-s2q8',true,'去','4th Tone (qù)')">4th<span class="tone-label">qù (falling)</span></button>
    </div>
  </div>

  <button class="btn" onclick="nextPage('s3')" style="margin-top:8px">Next Section →</button>
</div>

<!-- SECTION 3: LISTENING -->
<div class="card" id="page-s3">
  <div class="section-tag">Section 3</div>
  <h2>Listening Comprehension</h2>
  <p>Click <strong>▶ Play</strong> to hear each sentence, then choose the correct English meaning.</p>

  <div class="listen-item">
    <div class="listen-item-top">
      <span style="font-size:0.85rem;color:var(--muted)">Item 1</span>
      <button class="btn" style="padding:8px 16px;font-size:0.85rem;margin-top:0" onclick="playAudio('你有好朋友吗','li1-text')">▶ Play</button>
    </div>
    <div class="listen-item-text" id="li1-text" style="display:none">你有好朋友吗？</div>
    <div class="option-grid" id="og-s3q1" style="margin-top:10px">
      <button class="option-btn" onclick="selectOption(this,'og-s3q1',false,'你有好朋友吗？','Do you have a teacher?')">A. Do you have a teacher?</button>
      <button class="option-btn" onclick="selectOption(this,'og-s3q1',true,'你有好朋友吗？','Do you have good friends?')">B. Do you have good friends?</button>
      <button class="option-btn" onclick="selectOption(this,'og-s3q1',false,'你有好朋友吗？','Are you busy today?')">C. Are you busy today?</button>
      <button class="option-btn" onclick="selectOption(this,'og-s3q1',false,'你有好朋友吗？','Is school far from here?')">D. Is school far from here?</button>
    </div>
  </div>

  <div class="listen-item">
    <div class="listen-item-top">
      <span style="font-size:0.85rem;color:var(--muted)">Item 2</span>
      <button class="btn" style="padding:8px 16px;font-size:0.85rem;margin-top:0" onclick="playAudio('我常问他问题','li2-text')">▶ Play</button>
    </div>
    <div class="listen-item-text" id="li2-text" style="display:none">我常问他问题</div>
    <div class="option-grid" id="og-s3q2" style="margin-top:10px">
      <button class="option-btn" onclick="selectOption(this,'og-s3q2',false,'我常问他问题','I often ask her to leave.')">A. I often ask her to leave.</button>
      <button class="option-btn" onclick="selectOption(this,'og-s3q2',false,'我常问他问题','He asks me questions often.')">B. He asks me questions often.</button>
      <button class="option-btn" onclick="selectOption(this,'og-s3q2',true,'我常问他问题','I often ask him questions.')">C. I often ask him questions.</button>
      <button class="option-btn" onclick="selectOption(this,'og-s3q2',false,'我常问他问题','We ask questions together.')">D. We ask questions together.</button>
    </div>
  </div>

  <div class="listen-item">
    <div class="listen-item-top">
      <span style="font-size:0.85rem;color:var(--muted)">Item 3</span>
      <button class="btn" style="padding:8px 16px;font-size:0.85rem;margin-top:0" onclick="playAudio('你去上课吗','li3-text')">▶ Play</button>
    </div>
    <div class="listen-item-text" id="li3-text" style="display:none">你去上课吗？</div>
    <div class="option-grid" id="og-s3q3" style="margin-top:10px">
      <button class="option-btn" onclick="selectOption(this,'og-s3q3',false,'你去上课吗？','Are you going home?')">A. Are you going home?</button>
      <button class="option-btn" onclick="selectOption(this,'og-s3q3',true,'你去上课吗？','Are you going to class?')">B. Are you going to class?</button>
      <button class="option-btn" onclick="selectOption(this,'og-s3q3',false,'你去上课吗？','Do you like school?')">C. Do you like school?</button>
      <button class="option-btn" onclick="selectOption(this,'og-s3q3',false,'你去上课吗？','Is the teacher going?')">D. Is the teacher going?</button>
    </div>
  </div>

  <div class="listen-item">
    <div class="listen-item-top">
      <span style="font-size:0.85rem;color:var(--muted)">Item 4</span>
      <button class="btn" style="padding:8px 16px;font-size:0.85rem;margin-top:0" onclick="playAudio('学校很大，人很多','li4-text')">▶ Play</button>
    </div>
    <div class="listen-item-text" id="li4-text" style="display:none">学校很大，人很多</div>
    <div class="option-grid" id="og-s3q4" style="margin-top:10px">
      <button class="option-btn" onclick="selectOption(this,'og-s3q4',false,'学校很大，人很多','The school is small with many people.')">A. The school is small with many people.</button>
      <button class="option-btn" onclick="selectOption(this,'og-s3q4',true,'学校很大，人很多','The school is very big, there are many people.')">B. The school is very big, there are many people.</button>
      <button class="option-btn" onclick="selectOption(this,'og-s3q4',false,'学校很大，人很多','The teacher is big and has friends.')">C. The teacher is big and has friends.</button>
      <button class="option-btn" onclick="selectOption(this,'og-s3q4',false,'学校很大，人很多','I go to a big school far away.')">D. I go to a big school far away.</button>
    </div>
  </div>

  <div class="listen-item">
    <div class="listen-item-top">
      <span style="font-size:0.85rem;color:var(--muted)">Item 5</span>
      <button class="btn" style="padding:8px 16px;font-size:0.85rem;margin-top:0" onclick="playAudio('明天见','li5-text')">▶ Play</button>
    </div>
    <div class="listen-item-text" id="li5-text" style="display:none">明天见</div>
    <div class="option-grid" id="og-s3q5" style="margin-top:10px">
      <button class="option-btn" onclick="selectOption(this,'og-s3q5',false,'明天见','Good morning!')">A. Good morning!</button>
      <button class="option-btn" onclick="selectOption(this,'og-s3q5',false,'明天见','See you later.')">B. See you later.</button>
      <button class="option-btn" onclick="selectOption(this,'og-s3q5',true,'明天见','See you tomorrow!')">C. See you tomorrow!</button>
      <button class="option-btn" onclick="selectOption(this,'og-s3q5',false,'明天见','It\'s a nice day!')">D. It's a nice day!</button>
    </div>
  </div>

  <button class="btn" onclick="nextPage('s4')" style="margin-top:16px">Next Section →</button>
</div>

<!-- SECTION 4: PRONUNCIATION WITH PINYIN -->
<div class="card" id="page-s4">
  <div class="section-tag">Section 4</div>
  <h2>Pronunciation (Speaking)</h2>
  <p>Read each phrase aloud. Press <strong>🎤 Record</strong> and speak clearly into your microphone.</p>
  <ul class="pronun-list">
    <li>
      <div><div class="pronun-char">谢谢</div><div class="pronun-pinyin">xièxiè</div></div>
      <button class="btn" onclick="runSpeech('谢谢',this)">🎤 Record</button>
    </li>
    <li>
      <div><div class="pronun-char">不客气</div><div class="pronun-pinyin">bù kèqi</div></div>
      <button class="btn" onclick="runSpeech('不客气',this)">🎤 Record</button>
    </li>
    <li>
      <div><div class="pronun-char">再见</div><div class="pronun-pinyin">zàijiàn</div></div>
      <button class="btn" onclick="runSpeech('再见',this)">🎤 Record</button>
    </li>
    <li>
      <div><div class="pronun-char">对不起</div><div class="pronun-pinyin">duìbuqǐ</div></div>
      <button class="btn" onclick="runSpeech('对不起',this)">🎤 Record</button>
    </li>
    <li>
      <div><div class="pronun-char">没关系</div><div class="pronun-pinyin">méi guānxi</div></div>
      <button class="btn" onclick="runSpeech('没关系',this)">🎤 Record</button>
    </li>
    <li>
      <div><div class="pronun-char">你好</div><div class="pronun-pinyin">nǐ hǎo</div></div>
      <button class="btn" onclick="runSpeech('你好',this)">🎤 Record</button>
    </li>
    <li>
      <div><div class="pronun-char">我不忙</div><div class="pronun-pinyin">wǒ bù máng</div></div>
      <button class="btn" onclick="runSpeech('我不忙',this)">🎤 Record</button>
    </li>
    <li>
      <div><div class="pronun-char">你有好朋友吗？</div><div class="pronun-pinyin">nǐ yǒu hǎo péngyǒu ma?</div></div>
      <button class="btn" onclick="runSpeech('你有好朋友吗',this)">🎤 Record</button>
    </li>
  </ul>
  <p id="speech-msg"></p>
  <button class="btn" onclick="nextPage('s5')">Next Section →</button>
</div>

<!-- SECTION 5: GRAMMAR -->
<div class="card" id="page-s5">
  <div class="section-tag">Section 5</div>
  <h2>Grammar & Sentence Structure</h2>
  <p>Tap words in the bank to build the sentence shown. Tap placed words to return them.</p>

  <div class="grammar-item" id="gi1">
    <div class="grammar-prompt">Arrange: <strong>"Are you busy?"</strong></div>
    <div class="scramble-label">Your sentence:</div>
    <div class="scramble-zone drop-area" id="drop1"></div>
    <div class="scramble-label">Word bank:</div>
    <div class="scramble-zone" id="bank1">
      <div class="chip" onclick="moveChip(this,'drop1','bank1')">你</div>
      <div class="chip" onclick="moveChip(this,'drop1','bank1')">忙</div>
      <div class="chip" onclick="moveChip(this,'drop1','bank1')">吗</div>
    </div>
    <button class="btn secondary" style="padding:8px 18px;font-size:0.85rem" onclick="checkGrammar('gi1','你忙吗','drop1','bank1')">✓ Check</button>
    <div class="feedback" id="gi1-fb" style="display:none"></div>
  </div>

  <div class="grammar-item" id="gi2">
    <div class="grammar-prompt">Arrange: <strong>"Goodbye, see you tomorrow."</strong></div>
    <div class="scramble-label">Your sentence:</div>
    <div class="scramble-zone drop-area" id="drop2"></div>
    <div class="scramble-label">Word bank:</div>
    <div class="scramble-zone" id="bank2">
      <div class="chip" onclick="moveChip(this,'drop2','bank2')">再见</div>
      <div class="chip" onclick="moveChip(this,'drop2','bank2')">，</div>
      <div class="chip" onclick="moveChip(this,'drop2','bank2')">明天见</div>
    </div>
    <button class="btn secondary" style="padding:8px 18px;font-size:0.85rem" onclick="checkGrammar('gi2','再见，明天见','drop2','bank2')">✓ Check</button>
    <div class="feedback" id="gi2-fb" style="display:none"></div>
  </div>

  <div class="grammar-item" id="gi3">
    <div class="grammar-prompt">Arrange: <strong>"I have a good friend."</strong></div>
    <div class="scramble-label">Your sentence:</div>
    <div class="scramble-zone drop-area" id="drop3"></div>
    <div class="scramble-label">Word bank:</div>
    <div class="scramble-zone" id="bank3">
      <div class="chip" onclick="moveChip(this,'drop3','bank3')">我</div>
      <div class="chip" onclick="moveChip(this,'drop3','bank3')">有</div>
      <div class="chip" onclick="moveChip(this,'drop3','bank3')">一个</div>
      <div class="chip" onclick="moveChip(this,'drop3','bank3')">好朋友</div>
    </div>
    <button class="btn secondary" style="padding:8px 18px;font-size:0.85rem" onclick="checkGrammar('gi3','我有一个好朋友','drop3','bank3')">✓ Check</button>
    <div class="feedback" id="gi3-fb" style="display:none"></div>
  </div>

  <div class="grammar-item" id="gi4">
    <div class="grammar-prompt">Arrange: <strong>"I often ask him questions."</strong></div>
    <div class="scramble-label">Your sentence:</div>
    <div class="scramble-zone drop-area" id="drop4"></div>
    <div class="scramble-label">Word bank:</div>
    <div class="scramble-zone" id="bank4">
      <div class="chip" onclick="moveChip(this,'drop4','bank4')">我</div>
      <div class="chip" onclick="moveChip(this,'drop4','bank4')">常</div>
      <div class="chip" onclick="moveChip(this,'drop4','bank4')">问他</div>
      <div class="chip" onclick="moveChip(this,'drop4','bank4')">问题</div>
    </div>
    <button class="btn secondary" style="padding:8px 18px;font-size:0.85rem" onclick="checkGrammar('gi4','我常问他问题','drop4','bank4')">✓ Check</button>
    <div class="feedback" id="gi4-fb" style="display:none"></div>
  </div>

  <div class="grammar-item" id="gi5">
    <div class="grammar-prompt">Arrange: <strong>"The teacher is very good."</strong></div>
    <div class="scramble-label">Your sentence:</div>
    <div class="scramble-zone drop-area" id="drop5"></div>
    <div class="scramble-label">Word bank:</div>
    <div class="scramble-zone" id="bank5">
      <div class="chip" onclick="moveChip(this,'drop5','bank5')">老师</div>
      <div class="chip" onclick="moveChip(this,'drop5','bank5')">很</div>
      <div class="chip" onclick="moveChip(this,'drop5','bank5')">好</div>
    </div>
    <button class="btn secondary" style="padding:8px 18px;font-size:0.85rem" onclick="checkGrammar('gi5','老师很好','drop5','bank5')">✓ Check</button>
    <div class="feedback" id="gi5-fb" style="display:none"></div>
  </div>

  <div class="grammar-item" id="gi6">
    <div class="grammar-prompt">Arrange: <strong>"We often make phone calls."</strong></div>
    <div class="scramble-label">Your sentence:</div>
    <div class="scramble-zone drop-area" id="drop6"></div>
    <div class="scramble-label">Word bank:</div>
    <div class="scramble-zone" id="bank6">
      <div class="chip" onclick="moveChip(this,'drop6','bank6')">我们</div>
      <div class="chip" onclick="moveChip(this,'drop6','bank6')">常</div>
      <div class="chip" onclick="moveChip(this,'drop6','bank6')">打电话</div>
    </div>
    <button class="btn secondary" style="padding:8px 18px;font-size:0.85rem" onclick="checkGrammar('gi6','我们常打电话','drop6','bank6')">✓ Check</button>
    <div class="feedback" id="gi6-fb" style="display:none"></div>
  </div>

  <div class="grammar-item" id="gi7">
    <div class="grammar-prompt">Arrange: <strong>"Are you busy?" (with question mark)</strong></div>
    <div class="scramble-label">Your sentence:</div>
    <div class="scramble-zone drop-area" id="drop7"></div>
    <div class="scramble-label">Word bank:</div>
    <div class="scramble-zone" id="bank7">
      <div class="chip" onclick="moveChip(this,'drop7','bank7')">你</div>
      <div class="chip" onclick="moveChip(this,'drop7','bank7')">忙</div>
      <div class="chip" onclick="moveChip(this,'drop7','bank7')">吗</div>
      <div class="chip" onclick="moveChip(this,'drop7','bank7')">？</div>
    </div>
    <button class="btn secondary" style="padding:8px 18px;font-size:0.85rem" onclick="checkGrammar('gi7','你忙吗？','drop7','bank7')">✓ Check</button>
    <div class="feedback" id="gi7-fb" style="display:none"></div>
  </div>

  <div class="grammar-item" id="gi8">
    <div class="grammar-prompt">Arrange: <strong>"I have one good friend."</strong></div>
    <div class="scramble-label">Your sentence:</div>
    <div class="scramble-zone drop-area" id="drop8"></div>
    <div class="scramble-label">Word bank:</div>
    <div class="scramble-zone" id="bank8">
      <div class="chip" onclick="moveChip(this,'drop8','bank8')">我</div>
      <div class="chip" onclick="moveChip(this,'drop8','bank8')">有</div>
      <div class="chip" onclick="moveChip(this,'drop8','bank8')">一个</div>
      <div class="chip" onclick="moveChip(this,'drop8','bank8')">好朋友</div>
    </div>
    <button class="btn secondary" style="padding:8px 18px;font-size:0.85rem" onclick="checkGrammar('gi8','我有一个好朋友','drop8','bank8')">✓ Check</button>
    <div class="feedback" id="gi8-fb" style="display:none"></div>
  </div>

  <button class="btn" onclick="finishExam()" style="margin-top:8px">Finish Exam →</button>
</div>

<!-- RESULTS -->
<div class="card" id="results">
  <div class="section-tag">Results</div>
  <h2>Exam Complete! 🎉</h2>
  <div class="score-circle" id="final-score">—</div>
  <p id="grade-comment"></p>

  <div class="breakdown">
    <h3>Section Breakdown</h3>
    <div class="breakdown-row"><span>Section 1 · Character Recognition</span><span id="br1">—</span></div>
    <div class="breakdown-row"><span>Section 2 · Tone Recognition</span><span id="br2">—</span></div>
    <div class="breakdown-row"><span>Section 3 · Listening</span><span id="br3">—</span></div>
    <div class="breakdown-row"><span>Section 4 · Pronunciation</span><span id="br4">—</span></div>
    <div class="breakdown-row"><span>Section 5 · Grammar</span><span id="br5">—</span></div>
  </div>

  <div class="breakdown" id="review-wrap" style="display:none">
    <h3>Answer Review</h3>
    <table class="review-table">
      <thead><tr><th>Question</th><th>Your Answer</th><th>Result</th></tr></thead>
      <tbody id="review-body"></tbody>
    </table>
  </div>

  <button class="btn" onclick="location.reload()">Retake Exam</button>
</div>

</div>

<script>
// ─── State ────────────────────────────────────────────────
let mcqAnswers = [];   // {question, answer, correct}
let toneAnswers = [];  // {question, answer, correct}
let grammarScore = 0;
let grammarTotal = 8;
let pronunciationDone = 0;
let timerInterval;
let seconds = 3600;

const PAGE_ORDER = [
  'start','s1',
  's1q1','s1q2','s1q3','s1q4','s1q5','s1q6','s1q7',
  's1q8','s1q9','s1q10','s1q11','s1q12','s1q13','s1q14','s1q15',
  's2','s3','s4','s5','results'
];
const PAGE_COUNT = PAGE_ORDER.length;

function getPageIndex(id) { return PAGE_ORDER.indexOf(id); }

function updateProgress(pageId) {
  const idx = getPageIndex(pageId);
  if (idx <= 0) return;
  const pct = Math.round((idx / (PAGE_COUNT - 2)) * 100);
  document.getElementById('progress-fill').style.width = pct + '%';
  document.getElementById('progress-pct').textContent = pct + '%';
  document.getElementById('progress-text').textContent = 'Page ' + idx + ' of ' + (PAGE_COUNT - 2);
}

function startExam() {
  document.getElementById('timer-row').style.display = 'flex';
  document.getElementById('progress-wrap').style.display = 'block';
  startTimer();
  nextPage('s1');
}

function shuffleBank(bankId) {
  const bank = document.getElementById(bankId);
  if (!bank) return;
  const chips = Array.from(bank.querySelectorAll('.chip'));
  chips.sort(() => Math.random() - 0.5);
  chips.forEach(c => bank.appendChild(c));
}

function nextPage(id) {
  document.querySelectorAll('.card').forEach(c => c.classList.remove('active'));
  document.getElementById('page-' + id).classList.add('active');
  updateProgress(id);
  window.scrollTo({ top: 0, behavior: 'smooth' });
  if (id === 's5') {
    ['bank1','bank2','bank3','bank4','bank5','bank6','bank7','bank8'].forEach(shuffleBank);
  }
}

function startTimer() {
  timerInterval = setInterval(() => {
    seconds--;
    if (seconds <= 0) { clearInterval(timerInterval); finishExam(); return; }
    const m = String(Math.floor(seconds/60)).padStart(2,'0');
    const s = String(seconds % 60).padStart(2,'0');
    document.getElementById('global-timer').textContent = m + ':' + s;
  }, 1000);
}

// ─── Vocab Reveal ─────────────────────────────────────────
function reveal(el) { el.classList.toggle('revealed'); }
function revealAll() { document.querySelectorAll('.vocab-tile').forEach(t => t.classList.add('revealed')); }

// ─── MCQ — record only, no immediate feedback ─────────────
function selectOption(btn, gridId, isCorrect, question, answer) {
  const grid = document.getElementById(gridId);
  // allow changing answer until Next is pressed
  grid.querySelectorAll('.option-btn').forEach(b => b.classList.remove('selected'));
  btn.classList.add('selected');
  // store / update answer
  const existing = mcqAnswers.findIndex(a => a.question === question);
  const entry = { question, answer, correct: isCorrect };
  if (existing >= 0) mcqAnswers[existing] = entry;
  else mcqAnswers.push(entry);
}

// ─── Tone — record only, no immediate feedback ────────────
function selectTone(btn, gridId, isCorrect, character, answer) {
  const grid = document.getElementById(gridId);
  grid.querySelectorAll('.tone-btn').forEach(b => b.classList.remove('selected'));
  btn.classList.add('selected');
  const existing = toneAnswers.findIndex(a => a.question === character);
  const entry = { question: character, answer, correct: isCorrect };
  if (existing >= 0) toneAnswers[existing] = entry;
  else toneAnswers.push(entry);
}

// ─── Audio ────────────────────────────────────────────────
function playAudio(text, revealId) {
  if (revealId) document.getElementById(revealId).style.display = 'block';
  if ('speechSynthesis' in window) {
    const u = new SpeechSynthesisUtterance(text);
    u.lang = 'zh-CN'; u.rate = 0.85;
    speechSynthesis.cancel();
    speechSynthesis.speak(u);
  }
}

// ─── Speech ───────────────────────────────────────────────
function runSpeech(target, btn) {
  const msg = document.getElementById('speech-msg');
  if (!('webkitSpeechRecognition' in window || 'SpeechRecognition' in window)) {
    msg.textContent = '⚠️ Speech recognition not supported. Try Chrome.';
    return;
  }
  const SR = window.SpeechRecognition || window.webkitSpeechRecognition;
  const r = new SR();
  r.lang = 'zh-CN'; r.interimResults = false; r.maxAlternatives = 1;
  btn.textContent = '● Recording…'; btn.style.background = '#e74c3c';
  msg.textContent = 'Listening…';
  r.start();
  r.onresult = e => {
    const heard = e.results[0][0].transcript;
    msg.textContent = `Heard: "${heard}" — Good job! ✅`;
    btn.textContent = '✅ Done'; btn.style.background = 'var(--success)';
    pronunciationDone++;
  };
  r.onerror = () => {
    msg.textContent = '⚠️ Could not hear clearly. Try again.';
    btn.textContent = '🎤 Retry'; btn.style.background = '';
  };
}

// ─── Grammar ──────────────────────────────────────────────
function moveChip(chip, dropId, bankId) {
  const drop = document.getElementById(dropId);
  const bank = document.getElementById(bankId);
  if (chip.parentElement.id === bankId) {
    chip.onclick = () => moveChip(chip, dropId, bankId);
    drop.appendChild(chip);
  } else {
    chip.onclick = () => moveChip(chip, dropId, bankId);
    bank.appendChild(chip);
  }
}

function checkGrammar(itemId, answer, dropId, bankId) {
  const drop = document.getElementById(dropId);
  const built = Array.from(drop.querySelectorAll('.chip')).map(c => c.textContent.trim()).join('');
  const fb = document.getElementById(itemId + '-fb');
  fb.style.display = 'inline-block';
  if (built === answer) {
    fb.textContent = '✅ Correct!';
    fb.className = 'feedback ok';
    grammarScore++;
  } else {
    fb.textContent = `✗ Try again. Correct: ${answer}`;
    fb.className = 'feedback err';
  }
}

// ─── Finish ───────────────────────────────────────────────
function finishExam() {
  clearInterval(timerInterval);

  const mcqCorrect = mcqAnswers.filter(a => a.correct).length;
  const toneCorrect = toneAnswers.filter(a => a.correct).length;
  const mcqTotal = 15;
  const toneTotal = 8;
  const listenTotal = 5;
  const listenCorrect = mcqAnswers.filter(a =>
    ['你有好朋友吗？','我常问他问题','你去上课吗？','学校很大，人很多','明天见'].includes(a.question)
  ).filter(a => a.correct).length;
  const s1Correct = mcqCorrect - listenCorrect;

  const totalCorrect = mcqCorrect + toneCorrect + grammarScore;
  const totalQ = mcqTotal + toneTotal + listenTotal + grammarTotal;
  const overall = Math.round(totalCorrect / totalQ * 100);

  // Score circle
  const el = document.getElementById('final-score');
  el.textContent = overall + '%';
  el.className = overall >= 75 ? 'score-circle' : overall >= 50 ? 'score-circle mid' : 'score-circle low';

  const comments = { 90:'优秀 Excellent! Outstanding!', 75:'良好 Well done! Keep it up.', 50:'及格 Passing. Review weak areas.', 0:'加油! Keep practicing!' };
  const grade = Object.keys(comments).reverse().find(k => overall >= k);
  document.getElementById('grade-comment').textContent = comments[grade];

  // Breakdown
  document.getElementById('br1').textContent = s1Correct + '/' + mcqTotal + ' correct';
  document.getElementById('br2').textContent = toneCorrect + '/' + toneTotal + ' correct';
  document.getElementById('br3').textContent = listenCorrect + '/' + listenTotal + ' correct';
  document.getElementById('br4').textContent = pronunciationDone + '/8 recorded';
  document.getElementById('br5').textContent = grammarScore + '/' + grammarTotal + ' correct';

  // Answer review table
  const tbody = document.getElementById('review-body');
  tbody.innerHTML = '';
  const allAnswers = [...mcqAnswers, ...toneAnswers];
  allAnswers.forEach(a => {
    const tr = document.createElement('tr');
    tr.innerHTML = `
      <td>${a.question}</td>
      <td>${a.answer}</td>
      <td class="${a.correct ? 'tag-correct' : 'tag-wrong'}">${a.correct ? '✅' : '✗'}</td>
    `;
    tbody.appendChild(tr);
  });
  document.getElementById('review-wrap').style.display = allAnswers.length > 0 ? 'block' : 'none';

  nextPage('results');
}
</script>
</body>
</html>
