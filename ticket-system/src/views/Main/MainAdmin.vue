<template>
  <v-container>
    <v-row justify="center">
      <v-tabs v-model="tab" color="deep-purple-accent-4" align-tabs="center">
        <v-tab :value="1">Активные</v-tab>
        <v-tab :value="2">Готовые</v-tab>
      </v-tabs>
    </v-row>
    <v-window v-model="tab">
      <v-window-item :value="1">
        <v-container fluid>
          <v-row class="ticket-pos">
            <div v-for="item in ticket" v-show="item.status == 'UNDONE'" class="ticket">
              <TicketCard :ticket="item"  />
            </div>
          </v-row>
        </v-container>
      </v-window-item>
      <v-window-item :value="2">
        <v-container fluid>
          <v-row class="ticket-pos">
            <div v-for="item in ticket" v-show="item.status == 'DONE'" class="ticket">
              <TicketCard :ticket="item" />
            </div>
          </v-row>
        </v-container>
      </v-window-item>
    </v-window>
  </v-container>
</template>
  
<script>
  
  import TicketCard from '../../components/Main/TicketCard'

  export default {
    name: 'MainAdmin',
  
    components: {
      TicketCard,
    },
    computed: {
      ticket(){
        return this.$store.state.ticket.tickets
      },
    },
    data: () => ({
      tab: 1,
    }),
  }
</script>
  
<style>

.ticket-pos{
    display: flex;
    align-items: center;
    justify-content: space-around;
    margin: 0;
  }
  .ticket{
    border-radius: 4px;
    margin: 10px 0 10px 0;
  }
</style>