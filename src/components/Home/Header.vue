<template>
  <section class="home-header">
    <form class="home-header__form">
      <h2>預訂獨一無二的住處和體驗行程。</h2>
      <div class="form-group">
        <span>地點</span>
        <input type="text" name="destination" placeholder="目的地">
      </div>
      <div class="form-group-wrapper">
        <div class="form-group">
          <span>入住</span>
          <input type="text" name="checkin-date" placeholder="年-月-日" readonly>
          <div class="date-picker"></div>
        </div>
        <div class="form-group">
          <span>退房</span>
          <input type="text" name="checkout-date" placeholder="年-月-日" readonly>
          <div class="date-picker"></div>
        </div>
      </div>
      <div class="form-group">
        <span>人數</span>
        <button class="select-btn" @click.prevent="showGuestMenu">
          <div>
            <span>房客</span>
            <span>
              <i class="fas fa-chevron-down"></i>
            </span>
          </div>
        </button>
      </div>
      <button class="standard">搜尋</button>
    </form>
  </section>
</template>

<script>
export default {
  name: "Header",
  data() {
    return {
      dateFormat: "D MMM",
      dateOne: "",
      dateTwo: ""
    };
  },
  methods: {
    showGuestMenu() {}
  }
};
</script>

<style lang="scss" scoped>
.home-header {
  position: relative;
  height: 100vh;
  background-image: url("../../assets/img/home_bg_1920_1060.jpg");
  background-size: cover;

  &__form {
    position: absolute;
    top: 150px;
    left: 100px;
    width: 450px;
    display: flex;
    flex-direction: column;
    padding: 40px 30px;
    background-color: #fff;
    border-radius: 5px;
    box-shadow: 0 10px 10px 0px rgba(0, 0, 0, 0.5);

    h2 {
      font-weight: bold;
      font-size: 1.6rem;
      margin-bottom: 20px;
    }

    .form-group {
      display: flex;
      flex-direction: column;
      margin-bottom: 15px;

      span {
        margin-bottom: 10px;
      }

      input {
        font-size: 1.2rem;
        padding: 10px;
        border: lightgray solid 1px;
        border-radius: 5px;
      }

      .select-btn {
        width: 100%;
        background-color: #fff;
        border: lightgray solid 1px;

        div {
          display: flex;
          justify-content: space-between;
          align-items: center;
          padding: 10px;
          font-size: 1.2rem;
          width: 100%;

          span {
            margin: 0;
          }
        }
      }
    }

    .form-group-wrapper {
      display: flex;

      .form-group {
        width: 50%;
      }
    }

    button {
      align-self: flex-end;
      margin-top: 10px;
    }
  }
}
</style>

