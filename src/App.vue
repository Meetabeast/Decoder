<template>
  <my-theme></my-theme>
  <div class="wrapper">
    <div class="decode-container">
      <h4 class="decode-title">Decode</h4>
      <textarea type="text" id="decode_field" class="input-field"></textarea>
      <div class="copy-icon">
          <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-clipboard" viewBox="0 0 16 16" id="decode_icon">
            <path d="M4 1.5H3a2 2 0 0 0-2 2V14a2 2 0 0 0 2 2h10a2 2 0 0 0 2-2V3.5a2 2 0 0 0-2-2h-1v1h1a1 1 0 0 1 1 1V14a1 1 0 0 1-1 1H3a1 1 0 0 1-1-1V3.5a1 1 0 0 1 1-1h1v-1z"/>
            <path d="M9.5 1a.5.5 0 0 1 .5.5v1a.5.5 0 0 1-.5.5h-3a.5.5 0 0 1-.5-.5v-1a.5.5 0 0 1 .5-.5h3zm-3-1A1.5 1.5 0 0 0 5 1.5v1A1.5 1.5 0 0 0 6.5 4h3A1.5 1.5 0 0 0 11 2.5v-1A1.5 1.5 0 0 0 9.5 0h-3z"/>
          </svg>
      </div>
      <br>
      <button type="submit" class="button blue" id="decode_button">Decode</button>
    </div>
    <div class="encode-container">
      <h4 class="encode-title">Encode</h4>
      <textarea type="text" id="encode_field" class="input-field"></textarea>
      <div class="copy-icon">
          <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-clipboard" viewBox="0 0 16 16" id="encode_icon">
            <path d="M4 1.5H3a2 2 0 0 0-2 2V14a2 2 0 0 0 2 2h10a2 2 0 0 0 2-2V3.5a2 2 0 0 0-2-2h-1v1h1a1 1 0 0 1 1 1V14a1 1 0 0 1-1 1H3a1 1 0 0 1-1-1V3.5a1 1 0 0 1 1-1h1v-1z"/>
            <path d="M9.5 1a.5.5 0 0 1 .5.5v1a.5.5 0 0 1-.5.5h-3a.5.5 0 0 1-.5-.5v-1a.5.5 0 0 1 .5-.5h3zm-3-1A1.5 1.5 0 0 0 5 1.5v1A1.5 1.5 0 0 0 6.5 4h3A1.5 1.5 0 0 0 11 2.5v-1A1.5 1.5 0 0 0 9.5 0h-3z"/>
          </svg>
      </div>
      <br>
      <button type="submit" class="button blue" id="encode_button">Encode</button>
    </div>
  </div>
  
  <div class="toast" id="toast">
    <span id="toast-text"></span>
  </div>
</template>

<script>
import myTheme from "./components/Theme.vue";

export default {
  name: 'App',
  components: {
    myTheme
  },
  mounted() {
    let decode_field = document.getElementById("decode_field");
    let decode_button = document.getElementById("decode_button");
    let decode_icon = document.getElementById("decode_icon");

    let encode_field = document.getElementById("encode_field");
    let encode_button = document.getElementById("encode_button");
    let encode_icon = document.getElementById("encode_icon");

    let toast = document.getElementById("toast");
    let toast_text = document.getElementById("toast-text");

    encode_button.onclick = function() {
      if(encode_field.value == '') {
        toast.classList.add("active");
        toast.classList.add("error");

        toast_text.innerText = `Please enter a Text`;

        setTimeout(() => {
          toast.classList.remove("active");
          toast.classList.remove("error");
          toast_text.innerText = "";
        }, 1000 * 2 + 700)
        return;
      }

      encode_field.value = `${encode(encode_field.value)}`
    }

    decode_button.onclick = function() {
      if(decode_field.value == '') {
        toast.classList.add("active");
        toast.classList.add("error");

        toast_text.innerText = `Please enter a Text`;

        setTimeout(() => {
          toast.classList.remove("active");
          toast.classList.remove("error");
          toast_text.innerText = "";
        }, 1000 * 2 + 700)
        return;
      }

      decode_field.value = `${decode(decode_field.value)}`
    }

    decode_icon.onclick = function() {
      if(decode_field.value == '') {
        toast.classList.add("active");
        toast.classList.add("error");
        toast_text.innerText = `No Text in decoder found`;

        setTimeout(() => {
          toast.classList.remove("active");
          toast.classList.remove("error");
          toast_text.innerText = "";
        }, 1000 * 2 + 700)
        return;
      }

      toast.classList.add("active");
      toast_text.innerText = `Successfully copied!`;

      setTimeout(() => {
        toast.classList.remove("active");
        toast_text.innerText = "";
      }, 1000 * 2 + 700)

      navigator.clipboard.writeText(decode_field.value);
    }

    encode_icon.onclick = function() {
      if(decode_field.value == '') {
        toast.classList.add("active");
        toast.classList.add("error");
        toast_text.innerText = `No Text in encoder found`;

        setTimeout(() => {
          toast.classList.remove("active");
          toast.classList.remove("error");
          toast_text.innerText = "";
        }, 1000 * 2 + 700)
        return;
      }

      toast.classList.add("active");
      toast_text.innerText = `Successfully copied!`;

      setTimeout(() => {
        toast.classList.remove("active");
        toast_text.innerText = "";
      }, 1000 * 2 + 700)

      navigator.clipboard.writeText(encode_field.value)
    }

    function decode(text) {
      let decode = btoa(text);
      return decode
    }

    function encode(text) {
      let encode = atob(text);
      return encode.toString();
    }
  }
}
</script>

<style>
body {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  background-color: var(--background1);
  color: var(--textColor);
}

.wrapper {
  display: flex;
  justify-content: center;
  padding: 20px 20px;
}

.decode-container {
  margin: 24px 24px;
  display: flex;
  flex-direction: column;
}

.encode-container {
  display: flex;
  flex-direction: column;
  margin: 24px 24px;
}

.input-field {
  display: block;
  position: relative;
  width: 440px;
  height: 500px;
  resize: none;
  border: solid black 0.1px;
  border-radius: 12px;
  padding: 12px 6px;
  background-color: var(--cardColor);
  color: var(--textColor)
}

.input-field:focus {
  outline: none;
}

.button {
  display: inline-block;
  font-weight: 400;
  text-align: center;
  white-space: nowrap;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
  border: 1px solid transparent;
  padding: 0.375rem 0.75rem;
  font-size: 1rem;
  line-height: 1.5;
  border-radius: 0.35rem;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-decoration: none;
  cursor: pointer;
}

.button.blue {
  background-color: #007bff;
  color: rgb(255, 255, 255)
}

.copy-icon {
  position: relative;
  bottom: 25px;
  right: -420px;
  cursor: pointer;
}

.toast {
  visibility: hidden;
  min-width: 250px;
  margin-left: -125px;
  background-color: rgb(22, 201, 15);
  color: #fff;
  text-align: center;
  border-radius: 2px;
  padding: 16px;
  border-radius: 15px;
  position: fixed;
  z-index: 1;
  left: 50%;
  bottom: 30px;
  font-size: 17px;
}

.toast.active {
  visibility: visible;
  animation: fadein 0.5s, fadeout 0.5s 2.5s;
}

.toast.error {
  background-color: rgb(201, 15, 15);
}

@keyframes fadein {
  from {bottom: 0; opacity: 0;}
  to {bottom: 30px; opacity: 1;}
}

@keyframes fadeout {
  from {bottom: 30px; opacity: 1;}
  to {bottom: 0; opacity: 0;}
}

@media (max-width: 800px) {
  .wrapper {
    display: flex;
    flex-direction: column;
    padding: 0;
  }

  .encode-container, .decode-container, .input-field {
    margin: 0;
    width: 350px;
  }

  .copy-icon {
    position: relative;
    left: 2%;
  }
}

@media (max-width: 800px) {

  .encode-container, .decode-container, .input-field {
    margin: 0;
    width: 330px;
  }
}
</style>
