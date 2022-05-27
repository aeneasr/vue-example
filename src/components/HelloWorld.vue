<template>
  <div class="hello">
    <h1>{{ msg }}</h1>

    <div v-if="!session">
      <p>Click on "login" or "Sign Up" below to sign in.</p>
      <li><a :href="basePath + '/ui/login'">Login</a></li>
      <li><a :href="basePath + '/ui/registration'">Sign Up</a></li>
    </div>

    <div v-if="session">
      <p>You successfully authenticated!</p>
      <pre><code>{{ session.identity }}</code></pre>
    </div>

    <h3>Common Actions</h3>
    <ul v-if="session">
      <li><a :href="logoutUrl">Logout</a></li>
      <li><a :href="basePath + '/ui/settings'">Settings</a></li>
    </ul>

    <h3>Essential Links</h3>
    <ul>
      <li><a href="https://www.ory.sh">Ory Website</a></li>
      <li><a href="https://github.com/ory">Ory GitHub</a></li>
      <li><a href="https://www.ory.sh/docs">Documentation</a></li>
    </ul>
  </div>
</template>

<script>
import {V0alpha2Api, Configuration} from '@ory/client'

const basePath =  'http://localhost:4000'
const ory = new V0alpha2Api(new Configuration({
  basePath,
  baseOptions: {
    withCredentials: true
  }
}))

export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return {
      session: null,
      logoutUrl: null,
      basePath
    }
  },
  mounted() {
    ory.toSession().then(({data})=>{
      this.session = data

      ory.createSelfServiceLogoutFlowUrlForBrowsers().then(({data})=>{
        this.logoutUrl = data.logout_url
      })
    })
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
pre {
  text-align: left;
  max-width: 400px;
  margin: 0 auto;
}
</style>
