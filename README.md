# Chinese-Exam-
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
  .option-btn.correct { border-color: var(--success); background: #edfaf4; color: var(--success); }
  .option-btn.wrong { border-color: var(--danger); background: #fdf0ef; color: var(--danger); }

  .listen-item { background: white; border: 2px solid var(--border); border-radius: 10px; padding: 14px 16px; margin-bottom: 10px; }
  .listen-item-top { display: flex; justify-content: space-between; align-items: center; margin-bottom: 10px; }
  .listen-item-text { font-family: 'Noto Serif SC', serif; font-size: 1.05rem; color: var(--primary); }

  #speech-msg { font-size: 0.88rem; color: var(--primary); margin-top: 10px; min-height: 20px; }

  .scramble-label { font-size: 0.8rem; font-weight: 600; text-transform: uppercase; letter-spacing: 0.06em; color: var(--muted); margin-bottom: 8px; }
  .scramble-zone { border: 2px dashed var(--border); min-height: 56px; display: flex; gap: 8px; padding: 10px; flex-wrap: wrap; margin-bottom: 12px; border-radius: 10px; background: white; align-items: center; }
  .scramble-zone.drop-area { border-color: var(--primary); background: #f5f8ff; }
  .chip { background: var(--primary); color: white; padding: 8px 16px; border-radius: 20px; cursor: pointer; font-family: 'Noto Serif SC', serif; font-size: 1rem; transition: all 0.2s; user-select: none; }
  .chip:hover { background: var(--accent); transform: scale(1.05); }
  #word-bank .chip, [id^="bank"] .chip { background: #e8e0d0; color: var(--text); }
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
  .pronun-list li { background: white; border: 2px solid var(--border); border-radius: 10px; padding: 14px 16px; margin-bottom: 8px; display: flex; justify-content: space-between; align-items: center; font-family: 'Noto Serif SC', serif; font-size: 1.2rem; color: var(--primary); }
  .pronun-list li .btn { margin-top: 0; padding: 8px 16px; font-size: 0.85rem; }

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
    <div class="meta-pill">📋 Sections<span>4</span></div>
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
  <div class="option-grid">
    <button class="option-btn" onclick="mcq(this,false)">A. Student</button>
    <button class="option-btn" onclick="mcq(this,true)">B. Teacher</button>
    <button class="option-btn" onclick="mcq(this,false)">C. School</button>
    <button class="option-btn" onclick="mcq(this,false)">D. Person</button>
  </div>
  <button class="btn" onclick="nextPage('s1q2')">Next →</button>
</div>

<!-- S1 Q2 -->
<div class="card" id="page-s1q2">
  <div class="section-tag">Section 1 · Q2</div>
  <h2>Character Recognition</h2>
  <p>Which word means <strong>"Tomorrow"</strong>?</p>
  <div class="option-grid">
    <button class="option-btn" onclick="mcq(this,true)">A. 明天</button>
    <button class="option-btn" onclick="mcq(this,false)">B. 早上</button>
    <button class="option-btn" onclick="mcq(this,false)">C. 再见</button>
    <button class="option-btn" onclick="mcq(this,false)">D. 上课</button>
  </div>
  <button class="btn" onclick="nextPage('s1q3')">Next →</button>
</div>

<!-- S1 Q3 -->
<div class="card" id="page-s1q3">
  <div class="section-tag">Section 1 · Q3</div>
  <h2>Character Recognition</h2>
  <p>What does <strong>对不起</strong> mean?</p>
  <div class="option-grid">
    <button class="option-btn" onclick="mcq(this,false)">A. You're welcome</button>
    <button class="option-btn" onclick="mcq(this,false)">B. Goodbye</button>
    <button class="option-btn" onclick="mcq(this,true)">C. Sorry / Excuse me</button>
    <button class="option-btn" onclick="mcq(this,false)">D. Good morning</button>
  </div>
  <button class="btn" onclick="nextPage('s1q4')">Next →</button>
</div>

<!-- S1 Q4 -->
<div class="card" id="page-s1q4">
  <div class="section-tag">Section 1 · Q4</div>
  <h2>Character Recognition</h2>
  <p>Which character means <strong>"Big"</strong>?</p>
  <div class="option-grid">
    <button class="option-btn" onclick="mcq(this,false)">A. 问</button>
    <button class="option-btn" onclick="mcq(this,false)">B. 去</button>
    <button class="option-btn" onclick="mcq(this,true)">C. 大</button>
    <button class="option-btn" onclick="mcq(this,false)">D. 忙</button>
  </div>
  <button class="btn" onclick="nextPage('s2')">Next Section →</button>
</div>

<!-- SECTION 2: LISTENING -->
<div class="card" id="page-s2">
  <div class="section-tag">Section 2</div>
  <h2>Listening Comprehension</h2>
  <p>Click <strong>▶ Play</strong> to hear each sentence, then choose the correct English meaning.</p>

  <div class="listen-item">
    <div class="listen-item-top">
      <span style="font-size:0.85rem;color:var(--muted)">Item 1</span>
      <button class="btn" style="padding:8px 16px;font-size:0.85rem;margin-top:0" onclick="playAudio('你有好朋友吗','li1-text')">▶ Play</button>
    </div>
    <div class="listen-item-text" id="li1-text" style="display:none">你有好朋友吗？</div>
    <div class="option-grid" style="margin-top:10px">
      <button class="option-btn" onclick="mcq(this,false)">A. Do you have a teacher?</button>
      <button class="option-btn" onclick="mcq(this,true)">B. Do you have good friends?</button>
      <button class="option-btn" onclick="mcq(this,false)">C. Are you busy today?</button>
      <button class="option-btn" onclick="mcq(this,false)">D. Is school far from here?</button>
    </div>
  </div>

  <div class="listen-item">
    <div class="listen-item-top">
      <span style="font-size:0.85rem;color:var(--muted)">Item 2</span>
      <button class="btn" style="padding:8px 16px;font-size:0.85rem;margin-top:0" onclick="playAudio('我常问他问题','li2-text')">▶ Play</button>
    </div>
    <div class="listen-item-text" id="li2-text" style="display:none">我常问他问题</div>
    <div class="option-grid" style="margin-top:10px">
      <button class="option-btn" onclick="mcq(this,false)">A. I often ask her to leave.</button>
      <button class="option-btn" onclick="mcq(this,false)">B. He asks me questions often.</button>
      <button class="option-btn" onclick="mcq(this,true)">C. I often ask him questions.</button>
      <button class="option-btn" onclick="mcq(this,false)">D. We ask questions together.</button>
    </div>
  </div>

  <div class="listen-item">
    <div class="listen-item-top">
      <span style="font-size:0.85rem;color:var(--muted)">Item 3</span>
      <button class="btn" style="padding:8px 16px;font-size:0.85rem;margin-top:0" onclick="playAudio('你去上课吗','li3-text')">▶ Play</button>
    </div>
    <div class="listen-item-text" id="li3-text" style="display:none">你去上课吗？</div>
    <div class="option-grid" style="margin-top:10px">
      <button class="option-btn" onclick="mcq(this,false)">A. Are you going home?</button>
      <button class="option-btn" onclick="mcq(this,true)">B. Are you going to class?</button>
      <button class="option-btn" onclick="mcq(this,false)">C. Do you like school?</button>
      <button class="option-btn" onclick="mcq(this,false)">D. Is the teacher going?</button>
    </div>
  </div>

  <div class="listen-item">
    <div class="listen-item-top">
      <span style="font-size:0.85rem;color:var(--muted)">Item 4</span>
      <button class="btn" style="padding:8px 16px;font-size:0.85rem;margin-top:0" onclick="playAudio('学校很大，人很多','li4-text')">▶ Play</button>
    </div>
    <div class="listen-item-text" id="li4-text" style="display:none">学校很大，人很多</div>
    <div class="option-grid" style="margin-top:10px">
      <button class="option-btn" onclick="mcq(this,false)">A. The school is small with many people.</button>
      <button class="option-btn" onclick="mcq(this,true)">B. The school is very big, there are many people.</button>
      <button class="option-btn" onclick="mcq(this,false)">C. The teacher is big and has friends.</button>
      <button class="option-btn" onclick="mcq(this,false)">D. I go to a big school far away.</button>
    </div>
  </div>

  <div class="listen-item">
    <div class="listen-item-top">
      <span style="font-size:0.85rem;color:var(--muted)">Item 5</span>
      <button class="btn" style="padding:8px 16px;font-size:0.85rem;margin-top:0" onclick="playAudio('明天见','li5-text')">▶ Play</button>
    </div>
    <div class="listen-item-text" id="li5-text" style="display:none">明天见</div>
    <div class="option-grid" style="margin-top:10px">
      <button class="option-btn" onclick="mcq(this,false)">A. Good morning!</button>
      <button class="option-btn" onclick="mcq(this,false)">B. See you later.</button>
      <button class="option-btn" onclick="mcq(this,true)">C. See you tomorrow!</button>
      <button class="option-btn" onclick="mcq(this,false)">D. It's a nice day!</button>
    </div>
  </div>

  <button class="btn" onclick="nextPage('s3')" style="margin-top:16px">Next Section →</button>
</div>

<!-- SECTION 3: PRONUNCIATION -->
<div class="card" id="page-s3">
  <div class="section-tag">Section 3</div>
  <h2>Pronunciation (Speaking)</h2>
  <p>Read each phrase aloud. Press <strong>🎤 Record</strong> and speak clearly into your microphone.</p>
  <ul class="pronun-list">
    <li>谢谢 <button class="btn" onclick="runSpeech('谢谢',this)">🎤 Record</button></li>
    <li>不客气 <button class="btn" onclick="runSpeech('不客气',this)">🎤 Record</button></li>
    <li>再见 <button class="btn" onclick="runSpeech('再见',this)">🎤 Record</button></li>
    <li>对不起 <button class="btn" onclick="runSpeech('对不起',this)">🎤 Record</button></li>
    <li>没关系 <button class="btn" onclick="runSpeech('没关系',this)">🎤 Record</button></li>
    <li>你好 <button class="btn" onclick="runSpeech('你好',this)">🎤 Record</button></li>
    <li>我不忙 <button class="btn" onclick="runSpeech('我不忙',this)">🎤 Record</button></li>
    <li>你有好朋友吗？ <button class="btn" onclick="runSpeech('你有好朋友吗',this)">🎤 Record</button></li>
  </ul>
  <p id="speech-msg"></p>
  <button class="btn" onclick="nextPage('s4')">Next Section →</button>
</div>

<!-- SECTION 4: GRAMMAR -->
<div class="card" id="page-s4">
  <div class="section-tag">Section 4</div>
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

  <button class="btn" onclick="finishExam()" style="margin-top:8px">Finish Exam →</button>
</div>

<!-- RESULTS -->
<div class="card" id="results">
  <div class="section-tag">Results</div>
  <h2>Exam Complete!</h2>
  <div class="score-circle" id="final-score">—</div>
  <p id="grade-comment"></p>
  <div class="breakdown">
    <h3>Section Breakdown</h3>
    <div class="breakdown-row"><span>Section 1 · Character Recognition</span><span id="br1">—</span></div>
    <div class="breakdown-row"><span>Section 2 · Listening</span><span id="br2">—</span></div>
    <div class="breakdown-row"><span>Section 3 · Pronunciation</span><span id="br3">—</span></div>
    <div class="breakdown-row"><span>Section 4 · Grammar</span><span id="br4">—</span></div>
  </div>
  <button class="btn" onclick="location.reload()">Retake Exam</button>
</div>

</div>

<script>
let score = 0;
let totalMCQ = 0;
let grammarScore = 0;
let grammarTotal = 6;
let pronunciationDone = 0;
let timerInterval;
let seconds = 3600;

const PAGE_ORDER = ['start','s1','s1q1','s1q2','s1q3','s1q4','s2','s3','s4','results'];
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

function mcq(btn, isCorrect) {
  const grid = btn.closest('.option-grid');
  if (grid.dataset.answered) return;
  grid.dataset.answered = '1';
  totalMCQ++;
  if (isCorrect) {
    btn.classList.add('correct');
    score++;
  } else {
    btn.classList.add('wrong');
    grid.querySelectorAll('.option-btn').forEach(b => {
      if (b !== btn && b.onclick.toString().includes('true')) b.classList.add('correct');
    });
  }
}

function playAudio(text, revealId) {
  if (revealId) document.getElementById(revealId).style.display = 'block';
  if ('speechSynthesis' in window) {
    const u = new SpeechSynthesisUtterance(text);
    u.lang = 'zh-CN';
    u.rate = 0.85;
    speechSynthesis.cancel();
    speechSynthesis.speak(u);
  }
}

function runSpeech(target, btn) {
  const msg = document.getElementById('speech-msg');
  if (!('webkitSpeechRecognition' in window || 'SpeechRecognition' in window)) {
    msg.textContent = '⚠️ Speech recognition not supported. Try Chrome.';
    return;
  }
  const SR = window.SpeechRecognition || window.webkitSpeechRecognition;
  const r = new SR();
  r.lang = 'zh-CN';
  r.interimResults = false;
  r.maxAlternatives = 1;
  btn.textContent = '● Recording…';
  btn.style.background = '#e74c3c';
  msg.textContent = 'Listening…';
  r.start();
  r.onresult = e => {
    const heard = e.results[0][0].transcript;
    msg.textContent = `Heard: "${heard}" — Good job! ✅`;
    btn.textContent = '✅ Done';
    btn.style.background = 'var(--success)';
    pronunciationDone++;
  };
  r.onerror = () => {
    msg.textContent = '⚠️ Could not hear clearly. Try again.';
    btn.textContent = '🎤 Retry';
    btn.style.background = '';
  };
}

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

function finishExam() {
  clearInterval(timerInterval);
  nextPage('results');
  const mcqTotal = totalMCQ || 1;
  const overall = Math.round((score + grammarScore) / (mcqTotal + grammarTotal) * 100);
  const el = document.getElementById('final-score');
  el.textContent = overall + '%';
  if (overall >= 75) el.className = 'score-circle';
  else if (overall >= 50) el.className = 'score-circle mid';
  else el.className = 'score-circle low';
  const comments = { 90:'优秀 Excellent!', 75:'良好 Well done!', 50:'及格 Passing.', 0:'加油! Keep practicing!' };
  const grade = Object.keys(comments).reverse().find(k => overall >= k);
  document.getElementById('grade-comment').textContent = comments[grade];
  document.getElementById('br1').textContent = score + '/' + totalMCQ + ' MCQ';
  document.getElementById('br2').textContent = '—';
  document.getElementById('br3').textContent = pronunciationDone + '/8 recorded';
  document.getElementById('br4').textContent = grammarScore + '/' + grammarTotal + ' correct';
}
</script>
</body>
</html>
