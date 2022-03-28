<template>
  <header class="header-wrapper">
    <div class="title">
      <v-icon>mdi-chart-box-outline</v-icon>
      <h1>Construtor de Gráficos</h1>
    </div>
    <h3 class="subtitle">Ferramenta de Desenvolvimento de Gráficos</h3>
  </header>
</template>

<script>
export default {
  name: "HeaderComp",
};
</script>

<style>
.header-wrapper {
  align-items: center;
  background: var(--blue-grey-darken-1);
  color: var(--grey-lighten-4);
  display: flex;
  flex-direction: column;
  font-family: var(--fontPrimary);
  padding: 16px;
}
.title {
  align-items: center;
  display: flex;
}
.title > h1 {
  font-size: 22px;
  font-weight: 700;
  margin-left: 8px;
}
.title > .v-icon.v-icon {
  color: currentColor;
  font-size: 32px !important;
}
.subtitle {
  font-size: 16px;
  font-weight: 400;
  margin-top: 8px;
}

@media only screen and (min-width: 600px) {
  .header-wrapper {
    align-items: center;
    flex-direction: row;
    justify-content: space-between;
  }
  .title > h1 {
    font-size: 36px;
  }
  .title > .v-icon.v-icon {
    font-size: 56px !important;
  }
  .subtitle {
    font-size: 22px;
    margin-left: 16px;
    margin-top: 0;
  }
}
</style>