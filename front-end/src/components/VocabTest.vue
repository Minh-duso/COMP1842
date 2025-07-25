<template>
  <div>
    <h2>Score: {{ score }} out of {{ words.length }}</h2>

   
    <div class="field">
      <label>Choose language to test:</label>
      <select v-model="selectedLang" @change="resetTest" :disabled="testStarted">
        <option value="german">🇩🇪 German</option>
        <option value="vietnamese">🇻🇳 Vietnamese</option>
        <option value="thai">🇹🇭 Thai</option>
        <option value="filipino">🇵🇭 Filipino</option>
      </select>
    </div>

    
    <div v-if="!testStarted && !testOver">
      <button class="ui blue button" @click="startTest">▶️ Start Test</button>
    </div>

    <form @submit.prevent="onSubmit" v-if="!testOver">
    
<div v-if="testStarted && !testOver" style="font-size: 18px; margin-bottom: 10px;">
  ⏱️ Time Left: <strong>{{ timeLeft }}s</strong>
</div>


      <div class="ui labeled input fluid">
  <div class="ui label">
    <i :class="[langFlagMap[selectedLang], 'flag']"></i>
    {{ langDisplayName[selectedLang] }}
      </div>
        <input type="text" readonly :disabled="testOver" :value="currWord[selectedLang]" />
        <button type="button" class="ui icon button" @click="speak(currWord[selectedLang])" :disabled="testOver || !currWord[selectedLang]">🔊</button>
      </div>

     
      <div class="ui labeled input fluid">
        <div class="ui label">
          <i class="united kingdom flag"></i> English
        </div>
        <input
          type="text"
          placeholder="Enter word in English..."
          v-model="english"
          :disabled="testOver"
          autocomplete="off"
        />
      </div>

      <button class="positive ui button" :disabled="testOver">Submit</button>
    </form>

    <p :class="['results', resultClass]">
      <span v-html="result"></span>
    </p>

    
    <button class="ui red button" @click="resetTest" v-if="testStarted">🔄 Reset Test</button>
  </div>
</template>

<script>
export default {
  name: 'vocab-test',
  props: {
    words: {
      type: Array,
      required: true
    }
  },
  data() {
    return {
      selectedLang: 'german',
      testStarted: false,
      randWords: [],
      incorrectGuesses: [],
      result: '',
      resultClass: '',
      english: '',
      score: 0,
      testOver: false,
      langDisplayName: {
        german: ' German',
        vietnamese: ' Vietnamese',
        thai: ' Thai',
        filipino: ' Filipino'
      },
      langFlagMap: {
  german: 'de',
  vietnamese: 'vn',
  thai: 'th',
  filipino: 'ph'
},
timeLeft: 30,
timer: null
    };
  },
  computed: {
    currWord() {
      return this.randWords.length ? this.randWords[0] : {};
    }
  },
  watch: {
    words: {
      immediate: true,
      handler(newWords) {
        this.randWords = [...newWords].sort(() => 0.5 - Math.random());
      }
    }
  },
  methods: {
    startTest() {
      this.testStarted = true;
      this.startTimer();
    },
    startTimer() {
    this.timeLeft = 30;
    this.timer = setInterval(() => {
      this.timeLeft--;
      if (this.timeLeft <= 0) {
        clearInterval(this.timer);
        this.testOver = true;
        this.displayResults();
      }
    }, 1000);
  },

    onSubmit() {
      if (!this.testStarted) {
    this.flash('⚠️ Please click "Start Test" to begin.', 'error', { timeout: 3000 });
    return;
  }
      if (this.english.trim().toLowerCase() === this.currWord.english.toLowerCase()) {
        this.flash('✅ Correct!', 'success', { timeout: 1000 });
        this.score += 1;
      } else {
        this.flash('❌ Wrong!', 'error', { timeout: 5000 });
        this.incorrectGuesses.push(this.currWord[this.selectedLang]);
      }

      this.english = '';
      this.randWords.shift();

      if (this.randWords.length === 0) {
        this.testOver = true;
        this.displayResults();
      }
    },
    resetTest() {
      this.randWords = [...this.words].sort(() => 0.5 - Math.random());
      this.testStarted = false;
      this.english = '';
      this.score = 0;
      this.testOver = false;
      this.result = '';
      this.resultClass = '';
      this.incorrectGuesses = [];
      clearInterval(this.timer);
      this.timer = null;
      this.timeLeft = 30;
    },
    displayResults() {
      if (this.incorrectGuesses.length === 0) {
        this.result = '🎉 You got everything correct. Well done!';
        this.resultClass = 'success';
      } else {
        const incorrect = this.incorrectGuesses.join(', ');
        this.result = `<strong>You got the following words wrong (${this.langDisplayName[this.selectedLang]}):</strong> ${incorrect}`;
        this.resultClass = 'error';
      }
    },
    flash(message, type, { timeout = 10000 } = {}) {
      this.result = message;
      this.resultClass = type;
      setTimeout(() => {
        this.result = '';
        this.resultClass = '';
      }, timeout);
    },
    speak(text) {
  if (!window.speechSynthesis) {
    alert('Speech Synthesis not supported in this browser.');
    return;
   } 

  const utterance = new SpeechSynthesisUtterance(text);
  utterance.lang = this.getVoiceLang(); 
  window.speechSynthesis.speak(utterance);
},
  getVoiceLang() {
  
  const langMap = {
    german: 'de-DE',
    vietnamese: 'vi-VN',
    thai: 'th-TH',
    filipino: 'fil-PH'
  };
  return langMap[this.selectedLang] || 'en-US';
    }
  }
};
</script>

<style scoped>
.results {
  margin: 25px auto;
  padding: 15px;
  border-radius: 5px;
}

.error {
  border: 1px solid #ebccd1;
  color: #a94442;
  background-color: #f2dede;
}

.success {
  border: 1px solid #d6e9c6;
  color: #3c763d;
  background-color: #dff0d8;
}

select {
  margin: 10px 0;
  padding: 5px;
  font-size: 16px;
}

.ui.icon.button {
  padding: 5px 10px;
  margin-left: 10px;
}

</style>
