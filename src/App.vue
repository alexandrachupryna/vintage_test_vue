<template>
  <div id="app">
    <Contacts/>
    <Offices/>
    <Form/>
  </div>
</template>

<script>
import Contacts from './components/Contacts.vue'
import Offices from './components/Offices.vue'
import Form from './components/Form.vue'
import '../src/style.css'

export default {
  name: 'app',
  components: {
    Contacts,
    Offices,
    Form
  }
}
</script>
