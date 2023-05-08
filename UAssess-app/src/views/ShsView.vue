<template>
    <div class="shs-page">
      <main class="app">
          <section class="quiz" v-if="!quizCompleted">
              <div class="quiz-info">
                  <span class="question">{{ getCurrentQuestion.question }}</span>
              </div>
              
              <div class="options">
                  <label 
                      v-for="(option, index) in getCurrentQuestion.options" 
                      :for="'option' + index" 
                      :class="`option ${
                          getCurrentQuestion.selected == index 
                              ? index == getCurrentQuestion.answer 
                                  ? 'correct' 
                                  : 'wrong'
                              : ''
                      } ${
                          getCurrentQuestion.selected != null &&
                          index != getCurrentQuestion.selected
                              ? 'disabled'
                              : ''
                      }`">
                      <input 
                          type="radio" 
                          :id="'option' + index" 
                          :name="getCurrentQuestion.index" 
                          :value="index" 
                          v-model="getCurrentQuestion.selected" 
                          :disabled="getCurrentQuestion.selected"
                          @change="SetAnswer" 
                      />
                      <span>{{ option }}</span>
                  </label>
              </div>
        <button 
                  @click="NextQuestion" 
                  :disabled="!getCurrentQuestion.selected">
                  {{ 
                      getCurrentQuestion.index == questions.length - 1 
                          ? 'Finish' 
                          : getCurrentQuestion.selected == null
                              ? 'Select an option'
                              : 'Next question'
                  }}
              </button>
          </section>

          <section v-else>
            <div class="summary">
              <h2>Congratulations!<br> You have finished the exam!</h2>
              <h1>Your score is <br> {{ score }}/{{ questions.length }}</h1>
            </div>
          </section>
      </main>
    </div>
  </template>
  
  <script setup>
  import { ref, computed } from 'vue'
  
  const questions = ref([
    // 1
    {
      question: 'What is the formula for the area of a rectangle?',
      answer: 0,
      options: [
        'length x width',
        'length + width',
        'length ÷ width'
      ],
      selected: null
    },
    // 2
    {
      question: 'What is the scientific name for the human thumb?',
      answer: 0,
      options: [
        'pollex',
        'manus',
        'pes'
      ],
      selected: null
    },
    // 3
    {
      question: 'Which of the following is NOT a state in the United States of America?',
      answer: 1,
      options: [
        'Ohio',
        'Ontario',
        'Oregon'
      ],
      selected: null
    },
    // 4
    {
      question: 'What is the capital of Australia?',
      answer: 2,
      options: [
        'Sydney',
        'Melbourne',
        'Canberra'
      ],
      selected: null
    },
    // 5
    {
      question: 'Which country is known as the "Land of the Rising Sun"?',
      answer: 0,
      options: [
        'Japan',
        'China',
        'South Korea'
      ],
      selected: null
    },
    // 6
    {
      question: 'What is the chemical symbol for gold?',
      answer: 1,
      options: [
        'Gu',
        'Au',
        'Ag'
      ],
      selected: null
    },
    // 7
    {
      question: 'Which of the following is a primary component of natural gas?',
      answer: 0,
      options: [
        'Methane',
        'Carbon dioxide',
        'Oxygen'
      ],
      selected: null
    },
    // 8
    {
      question: 'What is the value of x in the equation 3x + 2 = 11?',
      answer: 0,
      options: [
        'Three (3)',
        'Nine (9)',
        'Five (5)'
      ],
      selected: null
    },
    // 9
    {
      question: 'Which of the following is an example of a fallacy?',
      answer: 2,
      options: [
        'All cats are animals. Fluffy is a cat. Therefore, Fluffy is an animal.',
        'All dogs are animals. Fluffy is not a dog. Therefore, Fluffy is not an animal.',
        'All cats are animals. Fluffy is not an animal. Therefore, Fluffy is not a cat.'
      ],
      selected: null
    },
    // 10
    {
      question: 'What type of bond holds the hydrogen and oxygen atoms together in a water molecule?',
      answer: 1,
      options: [
        'Ionic bond',
        'Covalent bond',
        'Hydrogen bond'
      ],
      selected: null
    },
    // 11
    {
      question: 'What is the slope of the line passing through the points (2, 3) and (4, 5)?',
      answer: 1,
      options: [
        '1',
        '2',
        '0.5'
      ],
      selected: null
    },
    // 12
    {
      question: 'What is the next number in the sequence: 1, 3, 5, 7, ...?',
      answer: 2,
      options: [
        '8',
        '9',
        '11'
      ],
      selected: null
    },
    // 13
    {
      question: 'Which of the following is NOT one of the four fundamental forces of nature?',
      answer: 2,
      options: [
        'Gravity',
        'Electromagnetism',
        'Strong force'
      ],
      selected: null
    },
    // 14
    {
      question: 'Which of the following is equivalent to the expression (x + 2)(x - 3)?',
      answer: 0,
      options: [
        'x^2 - x - 6',
        'x^2 + x - 6',
        'x^2 - 5x - 6'
      ],
      selected: null
    },
    // 15
    {
      question: 'If all cats are animals, and all animals have four legs, what can be concluded about cats?',
      answer: 0,
      options: [
        'All cats have four legs.',
        'All cats do not have four legs.',
        'Some cats have four legs.'
      ],
      selected: null
    },
    // 16
    {
      question: 'What is the value of the square root of 121?',
      answer: 0,
      options: [
        '11',
        '10',
        '12'
      ],
      selected: null
    },
    // 17
    {
      question: 'Which of the following is NOT a function of the liver?',
      answer: 2,
      options: [
        'Producing Bile',
        'Regulating blood sugar levels',
        'Producing insulin'
      ],
      selected: null
    },
    // 18
    {
      question: 'If A implies B, and B implies C, what can be concluded about A and C?',
      answer: 0,
      options: [
        'A implies C',
        'C implies A',
        'A and C are independent'
      ],
      selected: null
    },
    // 19
    {
      question: 'Which of the following is NOT an example of a renewable energy source?',
      answer: 2,
      options: [
        'Solar power',
        'Wind power',
        'Coal power'
      ],
      selected: null
    },
    // 20
    {
      question: 'Which of the following is a product of cellular respiration?',
      answer: 1,
      options: [
        'Oxygen',
        'Glucose',
        'Methanol'
      ],
      selected: null
    }
  ])
  
  const quizCompleted = ref(false)
  const currentQuestion = ref(0)
  const score = computed(() => {
    let value = 0
    questions.value.map(q => {
      if (q.selected != null && q.answer == q.selected) {
        console.log('correct');
        value++
      }
    })
    return value
  })
  
  const getCurrentQuestion = computed(() => {
    let question = questions.value[currentQuestion.value]
    question.index = currentQuestion.value
    return question
  })
  
  const SetAnswer = (e) => {
    questions.value[currentQuestion.value].selected = e.target.value
    e.target.value = null
  }
  
  const NextQuestion = () => {
    if (currentQuestion.value < questions.value.length - 1) {
      currentQuestion.value++
      return
    }
    
    quizCompleted.value = true
  }
  </script>
  
  <style>
  * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      font-family: 'Montserrat', sans-serif;
  }
  
  
  .app {
      display: flex;
      flex-direction: column;
      padding: 200px 0px 0px 1050px;
      height: 100vh;
  }
  
  .summary{
      background-color: #ffffff;
      padding: 3rem;
      width: 850px;
      height: 700px;
  }

  h1 {
      color: #212121;
      font-size: 35px;
      font-weight: bold;
      text-align: center;
  }

  h2{
      color: #212121;
      font-size: 100px;
      font-weight: bold;
      text-align: center;
      margin-top: 100px;
  }
  
  .quiz {
      background-color: #ffffff;
      padding: 3rem;
      width: 850px;
      height: 700px;
  }
  
  .quiz-info {
      display: flex;
      justify-content: space-between;
      margin-bottom: 3rem;
  }
  
  .quiz-info .question {
      color: #212121;
      font-size: 35px;
      font-weight: bold;
  }
  
  .quiz-info.score {
      color: #000000;
      font-size: 30px;
  }
  
  .options {
    margin-top: 4rem;
    margin-bottom: 2.5rem;
  }
  
  .option {
      padding: 1rem;
      display: block;
      background-color: #d2d2d2;
      margin-bottom: 1rem;
      border-radius: 0.5rem;
      cursor: pointer;
      font-size: 25px;
      color: #212121;
  }
  
  .option:hover {
      background-color: #f0f0f0;
  }
  
  .option.correct {
      background-color: #9fff9a;
  }
  
  .option.wrong {
      background-color: #ff5a5f;
  }
  
  .option:last-of-type {
      margin-bottom: 0;
  }
  
  .option.disabled {
      opacity: 0.7;
  }
  
  .option input {
      display: none;
  }
  
  button {
      appearance: none;
      outline: none;
      border: none;
      cursor: pointer;
      padding: 1rem 1.5rem;
      background-color: #F5D43E;
      color: #212121;
      font-weight: 700;
      text-transform: uppercase;
      font-size: 1.2rem;
      border-radius: 2rem;
  }
  
  button:disabled {
      opacity: 1.0;
  }
  
  h2 {
      font-size: 2rem;
      margin-bottom: 2rem;
      text-align: center;
  }
  
  p {
      color: #ffffff;
      font-size: 1.5rem;
      text-align: center;
  }

  .shs-page{
    background-image: url(../assets/images/shs-bg.png);
    background-position: center;
    background-repeat: no-repeat;
    background-attachment: fixed;
    background-size: cover;
  }
  </style>
  