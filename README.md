<!DOCTYPE html><html lang="ar">
<head>
  <meta charset="UTF-8">
  <title>غرفة الأسرار</title>
  <style>
    body { font-family: Arial; background: #111; color: white; text-align: center; padding: 50px; direction: rtl; }
    .menu, .puzzle-box { background: #222; padding: 20px; border-radius: 10px; width: 80%; margin: auto; display: none; }
    .menu.active, .puzzle-box.active { display: block; }
    input, button { padding: 10px; font-size: 18px; margin-top: 10px; }
    button { cursor: pointer; margin: 10px; }
  </style>
</head>
<body>
  <h1>غرفة الأسرار</h1>  <div id="mainMenu" class="menu active">
    <button onclick="startNewGame()">لعبة جديدة</button>
    <button onclick="continueGame()">تكملة اللعب</button>
    <button onclick="openSettings()">الإعدادات</button>
  </div>  <div id="settings" class="menu">
    <p>لا توجد إعدادات حاليًا. (يتم التطوير)</p>
    <button onclick="backToMenu()">عودة</button>
  </div>  <div id="game" class="puzzle-box">
    <p id="puzzle">لفتح الباب، ما هو الرقم التالي في التسلسل: 2، 4، 8، 16، ؟</p>
    <input type="text" id="answer" placeholder="اكتب إجابتك هنا">
    <br>
    <button onclick="checkAnswer()">تحقق</button>
    <p id="feedback"></p>
  </div>  <script>
    let currentLevel = 1;

    function showSection(id) {
      document.querySelectorAll('.menu, .puzzle-box').forEach(el => el.classList.remove('active'));
      document.getElementById(id).classList.add('active');
    }

    function startNewGame() {
      currentLevel = 1;
      showSection('game');
      loadLevel(currentLevel);
    }

    function continueGame() {
      showSection('game');
      loadLevel(currentLevel);
    }

    function openSettings() {
      showSection('settings');
    }

    function backToMenu() {
      showSection('mainMenu');
    }

    function loadLevel(level) {
      const puzzle = document.getElementById("puzzle");
      const feedback = document.getElementById("feedback");
      const answer = document.getElementById("answer");
      answer.value = "";
      feedback.textContent = "";

      if (level === 1) {
        puzzle.textContent = "لفتح الباب، ما هو الرقم التالي في التسلسل: 2، 4، 8، 16، ؟";
      } else if (level === 2) {
        puzzle.textContent = "كلمة السر هي كلمة تتكون من أربعة حروف، إذا حذفت أول حرف أصبحت فرد، إذا حذفت الثاني أصبحت شيء يُشرب، إذا حذفت الثالث أصبحت حرف، ما هي؟";
      } else if (level === 3) {
        puzzle.textContent = "ما هو الرقم التالي في التسلسل: 1، 1، 2، 3، 5، 8، ؟";
      }
    }

    function checkAnswer() {
      const userAnswer = document.getElementById("answer").value.trim();
      const feedback = document.getElementById("feedback");

      if (currentLevel === 1 && userAnswer === "32") {
        feedback.textContent = "أحسنت! تم فتح الباب. المستوى التالي قادم...";
        currentLevel++;
        setTimeout(() => loadLevel(currentLevel), 2000);
      } else if (currentLevel === 2 && userAnswer === "فرد") {
        feedback.textContent = "ممتاز! لقد تجاوزت المرحلة الثانية.";
        currentLevel++;
        setTimeout(() => loadLevel(currentLevel), 2000);
      } else if (currentLevel === 3 && userAnswer === "13") {
        feedback.textContent = "ممتاز! لقد تجاوزت المرحلة الثالثة.";
        // يمكن إضافة مستويات أكثر هنا لاحقًا
      } else {
        feedback.textContent = "إجابة خاطئة، حاول مجددًا.";
      }
    }
  </script></body>
</html>
