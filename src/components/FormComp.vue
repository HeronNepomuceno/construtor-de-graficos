<template>
  <main class="main-wrapper">
    <div class="get-show-data">
      <form class="settings">
        <div class="head">
          <h6 class="title">Preencha os campos abaixo</h6>
          <v-icon>mdi-help-rhombus</v-icon>
        </div>
        <div class="body">
          <div class="input-name">
            <label>Nome do gráfico:</label>
            <input type="text" v-model="graph_name" />
          </div>
          <div class="input-item">
            <label>Nome do item do gráfico:</label>
            <input type="text" />
          </div>
          <div class="input-number">
            <label>Número do item do gráfico:</label>
            <input type="number" step="0.1" />
          </div>
          <v-alert color="#E53935" type="error" dense v-if="empty_error"
            ><label class="text-error"
              >Preencha todos os campos!</label
            ></v-alert
          >
        </div>
        <div class="footer">
          <button class="clear-button" title="Limpar respostas" @click="clearForm">
            <v-icon>mdi-eraser-variant</v-icon>
          </button>
          <button class="send-button" @click="getItemData">Enviar item</button>
        </div>
      </form>
      <div class="show-data" v-if="show_data_graph">
        <div class="head">
          <h6 class="title">Dados do gráfico</h6>
        </div>
        <ul class="data" v-for="(item, index) in item_name" :key="item">
          <li class="item">
            {{ index + 1 }}. {{ item }}: {{ item_number[index] }}
          </li>
          <button
            class="delete-item"
            :class="['btn-' + index]"
            @click="deleteItem(index)"
            title="deletar item"
          >
            <v-icon>mdi-delete</v-icon>
          </button>
        </ul>
      </div>
    </div>
    <div class="graph-wrapper">
      <div class="head">
        <h6 class="title" v-if="!show_graph_name">Seu gráfico aparece aqui:</h6>
        <h6 class="title" v-if="show_graph_name">{{ graph_name }}</h6>
      </div>
      <div class="body ct-chart ct-perfect-fourth"></div>
    </div>
  </main>
</template>

<script>
import Chartist from "chartist";
export default {
  name: "FormComp",
  data: function () {
    return {
      graph_name: "",
      item_name: [],
      item_number: [],
      empty_error: false,
      show_data_graph: false,
      show_graph_name: false
    }
  },

  watch: {
    item_name() {
      if (this.item_name.length != 0) {
        this.show_data_graph = true
      } else {
        this.show_data_graph = false
      }
    },

    graph_name() {
      if (this.graph_name != '') {
        this.show_graph_name = true
      } else {
        this.show_graph_name = false
      }
    }
  },

  methods: {
    getItemData: function (event) {
      event.preventDefault()
      let item = document.querySelector(".input-item input").value
      let number = document.querySelector(".input-number input").value

      if (item == "" || number == "") {
        this.empty_error = true
      } else {
        this.empty_error = false
        this.item_name.push(item)
        this.item_number.push(number)
        document.querySelector(".input-item input").value = ""
        document.querySelector(".input-number input").value = ""
        this.showGraph()
      }
    },

    clearForm: function (event) {
      event.preventDefault()
      document.querySelector(".input-item input").value = ""
      this.graph_name = ''
      document.querySelector(".input-number input").value = ""
    },

    deleteItem: function (index) {
      this.item_name.splice(index, 1)
      this.item_number.splice(index, 1)
      this.showGraph()
    },

    showGraph() {
      var data = {
        labels: this.item_name,
        series: [this.item_number]
      }
      new Chartist.Line(".ct-chart", data)
    },
  },
}
</script>

<style>
.main-wrapper {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 16px;
  width: 100%;
}

.get-show-data {
  display: flex;
  flex-direction: column;
}

.settings,
.show-data,
.graph-wrapper {
  border-radius: 24px;
  border: 1px solid var(--blue-grey-darken-1);
  color: var(--grey-lighten-4);
  display: flex;
  flex-direction: column;
  font-family: var(--fontPrimary);
  padding: 16px;
  width: 360px;
  margin-top: 16px;
}
.head {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 32px;
}
.head > .title {
  font-size: 18px;
  font-weight: 700;
}
.head > .v-icon.v-icon {
  color: var(--amber-lighten-2);
  font-size: 24px;
}
.body {
  display: flex;
  flex-direction: column;
}
.body > input {
  transition: border.3s;
}
.body > input:focus {
  border: 1.6px solid var(--grey-lighten-4);
}
.input-item,
.input-number,
.input-name {
  display: flex;
  flex-direction: column;
  margin-bottom: 16px;
}
.input-item > label {
  font-size: 15px;
  font-weight: 400;
  margin-bottom: 8px;
}
.input-item > input {
  border-radius: 4px;
  border: 1px solid var(--blue-grey-darken-1);
  color: var(--grey-lighten-4);
  font-weight: 300;
  padding-left: 8px;
}
.input-number > label {
  font-size: 15px;
  font-weight: 400;
  margin-bottom: 8px;
}
.input-number > input {
  border-radius: 4px;
  border: 1px solid var(--blue-grey-darken-1);
  color: var(--grey-lighten-4);
  font-weight: 300;
  padding-left: 8px;
}
.input-name > label {
  font-size: 15px;
  font-weight: 400;
  margin-bottom: 8px;
}
.input-name > input {
  border-radius: 4px;
  border: 1px solid var(--blue-grey-darken-1);
  color: var(--grey-lighten-4);
  font-weight: 300;
  padding-left: 8px;
}
.footer {
  display: flex;
  justify-content: flex-end;
  margin-top: 16px;
}
.send-button {
  background: var(--blue-grey-darken-1);
  border-radius: 9999px;
  margin-left: 16px;
  opacity: 1;
  padding: 8px 16px;
  transition: opacity 0.5s, transform 0.5s;
}
.send-button:hover,
.clear-button:hover {
  opacity: 0.8;
}
.send-button:active,
.clear-button:active {
  transform: scale(1.1);
}
.clear-button {
  background: var(--grey-darken-1);
  border-radius: 9999px;
  padding: 8px;
  transition: opacity 0.5s, transform 0.5s;
}
.clear-button > .v-icon.v-icon {
  color: var(--grey-lighten-4);
}
.text-error {
  margin-left: 16px;
}
.data-wrapper {
  display: flex;
  flex-direction: column;
}
.data {
  display: flex;
  justify-content: space-between;
  width: 100%;
}
.delete-item > .v-icon.v-icon {
  color: var(--red-darken-1);
}

.graph-wrapper {
  display: flex;
  align-items: flex-start;
}

.ct-label {
  color: #fff;
}

.ct-chart {
  height: 460px;
}

@media only screen and (min-width: 1115px) {
  .main-wrapper {
    align-items: flex-start;
    display: grid;
    grid-template-columns: 35% 60%;
  }
  .graph-wrapper {
    width: auto;
  }
  .graph-wrapper > .body {
    max-height: 640px;
  }
}
</style>