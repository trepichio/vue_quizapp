<template>
	<div>
		<h1>Questions here?</h1>
		<hr>
		<p>Answers List here</p>
		<ul>
			<li>Answer 1</li>
			<li>Answer 2</li>
			<li>Answer 3</li>
			<li>Answer 4</li>
		</ul>
	</div>
</template>

<script>

export default {

  name: 'QuestionBox'
  
}
</script>

<style scoped>
	ul {
		width: 50%;
		margin: 0 auto;
		list-style-type: none;
	}

	li {
		padding: 5px;
	}
</style>