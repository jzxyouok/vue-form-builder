<template>
  <div id="app">
    <h2>Form:</h2>
    <vue-form 
      :schema="myFormSchema"
      :options="myFormOptions"
      :model.sync="myModel"
      @submit="onFormSubmitted"
      :validation="myValidation"
      id="myCoolForm" />
      <h2>Model:</h2>
      <pre>
{{ myModel }}
      </pre>
      <h2>Schema:</h2>
      <pre>
{{ myFormSchema }}
      </pre>

    </div>
</template>

<script>
import { FormRegistry } from '../../../src/';
import SwitchField from './custom/SwitchField';

FormRegistry.registerCustomComponent('bootstrap', 'switch', SwitchField);

export default {
  methods: {
    onFormSubmitted () {
      alert ("Form is submitted: " + JSON.stringify(this.myModel))
    }
  },
  data () {
    return {
      myFormOptions: {
        name: "My Form",
        template: 'bootstrap'
      },
      myModel: {
        name: "",
        address: "",
        subscribed: false
      },
      myValidation: {
        constraints: {
          name: {
            presence: true,
            length: {minimum: 3}
          },
          address: {
            presence: true,
            length: {maximum: 5}
          },
          subscribed: {}
        }
      },
      myFormSchema: [
        {key: 'name', label: "Name", type: "text"},
        {key: 'address', label: "Address", type: "textarea"},
        {key: 'subscribed', label: "Subscribed", type: "switch"},
      ]
    }
  }
}
</script>

<style>
body {
  font-family: Helvetica, sans-serif;
}
</style>
