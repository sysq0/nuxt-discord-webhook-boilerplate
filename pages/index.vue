<template>
  <div>
    <form action="">
      <input v-model="messageTitle" type="text" name="title" placeholder="Titre du message">
      <textarea v-model="messageContent" name="content" placeholder="Contenu du message" />
      <input v-model="emailAddress" type="email" name="title" placeholder="Email de contact">
      <input v-model="names" type="text" name="title" placeholder="Nom & Prénom">

      <button type="button" @click="sendWebhookMessage()">
        Envoyer vers Discord
      </button>
    </form>
  </div>
</template>

<script>
export default {
  name: 'IndexPage',

  data () {
    return {
      messageTitle: '',
      messageContent: '',
      emailAddress: '',
      names: ''
    }
  },

  methods: {
    async sendWebhookMessage () {
      const params = {
        username: 'sysc0-b0T',
        avatar_url: 'https://static.wikia.nocookie.net/napoleondynamite/images/a/a2/Napoleon_dynamite.jpg/revision/latest?cb=20091207010338',
        content: 'Un nouveau message a été envoyé depuis le site 🌐 **temanamuller.com**',
        embeds: [
          {
            title: '📩 Message reçu',
            description: 'Voici les détails du message. ✒ [Répondre](mailto://' + this.emailAddress + '?subject=Concernant votre demande : "' + this.truncate(this.messageTitle, 20) + '"&body=Bonjour ' + this.names + ', \n)',
            color: 5814783,
            fields: [
              {
                name: 'Sujet',
                value: ''
              },
              {
                name: 'Contenu',
                value: this.messageContent
              },
              {
                name: 'Nom & Prénom',
                value: 'Pedro Dos Santos McAllister'
              },
              {
                name: 'Adresse e-mail de contact',
                value: 'pedro@santa-maria.mex'
              }
            ]
          }
        ]
      }

      this.$axios.setHeader('Content-Type', 'application/json')
      await this.$axios.$post('WEBHOOK_URL', params)

      this.messageTitle = null
      this.messageContent = null
    },

    truncate (string, limit) {
      return (string.length > limit) ? string.substr(0, limit - 1) + '&hellip;' : string
    }
  }
}
</script>
