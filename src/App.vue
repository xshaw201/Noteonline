<script setup>
import Path from "./components/path.vue";
import Text from "./components/text.vue";
import LC from "leancloud-storage";

LC.init({
  appId: "cPGPCdYR5yIcWCNjt7aB6MAU-MdYXbMMI",
  appKey: "J2f3dcbWcnJVun3fm1FsA4A7",
  serverURL: "https://lc.xshaw.xyz",
});

console.log(`\x1B[31m _   _       _                   _ _              _   _____ 
\x1B[32m| \\ | | ___ | |_ ___  ___  _ __ | (_)_ __   ___  / | |___ / 
\x1B[33m|  \\| |/ _ \\| __/ _ \\/ _ \\| '_ \\| | | '_ \\ / _ \\ | |   |_ \\ 
\x1B[34m| |\\  | (_) | ||  __/ (_) | | | | | | | | |  __/ | |_ ___) |
\x1B[35m|_| \\_|\\___/ \\__\\___|\\___/|_| |_|_|_|_| |_|\\___| |_(_)____/ `);
</script>

<template>
  <header>
    <Path />
  </header>

  <main>
    <Text />
  </main>
</template>
