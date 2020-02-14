<template>
  <v-container>
    <v-layout text-center wrap>
      <v-card class="mx-auto" max-width="400" tile>
        <v-form v-model="valid">
          <v-container>
            <v-row>
              <v-col cols="12" md="12">
                <v-text-field v-model="title" :rules="titleRules" label="Title" required></v-text-field>
              </v-col>

              <v-col cols="12" md="12">
                <v-textarea v-model="content" label="Content" required></v-textarea>
                <v-col class="text-center" cols="12" sm="4">
                  <div class="my-2">
                    <v-btn color="primary" @click="buttonClicked" :disabled="!valid">Send</v-btn>
                  </div>
                </v-col>
              </v-col>
            </v-row>
          </v-container>
        </v-form>
        <v-container>
          <v-layout text-center wrap>
            <v-card class="mx-auto" max-width="400" tile>
              <v-list-item v-if="!todos.length">
                <v-list-item-content>
                  <v-list-item-title>The list is empty</v-list-item-title>
                </v-list-item-content>
              </v-list-item>
              <v-list-item v-else v-for="(item, index) in todos" :key="item.id">
                <v-list-item-content>
                  <v-list-item-title>{{ item.title}}</v-list-item-title>
                  <v-list-item-subtitle>{{ item.content }}</v-list-item-subtitle>
                  <v-btn color="error" @click="deleteItem(index)">Delete</v-btn>
                </v-list-item-content>
              </v-list-item>
            </v-card>
          </v-layout>
        </v-container>
      </v-card>
    </v-layout>
  </v-container>
</template>

<script>
export default {
  name: 'HelloWorld',

  data: () => ({
    valid: false,
    title: '',
    content: '',
    todos: [],
    titleRules: [v => !!v || 'Title is required']
  }),
  methods: {
    buttonClicked () {
      if (!this.valid) return
      let id
      if (this.todos.length) {
        id = this.todos[this.todos.length - 1].id + 1
      } else {
        id = 0
      }
      this.todos.push({
        id,
        title: this.title,
        content: this.content
      })
      console.log('TODO: ', JSON.parse(JSON.stringify(this.todos)))
    },
    deleteItem (index) {
      this.todos.splice(index, 1)
    }
  }
}
</script>
