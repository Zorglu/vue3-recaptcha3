# Vue3-ReCaptcha (vue3-recaptcha)

Simple and effective component to manage Google Recaptcha v3 with vue3 in composition mode or not

## Install the dependencies
There is no dependency to install. You just have to install the component in the directory of your choice then install the component in your page.

## examples of use

```html
<template>
    <form @submit="onSubmit">
        <input v-model="text" type="text" />
        <button type="submit" />
    </form>
    <ReCaptcha ref="recaptcha" sitekey="abcdef0123456789abcdef0123456789" />
</template>

<script setup>
    import { ref} from "vue";
import ReCaptcha from "./ReCaptcha.vue";


const recaptcha = ref(null); // Get an instance of the component
const text = ref("");



const onSubmit = async () => {
    /*
    getToken() it's a Promise and you MUST wait the result before all
    */
     const token = await recaptcha.value.getToken();
     /*
     Send the form values ​​to your server along with the requested token from Google.

     On your server you will need to verify the token with google.
     This will inform you if the token is good and will assign a score to your request.
     This score will tell you how Google judged your customer. If it's a human or a robot
    */
};

</script>
```



