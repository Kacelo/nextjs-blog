---
title: "How to encrypt your local storage data with crypto.js"
date: "2023-05-29"
---

What is crypto-js?
well, I tried to find a formal definition for it on the internet but didn't really find something out there to match what I had in mind, so here's my version, crypto-JS is a library that is commonly used for encrypting data, hence the name crypto-js, (quite straight forward right?) crypto JS is perfect for hiding important local storage data like user details, which may include their username, email, and passwords, leaving this data unattended to could make your application vulnerable to malicious attacks. so in this blog, I am going to give you a step by step guide on how to implement.

1. first off we will start by importing the libray (assuming you already have a working application with local storage).

- npm install crypto-js

2. Next we import the library into your component

- import CryptoJS from 'crypto-js';

3. The next step is to define a secret key, I would suggesting importing your secret key in your environment variables file ".env"

- import REACT_APP_SECRET_ENV_KEY

4. The next step is to define the encryption function

- const encryptData =(name,data)=> {
- const encrypted = CryptoJS.AES.encrypt(JSON.stringify(data), REACT_APP_SECRET_ENV_KEY).toString();
  localStorage.setItem(name, encrypted);
  }

- The encryptData the function takes the data to be encrypted as a parameter, converts it to a JSON string, encrypts it using the AES encryption algorithm and the secret key, and stores the encrypted data in the local storage under the key name.

5. The follwing step is to define the decryption function

- import REACT_APP_SECRET_ENV_KEY

- const decryptData = (name) => {
  const encrypted = localStorage.getItem(name);
  const decrypted = CryptoJS.AES.decrypt(encrypted, REACT_APP_SECRET_ENV_KEY).toString(CryptoJS.enc.Utf8);
  return JSON.parse(decrypted);
  }
- The decryptData the function retrieves the encrypted data from local storage, decrypts it using the AES encryption algorithm and the secret key, converts it to a string using UTF-8 encoding, and parses it back to the original data format using JSON.parse().
