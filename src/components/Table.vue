<template>
  <div class="table-component">
    <table class="table table-borderless table-memoria-fisica">
      <thead>
        <tr>
          <th v-for="item in arrColunas">{{ item }}</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="item in arrDados" :bgcolor="corFundo ? corFundo : item.corFundo">
          <td v-for="key in Object.keys(item)" v-if="item[key].indexOf('#') < 0">{{ item[key] }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  props: ["arrDados", "arrColunas", "corFundo"]
};
</script>

<style scoped>
.table {
  font-size: 14px;
  text-align: center;
}
td {
  padding: 0;
  margin: 0;
  font-weight: bold;
}
.table-memoria-fisica {
  background-color: #f0e68c;
  width: 80%;
}
</style>