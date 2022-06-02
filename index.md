## Project Purpose and Components
More server-side practice was the main objective of project 4, which asked students to use fastify, postman, and code modules to create and test dynamic outputs.

## What I Learned
This project really helped me learn to combine skills I had been learning throughout the term. It was really satisfying to complete, and forced me to excercise my creative problem solving skills.

## Code
### p4-data.js
// Question and answer data array
const data = [
    {
      question: "Q1",
      answer: "A1",
    },
    {
      question: "Q2",
      answer: "A2",
    },
    {
      question: "Q3",
      answer: "A3",
    },
];
  
// Export statement must be below data declaration - no hoisting with const
module.exports = {
  data,
};

### p4-module.js
const {data} = require('./p4-data.js');

function getQuestions() {
    let questionsArray = []
    for (const object of data) {
        questionsArray.push(object.question)
    }
    return questionsArray;
}

function getAnswers() {
    let answersArray = []
    for (const object of data) {
        answersArray.push(object.answer)
    }
    return answersArray;
}

function getQuestionsAnswers() {
    const clonedData = [...data]; //extra credit?
    return clonedData;
}

function getQuestion(number="") {
    const parsedNumber = parseInt(number);
    const index = parsedNumber-1;
    switch (true) {
        case data[index] !== undefined:
            questionResult = data[index].question;
            numberResult = parsedNumber;
            errorResult = "";
            break;
        case parsedNumber < 1:
            questionResult = "";
            numberResult = "";
            errorResult = "Question number must be >= 1";
            break;
        case parsedNumber > 3:
            questionResult = "";
            numberResult = "";
            errorResult = "Question number must be less than the number of questions (3)";
            break;
        default:
            questionResult = "";
            numberResult = "";
            errorResult = "Question number must be an integer"
    }
    let questionObject = {question: questionResult, number: numberResult, error: errorResult};
    return questionObject;
}

function getAnswer(number="") {
    const parsedNumber = parseInt(number);
    const index = parsedNumber-1;
    switch (true) {
        case data[index] !== undefined:
            answerResult = data[index].answer;
            numberResult = parsedNumber;
            errorResult = "";
            break;
        case parsedNumber < 1:
            answerResult = "";
            numberResult = "";
            errorResult = "Answer number must be >= 1";
            break;
        case parsedNumber > 3:
            answerResult = "";
            numberResult = "";
            errorResult = "Answer number must be less than the number of questions (3)";
            break;
        default:
            answerResult = "";
            numberResult = "";
            errorResult = "Answer number must be an integer"
    }
    let AnswerObject = {answer: answerResult, number: numberResult, error: errorResult};
    return AnswerObject;
}

function getQuestionAnswer(number="") {
    const parsedNumber = parseInt(number);
    const index = parsedNumber-1;
    switch (true) {
        case data[index] !== undefined:
            questionResult = data[index].question;
            answerResult = data[index].answer;
            numberResult = parsedNumber;
            errorResult = "";
            break;
        case parsedNumber < 1:
            questionResult = "";
            answerResult = "";
            numberResult = "";
            errorResult = "Question number must be >= 1";
            break;
        case parsedNumber > 3:
            questionResult = "";
            answerResult = "";
            numberResult = "";
            errorResult = "Question number must be less than the number of questions (3)";
            break;
        default:
            questionResult = "";
            answerResult = "";
            numberResult = "";
            errorResult = "Question number must be an integer"
    }
    let qAndAObject = {question: questionResult, answer: answerResult, number: numberResult, error: errorResult};
    return qAndAObject;
}


module.exports = {
    getQuestions,
    getAnswers,
    getQuestionsAnswers,
    getQuestion,
    getAnswer,
    getQuestionAnswer
};


/*****************************
  Module function testing
******************************/
function testing(category, ...args) {
    console.log(`\n** Testing ${category} **`);
    console.log("-------------------------------");
    for (const o of args) {
        console.log(`-> ${category}${o.d}:`);
        console.log(o.f);
    }
}
  
// Set a constant to true to test the appropriate function
const testGetQs = false;
const testGetAs = false;
const testGetQsAs = false;
const testGetQ = false;
const testGetA = false;
const testGetQA = false;
const testAdd = false;      // Extra credit
const testUpdate = false;   // Extra credit
const testDelete = false;   // Extra credit

// getQuestions()
if (testGetQs) {
    testing("getQuestions", { d: "()", f: getQuestions() });
}
  
// getAnswers()
if (testGetAs) {
    testing("getAnswers", { d: "()", f: getAnswers() });
}
  
// getQuestionsAnswers()
if (testGetQsAs) {
    testing("getQuestionsAnswers", { d: "()", f: getQuestionsAnswers() });
}
  
// getQuestion()
if (testGetQ) {
    testing(
        "getQuestion",
        { d: "()", f: getQuestion() },      // Extra credit: +1
        { d: "(0)", f: getQuestion(0) },    // Extra credit: +1
        { d: "(1)", f: getQuestion(1) },
        { d: "(4)", f: getQuestion(4) }     // Extra credit: +1
    );
}
  
// getAnswer()
if (testGetA) {
    testing(
        "getAnswer",
        { d: "()", f: getAnswer() },        // Extra credit: +1
        { d: "(0)", f: getAnswer(0) },      // Extra credit: +1
        { d: "(1)", f: getAnswer(1) },
        { d: "(4)", f: getAnswer(4) }       // Extra credit: +1
    );
}
  
// getQuestionAnswer()
if (testGetQA) {
    testing(
        "getQuestionAnswer",
        { d: "()", f: getQuestionAnswer() },    // Extra credit: +1
        { d: "(0)", f: getQuestionAnswer(0) },  // Extra credit: +1
        { d: "(1)", f: getQuestionAnswer(1) },
        { d: "(4)", f: getQuestionAnswer(4) }   // Extra credit: +1
    );
}

## p4-server.js
const fastify = require("fastify")(); 
const {getQuestions, getAnswers, getQuestionsAnswers, getQuestion, getAnswer, getQuestionAnswer} = require('./p4-module.js');

fastify.get("/cit/question", function (request, reply) {
    const response = {
        "error": "",
        "statusCode": 200,
        "questions": getQuestions()
    }
    reply
    .code(200)
    .header("Content-Type", "application/json; charset=utf-8")
    .send(response);
});

fastify.get("/cit/answer", function (request, reply) {
    const response = {
        "error": "",
        "statusCode": 200,
        "answers": getAnswers()
    }
    reply
    .code(200)
    .header("Content-Type", "application/json; charset=utf-8")
    .send(response);
});

fastify.get("/cit/questionanswer", function (request, reply) {
    const response = {
        "error": "",
        "statusCode": 200,
        "questions_answers": getQuestionsAnswers()
    }
    reply
    .code(200)
    .header("Content-Type", "application/json; charset=utf-8")
    .send(response);
});

//http://localhost:8080/cit/question/:number?number=2
fastify.get("/cit/question/:number", function (request, reply) {
    console.log(request.query);
    const { number } = request.query;
    const questionNumber = getQuestion(number);
    const response = {
        "error": questionNumber.error,
        "statusCode": 200,
        "question": questionNumber.question,
        "number": questionNumber.number
    }
    reply
    .code(200)
    .header("Content-Type", "application/json; charset=utf-8")
    .send(response);
});

//http://localhost:8080/cit/answer/:number?number=1
fastify.get("/cit/answer/:number", function (request, reply) {
    console.log(request.query);
    const { number } = request.query;
    const answerNumber = getAnswer(number);
    const response = {
        "error": answerNumber.error,
        "statusCode": 200,
        "answer": answerNumber.answer,
        "number": answerNumber.number
    }
    reply
    .code(200)
    .header("Content-Type", "application/json; charset=utf-8")
    .send(response);
});

//http://localhost:8080/cit/questionanswer/:number?number=3
fastify.get("/cit/questionanswer/:number", function (request, reply) {
    console.log(request.query);
    const { number } = request.query;
    const qAndANumber = getQuestionAnswer(number);
    const response = {
        "error": qAndANumber.error,
        "statusCode": 200,
        "question": qAndANumber.question,
        "answer": qAndANumber.answer,
        "number": qAndANumber.number
    }
    reply
    .code(200)
    .header("Content-Type", "application/json; charset=utf-8")
    .send(response);
});

fastify.get("*", function (request, reply) {
    const response = {
        "error": "Route not found",
        "statusCode": 404
    }
    reply
    .code(404)
    .header("Content-Type", "application/json; charset=utf-8")
    .send(response);
});

const listenIP = "localhost";
const listenPort = 8080;
fastify.listen(listenPort, listenIP, function (err, address) {
    if (err) {
        console.log(err);
        process.exit(1);
    }
    console.log(`Server listening on ${address}`);
})

### [Home Page](https://slynsky.github.io)

