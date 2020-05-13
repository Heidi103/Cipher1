<script>
  const shift = 3;
  let input = "";
  let output = "";


  function encrypt() {
    let plaintext = input;
    let ciphertext = "";

    for (let i = 0; i < plaintext.length; i++) {
      //ciphertext += plaintext.charCodeAt(i) + "|";
      let charCode = plaintext.charCodeAt(i);
      charCode += shift;
      ciphertext += charCode + "|";
    }

    output = ciphertext;
  }
  function decrypt() {
    console.log(`Decrypt button was click... `);
    let ciphertext = input;
    let plaintext = "";
    let charCode = "";

    for (let i = 0; i < ciphertext.length; i++) {
      if (ciphertext[i] !== "|") {
        charCode += ciphertext[i];
      } else {
        charCode -= shift;
        plaintext += String.fromCharCode(charCode);
        charCode = "";
      }
    }
    output = plaintext;
  }
  function analyse() {
    console.log("Analyse button has been clicked...");
    let ciphertext = input;
    let charCode = "";
    let codes = [];
    let analysis = ''

    for (let i = 0; i < ciphertext.length; i++) {
      if (ciphertext[i] !== "|") {
        charCode += ciphertext[i];
      } else {
        codes = [...codes, charCode];
        charCode = "";
      }
    }
    if (codes.length) {
      codes.sort();

      let currentCode = codes;
      let count = 0;

      for (let i = 0; i < codes.length; i++) {
        if (codes[i] === currentCode) {
          count++;
        } else {
          analysis += currentCode + " appears " + count + " times.";
          currentCode = codes[i];
          count = 1;
        }
      }
      analysis += currentCode + ' appears'  + count + ' times. ';
    }
    output = analysis;
  }
</script>

<section class="section content">
  <h1>Cipher</h1>

  <label class="label">
    Text:
    <input class="input" bind:value={input} />
  </label>
  <button class="button is-success is-outlined" on:click={encrypt}>
    Encrypt
  </button>
  <button class="button is-warning is-outlined" on:click={decrypt}>
    Decrypt
  </button>
  <button class="button" on:click={analyse}>Analyse</button>

  <h2>Result:</h2>
  <p>{output}</p>
</section>

