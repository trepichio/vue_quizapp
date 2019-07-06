<template>
	<div>
	  <b-jumbotron>
	    <template slot="lead">
	    	{{currentQuestion.question}}
	    </template>

	    <hr class="my-4">


		<b-list-group>
		  <b-list-group-item>
		  	Answer 1
		  </b-list-group-item>
		  <b-list-group-item>
		  	Answer 2
		  </b-list-group-item>
		  <b-list-group-item>
		  	Answer 3
		  </b-list-group-item>
		  <b-list-group-item>
		  	Answer 4
		  </b-list-group-item>
		</b-list-group>

	    <b-button variant="primary">
			Submit
		</b-button>
	    <b-button variant="success">
	    	Next
	    </b-button>
	  </b-jumbotron>
	</div>
</template>

<script>

export default {

  name: 'QuestionBox',
  props: {
  	currentQuestion: Object
  },
  
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
</style>