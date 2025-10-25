<template>
  <b-container class="page animate__animated animate__fadeIn">
    <b-row class="justify-content-center">
      <b-col cols="md-6">
        <h2>Get in touch 💌</h2>

        <p class="text-left">
          If you have any question or just want to say hi, I'll try my best to
          get back to you.
        </p>

        <b-alert show variant="success" v-if="showAlert">
          <strong>All done 🎉</strong><br />
          Thanks for reaching out {{ formData.name }}, I'll reply as soon as I can.
        </b-alert>

        <b-form class="mb-5" @submit.prevent="sendEmail">
          <b-form-group label="Your Name:">
            <b-form-input
              placeholder="John Doe"
              v-model="formData.name"
              required
            ></b-form-input>
          </b-form-group>

          <b-form-group label="Your Email:">
            <b-form-input
              v-model="formData.email"
              type="email"
              placeholder="john@doe.com"
              required
            ></b-form-input>
          </b-form-group>

          <b-form-group label="Your Message:">
            <b-form-textarea
              v-model="formData.message"
              no-resize
              rows="3"
              placeholder="Hey Murad, are you available for..."
              required
            ></b-form-textarea>
          </b-form-group>

          <b-button type="submit" variant="primary" :disabled="loading">
            {{ loading ? "Sending..." : "Submit" }}
          </b-button>
        </b-form>
      </b-col>
    </b-row>
  </b-container>
</template>

<script>
import emailjs from "emailjs-com";

export default {
  data() {
    return {
      loading: false,
      showAlert: false,
      formData: {
        name: "",
        email: "",
        message: ""
      }
    };
  },
  methods: {
    async sendEmail() {
      this.loading = true;

      // 🔧 Replace these values with your real EmailJS credentials
      const serviceID = "service_e44e1yo"; // Example: service_1a2b3c
      const templateID = "template_qvosflb"; // Example: template_contact
      const publicKey = "eY7nmMGT2HwJ9U2y5"; // Example: wLx0sAbCDeFGHIJ

      const templateParams = {
        from_name: this.formData.name,
        from_email: this.formData.email,
        message: this.formData.message,
        to_name: "Murad Mursela",
        contact_number: "+251947485789"
      };

      try {
        await emailjs.send(serviceID, templateID, templateParams, publicKey);
        this.showAlert = true;
        this.formData = { name: "", email: "", message: "" };
      } catch (error) {
        alert("❌ Sending failed, please try again later.");
        console.error("EmailJS Error:", error);
      } finally {
        this.loading = false;
      }
    }
  },
  head: {
    title: "Contact 📧 - Murad Mursela",
    meta: [
      {
        hid: "description",
        name: "description",
        content: "Do you have any enquiries? Send a message now to Murad Mursela"
      },
      {
        hid: "og:title",
        name: "og:title",
        content: "Contact 📧 - Murad Mursela"
      },
      {
        property: "og:description",
        content: "Do you have any enquiries? Send a message now to Murad Mursela"
      },
      {
        hid: "og:image",
        name: "og:image",
        content: require("@/assets/contact.jpg")
      }
    ]
  }
};
</script>

<style scoped>
.container {
  margin-top: 120px;
}
form {
  margin-top: 40px;
  text-align: left;
}
</style>
