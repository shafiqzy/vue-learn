<script>
export default{
  name:'app',
    data(){
        return{
            showBooks: true,
            books: [
            {title: 'The Final Empire', author: 'Brandon Sanderson', year: '2020', isFav:true},
            {title: 'Joker', author: 'Anderson', year: '2020', isFav:false},
            {title: 'The Spartan', author: 'Dabvid', year: '2020', isFav:true}
            ],
            age: '45',
            x: 0,
            y: 0
        }
    },
    methods:{
        toggleShowBooks(){
            this.showBooks = !this.showBooks
        },
        handleEvent(e,data){//e can change another name
          console.log(e.type)
          if (data) {
            console.log(data)
          }
        },
        handleMouseMove (e){
          this.x = e.offsetX 
          this.y = e.offsetY
        },
        toggleFav(book){
          book.isFav = !book.isFav
        }
    }
}
</script>
 <style scoped>
  .box{
    padding: 100px 0;
    width: 400px;
    color: black;
    text-align: center;
    background: #ddd;
    margin: 20px;
    display: inline-block;  
  }
  body{
    background: #eee;
    max-width: 960px;
    margin: 20px auto;
  }
  p, h3, ul{
    margin: 0;
    padding: 0;
  }
  li{
    list-style-type: none;
    background: #fff;
    color: #000;
    margin: 20px auto;
    padding: 10px 20px;
    border-radius: 10px;
    display: flex;
    align-items: center;
    justify-content: space-between;
  }
  li.fav{
    background-color: violet;
  }
</style>
<template>
  <div id="app">

    <div v-if="showBooks">
      <ul>
        <li v-for="book in books" v-bind:class="{ fav: book.isFav }" @click="toggleFav(book)">
          <h3>{{ book.title }}</h3>
          <p>{{ book.year }}</p>
          <p>{{ book.author }}</p>
        </li>
      </ul>
      <br>
    </div>

    <button @click="toggleShowBooks">
      <span v-if="showBooks">Hide Books</span>
      <span v-else>Show Books</span>
    </button>
    <div v-show="showBooks">Currently showing book</div>

    <br>
    <!--Mouse Event-->
    <div class="box" @mouseover="handleEvent($event,5)">mouseover (enter)</div>
    <div class="box" @mouseleave="handleEvent">mouseleave</div>
    <div class="box" @dblclick="handleEvent">double click</div>
    <div class="box" @mousemove="handleMouseMove">position {{ x }} - {{ y }}</div>
  </div>
</template>