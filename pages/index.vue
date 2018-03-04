<template>
  <section class="container">
    <div>
      <h1 class="title">

      </h1>
      <h2 class="subtitle">
        My test project
      </h2>

      <div :key="index" v-for="(teamMember, index) in teamMembers">
        <h3>{{ teamMember.fields.name }}</h3>
        <p>{{ teamMember.fields.bio }}</p>
        <img v-if="teamMember.fields.image" :src="teamMember.fields.image.fields.file.url + '?w=100&h=100;fit=crop'"/>
      </div>

      <form name="contact" method="POST" netlify>
        <p>
          <label>Your Name: <input type="text" name="name"></label>
        </p>
        <p>
          <label>Your Email: <input type="email" name="email"></label>
        </p>
        <p>
          <label>Message: <textarea name="message"></textarea></label>
        </p>
        <p>
          <button type="submit">Send</button>
        </p>
      </form>

    </div>
  </section>
</template>

<script>

import {createClient} from '~/plugins/contentful.js'

const client = createClient()

export default {
  // `env` is available in the context object

  data() {
    // declare message with an empty value
    return {
      teamMembers: ''
    }
  },
  asyncData ({env}) {
    return Promise.all([

      client.getEntries({
        // 'order': 'name',
        'content_type': 'teamMember',

      })
    ]).then((entries) => {

      console.log(entries);
      return {
        teamMembers: entries[0].items
      }

    }).catch(console.error)
  }
}

</script>

<style>
.container {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif; /* 1 */
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
