
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>What Kuih Raya TFM Fellow Are You?</title>
  <style>
    body {
      font-family: 'Segoe UI', sans-serif;
      background: #fef9f5;
      color: #333;
      padding: 2rem;
      text-align: center;
    }
    .quiz-container, .start-container {
      max-width: 600px;
      margin: auto;
      background: #ffffff;
      padding: 2rem;
      border-radius: 1.5rem;
      box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
    }
    .question {
      font-size: 1.5rem;
      margin-bottom: 1rem;
    }
    .choices button, .start-button {
      display: block;
      width: 100%;
      margin: 0.5rem 0;
      padding: 1rem;
      border: none;
      background: #e0f2e9;
      border-radius: 1rem;
      font-size: 1rem;
      cursor: pointer;
      transition: 0.3s;
    }
    .choices button:hover, .start-button:hover {
      background: #b8e4d0;
    }
    .result {
      display: none;
      margin-top: 2rem;
    }
    .result img {
      width: 200px;
      border-radius: 1rem;
    }
    .start-container img {
      width: 100%;
      border-radius: 1rem;
      margin-bottom: 1rem;
    }
  </style>
</head>
<body>
  <div class="start-container" id="start-container">
    <img src="cover.png" alt="Quiz Cover">
    <button class="start-button" onclick="startQuiz()">Start Quiz</button>
  </div>

  <div class="quiz-container" id="quiz-container" style="display: none;">
    <div id="quiz">
      <div class="question" id="question">Loading question...</div>
      <div class="choices" id="choices"></div>
    </div>
    <div class="result" id="result">
      <h2 id="result-title"></h2>
      <img id="result-img" src="" alt="Result image">
      <p id="result-description"></p>
    </div>
  </div>

  <script>
    const quizData = [
      {
        question: "I got 5 minutes before class starts?",
        choices: [
          "Hype playlist blasting. I'm doing a lil dance.",
          "Laptop plugged in, slides triple-checked, seating chart ready.",
          "Sipping kopi, chatting with kids like it’s teh tarik time.",
          "Scribbling last-minute quotes on the board. Deep, obviously.",
          "Seated, materials ready. Early. As always."
        ]
      },
      {
        question: "My teaching tool of choice?",
        choices: [
          "My voice and vibes",
          "PowerPoint with transitions, hyperlinks, and back-up plan C",
          "Whiteboard and funny analogies up my sleeves",
          "Handwritten notes and maybe a mind map if I’m feeling artsy",
          "That one recycled worksheet that always works"
        ]
      },
      {
        question: "During team meetings, I will always...",
        choices: [
          "Crack a joke then gets distracted by it because I am hilarious",
          "Have my colour-coded document open, 4 tabs, and a spreadsheet",
          "Offers snacks. Always.",
          "Drop a quiet truth bomb leaving everyone in deep thought",
          "Listens 90%, says one thing, but it solves the whole problem"
        ]
      },
      {
        question: "Last-minute timetable change?",
        choices: [
          "Laugh, panic internally, then SLAY.",
          "Whip out my emergency backup plan folder—duh.",
          "Smile and check in on how my students are feeling first.",
          "“Copy page 37 while I sort this out.” Efficienttt.",
          "“Surprise outdoor lesson today, kids!” (I was born for chaos.)"
        ]
      },
      {
        question: "On my desk? Ermm I have..?",
        choices: [
          "Random stickers, snacks, peculiar gifts from students",
          "Laptop stand, planner, matching stationery",
          "Drawer full of pens, phone that’s always 5% for some reason",
          "Books with intense titles like ‘Pedagogy of the Oppressed’",
          "One water bottle, one pen, vibes of quiet resilience"
        ]
      }
    ];

    const results = [
      {
        title: "🍡 Onde-onde – The Firecracker Fellow",
        img: ![onde-onde](https://github.com/user-attachments/assets/684de367-25f1-44ab-bbdc-b9714ec949a5),
        description: "Explosive energy, major charm. Your classroom’s never boring and neither are you. You’re the kind of Fellow who can make anything fun—even grammar. (You probably also overshare with your students, and they love you for it.)"
      },
      {
        title: "🌈 Kuih Lapis – The Layered Strategist",
        img: ![kuih-lapis](https://github.com/user-attachments/assets/cab544a6-c308-4654-84db-9fe7902554f3),
        description: "You’ve got range. Your lesson plans? Immaculate. Your Google Sheets? Colour-coded. You bring structure with flair."
      },
      {
        title: "🌿 Kuih Seri Muka – The Calm Hustler",
        img: ![seri-muka](https://github.com/user-attachments/assets/a10e31ce-1c21-42ff-bd50-7d74b32b0161),
        description: "Understated brilliance. You keep your cool even when the projector dies again. Students know you’re the real MVP."
      },
      {
        title: "🍃✨ Kuih Bingka Pandan – The Silent Slayer",
        img: ![kuih-talam](https://github.com/user-attachments/assets/d7bdfbe7-50c4-449f-a247-2e0b0a22e981),
        description: "Lowkey iconic and always dependable. You’re the calm in chaos, the toastiest of team players. Quietly slaying group projects since forever."
      },
      {
        title: "🍌 Lepat Pisang – The Quiet Rock",
        img: ![lepat-pisang](https://github.com/user-attachments/assets/81881bc8-73f7-4f14-92e3-ad7f585922ad),
        description: "Reliable, consistent, full of soul. First to show up, last to complain. Your students feel safe with you."
      }
    ];

    let currentQuestion = 0;
    let answers = [];

    function startQuiz() {
      document.getElementById('start-container').style.display = 'none';
      document.getElementById('quiz-container').style.display = 'block';
      loadQuestion();
    }

    function loadQuestion() {
      const q = quizData[currentQuestion];
      document.getElementById('question').textContent = q.question;
      const choicesEl = document.getElementById('choices');
      choicesEl.innerHTML = '';
      q.choices.forEach((choice, idx) => {
        const btn = document.createElement('button');
        btn.textContent = choice;
        btn.onclick = () => {
          answers.push(idx);
          currentQuestion++;
          if (currentQuestion < quizData.length) {
            loadQuestion();
          } else {
            showResult();
          }
        };
        choicesEl.appendChild(btn);
      });
    }

    function showResult() {
      const score = answers.reduce((a, b) => a + b, 0);
      const resultIndex = Math.round(score / answers.length);
      const result = results[resultIndex];
      document.getElementById('quiz').style.display = 'none';
      document.getElementById('result-title').textContent = result.title;
      document.getElementById('result-img').src = result.img;
      document.getElementById('result-description').textContent = result.description;
      document.getElementById('result').style.display = 'block';
    }
  </script>
</body>
</html>

