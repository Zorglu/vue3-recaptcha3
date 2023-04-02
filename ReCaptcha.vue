<template>
    <div><!-- There's nothing to show but if you want, it's here--></div>
  </template>

  <script setup>
  import { defineExpose, onMounted, onUnmounted } from "vue";

  /**
   * our component wait a public site key from Google ReCaptcha
   * show https://developers.google.com/recaptcha/docs/v3
   */
  const props = defineProps({
    sitekey: { type: String, required: true },
  });

  /**
   * Save the html'node script
   */
  let script = null;

  /**
   * function getToken()
   * Ask Google for give a token
   * call this function with await. ex await getToken();
   * return string token if all are allright
   */
  const getToken = () => {
    return new Promise((resolve) => {
      grecaptcha.ready(() => {
        grecaptcha
          .execute(props.sitekey, {
            action: "submit",
          })
          .then((token) => {
            resolve(token);
          });
      });
    });
  };

  /**
   * Make getToken method visible outside component
   */
  defineExpose({ getToken });

  /**
   * Google ReCaptcha uninstall
   */
  onUnmounted(() => {
    // Remove google captcha
    script.remove();
    const arr = [].slice.call(document.head.children);
    arr.forEach((el) => {
      if (el.src != undefined && el.src.indexOf("recaptcha") >= 0) {
        el.remove();
      }
    });
    document.querySelector(".grecaptcha-badge").remove();
  });

  /**
   * Google ReCaptcha Install
   */
  onMounted(() => {
    script = document.createElement("script");
    script.src = `https://www.google.com/recaptcha/api.js?render=${props.sitekey}`;
    script.async = true;
    script.defer = true;
    document.head.append(script);
  });
  </script>
