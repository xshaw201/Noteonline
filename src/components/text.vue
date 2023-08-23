<script setup>
import LC from "leancloud-storage";
import pangu from "https://cdn.skypack.dev/pangu@4.0.7";
import { ref } from "vue";

const Pathname = window.location.pathname;
const Textarea = ref("");
const TextareaRead = ref(false);

const query = new LC.Query("Text");
if (/[\s\S]+(@info)$/gi.test(Pathname) == true) {
  query.equalTo("path", /[\s\S]+(?=@info)/gi.exec(Pathname)[0]);
  query.find().then((students) => {
    if (students[0] != null) {
      Textarea.value =
        "创建时间：" +
        students[0]["createdAt"] +
        "\n更新时间：" +
        students[0]["updatedAt"] +
        "\n更新者身份：\n" +
        students[0]["attributes"]["info"];
    } else {
      Textarea.value = "此页面尚未创建";
    }
    TextareaRead.value = true;
  });
} else if (Pathname == "/0") {
  // 向 Note.ms 致敬
  Textarea.value = `救命啊

？

？
`;
} else {
  query.equalTo("path", Pathname);
  query.find().then((students) => {
    if (students[0] != null) {
      Textarea.value = pangu.spacing(students[0]["attributes"]["content"]);
    } else {
      const Text = LC.Object.extend("Text");
      const text = new Text();
      text.set("info", "");
      text.set("path", Pathname);
      text.set("content", "");
      text.save();
    }
  });
}

function updata() {
  query.find().then((students) => {
    if (students[0]["id"] != null) {
      if (Pathname != "/0") {
        const text = LC.Object.createWithoutData("Text", students[0]["id"]);
        const Http = new XMLHttpRequest();
        const url = "https://tenapi.cn/v2/getip";
        Http.open("GET", url);
        Http.send();
        Http.onreadystatechange = (e) => {
          if (Http.responseText != null) {
            text.set("info", Http.responseText);
          }
          text.set("content", Textarea.value);
          text.save();
        };
      }
    }
  });
}
</script>

<template>
  <textarea
    autofocus
    name="text"
    cols="42"
    rows="42"
    autocomplete="off"
    v-on:keyup="updata()"
    spellcheck="false"
    v-model="Textarea"
    :readonly="TextareaRead"
  ></textarea>
  <div id="marked"></div>
</template>

<style scoped>
textarea {
  background: var(--color-background);
  padding: 0;
  font-size: 1em;
  color: var(--color-text);
  border: 0;
  width: 100%;
  width: calc(100% - 1em);
  height: 100%;
  height: calc(100% - 1em);
  resize: none;
  -moz-box-sizing: border-box;
  box-sizing: content-box;
  overflow: auto;
  vertical-align: top;
  font-family: "HarmonyOS_Regular";
}

textarea:focus {
  outline: none;
}
</style>
