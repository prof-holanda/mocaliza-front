<script setup>
  import { ref, onMounted } from 'vue';

  const headers = ref([
    { title: 'ID', align: 'start', key: 'id', sortable: false, },
    { title: 'Nome', key: 'name' },
    { title: 'Actions', key: 'actions', sortable: false,  align: 'end' },
  ]);

  const categories = ref([]);
  const dialog = ref(false);
  const dialogDelete = ref(false);
  const editedItem = ref({});

  const initialize = () => {
    categories.value = [
      { id: 1, name: 'Category 1' },
      { id: 2, name: 'Category 2' },
      { id: 3, name: 'Category 3' },
    ];
  };

  onMounted(() => {
    initialize();
  });

  const editItem = (item) => {
    console.log('Edit item', item);
  };

  const deleteItem = (item) => {
    console.log('Delete item', item);
  };

  const close = () => {
    this.dialog.value = false;
  };

  const save = () => {
    console.log('Save item', this.editedItem.value);
  };

  const closeDelete = () => {
    this.dialogDelete.value = false;
  };

  const deleteItemConfirm = () => {
    console.log('Delete item', this.editedItem.value);
  };

  const formTitle = ref('Nova Categoria');
</script>

<template>
  <v-data-table
    :headers="headers"
    :items="categories"
    :sort-by="[{ key: 'id', order: 'asc' }]"
  >
    <template v-slot:top>
      <v-toolbar
        flat
      >
        <v-toolbar-title>Categorias</v-toolbar-title>
      </v-toolbar>
      <v-dialog
        v-model="dialog"
        max-width="500px"
      >
        <template v-slot:activator="{ props }">
          <v-col
            cols="12"
            sm="6"
            md="3"
            >
            <v-btn
              color="primary"
              class="mb-2"
              v-bind="props"
            >
              Nova Categoria
            </v-btn>
          </v-col>
        </template>
        <v-card>
          <v-card-title>
            <span class="text-h5">{{ formTitle }}</span>
          </v-card-title>

          <v-card-text>
            <v-container>
              <v-row>
                <v-col
                  cols="12"
                  sm="12"
                  md="12"
                >
                  <v-text-field
                    v-model="editedItem.name"
                    label="Nome da Categoria"
                  ></v-text-field>
                </v-col>
              </v-row>
            </v-container>
          </v-card-text>

          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn
              color="blue-darken-1"
              variant="text"
              @click="close"
            >
              Cancel
            </v-btn>
            <v-btn
              color="blue-darken-1"
              variant="text"
              @click="save"
            >
              Save
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>
      <v-dialog v-model="dialogDelete" max-width="500px">
        <v-card>
          <v-card-title class="text-h5">Você deseja remover esse item?</v-card-title>
          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn color="blue-darken-1" variant="text" @click="closeDelete">Cancelar</v-btn>
            <v-btn color="blue-darken-1" variant="text" @click="deleteItemConfirm">OK</v-btn>
            <v-spacer></v-spacer>
          </v-card-actions>
        </v-card>
      </v-dialog>
    </template>
    <template v-slot:item.actions="{ item }">
      <v-icon
        size="small"
        class="me-2"
        @click="editItem(item)"
      >
        mdi-pencil
      </v-icon>
      <v-icon
        size="small"
        @click="deleteItem(item)"
      >
        mdi-delete
      </v-icon>
    </template>
    <template v-slot:no-data>
      <v-btn
        color="primary"
        @click="initialize"
      >
        Reset
      </v-btn>
    </template>
  </v-data-table>
</template>

<style scoped>

</style>
