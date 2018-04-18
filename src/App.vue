<script src="https://www.gstatic.com/firebasejs/4.12.1/firebase.js">/* eslint-disable */</script>
/* eslint-disable */
//App.vue
<template>
<div id="app" class="jumbotron">
			<div class="container">
					<h1>Hello! Nice to meet you!</h1>
					<hr />
					<form class="form-group" @submit="addMessage">
							<div>
									<input v-model="newMessage.title" class="form-control"maxlength="40" autofocus placeholder="Please introduce yourself :)" />
							</div>
							<div class="mt-2">
									<textarea v-model="newMessage.text" class="form-control"placeholder="Leave your message!"		rows="3">
									</textarea>
							</div>
							<button class="btn btn-primary mt-2"type="submit">Send</button>
					</form>
					<hr />
          <div class="container">


            <div class="row">
              <div v-for="message in messages" class="card-group m-2" style="width: 2000px;">
                <div class="card col-12">
                  <div class="card-block">
                    <h5 class="card-title">{{ message.title }}</h5>
                    <p class="card-text">{{ message.text }}</p>
                    <p class="card-text"><small class="text-muted">Added on {{ dateToString(message.timestamp) }}</small></p>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
			</div>
</div>
</template>


<script>
// Initialize Firebase
/* eslint-disable */
import { dateToString } from './utils/utils'
import Firebase from 'firebase'

let config = {
  apiKey: "AIzaSyC_jXSHxRIc4Fvr0ISfpYoy59PPkN06Tdw",
    authDomain: "test-84deb.firebaseapp.com",
    databaseURL: "https://test-84deb.firebaseio.com",
    projectId: "test-84deb",
    storageBucket: "test-84deb.appspot.com",
    messagingSenderId: "135466648946"
}
let app =Firebase.initializeApp(config);
let db = app.database()
let messagesRef = db.ref('messages')
export default {

  data () {
					return {
							newMessage: {
									title: '',
									text: '',
									timestamp: null
							}
					}
			},
      name: 'app',
      firebase: {
          messages: messagesRef
      },
      methods: {
        dateToString,
        addMessage (e) {
            e.preventDefault()
            if (this.newMessage.title === '') {
			return
      }
      this.newMessage.timestamp = Date.now()
      messagesRef.push(this.newMessage)
      this.newMessage.text = ''
      this.newMessage.title = ''
      this.newMessage.timestamp = null
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
</style>
