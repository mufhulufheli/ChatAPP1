<script>
	import {FirebaseApp, User} from 'sveltefire'
	import firebase from 'firebase/app'
	import 'firebase/firestore'
	import 'firebase/auth'
	import AuthForm from './components/AuthForm.svelte'
	import Chats from './components/Chats.svelte'
	const firebaseConfig = {
    apiKey: "AIzaSyDge9X9V99z41ExFKrJTqbW9bxcgvl8qvw",
    authDomain: "sbilo-chatapp.firebaseapp.com",
    databaseURL: "https://sbilo-chatapp.firebaseio.com",
    projectId: "sbilo-chatapp",
    storageBucket: "sbilo-chatapp.appspot.com",
    messagingSenderId: "432865139944",
    appId: "1:432865139944:web:259582dfea36f72b7cfd5d"
  };
 
  firebase.initializeApp(firebaseConfig);
</script>
<style>
	.app{
		min-height: 100vh;
		display: flex;
		flex-direction: column;
		max-height: 100vh;
	}
</style>
<main class="container section">
<FirebaseApp {firebase}>
	<User let:user let:auth>
		<Chats {user} />
		<button class="button is-fullwidth" on:click={() => auth.signOut()}>Sign out</button>
		<div slot="signed-out">
			<AuthForm {auth}/>

		</div>
	</User>

</FirebaseApp>	
</main>

