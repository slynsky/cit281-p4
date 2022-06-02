## Project Purpose and Components
More server-side practice was the main objective of project 4, which asked students to use fastify, postman, and code modules to create and test dynamic outputs.

## What I Learned
This project really helped me learn to combine skills I had been learning throughout the term. It was really satisfying to complete, and forced me to excercise my creative problem solving skills.

## Code
### p4-data.js
// Question and answer data array<br>
const data = [<br>
    {<br>
      question: "Q1",<br>
      answer: "A1",<br>
    },<br>
    {<br>
      question: "Q2",<br>
      answer: "A2",<br>
    },<br>
    {<br>
      question: "Q3",<br>
      answer: "A3",<br>
    },<br>
];<br>
  
// Export statement must be below data declaration - no hoisting with const<br>
module.exports = {<br>
  data,<br>
};<br>

### p4-module.js<br>
const {data} = require('./p4-data.js');<br>

function getQuestions() {<br>
    let questionsArray = []<br>
    for (const object of data) {<br>
        questionsArray.push(object.question)<br>
    }<br>
    return questionsArray;<br>
}<br>

function getAnswers() {<br>
    let answersArray = []<br>
    for (const object of data) {<br>
        answersArray.push(object.answer)<br>
    }<br>
    return answersArray;<br>
}<br>

function getQuestionsAnswers() {<br>
    const clonedData = [...data]; //extra credit?<br>
    return clonedData;<br>
}

function getQuestion(number="") {<br>
    const parsedNumber = parseInt(number);<br>
    const index = parsedNumber-1;<br>
    switch (true) {<br>
        case data[index] !== undefined:<br>
            questionResult = data[index].question;<br>
            numberResult = parsedNumber;<br>
            errorResult = "";<br>
            break;<br>
        case parsedNumber < 1:<br>
            questionResult = "";<br>
            numberResult = "";<br>
            errorResult = "Question number must be >= 1";<br>
            break;<br>
        case parsedNumber > 3:<br>
            questionResult = "";<br>
            numberResult = "";<br>
            errorResult = "Question number must be less than the number of questions (3)";<br>
            break;<br>
        default:<br>
            questionResult = "";<br>
            numberResult = "";<br>
            errorResult = "Question number must be an integer"<br>
    }<br>
    let questionObject = {question: questionResult, number: numberResult, error: errorResult};<br>
    return questionObject;<br>
}<br>

function getAnswer(number="") {<br>
    const parsedNumber = parseInt(number);<br>
    const index = parsedNumber-1;<br>
    switch (true) {<br>
        case data[index] !== undefined:<br>
            answerResult = data[index].answer;<br>
            numberResult = parsedNumber;<br>
            errorResult = "";<br>
            break;<br>
        case parsedNumber < 1:<br>
            answerResult = "";<br>
            numberResult = "";<br>
            errorResult = "Answer number must be >= 1";<br>
            break;<br>
        case parsedNumber > 3:<br>
            answerResult = "";<br>
            numberResult = "";<br>
            errorResult = "Answer number must be less than the number of questions (3)";<br>
            break;<br>
        default:<br>
            answerResult = "";<br>
            numberResult = "";<br>
            errorResult = "Answer number must be an integer"<br>
    }<br>
    let AnswerObject = {answer: answerResult, number: numberResult, error: errorResult};<br>
    return AnswerObject;<br>
}<br>

function getQuestionAnswer(number="") {<br>
    const parsedNumber = parseInt(number);<br>
    const index = parsedNumber-1;<br>
    switch (true) {<br>
        case data[index] !== undefined:<br>
            questionResult = data[index].question;<br>
            answerResult = data[index].answer;<br>
            numberResult = parsedNumber;<br>
            errorResult = "";<br>
            break;<br>
        case parsedNumber < 1:<br>
            questionResult = "";<br>
            answerResult = "";<br>
            numberResult = "";<br>
            errorResult = "Question number must be >= 1";<br>
            break;<br>
        case parsedNumber > 3:<br>
            questionResult = "";<br>
            answerResult = "";<br>
            numberResult = "";<br>
            errorResult = "Question number must be less than the number of questions (3)";<br>
            break;<br>
        default:<br>
            questionResult = "";<br>
            answerResult = "";<br>
            numberResult = "";<br>
            errorResult = "Question number must be an integer"<br>
    }<br>
    let qAndAObject = {question: questionResult, answer: answerResult, number: numberResult, error: errorResult};<br>
    return qAndAObject;<br>
}<br>


module.exports = {<br>
    getQuestions,<br>
    getAnswers,<br>
    getQuestionsAnswers,<br>
    getQuestion,<br>
    getAnswer,<br>
    getQuestionAnswer<br>
};<br>


/*****************************<br>
  Module function testing<br>
******************************/<br>
function testing(category, ...args) {<br>
    console.log(`\n** Testing ${category} **`);<br>
    console.log("-------------------------------");<br>
    for (const o of args) {<br>
        console.log(`-> ${category}${o.d}:`);<br>
        console.log(o.f);<br>
    }<br>
}<br>
  
// Set a constant to true to test the appropriate function<br>
const testGetQs = false;<br>
const testGetAs = false;<br>
const testGetQsAs = false;<br>
const testGetQ = false;<br>
const testGetA = false;<br>
const testGetQA = false;<br>
const testAdd = false;      // Extra credit<br>
const testUpdate = false;   // Extra credit<br>
const testDelete = false;   // Extra credit<br>

// getQuestions()<br>
if (testGetQs) {<br>
    testing("getQuestions", { d: "()", f: getQuestions() });<br>
}<br>
  
// getAnswers()<br>
if (testGetAs) {<br>
    testing("getAnswers", { d: "()", f: getAnswers() });<br>
}<br>
  
// getQuestionsAnswers()<br>
if (testGetQsAs) {<br>
    testing("getQuestionsAnswers", { d: "()", f: getQuestionsAnswers() });<br>
}<br>
  
// getQuestion()<br>
if (testGetQ) {<br>
    testing(<br>
        "getQuestion",<br>
        { d: "()", f: getQuestion() },      // Extra credit: +1<br>
        { d: "(0)", f: getQuestion(0) },    // Extra credit: +1<br>
        { d: "(1)", f: getQuestion(1) },<br>
        { d: "(4)", f: getQuestion(4) }     // Extra credit: +1<br>
    );<br>
}<br>
  
// getAnswer()<br>
if (testGetA) {<br>
    testing(<br>
        "getAnswer",<br>
        { d: "()", f: getAnswer() },        // Extra credit: +1<br>
        { d: "(0)", f: getAnswer(0) },      // Extra credit: +1<br>
        { d: "(1)", f: getAnswer(1) },<br>
        { d: "(4)", f: getAnswer(4) }       // Extra credit: +1<br>
    );<br>
}<br>
  
// getQuestionAnswer()<br>
if (testGetQA) {<br>
    testing(<br>
        "getQuestionAnswer",<br>
        { d: "()", f: getQuestionAnswer() },    // Extra credit: +1<br>
        { d: "(0)", f: getQuestionAnswer(0) },  // Extra credit: +1<br>
        { d: "(1)", f: getQuestionAnswer(1) },<br>
        { d: "(4)", f: getQuestionAnswer(4) }   // Extra credit: +1<br>
    );<br>
}<br>

## p4-server.js
const fastify = require("fastify")(); <br>
const {getQuestions, getAnswers, getQuestionsAnswers, getQuestion, getAnswer, getQuestionAnswer} = require('./p4-module.js');<br>

fastify.get("/cit/question", function (request, reply) {<br>
    const response = {<br>
        "error": "",<br>
        "statusCode": 200,<br>
        "questions": getQuestions()<br>
    }<br>
    reply<br>
    .code(200)<br>
    .header("Content-Type", "application/json; charset=utf-8")<br>
    .send(response);<br>
});<br>

fastify.get("/cit/answer", function (request, reply) {<br>
    const response = {<br>
        "error": "",<br>
        "statusCode": 200,<br>
        "answers": getAnswers()<br>
    }<br>
    reply<br>
    .code(200)<br>
    .header("Content-Type", "application/json; charset=utf-8")<br>
    .send(response);<br>
});<br>

fastify.get("/cit/questionanswer", function (request, reply) {<br>
    const response = {<br><br>
        "error": "",<br>
        "statusCode": 200,<br>
        "questions_answers": getQuestionsAnswers()<br>
    }<br>
    reply<br>
    .code(200)<br>
    .header("Content-Type", "application/json; charset=utf-8")<br>
    .send(response);<br>
});<br>

//http://localhost:8080/cit/question/:number?number=2<br>
fastify.get("/cit/question/:number", function (request, reply) {<br>
    console.log(request.query);<br>
    const { number } = request.query;<br>
    const questionNumber = getQuestion(number);<br>
    const response = {<br>
        "error": questionNumber.error,<br>
        "statusCode": 200,<br>
        "question": questionNumber.question,<br>
        "number": questionNumber.number<br>
    }<br>
    reply<br>
    .code(200)<br>
    .header("Content-Type", "application/json; charset=utf-8")<br>
    .send(response);<br>
});<br>

//http://localhost:8080/cit/answer/:number?number=1<br>
fastify.get("/cit/answer/:number", function (request, reply) {<br>
    console.log(request.query);<br>
    const { number } = request.query;<br>
    const answerNumber = getAnswer(number);<br>
    const response = {<br>
        "error": answerNumber.error,<br>
        "statusCode": 200,<br>
        "answer": answerNumber.answer,<br>
        "number": answerNumber.number<br>
    }<br>
    reply<br>
    .code(200)<br>
    .header("Content-Type", "application/json; charset=utf-8")<br>
    .send(response);<br>
});<br>

//http://localhost:8080/cit/questionanswer/:number?number=3<br>
fastify.get("/cit/questionanswer/:number", function (request, reply) {<br>
    console.log(request.query);<br>
    const { number } = request.query;<br>
    const qAndANumber = getQuestionAnswer(number);<br>
    const response = {<br>
        "error": qAndANumber.error,<br>
        "statusCode": 200,<br>
        "question": qAndANumber.question,<br>
        "answer": qAndANumber.answer,<br>
        "number": qAndANumber.number<br>
    }<br>
    reply<br>
    .code(200)<br>
    .header("Content-Type", "application/json; charset=utf-8")<br>
    .send(response);<br>
});<br>

fastify.get("*", function (request, reply) {<br>
    const response = {<br>
        "error": "Route not found",<br>
        "statusCode": 404<br>
    }<br>
    reply<br>
    .code(404)<br>
    .header("Content-Type", "application/json; charset=utf-8")<br>
    .send(response);<br>
});<br>

const listenIP = "localhost";<br>
const listenPort = 8080;<br>
fastify.listen(listenPort, listenIP, function (err, address) {<br>
    if (err) {<br>
        console.log(err);<br>
        process.exit(1);<br>
    }
    console.log(`Server listening on ${address}`);<br>
})<br>

### [Home Page](https://slynsky.github.io)

