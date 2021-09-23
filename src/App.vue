<template>
  <div class="globalContainer d-flex align-items-center justify-content-center">
    <div v-if="alert" class="alert alert-primary" role="alert">
      This is a primary alert—check it out!
    </div>

    <form>
      <h1 class="title">🖥️ To do Application 🖥️</h1>
      <span class="data">🗓️ {{ dataOdierna }} </span>
      <hr />
      <div class="d-flex gap">
        <div class="d-flex flex-column flex-grow-1">
          <label for="text">Titolo Task :</label>
          <input
            type="text"
            v-model="userData.textValue"
            id="text"
            maxlength="50"
            class="inputFields"
            placeholder="Inserisci un titolo"
          />
          <br />
          <label for="text">Descrizione :</label>
          <input
            type="text"
            v-model="userData.textValueDescription"
            id="text"
            maxlength="50"
            class="inputFields"
            placeholder="Inserisci una descrizione"
          />
          <div>
            <button
              @click.prevent="addTask"
              class="btn btn-outline-success btn-lg but"
            >
              Aggiungi
            </button>
            <button
              @click.prevent="deleteAll"
              class="btn btn-outline-danger btn-lg but"
            >
              Elimina lista
            </button>
            <hr />
          </div>
          <div class="flex-grow-1 mt-5">
            <div class="panel panel-default opacity">
              <div class="panel-heading">
                <h3>Lista task cancellati: ❌</h3>
              </div>
              <div class="panel-body">
                <ul>
                  <li :key="j" v-for="(taskDel, j) in tasksDeleted">
                    <b>Task n°:</b> {{ j + 1 }} <br />
                    <b>Titolo:</b> {{ taskDel[0] }} <br />
                    <b>Descrizione:</b> {{ taskDel[1] }} <br />
                    <button
                      class="btn btn-outline-success btn-lg but"
                      @click.prevent="resume(j)"
                    >
                      Ripristina
                    </button>
                    <button
                      class="btn btn-outline-danger btn-lg but"
                      @click.prevent="deleteDefinitely(j)"
                    >
                      Cancella Definitivamente
                    </button>
                  </li>
                </ul>
              </div>
            </div>
          </div>
        </div>
        <div class="flex-grow-1 panel panel-default opacity">
          <div class="panel-heading">
            <h3>Lista task: 📃</h3>
          </div>
          <div class="panel-body">
            <ul>
              <li :key="i" v-for="(task, i) in tasksArray">
                <b>Task n°:</b> {{ i + 1 }} <br />
                <b>Titolo:</b> {{ task[0] }} <br />
                <b>Descrizione:</b> {{ task[1] }} <br />
                <button
                  class="btn btn-outline-danger btn-lg but"
                  @click.prevent="deleteTask(i)"
                >
                  Cancella
                </button>
              </li>
            </ul>
          </div>
        </div>
      </div>
    </form>
    <hr />

    <div class="d-flex gap"></div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      tasksArray: [],
      tasksDeleted: [],
      userData: {
        textValue: "",
        textValueDescription: "",
      },
      dataOdierna: "",
    };
  },
  created() {
    setInterval(this.getNow, 1000);
  },
  mounted() {
    //per il local storage (https://vuejs.org/v2/cookbook/client-side-storage.html)
    if (localStorage.getItem("tasksArray")) {
      try {
        this.tasksArray = JSON.parse(localStorage.getItem("tasksArray")); //serve ad analizzare il formato testuale (stringa) di JSON e a costruire il valore JavaScript o l'oggetto
      } catch (e) {
        console.log(e);
      }
    }
  },

  methods: {
    getNow() {
      const today = new Date();
      const date =
        today.getDate() +
        "/" +
        (today.getMonth() + 1) +
        "/" +
        today.getFullYear();

      const time =
        today.getHours() + ":" + today.getMinutes() + ":" + today.getSeconds();
      const dateTime = date + " " + time;
      this.dataOdierna = dateTime;
    },
    localStorageMethod() {
      const parsed = JSON.stringify(this.tasksArray); // per il local storage
      localStorage.setItem("tasksArray", parsed);
    },
    addTask() {
      if (this.tasksArray.length < 5) {
        if (
          this.userData.textValue != "" ||
          this.userData.textValueDescription != ""
        ) {
          this.tasksArray.push([
            this.userData.textValue,
            this.userData.textValueDescription,
          ]);
          this.userData.textValue = "";
          this.userData.textValueDescription = "";
          this.localStorageMethod();
        } else {
          alert("Secondo te cosa inserisco se non hai scritto nulla????");
        }
      } else {
        alert("Si,sono un 3310...ho già finito la memoria");
      }
    },

    deleteTask(index) {
      this.tasksDeleted.push(this.tasksArray[index]);
      this.tasksArray.splice(index, 1);
      this.localStorageMethod();
    },
    deleteAll() {
      if (this.tasksArray.length > 0) {
        this.tasksArray = [];
        this.localStorageMethod();
      } else {
        alert("la lista è gia vuota");
      }
    },

    resume(i) {
      this.tasksArray.push(this.tasksDeleted[i]);
      this.tasksDeleted.splice(i, 1);
      this.localStorageMethod();
    },

    deleteDefinitely(i) {
      this.tasksDeleted.splice(i, 1);
    },
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Roboto:wght@100&family=Shadows+Into+Light&display=swap");
@import url("https://fonts.googleapis.com/css2?family=Indie+Flower&display=swap");
li {
  padding: 1rem;
  font-size: 2rem;
  font-family: "Shadows Into Light", cursive;
}

.gap {
  gap: 50px;
}

label {
  font-size: 2rem;
  font-family: "Indie Flower", cursive;
  font-weight: bolder;
  color: white;
}

.title {
  color: white;
}
.inputFields {
  font-size: 1.8rem;
  border-style: inset;
  border-color: currentColor;
  margin-bottom: 1.5rem;
  border-radius: 5px;
  padding: 0.7rem;
  width: 100%;
  opacity: 0.7;
  font-family: "Indie Flower", cursive;
  font-weight: bolder;
}

.data {
  color: white;
  font-size: 3rem;
  font-family: "Indie Flower", cursive;
}

.inputFields::placeholder {
  font-family: "Indie Flower", cursive;
}

h1,
h2,
h3,
h4,
h5 {
  font-family: "Indie Flower", cursive;
  font-weight: bolder;
  text-transform: capitalize;
}

.globalContainer {
  height: 100vh;
  background-image: url(https://static.vecteezy.com/ti/foto-gratuito/p1/1854615-bolle-su-sfondo-nero-gratuito-foto.jpg);
  background-position: center;
  background-size: cover;
  background-repeat: no-repeat;
}

form {
  width: 70%;
  padding: 2rem;

  box-shadow: 0 8px 32px 0 rgba(31, 38, 135, 0.37);
  backdrop-filter: blur(5px);
  -webkit-backdrop-filter: blur(5px);
  border-radius: 10px;
  border: 1px solid rgba(255, 255, 255, 0.18);
}

.opacity {
  opacity: 0.7;
}

.but {
  margin-right: 2rem;
  margin-top: 1rem;
  padding: 0.8rem;
  font-size: 1.7rem;
}
ul {
  position: relative;
  list-style: none;
  margin-left: 0;
  padding-left: 2.2em;
}
ul li:before {
  content: "📌";
  position: absolute;
  left: 0;
}
</style>
