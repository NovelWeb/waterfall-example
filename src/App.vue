<template>
  <div id="app">
    <div class="container">
      <Waterfall :list="list" :gutter="10" :width="240" :phoneCol="2" backgroundColor="rgb(73, 74, 95)" @handleClick="handleClick" ref="waterfall">
        <template slot="item" slot-scope="props">
          <div class="card">
            <div class="cover"><img :src="props.data.src" alt="" @load="$refs.waterfall.refresh()"></div>
            <div class="name">
              <p>{{props.data.name}}</p>
            </div>
          </div>
        </template>
      </Waterfall>
      <div class="menu-wrapper">
        <button class="menu" @click="addNewList">Add More</button>
      </div>
    </div>
  </div>
</template>

<script>
import Waterfall from "vue-waterfall-plugin";
export default {
  name: 'app',
  data () {
    return {
      list: [],
    }
  },
  mounted() {
    this.list = this.createList();
  },
  methods: {
    addNewList() {
      this.list.push(...this.createList())
    },
    createList() {
      let list = [];
      for (let i = 0; i < 15; i++) {
        list.push({
          src: require(`./assets/img/${i+1}.jpg`),
          name: `Image${i}`
        })
      }
      return list;
    },
    handleClick(item) {
      console.log(item)
    }
  },
  components: {
    Waterfall
  }
}
</script>

<style lang="scss">
* {
	margin: 0;
	padding: 0;
}
#app {
	font-family: "Avenir", Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;
	color: #2c3e50;
}
.container {
	background: #66677c;
}
.card {
	background: #fff;
	border-radius: 5px;
	overflow: hidden;
	cursor: pointer;
	position: relative;
	transition: 0.2s;
	top: 0;
	&:hover {
		top: -3px;
	}
	.cover {
		padding: 10px 10px 0 10px;
		line-height: 0;
		img {
			width: 100%;
		}
	}
	.name {
		background: #fff;
		color: #666;
		font-weight: 600;
		padding: 10px 20px;
		font-size: 14px;
	}
}
.menu-wrapper {
	padding: 20px;
	.menu {
		display: block;
		width: 180px;
		height: 40px;
		border-radius: 3px;
		background: #fff;
		border: none;
		outline: none;
		color: #666;
		margin: 0 auto;
		cursor: pointer;
	}
}
</style>
