<template>
  <div id="app">
    <br><br>
    <h1 class="content">ฝากขาย-เช่าอสังหาริมทรัพย์ฟรี</h1>
    <h1 class="content">สนใจคลิ๊ก
      <!-- <img @click="sign()" width="60" src="https://upload.wikimedia.org/wikipedia/commons/1/13/Facebook_like_thumb.png"> -->
      <a href="" @click="sign()">ที่นี่</a>
      <!-- <button @click="signOut()"> signout </button> -->
    </h1>
    <br>
    <img :src="photoURL"> <br>
    {{ displayName }}
    <router-view></router-view>
  </div>
</template>

<script>
import firebase from 'firebase'
var config = {
  apiKey: 'AIzaSyBTNGb-m_8TKgDZxMKq4hDnhYTi1kfwxnI',
  authDomain: 'mvpplace-a6868.firebaseapp.com',
  databaseURL: 'https://mvpplace-a6868.firebaseio.com',
  projectId: 'mvpplace-a6868',
  storageBucket: 'mvpplace-a6868.appspot.com',
  messagingSenderId: '330534575914'
}
firebase.initializeApp(config)
var provider = new firebase.auth.FacebookAuthProvider()
provider.addScope('public_profile')
provider.setCustomParameters({
  'display': 'popup'
})
export default {
  name: 'app',
  data () {
    return {
      displayName: '',
      photoURL: ''
    }
  },
  methods: {
    sign () {
      console.log('yes')
      var vm = this
      firebase.auth().signInWithPopup(provider).then(function (result) {
        var token = result.credential.accessToken
        var user = result.user
        console.log(token, user)
        console.log('displayName :: ', user.displayName)
        console.log('photoURL ::', user.photoURL)
        vm.displayName = user.displayName
        vm.photoURL = user.photoURL
      }).catch(function (error) {
        console.log(error)
      })
    },
    signOut () {
      var vm = this
      firebase.auth().signOut().then(function () {
        console.log('logOut')
        vm.displayName = ''
        vm.photoURL = ''
      }, function (error) {
        console.log(error)
      })
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /*text-align: center;*/
  color: #2c3e50;
  background-image: url("http://www.justrightselfstorage.ca/uploads/images/condos%20ottawa.jpg");
  height: 100vh;
  width:  100%;
}
.content {
  margin-left: 20%;
}
</style>
