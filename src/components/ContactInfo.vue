<template>
  <div id="addContact">
    <form v-if="!submitted">
      <h1>
        If you have any suggestions or wanna get contact with me please leave a
        comment below!
      </h1>
      <label>
        <b>Name:</b>
      </label>
      <input type="text" v-model.lazy="contact.name" />
      <label>
        <b>Email address/Phone number:</b>
      </label>
      <input type="text" v-model.lazy="contact.method" />
      <label>
        <b>Message:</b>
      </label>
      <textarea v-model.lazy="contact.content"></textarea>
      <button
        v-bind:disabled="!contact.name || !contact.method || !contact.content"
        type="button"
        v-on:click.prevent="post"
      >Submit</button>
    </form>
    <div v-if="submitted">
      <h3>Thank you for your message! I'll get back to you soon!</h3>
      <div id="preview">
        <h3>Preview submission</h3>
        <p>Name: {{ contact.name }}</p>
        <p>Contact: {{ contact.method }}</p>
        <p>Message:</p>
        <p>{{ contact.content }}</p>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      contact: {
        name: "",
        method: "",
        content: ""
      },
      submitted: false
    };
  },
  methods: {
    post() {
      let self = this;
      axios
        .post("https://jsonplaceholder.typicode.com/posts", {
          title: self.contact.name,
          body: self.contact.content,
          userId: 1
        })
        .then(function(data) {
          console.log(data);
          self.submitted = true;
        });
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
#addContact * {
  box-sizing: border-box;
}

#addContact {
  margin: 20px auto;
  max-width: 500px;
}

label {
  text-align: left;
  display: block;
  margin: 20px 0 10px;
}

input {
  width: 100%;
  height: 50px;
  font-size: 30px;
}

textarea {
  display: block;
  width: 100%;
  height: 300px;
  padding: 8px;
  font-size: 30px;
}

button {
  width: 30%;
  height: 50px;
  font-size: 25px;
  border-radius: 8px;
  margin: 20px 0 10px;
}

#preview {
  background-color: rgb(240, 240, 240);
  text-align: left;
  border-radius: 8px;
  padding: 10px 20px;
  border: 1px solid #ccc;
  margin: 30px 0;
}

h3 {
  margin-top: 10px;
  text-align: center;
}
</style>
