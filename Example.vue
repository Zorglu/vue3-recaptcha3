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
     const token = await recaptcha.value.getToken();
     alert(`token=${token}`);
};

</script>