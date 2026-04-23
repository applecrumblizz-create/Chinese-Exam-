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

  .vocab-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 12px; margin: 20px 0; }
  @media (min-width: 480px) { .vocab-grid { grid-template-columns: repeat(4, 1fr); } }

  .vocab-tile { background: white; border: 2px solid var(--border); border-radius: 10px; padding: 16px 8px; text-align: center; cursor: pointer; transition: all 0.2s; font-family: 'Noto Serif SC', serif; font-size: 1.5rem; color: var(--primary); position: relative; }
  .vocab-tile:hover { border-color: var(--accent); transform: translateY(-2px); box-shadow: 0 4px 12px rgba(0,0,0,0.1); }
  .vocab-tile.revealed { border-color: var(--success); background: #f0faf5; }
  .vocab-tile .meaning { display: none; font-family: 'DM Sans', sans-serif; font-size: 0.72rem; color: var(--success); margin-top: 6px; font-weight: 600; }
  .vocab-tile.revealed .meaning { display: block; }
  .vocab-instruction { font-size: 0.85rem; color: var(--muted); text-align: center; margin-bottom: 16px; font-style: italic; }

  .option-grid { display: grid; grid-template-columns: 1fr; gap: 10px; margin: 16px 0; }
  @media (min-width: 480px) { .option-grid { grid-template-columns: 1fr 1fr; } }

  .option-btn { padding: 14px 12px; border: 2px solid var(--border); border-radius: 10px; background: white; cursor: pointer; text-align: left; font-family: 'DM Sans', sans-serif; font-size: 0.92rem; color: var(--text); transition: all 0.2s; line-height: 1.4; }
  .option-btn:hover { border-color: var(--accent); background: #fff8f2; }
  .option-btn.selected { border-color: var(--primary); background: #f0f5ff; font-weight: 600; }

  .tone-big { font-family: 'Noto Serif SC', serif; font-size: 4rem; text-align: center; margin: 16px 0; color: var(--primary); }
  .tone-grid { display: grid; grid-template-columns: repeat(2, 1fr); gap: 10px; margin: 16px 0; }
  @media (min-width: 480px) { .tone-grid { grid-template-columns: repeat(4, 1fr); } }

  .tone-btn { padding: 16px 8px; border: 2px solid var(--border); border-radius: 10px; background: white; cursor: pointer; text-align: center; font-family: 'Noto Serif SC', serif; font-size: 1.3rem; color: var(--primary); transition: all 0.2s; }
  .tone-btn:hover { border-color: var(--accent); background: #fff8f2; transform: translateY(-2px); }
  .tone-btn.selected { border-color: var(--primary); background: #f0f5ff; font-weight: 600; }
  .tone-label { font-family: 'DM Sans', sans-serif; font-size: 0.7rem; color: var(--muted); display: block; margin-top: 4px; }

  .listen-item { background: white; border: 2px solid var(--border); border-radius: 10px; padding: 14px 16px; margin-bottom: 10px; }
  .listen-item-top { display: flex; justify-content: space-between; align-items: center; margin-bottom: 10px; }
  .listen-item-text { font-family: 'Noto Serif SC', serif; font-size: 1.05rem; color: var(--primary); }

  #speech-msg { font-size: 0.88rem; color: var(--primary); margin-top: 10px; min-height: 20px; text-align: center; font-weight: 500; }

  .scramble-label { font-size: 0.8rem; font-weight: 600; text-transform: uppercase; letter-spacing: 0.06em; color: var(--muted); margin-bottom: 8px; }
  .scramble-zone { border: 2px dashed var(--border); min-height: 56px; display: flex; gap: 8px; padding: 10px; flex-wrap: wrap; margin-bottom: 12px; border-radius: 10px; background: white; align-items: center; }
  .scramble-zone.drop-area { border-color: var(--primary); background: #f5f8ff; }
  .chip { background: var(--primary); color: white; padding: 8px 16px; border-radius: 20px; cursor: pointer; font-family: 'Noto Serif SC', serif; font-size: 1rem; transition: all 0.2s; user-select: none; }
  .chip:hover { background: var(--accent); transform: scale(1.05); }
  [id^="bank"] .chip { background: #e8e0d0; color: var(--text); }

  .btn { display: inline-block; padding: 12px 26px; border: none; border-radius: 10px; cursor: pointer; font-size: 0.95rem; font-family: 'DM Sans', sans-serif; font-weight: 600; transition: all 0.2s; background: var(--primary); color: white; margin-top: 8px; }
  .btn:hover { background: var(--accent); transform: translateY(-1px); box-shadow: 0 4px 12px rgba(0,0,0,0.15); }
  .btn.secondary { background: white; color: var(--primary); border: 2px solid var(--primary); }

  .welcome-meta { display: flex; gap: 16px; margin: 20px 0; flex-wrap: wrap; }
  .meta-pill { background: white; border: 1px solid var(--border); border-radius: 8px; padding: 10px 16px; font-size: 0.85rem; }
  .meta-pill span { font-weight: 700; color: var(--primary); display: block; font-size: 1.1rem; }

  .pronun-list { list-style: none; margin: 12px 0; }
  .pronun-list li { background: white; border: 2px solid var(--border); border-radius: 10px; padding: 14px 16px; margin-bottom: 8px; display: flex; justify-content: space-between; align-items: center; }
  .pronun-char { font-family: 'Noto Serif SC', serif; font-size: 1.2rem; color: var(--primary); }
  .pronun-pinyin { font-size: 0.8rem; color: var(--muted); margin-top: 3px; font-style: italic; }

  .grammar-item { background: white; border: 2px solid var(--border); border-radius: 10px; padding: 16px; margin-bottom: 16px; }
  .feedback { font-size: 0.85rem; font-weight: 600; padding: 4px 12px; border-radius: 99px; display: inline-block; margin-top: 8px; }
  .feedback.ok { background: #edfaf4; color: var(--success); }
  .feedback.err { background: #fdf0ef; color: var(--danger); }

  #results { text-align: center; }
  .score-circle { width: 140px; height: 140px; border-radius: 50%; border: 6px solid var(--success); display: flex; align-items: center; justify-content: center; font-size: 2.4rem; font-weight: 700; color: var(--success); margin: 24px auto; font-family: 'Noto Serif SC', serif; background: #f0faf5; }
  .score-circle.mid { border-color: var(--accent); color: var(--accent); background: #fff8f0; }
  .score-circle.low { border-color: var(--danger); color: var(--danger); background: #fdf0ef; }

  .breakdown { background: #f9f6f0; border-radius: 12px; padding: 20px; margin: 16px 0; text-align: left; }
  .breakdown-row { display: flex; justify-content: space-between; padding: 8px 0; border-bottom: 1px solid var(--border); font-size: 0.9rem; }

  .review-table { width: 100%; border-collapse: collapse; margin-top: 10px; font-size: 0.85rem; text-align: left; }
  .review-table th { background: #f0ece4; padding: 8px 10px; color: var(--muted); text-transform: uppercase; font-size: 0.75rem; }
  .review-table td { padding: 8px 10px; border-bottom: 1px solid var(--border); }
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

<div class="card" id="page-s2">
  <div class="section-tag">Section 2 · 声调</div>
  <h2>Tone Recognition</h2>
  <p>Select the correct tone for each character.</p>

  <div class="listen-item">
    <div class="listen-item-top"><span style="font-size:0.8rem">Q1</span> <button class="btn" style="padding:6px 12px; font-size:0.8rem; margin:0" onclick="playAudio('你')">▶ Listen</button></div>
    <div class="tone-big">你</div>
    <div class="tone-grid" id="tg-s2q1">
      <button class="tone-btn" onclick="selectTone(this,'tg-s2q1',false,'你','1st')">1st</button>
      <button class="tone-btn" onclick="selectTone(this,'tg-s2q1',false,'你','2nd')">2nd</button>
      <button class="tone-btn" onclick="selectTone(this,'tg-s2q1',true,'你','3rd')">3rd</button>
      <button class="tone-btn" onclick="selectTone(this,'tg-s2q1',false,'你','4th')">4th</button>
    </div>
  </div>

  <button class="btn" onclick="nextPage('s3')">Next Section →</button>
</div>

<div class="card" id="page-s3">
  <div class="section-tag">Section 3</div>
  <h2>Listening Comprehension</h2>
  <p>Listen then choose the meaning.</p>

  <div class="listen-item">
    <div class="listen-item-top"><button class="btn" style="padding:8px 16px; margin:0" onclick="playAudio('你有好朋友吗','li1-text')">▶ Play</button></div>
    <div class="listen-item-text" id="li1-text" style="display:none; margin-top:10px">你有好朋友吗？</div>
    <div class="option-grid" id="og-s3q1">
      <button class="option-btn" onclick="selectOption(this,'og-s3q1',false,'你有好朋友吗？','A')">Do you have a teacher?</button>
      <button class="option-btn" onclick="selectOption(this,'og-s3q1',true,'你有好朋友吗？','B')">Do you have good friends?</button>
    </div>
  </div>
  <button class="btn" onclick="nextPage('s4')">Next Section →</button>
</div>

<div class="card" id="page-s4">
  <div class="section-tag">Section 4</div>
  <h2>Pronunciation</h2>
  <ul class="pronun-list">
    <li>
      <div><div class="pronun-char">谢谢</div><div class="pronun-pinyin">xièxiè</div></div>
      <button class="btn" onclick="runSpeech('谢谢',this)">🎤 Record</button>
    </li>
  </ul>
  <p id="speech-msg"></p>
  <button class="btn" onclick="nextPage('s5')">Next Section →</button>
</div>

<div class="card" id="page-s5">
  <div class="section-tag">Section 5</div>
  <h2>Grammar</h2>

  <div class="grammar-item" id="gi1">
    <div class="grammar-prompt">Arrange: <strong>"I am not busy."</strong></div>
    <div class="scramble-zone drop-area" id="drop1"></div>
    <div class="scramble-zone" id="bank1">
      <div class="chip" onclick="moveChip(this,'drop1','bank1')">我</div>
      <div class="chip" onclick="moveChip(this,'drop1','bank1')">不</div>
      <div class="chip" onclick="moveChip(this,'drop1','bank1')">忙</div>
      <div class="chip" onclick="moveChip(this,'drop1','bank1')">。</div>
    </div>
    <button class="btn secondary" onclick="checkGrammar('gi1','我不忙。','drop1','bank1')">Check</button>
    <div class="feedback" id="gi1-fb" style="display:none"></div>
  </div>

  <div class="grammar-item" id="gi3">
    <div class="grammar-prompt">Arrange: <strong>"I have a good friend."</strong></div>
    <div class="scramble-zone drop-area" id="drop3"></div>
    <div class="scramble-zone" id="bank3">
      <div class="chip" onclick="moveChip(this,'drop3','bank3')">我</div>
      <div class="chip" onclick="moveChip(this,'drop3','bank3')">有</div>
      <div class="chip" onclick="moveChip(this,'drop3','bank3')">一个</div>
      <div class="chip" onclick="moveChip(this,'drop3','bank3')">好朋友</div>
      <div class="chip" onclick="moveChip(this,'drop3','bank3')">。</div> </div>
    <button class="btn secondary" onclick="checkGrammar('gi3','我有一个好朋友。','drop3','bank3')">Check</button>
    <div class="feedback" id="gi3-fb" style="display:none"></div>
  </div>

  <button class="btn" onclick="finishExam()">Finish Exam →</button>
</div>

<div class="card" id="results">
  <div class="section-tag">Results</div>
  <div class="score-circle" id="final-score">—</div>
  <div class="breakdown">
    <div class="breakdown-row"><span>Character Recognition</span><span id="br1">—</span></div>
    <div class="breakdown-row"><span>Tone Recognition</span><span id="br2">—</span></div>
    <div class="breakdown-row"><span>Listening</span><span id="br3">—</span></div>
    <div class="breakdown-row"><span>Grammar</span><span id="br5">—</span></div>
  </div>
  <button class="btn" onclick="location.reload()">Retake</button>
</div>

</div>

<script>
let mcqAnswers = [];
let toneAnswers = [];
let grammarScore = 0;
let pronunciationDone = 0;
let timerInterval;
let seconds = 3600;

const PAGE_ORDER = ['start','s1','s1q1','s1q2','s1q3','s1q4','s1q5','s1q6','s1q7','s1q8','s1q9','s1q10','s1q11','s1q12','s1q13','s1q14','s1q15','s2','s3','s4','s5','results'];

function updateProgress(pageId) {
  const idx = PAGE_ORDER.indexOf(pageId);
  if (idx <= 0) return;
  const pct = Math.round((idx / (PAGE_ORDER.length - 1)) * 100);
  document.getElementById('progress-fill').style.width = pct + '%';
  document.getElementById('progress-pct').textContent = pct + '%';
}

function startExam() {
  document.getElementById('timer-row').style.display = 'flex';
  document.getElementById('progress-wrap').style.display = 'block';
  startTimer();
  nextPage('s1');
}

function nextPage(id) {
  document.querySelectorAll('.card').forEach(c => c.classList.remove('active'));
  document.getElementById('page-' + id).classList.add('active');
  updateProgress(id);
  window.scrollTo({ top: 0, behavior: 'smooth' });
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

function reveal(el) { el.classList.toggle('revealed'); }
function revealAll() { document.querySelectorAll('.vocab-tile').forEach(t => t.classList.add('revealed')); }

function selectOption(btn, gridId, isCorrect, question, answer) {
  const grid = document.getElementById(gridId);
  grid.querySelectorAll('.option-btn').forEach(b => b.classList.remove('selected'));
  btn.classList.add('selected');
  const existing = mcqAnswers.findIndex(a => a.question === question);
  const entry = { question, answer, correct: isCorrect };
  if (existing >= 0) mcqAnswers[existing] = entry; else mcqAnswers.push(entry);
}

function selectTone(btn, gridId, isCorrect, char, answer) {
  const grid = document.getElementById(gridId);
  grid.querySelectorAll('.tone-btn').forEach(b => b.classList.remove('selected'));
  btn.classList.add('selected');
  const existing = toneAnswers.findIndex(a => a.question === char);
  const entry = { question: char, answer, correct: isCorrect };
  if (existing >= 0) toneAnswers[existing] = entry; else toneAnswers.push(entry);
}

function playAudio(text, revealId) {
  if (revealId) document.getElementById(revealId).style.display = 'block';
  if ('speechSynthesis' in window) {
    const u = new SpeechSynthesisUtterance(text);
    u.lang = 'zh-CN'; u.rate = 0.8;
    speechSynthesis.cancel();
    speechSynthesis.speak(u);
  }
}

function runSpeech(target, btn) {
  const msg = document.getElementById('speech-msg');
  const SR = window.SpeechRecognition || window.webkitSpeechRecognition;
  if (!SR) { msg.textContent = 'Browser not supported.'; return; }
  const r = new SR();
  r.lang = 'zh-CN';
  btn.textContent = '● Listening...';
  r.start();
  r.onresult = e => {
    msg.textContent = 'Heard: ' + e.results[0][0].transcript + ' ✅';
    btn.textContent = '✅ Recorded';
    pronunciationDone++;
  };
}

function moveChip(chip, dropId, bankId) {
  const drop = document.getElementById(dropId);
  const bank = document.getElementById(bankId);
  if (chip.parentElement.id === bankId) drop.appendChild(chip);
  else bank.appendChild(chip);
}

function checkGrammar(itemId, answer, dropId, bankId) {
  const drop = document.getElementById(dropId);
  const built = Array.from(drop.querySelectorAll('.chip')).map(c => c.textContent.trim()).join('').replace(/\s/g,'');
  const cleanAnswer = answer.replace(/\s/g,'');
  const fb = document.getElementById(itemId + '-fb');
  fb.style.display = 'inline-block';
  if (built === cleanAnswer) {
    fb.textContent = '✅ Correct!'; fb.className = 'feedback ok';
    grammarScore++;
  } else {
    fb.textContent = '❌ Try again'; fb.className = 'feedback err';
  }
}

function finishExam() {
  clearInterval(timerInterval);
  // Logic to separate Section 1 from Section 3 Listening
  const listeningQuestions = ['你有好朋友吗？','我常问他问题','你去上课吗？','学校很大，人很多','明天见'];
  const listenCorrect = mcqAnswers.filter(a => listeningQuestions.includes(a.question) && a.correct).length;
  const s1Correct = mcqAnswers.filter(a => !listeningQuestions.includes(a.question) && a.correct).length;
  
  const score = Math.round(((s1Correct + toneAnswers.filter(a=>a.correct).length + listenCorrect + grammarScore) / 36) * 100);
  document.getElementById('final-score').textContent = score + '%';
  document.getElementById('br1').textContent = s1Correct + '/15';
  document.getElementById('br2').textContent = toneAnswers.filter(a=>a.correct).length + '/8';
  document.getElementById('br3').textContent = listenCorrect + '/5';
  document.getElementById('br5').textContent = grammarScore + '/8';
  nextPage('results');
}
</script>
</body>
</html>
