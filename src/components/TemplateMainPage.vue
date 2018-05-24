<template>
  <div>
    <div class="header">
      <h2>Bacaan Baik</h2>
      <h6>Get your book reference here</h6>
    </div>

    <div class="row">
      <div class="leftcolumn">
        <div v-for="( image,index ) in listImage" :key="index" :image="image" class="card">
          <h2>{{image.title}}</h2>
          <h5>Author: {{image.author}}</h5>
          <img :src="image.url" width="400" height="350">
          <p>{{image.description}}</p>
        </div>
        <div>
          <h2>Ulasan</h2>
          <textarea name="" id="" cols="120" rows="5"></textarea>
          <br>
          <button>Submit</button>
        </div>
      </div>
      <div class="rightcolumn">
        <div class="card">
          <h2>About Me</h2>
          <div class="fakeimg" style="height:100px;">Image</div>
          <p>Some text about me in culpa qui officia deserunt mollit anim..</p>
        </div>
        <div class="card">
          <h3>Other Books</h3>
          <div class="modal fade">Image</div><br>
          <div class="modal fade">Image</div><br>
          <div class="modal fade">Image</div>
        </div>
        <div class="card">
          <h3>Friends List</h3>
          <p>Some text..</p>
        </div>
      </div>
    </div>
    <div class="footer">
      <h2>“A reader lives a thousand lives before he dies, said Jojen. The man who never reads lives only one.” ― George R.R. Martin, A Dance with Dragons</h2>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'TemplateMainPage',
  data () {
    return {
      listImage: []
    }
  },
  methods: {
    showImage: function () {
      let self = this
      axios.get('http://localhost:3000/images', {
        headers: {
          token: localStorage.getItem('token')
        }
      })
      .then(response => {
        // console.log('ini response',response)
        // console.log('ini response.data',response.data)
        // console.log('ini response.data.result',response.data.result)
        // console.log('ini response.data.result array',response.data.result[0])
        self.listImage = response.data.result
      })
      .catch(err => {
        console.log(err)
      })
    }
  },
  mounted () {
    if (localStorage.getItem('token')) {
      this.showImage()
    }
  }
}
</script>

<style>
* {
    box-sizing: border-box;
}

/* Add a gray background color with some padding */
body {
    font-family: Arial;
    padding: 20px;
    background: #f1f1f1;
}

/* Header/Blog Title */
.header {
    padding: 30px;
    font-size: 40px;
    text-align: center;
    background: white;
}

/* Create two unequal columns that floats next to each other */
/* Left column */
.leftcolumn {   
    float: left;
    width: 75%;
}

/* Right column */
.rightcolumn {
    float: left;
    width: 25%;
    padding-left: 20px;
}

/* Fake image */
.fakeimg {
    background-color: #aaa;
    width: 100%;
    padding: 20px;
}

/* Add a card effect for articles */
.card {
     background-color: white;
     padding: 20px;
     margin-top: 20px;
}

/* Clear floats after the columns */
.row:after {
    content: "";
    display: table;
    clear: both;
}

/* Footer */
.footer {
    padding: 20px;
    text-align: center;
    background: #ddd;
    margin-top: 20px;
}

/* Responsive layout - when the screen is less than 800px wide, make the two columns stack on top of each other instead of next to each other */
@media screen and (max-width: 800px) {
    .leftcolumn, .rightcolumn {   
        width: 100%;
        padding: 0;
    }
}
</style>
