<template>
  <div class="contact">
    <ContactInfo />
  </div>
</template>

<script>
// @ is an alias to /src
import ContactInfo from "@/components/ContactInfo.vue";

export default {
  name: "Contact",
  components: {
    ContactInfo
  }
};
</script>