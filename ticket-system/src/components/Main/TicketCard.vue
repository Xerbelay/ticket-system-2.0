<template>
    <v-dialog max-width="500">
        <template v-slot:activator="{ props: activatorProps }">
            <v-card variant='outlined' width="250px"
                :color="ticket.priority == 'HIGH' ? 'red' : ticket.priority == 'MED' ? 'orange' : 'grey'">
                <v-card-item class="padding">
                    <div>
                        <div class="text-overline mb-1">
                            {{ ticket.from }}
                        </div>
                        <div class="text-h6 mb-1">
                            {{ ticket.summary }}
                        </div>
                        <div class="text-caption ticket_content ticket">{{ ticket.content }}</div>
                    </div>
                </v-card-item>

                <v-card-actions class="flex">
                    <div>
                        <v-btn v-show="user.role == 'user'">
                            <p>Удалить</p>
                        </v-btn>
                        <v-btn v-show="user.role == 'admin' && ticket.status == 'UNDONE'">
                            <p>Ответить</p>
                        </v-btn>
                        <v-btn v-bind="activatorProps">
                            <p>Показать</p>
                        </v-btn>
                    </div>
                </v-card-actions>
            </v-card>
        </template>
        <template v-slot:default="{ isActive }">
            <v-card title="Dialog">
                <v-card-text>
                    <div>
                        <div class="ticket">
                            <p>{{ 'Тема: ' + ticket.summary }}</p>
                            <p>{{ 'Содержание: ' + ticket.content }}</p>
                            <p>Важность: <span :style="{ 'color': ticket.priority == 'HIGH' ? 'red' : ticket.priority == 'MED' ? 'orange' : 'grey' }">{{ticket.priority }}</span></p>
                            <p>{{ 'Пользователь: ' + ticket.from }}</p>
                            <p>Статус: <span :style="{ 'color': ticket.status == 'DONE' ? 'green' : 'red' }">{{ ticket.status }}</span></p>
                            <p>{{ 'Дата создания: ' + ticket.create_date }}</p>
                            <hr class="hr" v-if="ticket.status == 'DONE'">
                            <p v-if="ticket.status == 'DONE'">{{ 'Ответ: ' + ticket.answ }}</p>
                            <p v-if="ticket.status == 'DONE'">{{ 'Дата ответа: ' + ticket.update_date }}</p>
                        </div>
                    </div>
                </v-card-text>

                <v-card-actions>
                    <v-spacer></v-spacer>

                    <v-btn text="Close Dialog" @click="isActive.value = false"></v-btn>
                </v-card-actions>
            </v-card>
        </template>
    </v-dialog>
</template>

<script>
export default {
    props: {
        ticket: Object,
    },
    computed: {
        tickets() {
            return this.$store.state.ticket.tickets
        },
        user() {
            return this.$store.state.user.curUser
        }
    },
}
</script>

<style>
.ticket_content {
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
}

.flex {
    display: flex;
    justify-content: space-around;
    padding-top: 0px;
}
.padding{
    padding-bottom: 0;
}
</style>