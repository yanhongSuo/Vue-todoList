<template>
  <div id="app">
  	<!--<img src="./assets/logo.png">-->
    <!--<router-view/>-->
  	<h1 v-text="title"></h1>
	  <input v-model="newItem" v-on:keyup.enter="addNew()" />
  	<ul>
	    	<li v-for="item in items">
	    		<div class="liDiv">
	    			<input type="checkbox" v-model="item.isFinished" />
	    			<label v-bind:class="{finished:item.isFinished}">{{item.label}}</label>
	    			<button v-on:click="removeTodo(item)" class="btn">×</button>
	    		</div>
	    	</li>
	   </ul>
  </div>
</template>

<script>
import Store from './store'

export default {
	name: 'App',
	data: function(){
    return {
      title: 'This is a todo list',
  	  newItem: '',
  	  items: Store.fatch()
    }
  },
 	components: {
 		
 	},
  methods: {
  	addNew: function(){
  		this.items.push({label:this.newItem, isFinished: false});
  		this.newItem = '';
  	},
  	toggleFinish: function(item){
  		item.isFinished = !item.isFinished
  	},
  	removeTodo: function(item){
  		console.log(item)
  		this.items.splice(this.items.indexOf(item),1)
  	}
  },
  watch: {
		items: {
			handler: function(val, oldVal){
//				console.log(val, oldVal)
				Store.save(this.items)
			},
			deep: true
		}
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.finished{
	text-decoration: underline;
}
ul, li{
	list-style: none;
}
</style>
