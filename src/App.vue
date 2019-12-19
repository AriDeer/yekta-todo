<template>
    <div id="app">
        <div class="container">

            <img class="logo" src="./assets/images/logo.png" alt="yektanet">

            <AddTodo @add="addTodo"/>

            <h4 class="sectionTitle">Pined:</h4>
            <template v-if="pin.length">
                <Item v-for="(item, index) in pin"
                      :key="item.note.replace(/\s+/g, '-')"
                      :data="item"
                      @done="checkToDone(item, index)"
                      @pin-unpin="togglePin(item, index)"/>
            </template>

            <empty v-else />


            <h4 class="sectionTitle">Todo:</h4>
            <template v-if="todo.length">
                <Item v-for="(item, index) in todo"
                      :key="item.note.replace(/\s+/g, '-')"
                      :data="item"
                      @done="checkToDone(item, index)"
                      @pin-unpin="togglePin(item, index)"/>
            </template>

            <empty v-else />


            <h4 class="sectionTitle">Done:</h4>
            <template v-if="done.length">
                <Item v-for="(item) in done"
                      :key="item.note.replace(/\s+/g, '-')"
                      :data="item"/>
            </template>

            <empty v-else />

        </div>
    </div>
</template>

<script>

    import AddTodo from '@/components/AddTodo.vue';
    import Item from '@/components/Item.vue';
    import empty from '@/components/Empty.vue';

    export default {

        name: 'App',

        components: {AddTodo, Item, empty},

        data() {
            return {
                pin: [],
                todo: [],
                done: []
            };
        },

        methods: {

            /**
             * This func add a note to todo_array
             * @param payload
             */
            addTodo(payload) {
                this.todo.unshift({
                    ...payload,
                    isPin: false,
                    isDone: false
                });

                this.sortByPriority(this.todo);
            },

            /**
             * Pin and Unpin
             *
             * @param item
             * @param index
             */
            togglePin(item, index) {

                if (item.isPin) {

                    item.isPin = false;
                    this.pin.splice(index, 1);
                    this.todo.unshift(item);

                    this.sortByPriority(this.todo);

                } else {

                    item.isPin = true;
                    this.todo.splice(index, 1);
                    this.pin.unshift(item);

                }
            },

            /**
             * Send note to done
             *
             * @param item
             * @param index
             */
            checkToDone(item, index) {
                item.isDone = true;
                this.todo.splice(index, 1);
                this.pin.splice(index, 1);
                this.done.unshift(item);
            },

            /**
             * Sort array by priority
             *
             * @param array
             */
            sortByPriority(array) {
                array.sort((a, b) => {
                    return a.priority - b.priority
                });
            }
        }

    };

</script>
