<template>
  <div>
		Conversation ID: {{ id }}
		<hr>
		<Message 
			v-for="message in conversation.messages" 
			:message="message" 
			:key="message.created" 
		/>
		<br />
		<input v-model="newMessageText" @keyup.enter="send" placeholder="Type something..." />
  </div>
</template>

<script>
	import Message from './Message.vue'
	import { mapState } from 'vuex'

  export default {
    name: 'ConversationContainer',

		data () {
			return {
				newMessageText: ''
			}
		},

		props: {
			conversation: {
				type: Object,
				required: true
			},
			id: {
				type: String,
				required: true
			}
		},

		methods: {
			send () {
				this.$store.dispatch('conversations/sendMessage', { 
					text: this.newMessageText, 
					created: Date.now(),
					conversationId: this.id,
					sender: this.$store.state.users.currentUser
				})	
			}
		},

		components: {
			Message,
		}
  }
</script>

<style scoped>
</style>
