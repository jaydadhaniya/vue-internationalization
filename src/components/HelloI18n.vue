<template>
  <div>
    <h1>{{ $t("language_select_info") }} :</h1>
    <select v-model="lang" class="minimal">
      <option
        v-for="(lang, i) in languageArray"
        :key="`lang${i}`"
        :value="lang"
      >
        {{ lang }}
      </option>
    </select>
    <div style="margin-top: 30px; font-size: larger">
      {{ $t("selected_language", { language: selected_language }) }}
    </div>

    <div class="hierarchy">
      <ul>
        <li>
          {{ $t("parent") }}
          <ul>
            <li>{{ $t("child") }} 1</li>
            <li>
              {{ $t("child") }} 2
              <ul>
                <li>{{ $t("parent.child.inner_child") }}</li>
              </ul>
            </li>
          </ul>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import i18n, { languages } from "@/plugins/i18n";

export default {
  name: "HelloI18n",

  data() {
    return {
      languageArray: languages,
      languagesMap: {
        en: "English",
        fr: "french",
        hi: "hindi",
      },
    };
  },

  computed: {
    lang: {
      get: function () {
        return this.$store.state.locale;
      },
      set: function (newLocale) {
        this.$store.dispatch("changeLocale", newLocale);
      },
    },

    selected_language() {
      return this.$t(this.languagesMap[this.lang]);
    },
  },

  created() {
    i18n.locale = this.$store.state.locale;
  },
};
</script>

<i18n>
{
  "en": {
    "parent": "parent from SFC",
    "child": "child"
  },
  "hi": {
    "parent": "माता-पिता",
    "child": "बालक"
  },
  "fr":{
    "parent": "parent",
    "child": "enfant"
  }
}
</i18n>

<style scoped>
select {
  /* styling */
  background-color: white;
  border: thin solid blue;
  border-radius: 4px;
  display: inline-block;
  font: inherit;
  line-height: 1.2em;
  padding: 0.5em 3.5em 0.5em 1em;

  /* reset */
  margin: 0;
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
  -webkit-appearance: none;
  -moz-appearance: none;
}

select.minimal {
  background-image: linear-gradient(45deg, transparent 50%, gray 50%),
    linear-gradient(135deg, gray 50%, transparent 50%),
    linear-gradient(to right, #ccc, #ccc);
  background-position: calc(100% - 20px) calc(1em + 2px),
    calc(100% - 15px) calc(1em + 2px), calc(100% - 2.5em) 0.5em;
  background-size: 5px 5px, 5px 5px, 1px 1.5em;
  background-repeat: no-repeat;
}

select.minimal:focus {
  background-image: linear-gradient(45deg, green 50%, transparent 50%),
    linear-gradient(135deg, transparent 50%, green 50%),
    linear-gradient(to right, #ccc, #ccc);
  background-position: calc(100% - 15px) 1em, calc(100% - 20px) 1em,
    calc(100% - 2.5em) 0.5em;
  background-size: 5px 5px, 5px 5px, 1px 1.5em;
  background-repeat: no-repeat;
  border-color: green;
  outline: 0;
}

select:-moz-focusring {
  color: transparent;
  text-shadow: 0 0 0 #000;
}

h1 {
  line-height: 100%;
  margin: 0 auto 2rem auto;
  max-width: 30rem;
  font-size: larger;
}

.hierarchy {
  line-height: 100%;
  margin: 0 auto 2rem auto;
  max-width: 15rem;
  font-size: larger;
  text-align: justify;
}
</style>
