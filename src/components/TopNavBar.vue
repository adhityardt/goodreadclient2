<template>
  <div id="home">
    <nav class="navbar navbar-default navbar-fixed-top" style="background-color:white">
      <div class="container">
        <div class="navbar-header">
          <button type="button" class="navbar-toggle collapsed" data-toggle="collapse" data-target="#bs-example-navbar-collapse-1"
            aria-expanded="false">
            <span class="sr-only">Toggle navigation</span>
            <span class="icon-bar"></span>
            <span class="icon-bar"></span>
            <span class="icon-bar"></span>
          </button>
          <a class="navbar-brand" href="#">Bacaan Baik</a>
        </div>

        <div class="collapse navbar-collapse" id="bs-example-navbar-collapse-1">
          <form class="navbar-form navbar-left">
            <div class="form-group">
              <input type="text" class="form-control" placeholder="Search">
            </div>
            <button type="submit" class="btn btn-default glyphicon glyphicon-search"></button>
          </form>
          <ul class="nav navbar-nav navbar-right">
            <li>
              <a data-toggle="modal" data-target="#myModal" style="cursor:pointer">
                <span class="glyphicon glyphicon-send"></span> POST</a>
            </li>
            <li>
              <a style="cursor:pointer" @click="doLogout">
                <span class="glyphicon glyphicon-log-out"></span> LOGOUT</a>
            </li>
          </ul>
        </div>
      </div>
    </nav>

    <div id="myModal" class="modal fade" role="dialog">
      <div class="modal-dialog modal-lg">

        <div class="modal-content">
          <div class="modal-header">
            <button type="button" class="close" data-dismiss="modal">&times;</button>
            <h4 class="modal-title">POST BOOK</h4>
          </div>
          <div class="modal-body">
            <div class="form-group">
              <label>Image File:</label>
              <input type="file" class="form-control" @change="postImageHandler">
            </div>
            <div class="form-group">
              <label>Title:</label>
              <input type="text" class="form-control" v-model="title">
            </div>
            <div class="form-group">
              <label>Author:</label>
              <input type="text" class="form-control" v-model="author">
            </div>
            <div class="form-group">
              <label>Description:</label>
              <textarea class="form-control" rows="4" cols="50" v-model="description"></textarea>
            </div>
            <button type="submit" class="btn btn-warning" @click="postImage" data-dismiss="modal">POST</button>
          </div>
          <div class="modal-footer">
            <button type="button" class="btn btn-default" data-dismiss="modal">Close</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name:'TopNavBar',
  data () {
    return {
      title: '',
      author: '',
      description: '',
      image: '',
      listImage: [],
      user: {
        id: localStorage.getItem('id'),
        name: localStorage.getItem('user'),
        email: localStorage.getItem('email')
      }
    }
  },
  methods: {
    doLogout () {
      localStorage.removeItem('token')
      localStorage.removeItem('id')
      localStorage.removeItem('user')
      localStorage.removeItem('email')
      this.$router.push({name: 'home'})
    },
    postImage: function () {
      let formData = new FormData()
      
      formData.append('title', this.title)
      formData.append('author', this.author)
      formData.append('description', this.description)
      formData.append('image', this.image)
      formData.append('userId', this.user.id)
      console.log(formData)


      axios.post('http://localhost:3000/images', formData, {
        'Content-Type': 'multipart/form-data',
        token: localStorage.getItem('token')
      })
      .then(response => {
        console.log(response.data)
        window.location.reload(true)
      })
      .catch(err => {
        console.log(err)
      })
    },
    postImageHandler: function (event) {
      this.image = event.target.files[0]
      console.log(this.image)
    }
  }
}
</script>

<style>
.home {
      background-color: #fafafa;
    }

    @media (min-width: 1200px) {
      .container {
        width: 970px;
      }
    }

    .dropdown-menu {
      position: none !important;
    }

</style>
