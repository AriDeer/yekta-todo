<template>
    <div class="todo-item"
         :style="data.selectedColor ? `background: rgba(${data.selectedColor}, .05)` : ''">

        <h3> {{ data.note }} </h3>

        <div class="todo-item-footer">

            <span class="priority">
                <span v-if="data.priority === 0"> High </span>
                <span v-else-if="data.priority === 1"> Medium </span>
                <span v-else> Low </span>
                Priority
            </span>

            <template v-if="data.isDone === false">
                <button class="pin" @click="togglePin">
                    <img src="@/assets/images/icons/pin.svg" alt="">
                    {{ data.isPin ? 'Unpin' : 'Pin' }}
                </button>

                <button class="done" @click="done">
                    Check to Done
                </button>
            </template>
        </div>

    </div>
</template>

<script>

    export default {

        name: 'TodoItem',

        props: {

            data: {
                type: Object,
                require: true
            },
        },

        methods: {

            /**
             * Pin and Unpin
             */
            togglePin() {
                this.$emit('pin-unpin')
            },

            /**
             * Done note
             */
            done() {
                this.$emit('done')
            },
        }

    };

</script>
