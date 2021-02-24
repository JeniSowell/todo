<template>
  <q-page class="flex flex-center">
    <div v-if="todo.length">
      <q-input color="grey-3" label-color="info" outlined v-model="todoName" label="todo name"/>
      <br>
      <q-input color="grey-3" label-color="info" outlined v-model="todoDescription" label="todo description"/>
      <q-btn color="primary" icon="add" label="Ajouter" />
      <br>
      <q-list bordered separator>
        <q-item v-for="(td, index) in todo" :key="index" clickable v-ripple>
          <q-item-section avatar>
            <q-checkbox v-model="completed" />
          </q-item-section>
          <q-item-section>
            <q-item-label>{{td.name}}</q-item-label>
            <q-item-label caption>{{td.description}}</q-item-label>
          </q-item-section>
          <q-item-section side> <q-icon name="delete" class="text-red" @click="removeTodoList(td.id)"/></q-item-section>
        </q-item>
      </q-list>
    </div>
    <div v-else>
      loading...
    </div>
  </q-page>
</template>

<script>
  import gql from 'graphql-tag'
  import DELETE_LIST from '../graphql/mutations/delete.gql'
  import ADD_LIST from '../graphql/mutations/insert.gql'
  const todoQuery = gql`
  query MyTodo {
    todo {
      id
      description
      name
      is_completed
    }
  }
  `
  export default {
    name: 'PageIndex',
    data() {
      return {
        todo: [],
        completed: [],
        todoName: '',
        todoDescription: '',
      }
    },
    apollo: {
      todo: {
        query: todoQuery,
      },
    },
    methods: {
    async removeTodoList(listId){
      await this.$apollo.mutate({
          mutation: DELETE_LIST,
          variables: {
            id: listId
          },
          refetchQueries: [
            {
              query: todoQuery
            }       
            
          ]

      })
    },
    async addTodoList(name, description) {
      await this.$apollo.mutate({
        mutation: ADD_LIST,
        variables: {    
            name,
            description,
        }
      })
      }
    }
  }
</script>
