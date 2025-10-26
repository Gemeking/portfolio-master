<template>
  <b-container class="page animate__animated animate__fadeIn">
    <b-row class="justify-content-center">
      <b-col cols="md-6">
        <h2>Get in touch</h2>

        <p class="text-left">
          If you have any questions or just want to say hi, I'll try my best to
          get back to you.
        </p>

        <!-- ✅ Success alert -->
        <b-alert show variant="success" v-if="showAlert">
          <strong>All done</strong><br />
          Thanks for reaching out {{ lastSentName }}, I'll reply as soon as I can.
        </b-alert>

        <!-- ✅ Contact Form -->
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
      lastSentName: "",
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

      // ✅ Replace these with your actual EmailJS credentials
      const serviceID = "service_e44e1yo"; // Your EmailJS service ID
      const templateID = "template_qvosflb"; // Your EmailJS template ID
      const publicKey = "eY7nmMGT2HwJ9U2y5"; // Your EmailJS public key

      const currentTime = new Date().toLocaleString();

      // ✅ Format message to include name, email, and time
      const formattedMessage = `
Name: ${this.formData.name}
Email: ${this.formData.email}
Time: ${currentTime}

Message:
${this.formData.message}
      `;

      const templateParams = {
        from_name: this.formData.name || "Anonymous",
        from_email: this.formData.email,
        message: formattedMessage,
        time: currentTime,
        to_name: "Murad Mursela"
      };

      try {
        await emailjs.send(serviceID, templateID, templateParams, publicKey);
        this.lastSentName = this.formData.name;
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
    title: "Contact - Murad Mursela",
    meta: [
      {
        hid: "description",
        name: "description",
        content:
          "Do you have any enquiries? Send a message now to Murad Mursela."
      },
      {
        hid: "og:title",
        name: "og:title",
        content: "Contact - Murad Mursela"
      },
      {
        property: "og:description",
        content:
          "Do you have any enquiries? Send a message now to Murad Mursela."
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
