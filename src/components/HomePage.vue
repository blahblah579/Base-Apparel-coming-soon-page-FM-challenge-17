<template>
  <v-container v-if="isScreenLarge" fluid class="body pa-0">
    <v-row class="main-row ma-0">
      <v-col cols="7" class="left">
        <v-container class="mx-10">
          <v-row class="d-flex flex-column mx-10 my-4">
            <v-col cols="12">
              <img src="/src/assets/logo.svg" alt="" />
            </v-col>
            <v-col cols="10" class="">
              <div class="heading mt-10">
                <span class="weare">WE'RE</span> COMING SOON
              </div>
              <div class="para pr-8 my-5">
                Hello fellow shoppers! We're currently building our new fashion
                store. Add your email below to stay up-to-date with
                announcements and our launch deals.
              </div>
            </v-col>
            <v-col cols="12" sm="10" md="9" class="px-3">
              <div
                :class="
                  errorMessage ? 'email-container-error' : 'email-container'
                "
              >
                <input
                  v-model="email"
                  type="email"
                  placeholder="Email Address"
                  class="email-input"
                />
                <div class="icn mr-2">
                  <v-icon
                    v-if="errorMessage"
                    color="deep-orange-darken-1"
                    icon="mdi-alert-circle"
                    size="large"
                  ></v-icon>
                </div>
                <div
                  class="pa-5 pa-md-0 btn d-flex justify-center align-center"
                  @click="validateEmail"
                >
                  <v-icon class="icon" color="white">mdi-chevron-right</v-icon>
                </div>
              </div>
              <div class="error-message px-5 mb-10">{{ errorMessage }}</div>
            </v-col>
          </v-row>
        </v-container>
      </v-col>
      <v-col cols="5" class="right pa-0">
        <img class="image" src="/src/assets/hero-desktop.jpg" alt="" />
      </v-col>
    </v-row>
  </v-container>

  <v-container v-else fluid class="body2 pa-0">
    <v-row class="main-row2 ma-0 middle">
      <v-col cols="12" class="my-10 mx-8">
        <div class="logo">
          <img src="/src/assets/logo.svg" alt="" />
        </div>
      </v-col>
      <v-col cols="12" class="image2 pa-0">
        <div class="img2">
          <img src="/src/assets/hero-mobile.jpg" alt="" />
        </div>
      </v-col>
      <v-col cols="12" class="mt-16 d-flex flex-column align-center">
        <div class="text">
          <div class="heading2 mb-4 text-center ml-16">
            <span class="weare2">WE'RE</span>
            COMING SOON
          </div>
          <div class="para2 mx-16">
            Hello fellow shoppers! We're currently building our new fashion
            store. Add your email below to stay up-to-date with announcements
            and our launch deals.
          </div>
        </div>
      </v-col>
      <v-col cols="12">
        <v-col cols="12" class="px-13 mb-10">
          <div
            :class="
              errorMessage ? 'email-container2-error' : 'email-container2'
            "
          >
            <input
              v-model="email"
              type="email"
              placeholder="Email Address"
              class="email-input"
            />
            <div class="icn mr-2">
              <v-icon
                v-if="errorMessage"
                color="deep-orange-darken-1"
                icon="mdi-alert-circle"
                size="large"
              ></v-icon>
            </div>
            <div
              class="pa-5 pa-md-0 btn2 d-flex justify-center align-center"
              @click="validateEmail"
            >
              <v-icon class="icon" color="white">mdi-chevron-right</v-icon>
            </div>
          </div>
          <div class="error-message px-5 mb-10">{{ errorMessage }}</div>
        </v-col>
      </v-col>
    </v-row>
  </v-container>
</template>

<script setup>
import Swal from "sweetalert2";
import { ref, onMounted, onUnmounted } from "vue";

const email = ref("");
const errorMessage = ref("");
const isScreenLarge = ref(window.innerWidth > 599.5); // Set initial value based on current window size

// Watch window resize to update isScreenLarge
const handleResize = () => {
  isScreenLarge.value = window.innerWidth > 599.5;
};

// Set up and clean up event listener
onMounted(() => {
  window.addEventListener("resize", handleResize);
});
onUnmounted(() => {
  window.removeEventListener("resize", handleResize);
});

// Email validation rules
const emailRules = [
  (v) => !!v || "Email is required",
  (v) => /.+@.+\..+/.test(v) || "E-mail must be valid",
  (v) =>
    v.endsWith(".co") ||
    v.endsWith(".com") ||
    "Email must end with .co or .com",
];

// Function to validate email
const validateEmail = () => {
  const error = emailRules.find((rule) => rule(email.value) !== true);

  if (error) {
    errorMessage.value = error(email.value);
  } else {
    errorMessage.value = "";
    email.value = "";
    showSuccessAlert();
  }
};

// Function to show success alert
const showSuccessAlert = () => {
  Swal.fire({
    title: "Hurrayyy!!! You are now subscribed to our newsletter.",
    text: "Thank you for subscribing!",
    icon: "success",
    confirmButtonText: "Thanks!",
    background: "hsl(0, 100%, 98%)",
    color: "#bd7676",
    confirmButtonColor: "#f6b5b5",
    customClass: {
      title: "swal-title",
      popup: "swal-popup",
      confirmButton: "swal-confirm-button",
    },
    scrollbarPadding: false, // Prevent hiding scrollbar to avoid layout shift
  });
};
</script>

<style scoped>
/* SMALL SCREEN */
.image2 {
  width: 100%;
  height: auto; /* Keep the original height */
}
.img2 img {
  width: 100%;
  height: 100%;
  object-fit: cover; /* Ensures the image fully covers the .image2 container */
  object-position: center; /* Centers the image */
}
.body2 {
  height: 100%;
  width: 100%;
  background-color: #4845d8;
}
.main-row2 {
  height: 100%;
  width: 100%;
  background-color: #e51fbd;
}
.middle {
  background-color: hsl(12, 71%, 99%);
  background-image: url("/src/assets/bg-pattern-desktop.svg"); /* Path to your background image */
  background-size: cover; /* Ensures the image covers the entire container */
  background-position: center; /* Centers the image */
  background-repeat: no-repeat; /* Prevents the image from repeating */
}
.heading2 {
  color: black;
  font-size: 60px;
  line-height: 65px;
  font-family: f2;
  letter-spacing: 10px;
  color: hsl(0, 6%, 24%);
  padding-right: 100px;
}
.weare2 {
  color: hsl(0, 36%, 70%);
  font-family: f1;
  letter-spacing: 10px;
}
.para2 {
  color: hsl(0, 36%, 70%);
  font-family: f3;
  text-align: justify; /* Justifies the text */
  text-align-last: center;
  line-height: 25px;
}
.email-container2 {
  display: flex;
  flex-direction: row;
  align-items: center;
  border: 1.3px solid hsl(0, 15%, 65%);
  border-radius: 50px;
  width: 100%;
  background-color: transparent;
}
.email-container2-error {
  display: flex;
  flex-direction: row;
  align-items: center;
  border: 1.8px solid hsl(0, 93%, 68%);
  border-radius: 50px;
  width: 100%;
  background-color: transparent;
}
.btn2 {
  background: linear-gradient(135deg, hsl(0, 80%, 86%), hsl(0, 74%, 74%));
  border-radius: 50px;
  cursor: pointer;
  height: 50px; /* Set a fixed height */
  width: 75px;
  display: flex; /* Ensure flex display for centering */
  align-items: center; /* Center icon vertically */
  justify-content: center; /* Center icon horizontally */
  box-shadow: 0px 4px 25px 0px rgba(244, 114, 114, 0.4);
}
.btn2:hover {
  background: linear-gradient(
    135deg,
    hsl(358, 68%, 91%),
    hsl(359, 86%, 89%)
  ); /* Darker gradient */
}

/* BIG SCREEN */
@font-face {
  font-family: f1;
  src: url(/src/assets/JosefinSans-Light.ttf);
}
@font-face {
  font-family: f2;
  src: url(/src/assets/JosefinSans-Medium.ttf);
}
@font-face {
  font-family: f3;
  src: url(/src/assets/JosefinSans-Regular.ttf);
}
.body {
  height: 100%;
  width: 100%;
  background-color: #4845d8;
}

.main-row {
  height: 100%;
  width: 100%;
  background-color: #bdd126;
}
.left {
  background-image: url("/src/assets/bg-pattern-desktop.svg"); /* Set the background image */
  background-size: cover; /* Ensure the image covers the entire container while maintaining aspect ratio */
  background-position: center; /* Center the image */
  background-repeat: no-repeat; /* Prevent the image from repeating */
  height: 100%; /* Make sure the left column takes the full height */
  background-color: hsl(12, 100%, 99%); /* Optional fallback background color */
}

.image {
  width: 100%;
  height: 100%;
  object-fit: cover; /* Ensures the image covers the right column and maintains its aspect ratio */
  object-position: center; /* Centers the image inside the container */
  display: block; /* Remove any inline display issues */
}
.heading {
  color: black;
  font-size: 60px;
  line-height: 65px;
  font-family: f2;
  letter-spacing: 10px;
  color: hsl(0, 6%, 24%);
  padding-right: 100px;
}
.weare {
  color: hsl(0, 36%, 70%);
  font-family: f1;
  letter-spacing: 10px;
}
.para {
  color: hsl(0, 36%, 70%);
  font-family: f3;
}
.email-container {
  display: flex;
  flex-direction: row;
  align-items: center;
  border: 1.3px solid hsl(0, 15%, 65%);
  border-radius: 50px;
  width: 100%;
  background-color: transparent;
}
.email-container-error {
  display: flex;
  flex-direction: row;
  align-items: center;
  border: 1.8px solid hsl(0, 93%, 68%);
  border-radius: 50px;
  width: 100%;
  background-color: transparent;
}
.email-input {
  flex: 1; /* Make input take available space */
  border: none; /* Remove border */
  border-radius: 50px; /* Keep rounded edges */
  padding: 12px 20px; /* Padding for input */
  font-size: 16px; /* Font size */
  color: hsl(0, 36%, 70%); /* Text color */
  background-color: transparent; /* Background transparent */
  outline: none; /* Remove outline */
}

.email-input::placeholder {
  color: hsla(0, 36%, 70%, 60%); /* Placeholder color */
  font-size: 14px;
}

.btn {
  background: linear-gradient(135deg, hsl(0, 80%, 86%), hsl(0, 74%, 74%));
  border-radius: 50px;
  cursor: pointer;
  height: 50px; /* Set a fixed height */
  width: 100px;
  display: flex; /* Ensure flex display for centering */
  align-items: center; /* Center icon vertically */
  justify-content: center; /* Center icon horizontally */
  box-shadow: 0px 4px 15px 0px rgba(244, 114, 114, 0.5);
}
.btn:hover {
  background: linear-gradient(
    135deg,
    hsl(358, 68%, 91%),
    hsl(359, 86%, 89%)
  ); /* Darker gradient */
}
.error-message {
  color: hsl(0, 93%, 68%); /* Error message color */
  font-size: 13px; /* Font size */
  margin-top: 10px;
}
.icon {
  font-size: 40px; /* Increase icon size */
}

/* Custom classes for SweetAlert */
.swal-title {
  color: #27248b; /* Title color */
}
.swal-popup {
  background: #f0f8ff; /* Popup background color */
}
.swal-confirm-button {
  background: linear-gradient(135deg, hsl(0, 80%, 86%), hsl(0, 74%, 74%));
  color: white; /* Button text color */
  border: none; /* Remove border */
}

@media (max-width: 915px) {
  .email-container {
    width: 130%;
  }
}
@media (max-width: 749.5px) {
  .heading {
    letter-spacing: 2px; /* Slight reduction for medium screens */
  }
  .email-container {
    flex-direction: column;
  }
}
@media (max-width: 675px) {
  .heading {
    letter-spacing: -8px; /* Slight reduction for medium screens */
  }
  .email-container {
    width: 140%;
  }
}
</style>
