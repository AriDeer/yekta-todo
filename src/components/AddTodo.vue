<template>
    <div class="add-todo">

        <input placeholder="Add a note..." v-model="model.note">

        <div class="add-todo-footer">

            <!-- Tags [colors, labels] -->
            <div class="tags">
                <div class="colors">

                    <div v-for="(color, index) in colors"
                         :key="index">
                        <input type="radio"
                               :id="`color-${color}`"
                               name="colors"
                               :value="color"
                               v-model="model.selectedColor"
                               hidden>
                        <label :style="`background: rgb(${color})`" :for="`color-${color}`">
                        </label>
                    </div>


                </div>

                <div class="labels">
                    <label for="labels">Priority: </label>
                    <select id="labels" v-model="model.priority">
                        <option :value="2">Low</option>
                        <option :value="1">Medium</option>
                        <option :value="0">High</option>
                    </select>
                </div>
            </div>
            <!-- / Tags [colors, labels] -->

            <!-- Add note button -->
            <button class="button button-primary space-l-5" @click="addNote">Add Note</button>
            <!-- / Add note button -->

        </div>

    </div>
</template>

<script>

    export default {

        name: 'AddTodo',

        data() {
            return {
                model: {
                    note: null,
                    selectedColor: '255, 255, 255',
                    priority: 2,
                },
                colors: [
                    '255, 255, 255',
                    '229, 57, 53',
                    '142, 36, 170',
                    '253, 216, 53',
                    '84, 110, 122'
                ],
            };
        },

        methods: {

            /**
             * Send data to parent
             */
            addNote() {
              this.$emit('add', this.model)
            },
        },

    };

</script>
