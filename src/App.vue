<template>
  <div class="min-h-screen bg-gradient-to-br from-purple-600 to-blue-500 p-8 flex items-center justify-center">
    <div class="max-w-2xl w-full bg-white rounded-2xl shadow-2xl p-8">
      <h1 class="text-4xl font-extrabold text-gray-800 mb-8 text-center">Todo list</h1>

      <div class="mb-4 text-center text-lg">
        <!-- dinamički dohvat varijable iz js-a-->
        <p class="font-semibold text-gray-600">Broj zadataka: {{ taskCount }}</p>
      </div>

      <div class="flex mb-6 justify-center">
        <!-- HTML element za korisnički input-->
         <!-- ako stisnemo enter, dodamo task-->
        <!-- isto tako, ako stisnemo botun, dodamo task-->  
        <input 
          v-model="newTask" 
          @keyup.enter="addTask" 
          placeholder="Add new task..."
          class="flex-1 p-4 text-lg border border-gray-300 rounded-l-xl focus:outline-none focus:ring-2 focus:ring-purple-500"
        />
        <button
          @click="addTask"
          class="bg-purple-600 text-white px-6 py-4 rounded-r-xl hover:bg-purple-800 transition-all"
        >
          ➕ Add
        </button>
      </div>

      <!-- Poruka ako nema zadataka -->
      <p v-if="tasks.length === 0" class="text-center text-lg text-gray-500">
        Nema zadataka. Dodaj neki!
      </p>

      <!-- lista taskova -->
      <ul v-if="tasks.length > 0" class="space-y-4">
        <!-- v-for iterira kroz sve unesene taskove u tasks arrayu i dohvaća ih po indexu -->
        <li v-for="(task, index) in tasks" :key="index"  
            class="flex items-center justify-between p-4 rounded-xl shadow-sm transition-all duration-300">
          
          <!-- Text zadatka -->
          <div :class="text-lg">
            {{ task.text }}
          </div>

          <!-- Div za sekciju s buttonima -->
          <div class="space-x-3">
            <!-- S @click povezujemo button i metodu. Metoda se poziva za onaj task koji se nalazi na proslijeđenom indexu -->
            <button @click="editTask(index)" class="text-blue-500 hover:text-blue-700 text-xl">
              ✏️
            </button>
            <button @click="deleteTask(index)" class="text-red-500 hover:text-red-700 text-xl">
              ❌
            </button>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  // podaci
  data() {
    return {
      newTask: "",
      tasks: []
    };
  },
  computed: {
    // computed property za broj zadataka
    taskCount() {
      return this.tasks.length; 
    }
  },
  methods: {
    // metoda za dodavanje taskova
    addTask() {
      if (this.newTask.trim() !== "") {
        this.tasks.push({ text: this.newTask });
        this.newTask = "";
      }
    },
    // metoda za uređivanje zadatka
    editTask(index) {
      const updatedText = prompt("Edit task", this.tasks[index].text);
      if (updatedText !== null) {
        this.tasks[index].text = updatedText;
      }
    },
    // metoda za brisanje zadatka
    deleteTask(index) {
      this.tasks.splice(index, 1);
    }
  },
  mounted() {
    alert("Mounted radi nešto čim se stvar pokrene...also, kad refreshamo stranicu, sve će se zbrisat jer nemamo pohranu");
  }
};
</script>

<style>
/*ovaj moj stil ne valja niš...napravite slobodno bolji ako znate :) ja stvarno ne znannnnn */
body {
  margin: 0;
  font-family: 'Inter', sans-serif;
  background: linear-gradient(135deg, #1f2937, #4b5563, #6b7280, #374151);
  background-size: 400% 400%;
  animation: gradientBG 10s ease infinite;
}



@keyframes gradientBG {
  0% { background-position: 0% 50%; }
  50% { background-position: 100% 50%; }
  100% { background-position: 0% 50%; }
}

.max-w-2xl {
  width: 100%;
}

.flex {
  display: flex;
}

.items-center {
  align-items: center;
}

.justify-center {
  justify-content: center;
}

.text-center {
  text-align: center;
}

.space-x-3 {
  margin-right: 1rem;
}
</style>
