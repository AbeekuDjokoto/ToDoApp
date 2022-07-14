<template>
  <div class="container">
    <div class="containerStuff">
      <div class="todoFlex">
        <h1 class="heroLogo">TODO</h1>
        <img src="../assets/CombinedShape.svg" alt="sun" />
      </div>
      <input
        type="text"
        placeholder="Create a new todo..."
        @keyup.enter="submitTask"
        v-model="task"
      />
    </div>

    <table class="table">
      <tbody>
        <tr v-for="(task, index) in tasks" :key="index">
          <td>
            <div class="info">
              
              <img v-if="complete" :src="uncompletedImg" alt="" @click="completedTask(index)"/>
              <img v-if="!complete" :src="completedImg" alt="" @click="completedTask(index)"/>
              <p class="para">{{ task.name }}</p>
              <img class="cross" src="../assets/Cross.svg" alt="" @click="deleteTask(index)"/>
            </div>
          </td>
        </tr>
      </tbody>
      <tfoot>
        <tr class="footerText">
          <div class="itemsLeft">
            <p>5 items left</p>
          </div>
          <div class="taskAction">
            <p>All</p>
            <p>Active</p>
            <p>Completed</p>
          </div>
          <div class="completed">
            <p @click="completelyClear">{{ clearCompleted }}</p>
          </div>
        </tr>
      </tfoot>
    </table>
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
      completedImg: require('@/assets/CompletedTask.svg'),
      uncompletedImg: require('@/assets/UncompletedTask.svg'),
      complete: true,
      clearCompleted: 'Clear Completed',
      tasks: [
        { name: "Steal bananas from the store", uncompletedImg: require('@/assets/UncompletedTask.svg'), complete: false},
        { name: "Steal bananas from the store" },
      ],
    };
  },
  methods: {
    submitTask() {
      if (this.task.length === 0) return;

      this.tasks.push({
        name: this.task,
      });

      this.task = "";
    },
    deleteTask(index){
        this.tasks.splice(index, 1);
    },
    completedTask(index){
      //  this.tasks[index].complete = !this.tasks[index].complete
      //  console.log(this.tasks[index].complete)
      //  if(this.tasks[index].complete = true){
      //   this.tasks[index].uncompletedImg = this.completedImg
      //  } else {
      //   this.tasks[index].uncompletedImg
      //  }
      this.complete = !this.complete
    },
    completelyClear(){
      this.tasks.splice(0, this.task.length)
      console.log('clicked')
      console.log(this.tasks.splice(0, this.task.length))
    }
  },
};
</script>

<style scoped>
.container {
  height: 100vh;
  background: linear-gradient(
    to bottom,
    #480ca8 0%,
    #480ca8 50%,
    #03071e 50%,
    #03071e 100%
  );
}

.containerStuff {
  text-align: center;
}

.todoFlex {
  display: flex;
  text-align: center;
  padding: 70px 812px 48px 335px;
  align-items: center;
}

/* .crossFlex{
    position: relative;
    left: 500px;
} */

.heroLogo {
  font-family: "Josefin Sans";
  font-style: normal;
  font-weight: 700;
  font-size: 40px;
  line-height: 40px;
  /* identical to box height */
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
  /* identical to box height */
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
  /* identical to box height */
  letter-spacing: -0.25px;
  color: #767992;
}

.table {
  margin-top: 5px;
  background: #25273d;
  box-shadow: 0px 35px 50px -15px rgba(0, 0, 0, 0.5);
  border-radius: 5px;
  margin-left: auto;
  margin-right: auto;
  margin-top: 24px;
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
  /* identical to box height */
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
  /* identical to box height */
  letter-spacing: -0.25px;
  color: #c8cbe7;
  margin-left: 24px;
}

.cross {
  position: fixed;
  left: 900px;
  cursor: pointer;
}

.cross:hover {
  background-color: red;
}

.activeClass{
    color: red
}

@media only screen and (max-width: 375px) {
  .container {
    background: linear-gradient(
      to bottom,
      #480ca8 0%,
      #480ca8 35%,
      #03071e 35%,
      #03071e 100%
    );
    text-align: center;
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
    /* identical to box height */
    letter-spacing: -0.166667px;
    color: #767992;
    border: none;
  }

  .todoFlex {
    display: flex;
    text-align: center;
    padding: 48px 0px 40px 26px;
  }

  .heroLogo {
    margin-right: 119px;
  }
}
</style>
