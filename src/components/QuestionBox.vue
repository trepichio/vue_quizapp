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
		  	:class="[selectedAnswer === index && 'selected']"
		  >
		  	{{ answer }}
		  </b-list-group-item>
		</b-list-group>

	    <b-button variant="primary">
			Submit
		</b-button>
	    <b-button variant="success"
	    	@click.prevent="next"
	    >
	    	Next
	    </b-button>
	  </b-jumbotron>
	</div>
</template>

<script>

export default {

  name: 'QuestionBox',
  props: {
  	currentQuestion: Object,
  	next: Function,
  },
  computed: {
    answers () {
		let answers = [...this.currentQuestion.incorrect_answers, this.currentQuestion.correct_answer];
	    return answers;
    }
  },
  data () {
    return {
      selectedAnswer: null
    };
  },
  methods: {
    selectAnswer (index) {
      this.selectedAnswer = index;
    }
  },
  watch: {
    currentQuestion: {
      immediate: true,
      handler () {
      	this.selectedAnswer = null
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
</style>