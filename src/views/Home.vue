<template>
  <div :class="!sunImg.sunBoolean ? 'whitebgcontainer' : 'container'">
    <div class="containerStuff">
      <div class="todoFlex">
        <h1 class="heroLogo">TODO</h1>
        <img v-if="sunImg.sunBoolean" :src="sunImg.url" alt="sun" @click="changeToMoon"/>
        <img v-if="!sunImg.sunBoolean" :src="moonImg.url" alt="moon" @click="changeToMoon"/>
      </div>
      <input 
        type="text"
        placeholder="Create a new todo..."
        @keyup.enter="submitTask"
        v-model="task"
        :class="!sunImg.sunBoolean ? 'whitebg' : 'none'"
      />
    </div>

    <table  :class="!sunImg.sunBoolean ? 'tablebg' : 'table'">
      <tbody>
        <tr v-for="(task, index) in tasksFiltered" :key="index">
          <td>
            <div class="info" :class="!sunImg.sunBoolean ? 'whitebg' : 'none'">
              <input
                type="checkbox"
                v-model="task.complete"
                :id="`task-${index}`"
                class="check_box"
              />
              <label :for="`task-${index}`" class="check_box"></label>
                <p class="para" :class="{ completed: task.complete }">
                {{ task.name }}
                </p>
              <img
                class="cross"
                src="../assets/Cross.svg"
                alt=""
                @click="deleteTask(index)"
              />
            </div>
          </td>
        </tr>
      </tbody>

      <tfoot>
        <tr class="footerText" :class="!sunImg.sunBoolean ? 'whitebg' : 'none'">
          <div class="itemsLeft">
            <p>{{ remaining }} items left</p>
          </div>
          <div class="taskAction">
            <p :class="{ active: filter === 'all' }" @click="filter = 'all'">
              All
            </p>
            <p
              :class="{ active: filter === 'active' }"
              @click="filter = 'active'"
            >
              Active
            </p>
            <p
              :class="{ active: filter === 'completed' }"
              @click="filter = 'completed'"
            >
              Completed
            </p>
          </div>
          <div>
            <p class="clearCompleted" @click="completelyClear">
              {{ clearCompleted }}
            </p>
          </div>
        </tr>
      </tfoot>
    </table>

    <div :class="!sunImg.sunBoolean ? 'whiteBgMobile' : 'taskActionMobile'">
      <p :class="{ active: filter === 'all' }" @click="filter = 'all'">All</p>
      <p :class="{ active: filter === 'active' }" @click="filter = 'active'">
        Active
      </p>
      <p
        :class="{ active: filter === 'completed' }"
        @click="filter = 'completed'"
      >
        Completed
      </p>
    </div>
  </div>
</template>

<script>
import CardVue from "@/components/Card.vue";
export default {
  components: {
    "app-card": CardVue,
  },
  data() {
    return {
      task: "",
      completedImg: require("@/assets/CompletedTask.svg"),
      uncompletedImg: require("@/assets/UncompletedTask.svg"),
      sunImg: {url: require('../assets/CombinedShape.svg'), sunBoolean: true},
      moonImg: {url: require('../assets/Moon.svg'),},
      complete: false,
      clearCompleted: "Clear Completed",
      idForTodo: 3,
      filter: "all",
      tasks: [],
    };
  },
  computed: {
    remaining() {
      return this.tasks.filter((todo) => !todo.complete).length;
    },
    tasksFiltered() {
      if (this.filter === "all") {
        return this.tasks;
      } else if (this.filter === "active") {
        return this.tasks.filter((todo) => !todo.complete);
      } else if (this.filter === "completed") {
        return this.tasks.filter((todo) => todo.complete);
      }

      return this.tasks;
    },
  },
  methods: {
    submitTask() {
      if (this.task.length === 0) return;

      this.tasks.push({
        id: this.idForTodo,
        name: this.task,
        completed: false,
      });

      this.task = "";
      this.idForTodo++;
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
    },
    completedTask() {
      this.tasks.completed = !this.tasks.completed;
      console.log(this.tasks.completed);
      
    },
    completelyClear() {
      this.tasks = this.tasks.filter((todo) => !todo.complete);
    },
    changeToMoon(){
      this.sunImg.sunBoolean = !this.sunImg.sunBoolean
      console.log(this.sunImg.sunBoolean)
      
    }
  },
};
</script>

<style scoped>
/*  start of Moon event styling */
.whitebg{
  background: #FFFFFF;
  color: #393A4B;
  border: none;
  box-shadow: 0px 35px 50px -15px rgba(194, 195, 214, 0.5);
  border-bottom: none;
}

.tablebg{
  background: #FFFFFF;
  box-shadow: 0px 35px 50px -15px rgba(194, 195, 214, 0.5);
  border-radius: 5px;
  position: relative;
  top: -50px;
  margin-left: auto;
  margin-right: auto;
  width: 600px;
}

.whiteBgMobile {
  display: none;
  background: red;
  justify-content: center;
  box-shadow: 0px 35px 50px -15px rgba(194, 195, 214, 0.5);
  border-radius: 5px;
  color: #9495A5;
  text-align: center;
  margin-left: auto;
  margin-right: auto;
  gap: 19px;
}

/* End of Moon event Styling */

.container{
  padding-bottom: 100vh;
  background: black;
  background-size: cover;
}
.containerStuff {
  text-align: center;
  background-image: url("../assets/desktop.jpg");
  background-size: 100% 120%;
  background-repeat: no-repeat;
  padding-bottom: 85px;
}

.todoFlex {
  display: flex;
  text-align: center;
  padding: 70px 812px 48px 335px;
  align-items: center;
}

.heroLogo {
  font-family: "Josefin Sans";
  font-style: normal;
  font-weight: 700;
  font-size: 40px;
  line-height: 40px;
  letter-spacing: 15px;
  color: #ffffff;
  margin-right: 395px;
}

input {
  background: #25273d;
  box-shadow: 0px 35px 50px -15px rgba(0, 0, 0, 0.5);
  border-radius: 5px;
  font-style: normal;
  font-weight: 400;
  font-size: 18px;
  line-height: 18px;
  letter-spacing: -0.25px;
  color: #767992;
  padding: 23px 312px 23px 72px;
  border: none;
}

::placeholder {
  font-family: "Josefin Sans";
  font-style: normal;
  font-weight: 400;
  font-size: 18px;
  line-height: 18px;
  letter-spacing: -0.25px;
  color: #767992;
}

.table {
  position: relative;
  top: -50px;
  background: #25273d;
  box-shadow: 0px 35px 50px -15px rgba(0, 0, 0, 0.5);
  border-radius: 5px;
  margin-left: auto;
  margin-right: auto;
  width: 600px;
}

.footerText {
  display: flex;
  justify-content: space-between;
  font-family: "Josefin Sans";
  font-style: normal;
  font-weight: 700;
  font-size: 14px;
  line-height: 14px;
  letter-spacing: -0.194444px;
  padding: 16px 24px 20px 24px;
}
.itemsLeft {
  margin-right: 96px;
}
.taskAction {
  display: flex;
  gap: 19px;
}

.complete {
  padding: 0px 24px 0px 56px;
}

.info {
  align-items: center;
  padding: 21px 24px 20px 24px;
  border-bottom: 1px solid #393a4b;
  display: flex;
}

.para {
  font-family: "Josefin Sans";
  font-style: normal;
  font-weight: 400;
  font-size: 18px;
  line-height: 18px;
  letter-spacing: -0.25px;
  color: #c8cbe7;
}

.cross {
  position: fixed;
  left: 900px;
  cursor: pointer;
}

.activeClass {
  color: red;
}

.completed {
  color: grey;
}

.active {
  color: #3a7cfd;
}

.active:hover {
  color: #e3e4f1;
}

.taskAction p {
  cursor: pointer;
}

.clearCompleted {
  cursor: pointer;
}

.check_box {
  display: none;
}

.check_box + label {
  background: url("../assets/UncompletedTask.svg") no-repeat;
  height: 30px;
  width: 40px;
  display: inline-block;
  padding: 0 0 0 0px;
}

.check_box:checked + label {
  background: url("../assets/CompletedTask.svg") no-repeat;
  height: 30px;
  width: 40px;
  display: inline-block;
  padding: 0 0 0 0px;
}

.taskActionMobile {
  display: none;
}

@media only screen and (max-width: 375px) {

/*  start of Moon event styling */
.whitebg{
  background: #FFFFFF;
  color: #393A4B;
  border: none;
  box-shadow: 0px 35px 50px -15px rgba(194, 195, 214, 0.5);
  border-bottom: none;
}

.tablebg{
  background: #FFFFFF;
  box-shadow: 0px 35px 50px -15px rgba(194, 195, 214, 0.5);
  border-radius: 5px;
  position: relative;
  top: -30px;
  margin-left: auto;
  margin-right: auto;
  width: 330px;
}


.whiteBgMobile{
  display: flex;
  background: #FFFF;
  justify-content: center;
  width: 330px;
  padding: 15px 0px 19px 0px;
  box-shadow: 0px 35px 50px -15px rgba(194, 195, 214, 0.5);
  border-radius: 5px;
  margin-top: 15px;
}
/* End of Moon event Styling */
.container {
    text-align: center;
  }

  .containerStuff {
    background-image: url("../assets/desktop.jpg");
    text-align: center;
    background-repeat: no-repeat;
  }

  input {
    padding: 18px 130px 18px 52px;
    background: #25273d;
    box-shadow: 0px 35px 50px -15px rgba(0, 0, 0, 0.5);
    border-radius: 5px;
    font-style: normal;
    font-weight: 400;
    font-size: 12px;
    line-height: 12px;
    letter-spacing: -0.166667px;
    color: #767992;
    border: none;
  }

  .todoFlex {
    display: flex;
    text-align: center;
    padding: 48px 0px 40px 0px;
    justify-content: center;
  }

  .heroLogo {
    margin-right: 119px;
  }
  .table {
    margin-top: 16px;
    width: 328px;
  }

  .footerText {
    display: flex;
    justify-content: center;
    padding: 16px 0px 20px 0px;
  }

  .itemsLeft {
    color: #5b5e7e;
  }

  .clearCompleted {
    color: #5b5e7e;
  }

  .cross {
    left: 310px;
    height: 12px;
  }

  .taskAction {
    display: none;
  }

  .taskActionMobile {
    display: inline-flex;
    text-align: center;
    gap: 15px;
    padding: 15px 80px 19px 81px;
    background: #25273d;
    box-shadow: 0px 35px 50px -15px rgba(0, 0, 0, 0.5);
    border-radius: 5px;
  }
}
</style>
