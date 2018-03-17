<template>
	<div class="hello">
		
	    
	</div>
</template>

<script>

	
export default {
  data: function(){
    return {
      msg: 'Welcome to Your Vue.js App',
      title: 'This is a todo list',
  	  newItem: '',
  	  items: Store.fatch()
    }
  },
  props: [this.items],
  methods: {
  	addNew: function(){
  		this.items.push({label:this.newItem, isFinished: false});
  		this.newItem = '';
  	},
  	onClickMe: function(){
  		console.log(this.msgfromfather)
  	}
  }
}
</script>

<style scoped>
</style>