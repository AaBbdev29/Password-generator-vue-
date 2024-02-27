<template>
  <div class="wrapper">
    <h2>Password Generator</h2>
    <section class="gen-section">
      <form class="gen-form">
        <div class="values">
          <label
            ><input
              type="checkbox"
              name="letter"
              v-model="letter"
            />Letter</label
          >
          <label
            ><input
              type="checkbox"
              name="spcial-char"
              v-model="char"
            />Symbols</label
          >
          <label
            ><input
              type="checkbox"
              name="number"
              v-model="number"
            />Number</label
          >
          <label
            ><input
              type="checkbox"
              name="Uppercase"
              v-model="uppercase"
            />Uppercase</label
          >
        </div>
        <label>Lenght:<input type="text" v-model="length" /></label>
        <button
        ref="genpass"
          type="button"
          class="gen-pass"
          @click.prevent="generatePassword"
        >
          Generate Password
        </button>
        <button ref="cpy" type="button" class="copy-clip" @click="copyToClipboard">Copy to Clipboard</button>
        <input type="text" class="result" />
      </form>
    </section>
  </div>
</template>
<script>
export default {
  name: "generator",
  data() {
    return {
      letter: false,
      char: false,
      number: false,
      uppercase: false,
      length: 12,
    };
  },
  methods: {
    generatePassword() {
      const result = document.querySelector(".result");
      let password = "";
      const lowercaseChars = this.letter ? "abcdefghijklmnopqrstuvwxyz" : "";
      const uppercaseChars = this.uppercase ? lowercaseChars.toUpperCase() : "";
      const numbers = this.number ? "0123456789" : "";
      const symbols = this.char ? "!@#$%^&*()_+-=[]{}|;':'\\,.<>/?" : "";
      const tempChar = [lowercaseChars, uppercaseChars, numbers, symbols].join(
        ""
      );
      //console.table(tempChar);
      if (tempChar !== "") {
        for (let index = 0; index < this.length; index++) {
          const randomIndex = Math.floor(Math.random() * tempChar.length);
          password += [...tempChar[randomIndex]].join("");
          this.$refs.genpass.style.backgroundColor="#19776c";
          this.$refs.cpy.style.backgroundColor="#c3c3c6"
          //console.log(password);
        }
      } else {
        const defaultChar = "abcdefghijklmnopqrstuvwxyz0123456789!@#$%^&*()_+";
        for (let index = 0; index < this.length; index++) {
          const randomIndex = Math.floor(Math.random() * defaultChar.length);
          password += [...defaultChar[randomIndex]].join("");
          this.$refs.genpass.style.backgroundColor="#19776c";
          this.$refs.cpy.style.backgroundColor="#c3c3c6"
        }
      }
      //console.log(password);
      result.value = password;
    },
    async copyToClipboard() {
        const text=document.querySelector(".result").value;
       
      try {
        await navigator.clipboard.writeText(text);
        console.log("Text copied to clipboard successfully!");
        this.$refs.cpy.style.backgroundColor="#1c8745";
        this.$refs.genpass.style.backgroundColor="#c3c3c6";
      } catch (err) {
        console.error("Failed to copy text to clipboard:", err);
      }
     
    },
  },
};
</script>
<style></style>
