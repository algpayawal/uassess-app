<template>
    <div class="jhs-page">
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
        question: 'What is the capital of the Philippines?',
        answer: 1,
        options: [
          'Cebu',
          'Manila',
          'Davao'
        ],
        selected: null
      },
      // 2
      {
        question: 'What is the national language of the Philippines?',
        answer: 1,
        options: [
          'English',
          'Tagalog',
          'Spanish'
        ],
        selected: null
      },
      // 3
      {
        question: 'What is the name of the largest ocean in the world?',
        answer: 2,
        options: [
          'Indian Ocean',
          'Atlantic Ocean',
          'Pacific Ocean'
        ],
        selected: null
      },
      // 4
      {
        question: 'What is the largest planet in our solar system?',
        answer: 1,
        options: [
          'Earth',
          'Jupiter',
          'Venus'
        ],
        selected: null
      },
      // 5
      {
        question: 'What is the name of the process by which plants make their own food?',
        answer: 1,
        options: [
          'Respiration',
          'Photosynthesis',
          'Digestion'
        ],
        selected: null
      },
      // 6
      {
        question: 'What is the name of the biggest continent on Earth?',
        answer: 1,
        options: [
          'Europe',
          'Asia',
          'Australia'
        ],
        selected: null
      },
      // 7
      {
        question: 'Who painted the Mona Lisa?',
        answer: 1,
        options: [
          'Vincent Van Gogh',
          'Leonardo Da Vinci',
          'Pablo Picasso'
        ],
        selected: null
      },
      // 8
      {
        question: 'Who is the current President of the United States?',
        answer: 0,
        options: [
          'Joe Biden',
          'Donald Trump',
          'Barack Obama'
        ],
        selected: null
      },
      // 9
      {
        question: 'Who invented telephone?',
        answer: 2,
        options: [
          'Thomas Edison',
          'Benjamin Franklin',
          'Alexander Graham Bell'
        ],
        selected: null
      },
      // 10
      {
        question: 'What is the name of the largest desert in the world?',
        answer: 0,
        options: [
          'Sahara Desert',
          'Gobi Desert',
          'Mojave Desert'
        ],
        selected: null
      },
      // 11
      {
        question: 'What is the name of the process by which water is turned into gas?',
        answer: 0,
        options: [
          'Evaporation',
          'Condensation',
          'Precipitation'
        ],
        selected: null
      },
      // 12
      {
        question: 'Who was the first person to walk on the moon?',
        answer: 1,
        options: [
          'Buzz Aldrin',
          'Neil Armstrong',
          'Yuri Gagarin'
        ],
        selected: null
      },
      // 13
      {
        question: 'What is the name of the device that measures earthquakes?',
        answer: 0,
        options: [
          'Seismometer',
          'Thermometer',
          'Barometer'
        ],
        selected: null
      },
      // 14
      {
        question: 'What is the name of the scientist who developed the theory of relativity?',
        answer: 1,
        options: [
          'Isaac Newton',
          'Albert Einstein',
          'Stephen Hawking'
        ],
        selected: null
      },
      // 15
      {
        question: 'Who wrote the novel "To Kill a Mockingbird"?',
        answer: 1,
        options: [
          'John Steinbeck',
          'Harper Lee',
          'William Faulkner'
        ],
        selected: null
      },
      // 16
      {
        question: 'What is the smallest country in the world?',
        answer: 0,
        options: [
          'Vatican City',
          'Monaco',
          'Leichtenstein'
        ],
        selected: null
      },
      // 17
      {
        question: 'Who is the founder of Facebook?',
        answer: 2,
        options: [
          'Jeff Bezos',
          'Bill Gates',
          'Mark Zuckerberg'
        ],
        selected: null
      },
      // 18
      {
        question: 'What is the largest organ in the human body?',
        answer: 2,
        options: [
          'Heart',
          'Brain',
          'Skin'
        ],
        selected: null
      },
      // 19
      {
        question: 'WWhat is the name of the process by which plants release water vapor?',
        answer: 1,
        options: [
          'Evaporation',
          'Transpiration',
          'Condensation'
        ],
        selected: null
      },
      // 20
      {
        question: 'What is the name of the instrument used to measure air pressure?',
        answer: 0,
        options: [
          'Barometer',
          'Thermometer',
          'Hygrometer'
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
  
   .jhs-page{
     background-image: url(../assets/images/jhs-bg.png);
     background-position: center;
     background-repeat: no-repeat;
     background-attachment: fixed;
     background-size: cover;
   }
   </style>
   