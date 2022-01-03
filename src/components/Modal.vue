<template>
  <div class="wrapper" v-if="showModal" @click="closeModal">
    <div class="mod">
      <img
        src="../assets/success.png"
        alt="Modal main icon"
        class="main-icon"
      />
      <button class="close-btn">
        <svg
          width="18"
          height="18"
          viewBox="0 0 18 18"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            d="M16 2L2 16M16 16L2 2L16 16Z"
            stroke="#989898"
            stroke-width="3"
            stroke-linecap="round"
            stroke-linejoin="round"
          />
        </svg>
      </button>
      <p class="success-descr">Клиент успешно создан.</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Modal',
  props: {
    showModal: Boolean,
  },
  model: {
    prop: 'showModal',
    event: 'showChange',
  },
  computed: {
    showModalLocal: {
      get: function () {
        return this.showModal;
      },
      set: function (value) {
        this.$emit('showChange', value);
      },
    },
  },
  methods: {
    closeModal(e){
      const target = e.target;
      if (target.classList.contains('wrapper') || target.closest('.close-btn')){
        this.showModalLocal = false;
      }
    }
  }
};
</script>

<style lang="scss" scoped>
.wrapper {
  position: fixed;
  left: 0;
  top: 0;
  z-index: 81;
  width: 100%;
  height: 100%;
  min-height: 12rem;
  background: rgba(0, 0, 0, 0.75);
  display: flex;
  justify-content: center;
  align-items: center;

  .mod {
    width: 18.75rem;
    height: 10rem;
    background: #24313c;
    color: #ffffff;
    border-radius: 0.625rem;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: space-between;
    padding: 2.5rem 2.625rem;
    position: relative;

    .success-descr {
      margin: 0;
      margin-top: 0.5rem;
      font-size: 1.3rem;
    }

    .close-btn {
      position: absolute;
      width: 0.75rem;
      right: 1rem;
      top: 1rem;
      width: fit-content;
      background: transparent;
      border: none;
      cursor: pointer;

      &:hover {
        path {
          stroke: #fff;
        }
      }
    }
  }
}
</style>
