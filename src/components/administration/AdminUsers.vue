<template>
  <div>
    <admin-user-dialog />
          <v-data-table :headers="headers" :items="users" :loading="loading" class="elevation-1" :no-data-text="$t('admin.usersTable.empty')" >
            <template slot="items" slot-scope="props">

              <td class="text-xs-right">{{ props.item.uid }}</td>
              <td class="text-xs-right">{{ props.item.email }}</td>
              <td class="text-xs-right">{{ props.item.username }}</td>
              <td class="text-xs-right">{{ props.item.role }}</td>

              <td class="justify-center layout px-0">
                <v-btn icon class="mx-0" @click="editUser(props.item)">
                  <v-icon color="teal">edit</v-icon>
                </v-btn>

                <v-btn icon class="mx-0" @click="removeUser(props.item)">
                  <v-icon color="pink">delete</v-icon>
                </v-btn>
              </td>

            </template>
    </v-data-table>
  </div>
</template>

<script>
  import AdminUserDialog from '@/components/administration/AdminUserDialog';
  import {db} from '@/main';

    export default {
      name: "admin-users",
      components: {AdminUserDialog},
      data() {
        return {
          headers: [
            {text: this.$t('admin.usersTable.uid'), value: 'uid', align: 'center'},
            {text: this.$t('admin.usersTable.email'), value: 'email', align: 'center'},
            {text: this.$t('admin.usersTable.username'), value: 'username', align: 'center'},
            {text: this.$t('admin.usersTable.role'), value: 'role', align: 'center'},
            {text: this.$t('common.actions'), value: 'name', sortable: false}
          ],
          users: [],
          loading: true,
        }
      },
        mounted(){
          this.loading = true;
          db.collection('users').onSnapshot(snapshot => {
            this.users = [];
            snapshot.forEach(user => {
              const userData = user.data();
              console.log(userData);
              this.users.push({
                uid: userData.uid,
                email: userData.email,
                username: userData.username || '----',
                role : userData.role || '----'
              });
            });
            this.loading = false;
          }, (error) => {
            console.log('listener users admin off...');
          })
        },

      methods: {
        editUser (user)
        {
          if(confirm ('Deseas a Editar este usuario'))
          this.$store.commit('toggleUsersDialog', {
            editMode: true, user
          });
        },
        removeUser (user) {
          if(confirm ('¿ Seguro de eliminar este usuario ?' ))
          db.collection('users').doc(user.uid).delete().then(() => {
            this.$store.commit('setalertMessage', {
              show: true,
              type: 'success',
              message: this.$t('messages.deleted', {item: this.$t('common.user')}),
              timeout: 5000
            });
          });
        }
      }
    }
</script>

