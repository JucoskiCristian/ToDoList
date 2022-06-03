<template>
  <b-container fluid>
    <b-row align-h="center">
      <h1>To do List</h1>
    </b-row>
    <b-row align-h="center">
      <b-col cols="3" md="4">
        <b-input-group>
          <b-form-input v-model="text" placeholder="Tarefa"></b-form-input>
          <b-input-group-append>
            <b-button
              v-if="text !== ''"
              variant="success"
              @click="adicionarLista({ nome: text })"
              >Adicionar</b-button
            >
            <b-button v-else disabled variant="success">Adicionar</b-button>
          </b-input-group-append>
        </b-input-group>
      </b-col>
    </b-row>
    <b-row align-h="center">
      <b-col cols="4" class="my-2">
        <b-alert
          :show="dismissCountDown"
          fade
          dismissible
          variant="success"
          @dismiss-count-down="countDownChanged"
          >Tarefa Cadastrada Com Sucesso!!!</b-alert
        >
      </b-col>
    </b-row>
    <b-row align-h="center" class="m-2">
      <b-col cols="3" md="4">
        <b-list-group>
          <b-list-group-item
            :key="item"
            v-model="variant"
            variant="dark"
            v-for="(item, index) in tarefas">
            <b-row align-h="center">
              <b-col cols="9" class="my-1">
                <strong>{{ item.nome }}</strong>
              </b-col>
                            <b-col cols="3">
                <b-button @click="removerLista(index)" variant="danger">Delete</b-button>
              </b-col>
            </b-row>
          </b-list-group-item>
        </b-list-group>
      </b-col>
    </b-row>
  </b-container>
</template>

<script>
export default {
  data() {
    return {
      dismissSecs: 3,
      dismissCountDown: 0,
      showDismissibleAlert: false,
      text: "",
      tarefas: [],
    };
  },
  methods: {
    adicionarLista(text) {
      this.tarefas.push(text);
      this.text = "";
      this.showAlert();
    },
    countDownChanged(dismissCountDown) {
      this.dismissCountDown = dismissCountDown;
    },
    showAlert() {
      this.dismissCountDown = this.dismissSecs;
    },
    removerLista(index) {
      this.tarefas.splice(index, 1);
    },
  },
};
</script>