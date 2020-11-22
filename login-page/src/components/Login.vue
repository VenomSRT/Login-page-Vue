<template>
  <div class="login">
    <div class="login__container">
      <h1 class="login__title">
        <span class="login__title-big">Bank</span> Support Portal
      </h1>
      <form action="POST" class="login__form">
        <div class="login__input-container">
          <input
            type="email"
            id="mail"
            class="login__input login__input--email"
            v-bind:class="{
              'borderGreen' : mail.isFilled && !mail.error,
              'borderRed' : mail.isFilled && mail.error
            }"
            placeholder="E-mail"
            v-on:input="handleInput"
            required
          />
          <div v-show="mail.isFilled">
            <img
              v-if="mail.error"
              src="../images/cross.png"
              alt="email valid"
              class="login__mark login__mark--email"
            />

            <img
              v-else
              src="../images/check-mark.png"
              alt="email valid"
              class="login__mark login__mark--email"
            />
          </div>
        </div>

        <div class="login__message-container">
          <p
            class="login__message login__message--email"
            v-show="mail.error"
          >
            Invalid Username
          </p>
        </div>

        <div class="login__input-container">
          <input
            type="password"
            id="password"
            class="login__input login__input--password login__input--valid"
            v-bind:class="{
              'borderGreen' : password.isFilled && !password.error,
              'borderRed' : password.isFilled && password.error
            }"
            placeholder="Password"
            v-on:input="handleInput"
            required
          />
          <div v-show="password.isFilled">
            <img
              v-if="password.error"
              src="../images/cross.png"
              alt="password valid"
              class="login__mark login__mark--password"
            />

            <img
              v-else
              src="../images/check-mark.png"
              alt="password valid"
              class="login__mark login__mark--password"
            />
          </div>
        </div>

        <div class="login__message-container">
          <p
            class="login__message login__message--password"
            v-show="password.error"
          >
            Invalid Password
          </p>
        </div>

        <input
          type="submit"
          class="login__submit"
          value="Login"
          v-on:click="handleSubmit"
        />

        <p class="login__recovery">
          Forgot your password?
          <a href="#" class="login__recovery-link"> Reset it here.</a>
        </p>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Login',
  data() {
    return {
      mail: {
        isFilled: false,
        error: false,
      },

      password: {
        isFilled: false,
        error: false,
      },

      handleInput: (e) => {
        const targetField = e.target;
        this[targetField.id].isFilled = !!targetField.value.length;
        this.inputValidator(targetField);
      },

      inputValidator: (targetField) => {
        const mailPattern = /[\d\w]+@[\d\w^.]+\.[\w]{2,4}/i;
        const passwordPattern = /[\w\d]{4,}/i;
        const currentRegExp = targetField.id === 'mail' ? mailPattern : passwordPattern;

        if (targetField.value.length) {
          this[targetField.id].error = !currentRegExp.test(String(targetField.value));
        } else {
          this[targetField.id].error = false;
        }
      },

      handleSubmit: (e) => {
        if (this.mail.error || this.password.error) {
          e.preventDefault();
        }
      },
    };
  },
};

</script>

<style lang="scss" scoped>
$border: 1px solid
  rgba(
    $color: #999,
    $alpha: 0.33,
  );

.borderGreen {
  &:focus {
    border-color: #048c48;
  }
}

.borderRed {
  &:focus {
    border-color: #ed1f24;
  }
}

.login {
  box-sizing: border-box;
  display: flex;
  justify-content: center;

  &__container {
    display: grid;
    row-gap: 22px;
  }

  &__title {
    margin: 0;
    padding-left: 73px;
    text-align: left;
    font-size: 18px;
    font-weight: 100;
  }

  &__title-big {
    font-size: 41px;
    font-weight: 700;
    color: #2fa2c3;
  }

  &__form {
    display: grid;
    justify-content: center;
    grid-template-rows: 42px 40px 42px 39px 40px 33px;
    grid-template-columns: 295px;
    width: 440px;
    padding-top: 38px;
    padding-bottom: 35px;
    border: $border;
    border-radius: 5.51px;
  }

  &__input-container {
    position: relative;
  }

  &__input {
    position: relative;
    box-sizing: border-box;
    width: 295px;
    height: 42px;
    padding-left: 39px;
    padding-right: 5px;
    border: $border;
    border-radius: 5px;
    background-repeat: no-repeat;

    &:focus {
      outline: none;
    }

    &--email {
      background-image: url("../images/person-icon.png");
      background-position: 15px 13px;
    }

    &--password {
      background-image: url("../images/lock-icon.png");
      background-position: 15px 12px;
    }
  }

  &__mark {
    position: absolute;
    top: 14px;
    right: -20px;
  }

  &__message {
    margin: 0;
    padding-top: 4px;
    padding-left: 2px;
    justify-self: left;
    font-size: 11px;
    color: #ed1f24;
  }

  &__submit {
    width: 93px;
    background-color: #36a2c1;
    color: #fff;
    font-size: 16px;
    border: 1px solid #36a2c1;
    border-radius: 3px;
    cursor: pointer;
    transition: color 0.3s, background-color 0.3s;

    &:hover {
      background-color: #fff;
      color: #36a2c1;
    }

    &:focus {
      outline: none;
    }
  }

  &__recovery {
    margin: 0;
    padding-top: 15px;
    text-align: left;
    font-size: 12px;
  }

  &__recovery-link {
    text-decoration: none;
    color: #36a2c1;
  }
}
</style>
