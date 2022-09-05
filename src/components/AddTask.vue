<template>
    <div>
        <form @submit.prevent="handleSubmit">
            <div class="form-input">
                <label>Text</label>
                <input v-model="text" type="text" placeholder="new task goes here..." />
            </div>
            <div class="form-input">
                <label>Day</label>
                <input v-model="day" type="text" placeholder="September 6, 2004" />
            </div>
            <div class="form-input checkbox">
                <input v-model="reminder" type="checkbox" />
                <label>Set Reminder?</label>
            </div>
            <div class="button">
                <input type="submit" value="Save Task" />
            </div>
        </form>
        <div class="border"></div>
    </div>
</template>

<script>
export default {
    name: "AddTask",
    data() {
        return {
            text: '',
            day: '',
            reminder: false
        }
    },
    methods: {
        handleSubmit() {
            if (!this.text) {
                alert('Please enter a task');
            }  
            const newTask = {
                text: this.text,
                day: this.day,
                reminder: this.reminder
            };
            this.$emit('add-task', newTask);
            this.text = '';
            this.day = '';
            this.reminder = false;
        }
    }
}
</script>

<style>
.form-input {
    display: flex;
    flex-direction: column;
    margin-bottom: 10px;
}
.form-input label {
    font-size: 1.2rem;
    font-weight: bold;
    margin-bottom: 5px;
}
.form-input input {
    padding: 5px;
    border: 1px solid #ccc;
    border-radius: 5px;
}
.form-input.checkbox {
    display: flex;
    flex-direction: row;
    align-items: center;
}
.form-input.checkbox input {
    margin-right: 5px;
}
.form-input.checkbox label {
    font-size: 1rem;
    font-weight: normal;
}
.border {
    border-bottom: 1px solid #ccc;
    margin-bottom: 20px;
}
.button {
    display: flex;
    justify-content: right;
}
.button input {
    padding: 5px 10px;
    border: 1px solid #ccc;
    border-radius: 5px;
    background-color: #000e6d;
    color: #fff;
    cursor: pointer;
    margin-bottom: 20px;
}
</style>