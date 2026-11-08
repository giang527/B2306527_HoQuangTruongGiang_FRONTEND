<template>
  <div v-if="contact" class="page">
    <h4>Thêm Liên hệ</h4>
    <ContactForm :key="formKey" :contact="contact" 
    @submit:contact="addContact" />
    <p>{{ message }}</p>
  </div>
</template>

<script>
import ContactForm from "@/components/ContactForm.vue";
import contactService from "@/services/contact.service";

export default {
  components: {
    ContactForm,
  },

  data() {
    return {
      contact: {
        name: "",
        email: "",
        address: "",
        phone: "",
        favorite: false,
      },
      message: "",
      formKey: 0,
    };
  },
  methods: {
    async addContact(data) {
      try {
        await contactService.create(data);
        this.message = "Liên hệ được thêm thành công.";
        this.contact = {
          name: "",
          email: "",
          address: "",
          phone: "",
          favorite: false,
        };
        this.formKey += 1;
      } catch (error) {
        console.log(error);
      }
    },
  },
  created() {
    this.message = "";
  },
};
</script>
