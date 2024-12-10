**index.html**
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <link rel="stylesheet" href="style.css" />
    <title>Quiz App</title>
  </head>
  <body>
    <div class="quiz-container" id="quiz">
      <div class="quiz-header">
        <h2 id="question">Question text</h2>
        <div id="questionNumber"></div>
        <ul>
          <li>
            <input type="radio" name="answer" id="a" class="answer">
            <label for="a" id="a_text">Question</label>
          </li>

          <li>
            <input type="radio" name="answer" id="b" class="answer">
            <label for="b" id="b_text">Question</label>
          </li>

          <li>
            <input type="radio" name="answer" id="c" class="answer">
            <label for="c" id="c_text">Question</label>
          </li>

          <li>
            <input type="radio" name="answer" id="d" class="answer">
            <label for="d" id="d_text">Question</label>
          </li>
        </ul>
      </div>
      <button id="submit">Submit</button>
    </div>
    <script src="script.js"></script>
  </body>
</html>


**style.css**
* {
    box-sizing: border-box;
  }
  
  body {
    background-color: #c43bd6;
    background-image: linear-gradient(315deg, #b8c6db 0%, #f5f7fa 100%);
    font-family: 'Poppins', sans-serif;
    display: flex;
    align-items: center;
    justify-content: center;
    height: 100vh;
    overflow: hidden;
    margin: 0;
  }
  
  .quiz-container {
    background-color: #cf0000;
    border-radius: 10px;
    box-shadow: 0 0 10px 2px rgba(100, 100, 100, 0.1);
    width: 600px;
    overflow: hidden;
  }
  
  .quiz-header {
    padding: 4rem;
  }
  
  h2 {
    padding: 1rem;
    text-align: center;
    margin: 0;
  }
  
  ul {
    list-style-type: none;
    padding: 0;
  }
  
  ul li {
    font-size: 1.2rem;
    margin: 1rem 0;
  }
  
  ul li label {
    cursor: pointer;
  }
  
  button {
    background-color: #ad7c44;
    color: #fff;
    border: none;
    display: block;
    width: 100%;
    cursor: pointer;
    font-size: 1.1rem;
    font-family: inherit;
    padding: 1.3rem;
  }
  
  button:hover {
    background-color: #432d91;
  }
  
  button:focus {
    outline: none;
    background-color: #337047;
  }
  


**script.js**
const quizData = [
    {
        question: "Which language runs in a web browser?",
        a: "Java",
        b: "C",
        c: "Python",
        d: "JavaScript",
        correct: "d",
    },
    {
        question: "What does CSS stand for?",
        a: "Central Style Sheets",
        b: "Cascading Style Sheets",
        c: "Cascading Simple Sheets",
        d: "Cars SUVs Sailboats",
        correct: "b",
    },
    {
        question: "What does HTML stand for?",
        a: "Hypertext Markup Language",
        b: "Hypertext Markdown Language",
        c: "Hyperloop Machine Language",
        d: "Helicopters Terminals Motorboats Lamborginis",
        correct: "a",
    },
    {
        question: "What year was JavaScript launched?",
        a: "1996",
        b: "1995",
        c: "1994",
        d: "none of the above",
        correct: "b",
    },
    {
        question: "Which HTML tag is used to define an internal style sheet?",
        a: "<css>",
        b: "<style>",
        c: "<script>",
        d: "<link>",
        correct: "b",
    },
    {
        question: "What does the 'id' attribute in HTML represent?",
        a: "It defines a unique identifier for an element",
        b: "It defines the style of an element",
        c: "It defines the class of an element",
        d: "It defines the content of an element",
        correct: "a",
    },
    {
        question: "Which of the following is not a programming language?",
        a: "Java",
        b: "Python",
        c: "HTML",
        d: "C++",
        correct: "c",
    },
  
    {
        question: "Which HTML tag is used to insert an image?",
        a: "<image>",
        b: "<img>",
        c: "<src>",
        d: "<picture>",
        correct: "b",
    },
    {
        question: "Which property is used to change the background color in CSS?",
        a: "bgcolor",
        b: "background-color",
        c: "color",
        d: "bg-color",
        correct: "b",
    },
    {
        question: "Which is the correct JavaScript syntax to print a message to the console?",
        a: "console.print('Hello World');",
        b: "console.log('Hello World');",
        c: "print.console('Hello World');",
        d: "log.console('Hello World');",
        correct: "b",
    }
];

const quiz = document.getElementById('quiz');
const answerEls = document.querySelectorAll('.answer');
const questionEl = document.getElementById('question');
const a_text = document.getElementById('a_text');
const b_text = document.getElementById('b_text');
const c_text = document.getElementById('c_text');
const d_text = document.getElementById('d_text');
const submitBtn = document.getElementById('submit');
let currentQuiz = 0;
let score = 0;
let answerFeedback = [];

loadQuiz();

function loadQuiz() {
    deselectAnswers();
    const currentQuizData = quizData[currentQuiz];
    questionEl.innerText = currentQuizData.question;
    a_text.innerText = currentQuizData.a;
    b_text.innerText = currentQuizData.b;
    c_text.innerText = currentQuizData.c;
    d_text.innerText = currentQuizData.d;
    document.getElementById('questionNumber').innerText = `Question ${currentQuiz + 1}/${quizData.length}`;
}

function deselectAnswers() {
    answerEls.forEach(answerEl => answerEl.checked = false);
}

function getSelected() {
    let answer = undefined;
    answerEls.forEach(answerEl => {
        if(answerEl.checked) {
            answer = answerEl.id;
        }
    });
    return answer;
}

submitBtn.addEventListener('click', () => {
    const answer = getSelected();
    if(answer) {
        const correctAnswer = quizData[currentQuiz].correct;
        if(answer === correctAnswer) {
            score++;
            answerFeedback.push({ question: quizData[currentQuiz].question, correct: true });
        } else {
            answerFeedback.push({ question: quizData[currentQuiz].question, correct: false });
        }

        currentQuiz++;
        if(currentQuiz < quizData.length) {
            loadQuiz();
        } else {
            const percentage = (score / quizData.length) * 100;
            let feedbackHtml = `
                <h2>You answered ${score}/${quizData.length} questions correctly</h2>
                <h3>Percentage: ${percentage.toFixed(2)}%</h3>
                <div><strong>Feedback:</strong></div>
                <ul>
            `;
            answerFeedback.forEach(feedback => {
                feedbackHtml += `
                    <li>${feedback.question}: ${feedback.correct ? "Correct" : "Incorrect"}</li>
                `;
            });

            feedbackHtml += `
                </ul>
                <button onclick="location.reload()">Reload</button>
            `;
            quiz.innerHTML = feedbackHtml;
        }
    }
});



