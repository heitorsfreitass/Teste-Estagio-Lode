<script setup>
  import { ref, computed } from 'vue'

  const tasks = ref([
    {
      id: 1,
      name: 'Limpeza de Filtro',
      concluded: false
    },
    {
      id: 2,
      name: 'Teste de Vazão',
      concluded: false
    },
    {
      id: 3,
      name: 'Lubrificação de Eixos',
      concluded: false
    },
  ])

  const progress = computed(() => {
    const concludedTasks = tasks.value.filter(t => t.concluded).length

    return Math.round((concludedTasks / tasks.value.length) * 100)
  })

  const toggleTask = (task) => {
    if (!task.concluded) {
      task.concluded = true
      return
    }

    const confirmed = confirm('Deseja desmarcar essa task?')
    if (confirmed) {
      task.concluded = false
    }

  }
</script>

<template>
  <div class="container py-5">

    <div class="d-flex justify-content-between align-items-center mb-4">

      <h1>
        Checklist de Manutenção
      </h1>

      <span class="badge text-bg-primary fs-6">
        {{ progress }}%
      </span>

    </div>

    <div class="row g-4">

      <div
        class="col-md-4"
        v-for="task in tasks"
        :key="task.id"
      >

        <div
          class="card h-100 shadow-sm task-card"
          :class="{
            concluded: task.concluded
          }"
          @click="toggleTask(task)"
        >

          <div class="card-body">

            <div class="d-flex justify-content-between">

              <h5 class="card-title">
                {{ task.name }}
              </h5>

              <span v-if="task.concluded">
                ✔
              </span>

            </div>

            <p class="card-text mt-3">

              Status:

              <strong>
                {{
                  task.concluded
                    ? 'Concluída'
                    : 'Pendente'
                }}
              </strong>

            </p>

          </div>

        </div>

      </div>

    </div>

  </div>
</template>

<style scoped>

.task-card {
  cursor: pointer;
  transition: 0.2s;
}

.task-card:hover {
  transform: translateY(-4px);
}

.concluded {
  background: #d1e7dd;
  border: 2px solid #198754;
}

</style>
