<template>
  <!-- Success Message Start -->
  <section class="success" v-if="success">
    <div class="success__img">
      <img src="../public/icon-success.svg" alt="Success Icons" />
    </div>

    <h2 class="main__title">Thanks for subscribing!</h2>

    <p class="base__font">
      A confirmation email has been sent to
      <span class="valid-email">{{ validEmail }}</span
      >. Please open it and click the button inside to confirm your
      subscription.
    </p>

    <button class="btn">Dismiss message</button>
  </section>
  <!-- Success Message End -->

  <!-- Main start -->
  <main class="main-container" v-else>
    <section class="main__img" ref="img"></section>

    <section class="main__description" ref="container">
      <h1 class="main__title">Stay updated!</h1>

      <p class="base__font">
        Join 60,000+ product managers receiving monthly updates on:
      </p>

      <div class="checklist-container">
        <!-- Checklist 1 -->

        <div class="main__checklist">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            width="21"
            height="21"
            viewBox="0 0 21 21"
          >
            <g fill="none">
              <circle cx="10.5" cy="10.5" r="10.5" fill="#FF6155" />
              <path
                stroke="#FFF"
                stroke-width="2"
                d="M6 11.381 8.735 14 15 8"
              />
            </g>
          </svg>

          <p class="base__font">Product discovery and building what matters</p>
        </div>

        <!-- Checklist 2 -->

        <div class="main__checklist">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            width="21"
            height="21"
            viewBox="0 0 21 21"
          >
            <g fill="none">
              <circle cx="10.5" cy="10.5" r="10.5" fill="#FF6155" />
              <path
                stroke="#FFF"
                stroke-width="2"
                d="M6 11.381 8.735 14 15 8"
              />
            </g>
          </svg>

          <p class="base__font">Measuring to ensure updates are a success</p>
        </div>

        <!-- Checklist 3 -->

        <div class="main__checklist">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            width="21"
            height="21"
            viewBox="0 0 21 21"
          >
            <g fill="none">
              <circle cx="10.5" cy="10.5" r="10.5" fill="#FF6155" />
              <path
                stroke="#FFF"
                stroke-width="2"
                d="M6 11.381 8.735 14 15 8"
              />
            </g>
          </svg>

          <p class="base__font">And much more!</p>
        </div>
      </div>

      <form class="main__form" @submit.prevent>
        <div>
          <div class="main__form-text">
            <label for="email" class="sm__font">Email address</label>
            <span
              v-for="(error, index) in Errors"
              :key="index"
              v-if="Errors.length"
              :class="inputError == true ? 'errors' : ''"
              >{{ error }}</span
            >
          </div>
          <input
            type="email"
            name="email"
            id="email"
            placeholder="email@company.com"
            v-model="email"
            :class="inputError == true ? 'errors' : ''"
          />
        </div>

        <button type="submit" class="btn" @click="addUser">
          Subscribe to monthly newsletter
        </button>
      </form>
    </section>
  </main>
  <!-- Main end -->

  <!-- Footer Start -->

  <footer class="attribution" ref="footer">
    <p>
      Challenge by
      <a href="https://www.frontendmentor.io?ref=challenge" target="_blank"
        >Frontend Mentor</a
      >
    </p>

    <p>
      Code <span>&hearts;</span> by
      <a href="https://github.com/SouleymaneSy7" target="_blank"
        >Souleymane Sy</a
      >
    </p>
  </footer>

  <!-- Footer End -->
</template>

<script setup>
// Imports
import { onMounted, ref } from "vue";
import gsap from "gsap";

// Form Data
const email = ref("");
const inputError = ref(false);
const Errors = ref([]);
const validEmail = ref("");
const success = ref(false);

// GSAP Data
const container = ref("");
const footer = ref("");
const img = ref("");

// Form Submit Function
const addUser = () => {
  Errors.value = [];

  if (email.value.length === 0) {
    Errors.value.push("Email cannot be empty");
    inputError.value = true;
    email.value = "";
  } else if (email.value.includes("@") && email.value.includes(".")) {
    Errors.value = [];
    inputError.value = false;
    validEmail.value = email;
    success.value = true;
    return;
  } else {
    Errors.value.push("Valid email required");
    inputError.value = true;
    return;
  }
};

// GSAP Functions
onMounted(() => {
  gsap.from(img.value, {
    duration: 1.2,
    delay: 0.7,
    scale: 3,
    autoAlpha: 0,
    ease: "back.out(1.8)",
  });

  gsap.from(container.value.children, {
    duration: 1,
    delay: 0.5,
    x: "-300",
    autoAlpha: 0,
    stagger: 0.25,
    ease: "back.out(1.7)",
  });

  gsap.from(footer.value.children, {
    duration: 1,
    delay: 0.5,
    y: "+100",
    autoAlpha: 0,
    stagger: 0.15,
    ease: "back.out(1.2)",
  });
});
</script>
