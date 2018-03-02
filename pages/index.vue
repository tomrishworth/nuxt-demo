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
      </div>

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
      // fetch the owner of the blog
      // client.getEntries({
      //   'sys.id': env.CTF_PERSON_ID
      // }),
      // client.fetchEntriesForContentType()
      // fetch all blog posts sorted by creation date
      client.getEntries({
        'content_type': 'teamMember',

      })
    ]).then((entries) => {
      // return data that should be available
      // in the template
      console.log(entries);
      return {
        teamMembers: entries[0].items
      }
      // this.teamMembers = entries[0].items[0]
      // return this.teamMembers = 'TEst'
      // return {
      // }
      // return {
      //   // teamMember: entries.items
      //   teamMember: "Hello"
      // }
      // entries.forEach((entry) => {
      //   // console.log(entry.items[0].fields.name);
      //   console.log(entry);

      // })
      // // return {
      //   person: entry.fields[contentType.displayField],
      // }
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
