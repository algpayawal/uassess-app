<template>
    <div class="college-page">
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
        question: 'What is the formula for calculating acceleration?',
        answer: 0,
        options: [
          'a = v/t',
          'a = t/v',
          'a = v^2/t'
        ],
        selected: null
      },
      // 2
      {
        question: 'What is the difference between a compound and a mixture?',
        answer: 0,
        options: [
          'A compound is a pure substance, while a mixture is a combination of two or more substances.',
          'A compound is a combination of two or more substances, while a mixture is a pure substance.',
          'A compound is a metal, while a mixture is a non-metal.'
        ],
        selected: null
      },
      // 3
      {
        question: 'If a car travels a distance of 120 km in 2 hours, what is its speed?',
        answer: 1,
        options: [
          '40 km/h',
          '60 km/h',
          '80 km/h'
        ],
        selected: null
      },
      // 4
      {
        question: 'Who is the author of "Meditations"?',
        answer: 2,
        options: [
          'Aristotle',
          'Plato',
          'Marcus Aurelius'
        ],
        selected: null
      },
      // 5
      {
        question: 'What is the formula for calculating force?',
        answer: 0,
        options: [
          'F = ma',
          'F = am',
          'F = mv'
        ],
        selected: null
      },
      // 6
      {
        question: 'What is the difference between an acid and a base?',
        answer: 0,
        options: [
          'An acid is a proton donor, while a base is a proton acceptor.',
          'An acid is a proton acceptor, while a base is a proton donor.',
          'An acid and a base are the same thing.'
        ],
        selected: null
      },
      // 7
      {
        question: 'What is the basic unit of life?',
        answer: 0,
        options: [
          'Cell',
          'Organism',
          'Atom'
        ],
        selected: null
      },
      // 8
      {
        question: 'If a company has a profit margin of 20% and a revenue of $500,000, what is its profit?',
        answer: 1,
        options: [
          '$50,000',
          '$100,000',
          '$125,000'
        ],
        selected: null
      },
      // 9
      {
        question: 'What is the main idea of utilitarianism?',
        answer: 1,
        options: [
          'Actions should be judged based on their conformity with duty.',
          'Actions should be judged based on their consequences.',
          'Actions should be judged based on their intrinsic value.'
        ],
        selected: null
      },
      // 10
      {
        question: 'What is the unit of power?',
        answer: 0,
        options: [
          'Joules',
          'Watts',
          'Volts'
        ],
        selected: null
      },
      // 11
      {
        question: 'What is the number of Avogadro?',
        answer: 2,
        options: [
          '3.14',
          '9.81',
          '6.02 x 10^23'
        ],
        selected: null
      },
      // 12
      {
        question: 'What is the limit of (x^2 - 4x + 3)/(x - 3) as x approaches 3?',
        answer: 1,
        options: [
          '0',
          '1',
          '2'
        ],
        selected: null
      },
      // 13
      {
        question: 'If it takes 6 workers 8 days to complete a project, how many days will it take 4 workers to complete the same project?',
        answer: 2,
        options: [
          '6 days',
          '9 days',
          '12 days'
        ],
        selected: null
      },
      // 14
      {
        question: 'What is the name of the protein that carries oxygen in the blood?',
        answer: 0,
        options: [
          'Hemoglobin',
          'Insulin',
          'Glucagon'
        ],
        selected: null
      },
      // 15
      {
        question: 'What is the name of the molecule that stores genetic information in all living organisms?',
        answer: 0,
        options: [
          'DNA',
          'RNA',
          'Proteins'
        ],
        selected: null
      },
      // 16
      {
        question: 'If a train travels a distance of 300 km in 5 hours, what is its speed?',
        answer: 1,
        options: [
          '30 km/h',
          '60 km/h',
          '100 km/h'
        ],
        selected: null
      },
      // 17
      {
        question: 'Which sentence is grammatically correct?',
        answer: 2,
        options: [
          'Their going to the store.',
          'There going to the store.',
          'They are going to the store.'
        ],
        selected: null
      },
      // 18
      {
        question: 'What is the correct order of adjectives in a sentence?',
        answer: 0,
        options: [
          'Opinion, size, age, shape, color, origin, material, purpose',
          'Color, size, shape, opinion, age, origin, material, purpose',
          'Age, size, shape, opinion, color, origin, material, purpose'
        ],
        selected: null
      },
      // 19
      {
        question: 'What is a dependent clause?',
        answer: 1,
        options: [
          'A clause that can stand alone as a sentence',
          'A clause that cannot stand alone as a sentence',
          'A clause that is used to modify a noun or pronoun'
        ],
        selected: null
      },
      // 20
      {
        question: 'Which word is a preposition?',
        answer: 1,
        options: [
          'Beautiful',
          'Under',
          'Run'
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
  
    .college-page{
      background-image: url(../assets/images/college-bg.png);
      background-position: center;
      background-repeat: no-repeat;
      background-attachment: fixed;
      background-size: cover;
    }
    </style>
    