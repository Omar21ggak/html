<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Learn HTML</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #f4f4f4;
      color: #333;
      margin: 0;
      padding: 0;
    }

    header {
      background-color: #007BFF;
      color: white;
      padding: 20px;
      text-align: center;
    }

    .container {
      display: flex;
      flex-wrap: wrap;
      padding: 20px;
    }

    main {
      flex: 2;
      min-width: 300px;
      padding-right: 20px;
    }

    aside {
      flex: 1;
      min-width: 250px;
      background-color: #fff;
      border-left: 2px solid #ccc;
      padding: 20px;
      box-shadow: 0 0 5px rgba(0, 0, 0, 0.1);
    }

    h2 {
      color: #007BFF;
    }

    ul {
      list-style-type: none;
      padding-left: 0;
    }

    li {
      margin: 10px 0;
    }

    a {
      text-decoration: none;
      color: #0056b3;
    }

    a:hover {
      text-decoration: underline;
    }

    footer {
      background-color: #eee;
      text-align: center;
      padding: 15px;
      margin-top: 20px;
    }

    input, button, select {
      padding: 8px;
      margin-top: 10px;
      font-size: 14px;
    }

    #message {
      margin-top: 10px;
      font-weight: bold;
    }

    #quiz-section {
      background-color: #fff;
      padding: 15px;
      margin-top: 30px;
      border: 1px solid #ccc;
      box-shadow: 0 0 5px rgba(0,0,0,0.05);
    }

    #quiz-result {
      margin-top: 10px;
      font-weight: bold;
    }

    .quiz-question {
      margin: 15px 0;
    }

  </style>
</head>
<body>
  <header>
    <h1>Welcome to Learn HTML</h1>
    <p>Start your journey in web development!</p>
  </header>

  <div class="container">
    <main>
      <h2> HTML Learning Resources</h2>
      <ul>
        <li><a href="https://developer.mozilla.org/en-US/docs/Web/HTML" target="_blank">MDN Web Docs - HTML</a></li>
        <li><a href="https://www.w3schools.com/html/" target="_blank">W3Schools HTML Tutorial</a></li>
        <li><a href="https://html.com/" target="_blank">HTML.com Beginner Guide</a></li>
        <li><a href="https://www.freecodecamp.org/learn/2022/responsive-web-design/" target="_blank">freeCodeCamp HTML Course</a></li>
        <li><a href="https://www.codecademy.com/learn/learn-html" target="_blank">Codecademy - Learn HTML</a></li>
        <li><a href="https://www.youtube.com/watch?v=pQN-pnXPaVg" target="_blank">YouTube: HTML Full Course - freeCodeCamp</a></li>
      </ul>

      <h2>💡 Tips for Beginners</h2>
      <ul>
        <li>Practice writing your own HTML code daily.</li>
        <li>Use browser developer tools to inspect elements.</li>
        <li>Build small projects like a portfolio or a to-do list.</li>
      </ul>

      <h2>📚 Test Your Knowledge</h2>
      <p><a href="#quiz-section">Take the HTML Quiz</a></p>

      <section id="quiz-section">
        <h2>📝 HTML Quiz</h2>
        <form id="quiz-form">
          <div id="quiz-questions"></div>
          <button type="button" onclick="submitQuiz()">Submit Quiz</button>
          <button type="button" onclick="nextQuestion()">Next Question</button>
        </form>
        <div id="quiz-result"></div>
      </section>
    </main>

    <aside>
      <h2> Guess the Number</h2>
      <label for="difficulty">Select Difficulty:</label><br />
      <select id="difficulty" onchange="changeDifficulty()">
        <option value="10">Easy (1–10)</option>
        <option value="50">Medium (1–50)</option>
        <option value="100">Hard (1–100)</option>
      </select>

      <p>Guess a number:</p>
      <input type="number" id="guess">
      <button onclick="checkGuess()">Guess</button>
      <button onclick="resetGame()"> Reset</button>

      <div id="message"></div>
      <p>✅ Score: <span id="score">0</span></p>
      <p>🏆 High Score: <span id="high-score">0</span></p>
      <p>❤️ Lives: <span id="lives">3</span></p>
    </aside>
  </div>

  <footer>
    <p>Made with beginner HTML script for beginners</p>
  </footer>

  <script>
    const questions = [
      { question: "What does HTML stand for?", options: ["Hyper Trainer Marking Language", "Hyper Text Markup Language", "Hyperlinks and Text Mark Language"], correct: 1 },
      { question: "What is the correct HTML tag for inserting a line break?", options: ["<break>", "<br>", "<lb>"], correct: 1 },
      { question: "Which HTML tag is used to define a table?", options: ["<table>", "<tr>", "<td>"], correct: 0 },
      { question: "Which tag is used for the largest heading in HTML?", options: ["<h1>", "<h2>", "<h3>"], correct: 0 },
      { question: "What is the correct HTML element for inserting an image?", options: ["<img>", "<image>", "<picture>"], correct: 0 },
    ];

    let currentQuestionIndex = 0;
    let score = 0;

    function showQuestion() {
      const questionData = questions[currentQuestionIndex];
      const quizQuestionsDiv = document.getElementById("quiz-questions");
      quizQuestionsDiv.innerHTML = `
        <div class="quiz-question">
          <strong>${questionData.question}</strong><br />
          ${questionData.options.map((option, index) => `
            <input type="radio" name="q${currentQuestionIndex}" value="${index}" id="option${index}">
            <label for="option${index}">${option}</label><br />
          `).join('')}
        </div>
      `;
    }

    function nextQuestion() {
      const selectedOption = document.querySelector(`input[name="q${currentQuestionIndex}"]:checked`);
      const resultDiv = document.getElementById("quiz-result");

      if (selectedOption) {
        const selectedAnswer = parseInt(selectedOption.value);
        if (selectedAnswer === questions[currentQuestionIndex].correct) {
          score++;
        }
      }

      currentQuestionIndex++;

      if (currentQuestionIndex < questions.length) {
        showQuestion();
      } else {
        resultDiv.textContent = `You scored ${score} out of ${questions.length}!`;
        resultDiv.style.fontWeight = 'bold';
        currentQuestionIndex = 0;  // Reset for a new round
      }
    }

    function submitQuiz() {
      const resultDiv = document.getElementById("quiz-result");
      resultDiv.textContent = `You scored ${score} out of ${questions.length}!`;
      resultDiv.style.fontWeight = 'bold';
      resultDiv.style.marginTop = '10px';
    }

    // Start the quiz when the page loads
    window.onload = showQuestion;
  </script>
</body>
</html>
