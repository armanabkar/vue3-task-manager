<template>
  <div class="modal is-active">
    <div class="modal-background"></div>
    <div class="modal-content">
      <div class="card">
        <div class="card-content">
          <div class="media">
            <div class="media-content">
              <p class="title is-4 pb-4">Title: {{ task.title }}</p>
              <p class="subtitle is-6">
                <b>Assigned To:</b> {{ task.assignedTo }}
              </p>
              <p class="subtitle is-6">
                <b>Created By:</b> {{ task.createdBy }}
              </p>
            </div>
          </div>
          <div class="content">
            <p class="subtitle is-6">
              <b>Description:</b> <br />
              {{ task.description }}
            </p>
          </div>
        </div>
      </div>
    </div>
    <button
      class="modal-close is-large"
      @click="closeModal"
      aria-label="close"
    ></button>
  </div>
</template>
<script lang="ts">
import { computed } from "vue"
import { useStore } from "@/store"
import { MutationType } from "@/store/mutations"
export default {
  name: "EditModal",
  props: {
    id: { type: Number, required: true },
  },
  // eslint-disable-next-line
  setup(props: any) {
    const store = useStore()

    const task = computed(() => store.getters.getTaskById(Number(props.id)))

    const closeModal = () => {
      store.commit(MutationType.SetTaskModal, {
        showModal: false,
        taskId: undefined,
      })
    }

    return { closeModal, task }
  },
}
</script>
<style scoped>
h1 {
  color: #ffffff;
  text-align: center;
  font-size: 2rem;
  margin-bottom: 3rem;
}
</style>