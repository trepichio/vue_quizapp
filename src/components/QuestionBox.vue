<template>
	<div>
	  <b-jumbotron>
	    <template slot="lead">
	    	{{currentQuestion.question}}
	    </template>

	    <hr class="my-4">


		<b-list-group>
		  <b-list-group-item
		  	v-for="(answer, index) in answers"
		  	:key="index"
		  	@click.prevent="selectAnswer(index)"
		  	:class="answerClass(index)"
		  	:disabled="answersed"
		  >
		  	{{ answer }}
		  </b-list-group-item>
		</b-list-group>

	    <b-button variant="primary"
	    	@click.prevent="submitAnswer"
	    	:disabled="answersed || selectedAnswer === null"
	    >
			Submit
		</b-button>
	    <b-button variant="success"
	    	@click.prevent="next"
	    	:disabled="lastQuestion"
	    >
	    	Next
	    </b-button>
	  </b-jumbotron>
	</div>
</template>

<script>
import shuffle from 'lodash.shuffle'

export default {

  name: 'QuestionBox',
  props: {
  	currentQuestion: Object,
  	next: Function,
  	increment: Function,
  	lastQuestion: Boolean
  },
  computed: {
    answers () {
		let answers = [...this.currentQuestion.incorrect_answers, this.currentQuestion.correct_answer];
		let shuffledAnswers = shuffle(answers);
		this.correctIndex = shuffledAnswers.indexOf(this.currentQuestion.correct_answer);
	    
	    return shuffledAnswers;
    }
  },
  data () {
    return {
      selectedAnswer: null,
      answersed: false,
      correctIndex: null
    };
  },
  methods: {
    selectAnswer (index) {
      this.selectedAnswer = index;
    },
    submitAnswer () {
    	let isCorrect = false;
    	isCorrect = this.selectedAnswer === this.correctIndex;
    	this.increment(isCorrect);
    	this.answersed = true;
    },
    answerClass (index) {

    	if (!this.answersed) {
	    	return (index === this.selectedAnswer) && 'selected';
    	}
	    else {
    		if (index === this.selectedAnswer && index !== this.correctIndex) return 'incorrect'
    		if (index === this.correctIndex) return 'correct';
	    } 
    }
  },
  watch: {
    currentQuestion: {
      immediate: true,
      handler () {
      	this.selectedAnswer = null,
      	this.answersed = false
      }
    }
  }
}
</script>

<style scoped>
	.list-group {
		margin-bottom: 15px;
	}

	.list-group-item:hover {
		background: #EEE;
		cursor: pointer;
	}

	.btn {
		margin: 0 5px;		
	}

	.selected {
		background: lightblue;
	}

	.correct {
		background: lightgreen;
	}

	.incorrect {
		background: red;
	}

	.lead {
		font-size: 1.7rem;
	}

</style>