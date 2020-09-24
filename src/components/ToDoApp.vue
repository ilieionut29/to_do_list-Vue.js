<template>
    <div id="toDoApp">
        <app-image-slider></app-image-slider>
        <ul class="list-group task-list">
            <transition-group name="slide">
                <li class="list-group-item task-li" 
                    v-for="(task, index) in taskList" :key="task"> 

                    <input type="checkbox" class="checkmark" v-model="task.check" true-value="yes" false-value="no">
                    <span class="task-line" 
                        :style="[task.check === 'no' ? {'text-decoration':'none'} : {'text-decoration':'line-through', 'color':'#718093'}]">
                            {{ task.description }} 
                    </span>

                    <button @click="removeTask(index)" class="remove-button">♻️</button>
                </li>
            </transition-group>
        </ul>

        <div class="textarea-zone">
            <div class="remaining-chr">Remaining characters: {{ textLength }} / 100</div>
            <b-form-textarea
                id="textarea-state"
                v-model="newTask"
                :state="newTask.length >= 7"
                placeholder="✍️ Add new task here ..."
                rows="2"
                maxlength="100"
                @keyup="countLetters"
                @change="countLetters">
            </b-form-textarea>
            <button class="btn new-task-button" @click="addNewTask()">NEW TASK</button>
        </div>
    </div>
</template>

<script>
import ImageSlider from "./ImageSlider.vue";

export default {
    data() {
        return {
            newTask: "",
            taskList: [],
            textLength: 0,
        }
    },
    methods: {
        countLetters() {
            this.textLength = this.newTask.length;
        },
        addNewTask() {
            let spaceRemove = this.newTask.replace(/\s/g, "");
            let newTaskWithoutSpace = spaceRemove;

            if (newTaskWithoutSpace.length >= 7) {
                this.taskList.push({check: "no", description: this.newTask})
                this.newTask = "";
                this.textLength = 0;
            }
        },
        removeTask(index) {
            this.taskList.splice(index, 1);
        }
    },
    components: {
        appImageSlider: ImageSlider
    }
}
</script>

<style scoped>
#toDoApp {
    max-width: 310px;
    margin: 10px auto;
}

.textarea-zone {
    margin-top: 13px;
    padding: 2px;
}

#textarea-state {
    resize: none;
    font-family: 'Roboto', sans-serif;
    font-size: 0.8rem;
    max-width: 310px;
}

.remaining-chr {
    color: #0c2461;
    font-family: 'Ubuntu', sans-serif;
    font-size: 0.65rem;
    transition: 0.2s;
    margin-bottom: 4px;
    margin-left: 4px;
}

.new-task-button {
    margin-top: 7px;
	padding: 12px 24px;
    outline: none;
    border: none;
    background-color: #0c2461;
    color: #f7f1e3;
    font-family: 'Tomorrow', sans-serif;
    border-radius: 8px;
    text-align: center;
    max-width: 130px;
    min-width: 130px;
    font-size: 0.8rem;
    transition: 0.4s ease-in-out;
}
.new-task-button:hover {
    letter-spacing: 0.7px;
    font-weight: 520;
    box-shadow: 0px 0px 4px #2e4175;
    background-color: #273c75;
    color: #f7f1e3;
}

.task-list {
    font-family: 'Roboto', sans-serif;
    font-size: 0.9rem;
    max-width: 310px;
    color: #0c2461;
    border: 1px rgba(83, 92, 104,0.6);
    margin-top: 1px;
}
.list-group-item {
    border: none;
}


.task-li {
    border-bottom: 1px solid rgba(83, 92, 104,0.6);
    border-top: none;
    border-left: none;
    border-right: none;
    word-break: break-all;
    word-spacing: normal;
}
.task-li:first-child {
    border-top: 1px solid rgba(83, 92, 104,0.6);
    border-left: none;
    border-right: none;
    border-top-left-radius: 10px;
    border-top-right-radius: 10px;
}
.task-line {
    font-family: 'Caladea', serif;
    font-size: 0.85rem;
    color:  #130f40;
    display: block;
    max-width: 95%;
    font-weight: 550;
}

.remove-button {
    outline: none;
    border: none;
    font-size: 1rem;
    background: none;
    position: absolute;
    right: 5px;
    bottom: 9px;
    transition: ease-in-out 1s;
}
.remove-button:hover {
    animation: rotate infinite 2s; 
}

.checkmark {
  position: absolute;
  top: 17px;
  left: 3px;
  height: 11px;
  width: 11px;
}

.slide-enter {
    opacity: 0;
}

.slide-enter-active {
    animation: slide-in ease-out forwards;
    transition: opacity .5s;
}



.slide-leave-active {
    animation: slide-out 1s ease-out forwards;
    transition: opacity 1s;
    opacity: 0;
    position: absolute;
}

.slide-move {
    transition: transform 1s;
}

@keyframes slide-in {
    from {
        transform: translateY(20px);
    }
    to {
        transform: translateY(0)
    }
}

@keyframes slide-out {
    from {
        transform: translateY(0)
    }
    to {
        transform: translateY(20px);
    }
}

@keyframes rotate {
    0% {
        transform: rotate(0deg);
    }
    50% {
        transform: rotate(250deg);
    }
    0% {
        transform: rotate(0deg);
    }
}
</style>
