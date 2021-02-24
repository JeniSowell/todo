<template>
  <q-page class="flex flex-center">
    <div v-if="todo.length">
      <q-input color="grey-3" label-color="info" outlined v-model="newTodo" label="todo">
        <template v-slot:append>
          <q-icon name="add" color="primary" />
        </template>
      </q-input>
      <q-list bordered separator>
        <q-item v-for="(td,index) in todo" :key="index" clickable v-ripple>
          <q-item-section avatar>
            <q-checkbox v-model="completed" />
          </q-item-section>
          <q-item-section>
            <q-item-label>{{td.name}}</q-item-label>
            <q-item-label caption>{{td.description}}</q-item-label>
          </q-item-section>
          <q-item-section side> <q-icon name="delete" class="text-red" click="removeTodo(td.id)"/></q-item-section>
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
  import ADD_TODO from '../graphql/mutations/insert.gql'
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
        newTodo: '',
        apollo: {
          todo: {
            query: todoQuery,
          },
        },
      }
    },
    created(){
      // console.log(DELETE_LIST)
    }
    methods: {
    async removeTodo(listId){
      await this.$apollo.mutate({
          mutation: REMOVE_BOOK,
          variables: {
            id: listId
          },
          refetchQueries: [
            {
              query: DELETE_LIST
            }       
            
          ]
      })
    },
    addTodoList() {
      await this.$apollo.mutate({
        mutation: ADD_BOOKS,
        variables: {    
            description,
            title,
            written_by
        }
      }).then(() =&gt; {
          this.$router.push({path: '/'})
      }).catch(err =&gt; console.log(err))
      }
    }
  }
</script>
