<script setup>
import { onMounted, ref } from "vue";

const modal = ref();

onMounted(() => {
  if (modal.value) {
    modal.value.addEventListener("click", (e) => {
      const dialogDimensions = modal.value.getBoundingClientRect();

      if (
        e.clientX < dialogDimensions.left ||
        e.clientY > dialogDimensions.right ||
        e.clientY < dialogDimensions.top ||
        e.clientY > dialogDimensions.bottom
      ) {
        modal.value.close();
      }
    });
  }
});
</script>

<template>
  <div class="container">
    <button class="btn" @click="modal.showModal()">Select date</button>
  </div>
  <Teleport to="body">
    <dialog ref="modal">
      <div class="modal-bg">
        <div class="modal-content">
          <h1>Hello from the modal</h1>
          <p>
            Lorem ipsum dolor sit amet consectetur adipisicing elit. Culpa alias
            <br />
            enim odio reprehenderit repudiandae voluptas, nulla sint molestias
            <br />
            omnis quia in, officia, velit porro corrupti ratione. Sit velit
            <br />
            autem fuga?
          </p>
        </div>
      </div>
    </dialog>
  </Teleport>
</template>

<style scoped>
.container {
  display: grid;
  place-items: center;
  height: 100%;
}

.btn {
  background: #0a0a0a;
  padding: 10px 15px;
  color: white;
  border: none;
  border-radius: 16px;
  font-size: 14px;
  line-height: 16px;
  text-align: center;
  cursor: pointer;
}

dialog {
  transition: display 0.5s allow-discrete, overlay 0.5s allow-discrete;
  animation: close 0.5s forwards;
  padding: 0px 1px;
  border-radius: 10px;
  background: #0a0a0a;
  border: none;
}

dialog:modal {
  transition: display 0.5s allow-discrete, overlay 0.5s allow-discrete;
  animation: close 0.5s forwards;
}

dialog:modal[open] {
  animation: open 0.5s forwards;
}

dialog::backdrop {
  animation: close 0.5s forwards;
}

dialog[open]::backdrop {
  animation: open 0.5s forwards;
}

@keyframes open {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

@keyframes close {
  from {
    opacity: 1;
  }
  to {
    opacity: 0;
  }
}

.modal-bg {
  background-image: radial-gradient(
    106.48% 50% at 50% 50%,
    #2a6fd7 0%,
    rgba(77, 159, 255, 0) 100%
  );
  padding: 2px;
}

.modal-content {
  background-image: linear-gradient(
      0deg,
      var(--Syntax-Darker-Dark, rgba(10, 10, 10, 0.85)),
      var(--Syntax-Darker-Dark, rgba(10, 10, 10, 0.85))
    ),
    radial-gradient(
      211.53% 35.8% at 50% 50%,
      rgba(42, 111, 215, 0.15) 14.46%,
      rgba(77, 148, 255, 0) 100%
    );
  padding: 15px;
  border-radius: 10px;
}
</style>
