<template>
  <div id="temperature">
    <p class="title">{{ message }}</p>
    <hr>
    <div class="center">
      <div style="display: inline; margin: 10px 4px;" v-for="(scale, index) in scales" :key="index">
        <input type="radio" :id="scale" name="scale" :value="index" v-model="whatScale">
        <label :for="scale">{{scale}}</label>
      </div>
      <hr>
      <button @click="sum(-100)">-100</button>
      <button @click="sum(-10)">-10</button>
      <button @click="sum(-1)">-1</button>
      <button @click="inputValue = 0">{{resetMessage}}</button>
      <button @click="sum(1)">+1</button>
      <button @click="sum(10)">+10</button>
      <button @click="sum(100)">+100</button>

      <br>
      <br>
      <label class="header" for="celsius">{{temperatureMessage}} {{ scales[whatScale] }}:</label>
      <input type="number" class="temperatureToShow" v-model="inputValue">
    </div>

    <hr>
    <div class="converted">
      <span class="convertedText">
        <span class="header">{{temperatureMessage}} {{scales[degree1]}}:</span>
        <span class="temperatureToShow">{{ degree1ToShow }}</span>
      </span>
      <span class="convertedText">
        <span class="header">{{temperatureMessage}} {{scales[degree2]}}:</span>
        <span class="temperatureToShow">{{ degree2ToShow }}</span>
      </span>
    </div>
    <hr>
    <div class="right">
      <select id="languageChanger" v-model="whatLanguage">
        <option v-for="(language, index) in languages" :key="index" :value="index">{{language}}</option>
      </select>
    </div>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  data: function() {
    return {
      languages: ["English", "Português", "Français", "Deutsch", "Español"],
      whatLanguage: 1,
      scales: ["Celsius", "Fahrenheit", "Kelvin"],
      whatScale: 0,
      degree1: 1,
      degree2: 2,
      inputValue: 0,
      cDegree: 0,
      fDegree: 0,
      kDegree: 0,
      message: "Bem-vindo ao conversor de temperatura!",
      temperatureMessage: "Temperatura em ",
      resetMessage: "Resetar"
    };
  },
  methods: {
    sum(number) {
      this.inputValue = this.inputValue * 1 + number;
    }
  },
  watch: {
    whatLanguage() {
      if (this.whatLanguage === 0) {
        this.message = "Welcome to the temperature converter!";
        this.temperatureMessage = "Temperature in ";
        this.resetMessage = "Reset";
      } else if (this.whatLanguage === 1) {
        this.message = "Bem-vindo ao conversor de temperatura!";
        this.temperatureMessage = "Temperatura em ";
        this.resetMessage = "Resetar";
      } else if (this.whatLanguage === 2) {
        this.message = "Bienvenue dans le convertisseur de température!";
        this.temperatureMessage = "Température en ";
        this.resetMessage = "Réinitialiser";
      } else if (this.whatLanguage === 3) {
        this.message = "Willkommen bei Temperaturwandler!";
        this.temperatureMessage = "Temperatur in ";
        this.resetMessage = "Zurücksetzen";
      } else if (this.whatLanguage === 4) {
        this.message = "Bienvenido al convertidor de temperatura!";
        this.temperatureMessage = "Temperatura en ";
        this.resetMessage = "Restablecer";
      }
    },
    whatScale() {
      this.inputValue = 0;

      if (this.whatScale === 0) {
        this.degree1 = 1;
        this.degree2 = 2;
      } else if (this.whatScale === 1) {
        this.degree1 = 0;
        this.degree2 = 2;
      } else {
        this.degree1 = 0;
        this.degree2 = 1;
      }
    },
    inputValue() {
      if (this.whatScale === 0) {
        if (this.inputValue <= -273.15) {
          this.inputValue = -273.15;
        }
      } else if (this.whatScale === 1) {
        if (this.inputValue <= -459.67) {
          this.inputValue = -459.67;
        }
      } else {
        if (this.inputValue <= 0) {
          this.inputValue = 0;
        }
      }
    }
  },
  computed: {
    degree1ToShow() {
      if (this.whatScale === 0) {
        let degree = this.inputValue * (9 / 5) + 32;
        return degree.toFixed(2);
      } else if (this.whatScale === 1) {
        let degree = ((this.inputValue - 32) * 5) / 9;
        return degree.toFixed(2);
      } else {
        let degree = this.inputValue * 1 - 273.15;
        return degree.toFixed(2);
      }
    },
    degree2ToShow() {
      if (this.whatScale === 0) {
        let degree = this.inputValue * 1 + 273.15;
        return degree.toFixed(2);
      } else if (this.whatScale === 1) {
        let degree = ((this.inputValue - 32) * 5) / 9 + 273.15;
        return degree.toFixed(2);
      } else {
        let degree = ((this.inputValue * 1 - 273.15) * 9) / 5 + 32;
        return degree.toFixed(2);
      }
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
@import url("https://fonts.googleapis.com/css?family=Roboto&display=swap");

* {
  font-family: "Roboto", sans-serif;
}

.center {
  margin: 16px;
  text-align: center;

  button {
    margin: 0 3px;
  }

  input[type="radio"] {
    margin-top: -1px;
    vertical-align: middle;
  }
}

#languageChanger {
  margin: 5px 5px;
}

.right {
  display: flex;
  justify-content: flex-end;
}

.title {
  font-size: 38px;
  margin: 5px;
  text-align: center;
}

.converted {
  display: flex;
  justify-content: space-between;

  .convertedText {
    margin: 0 10px;
  }
}

.text {
  font-size: 24px;
  color: black;
}

.header {
  font-size: 18px;
  font-weight: 800;
}

.temperatureToShow {
  margin-left: 2px;
}
</style>
