<template>
  <form @submit.prevent="handleSubmit">
    <fieldset>
      <div class="col-xs-12">
        <h2>Ich bin ein neuer Kunde</h2>
      </div>
    </fieldset>
    <fieldset>
      <div class="col-xs-12">
        <div class="personality">
          <h3>Ihre persönlichen Daten</h3>
        </div>
      </div>
      <div class="form-group row">
        <div class="col-xs-12 col-sm-6">
          <label for="gender">Anrede*</label>
          <select
            v-model="gender"
            name="client-gender-select"
            class="input-form select-arrow"
            id="customer-gender"
          >
            <option value="f">Frau</option>
            <option value="m">Herr</option>
          </select>
        </div>
      </div>
      <div class="form-group row">
        <div class="col-xs-12 col-sm-6 mobile">
          <label for="vname">Vorname* </label>
          <input
            type="text"
            v-model="fname"
            id="vname"
            name="vname"
            class="input-form"
          />
          <div v-if="fnameError" class="error">{{ fnameError }}</div>
        </div>
        <div class="col-xs-12 col-sm-6">
          <label for="nname">Nachname*</label>
          <input
            type="text"
            v-model="lname"
            id="nname"
            name="nname"
            class="input-form"
          />
          <div v-if="lnameError" class="error">
            {{ lnameError }}
          </div>
        </div>
      </div>
      <div class="form-group row">
        <div class="col-xs-12 col-sm-6 mobile">
          <label for="email">E-mail Adresse*</label>
          <input
            type="email"
            required
            v-model="email"
            @blur="validateEmail"
            id="email"
            name="email"
            class="input-form"
          />
          <div v-if="emailError" class="error">
            {{ emailError }}
          </div>
        </div>

        <div class="col-xs-12 col-sm-6">
          <label for="user">Benutzer Name*</label>
          <input
            type="text"
            v-model="user"
            id="user"
            name="user"
            class="input-form"
          />
          <div v-if="userError" class="error">
            {{ userError }}
          </div>
        </div>
      </div>
    </fieldset>
    <fieldset>
      <div class="col-xs-12">
        <div class="personality">
          <h3>Ihr Passwort</h3>
        </div>
      </div>
      <div class="form-group row">
        <div class="col-xs-12 col-sm-6 mobile">
          <label for="pass">Passwort*</label>
          <input
            type="password"
            v-model="password"
            id="pass"
            name="pass"
            class="input-form"
          />
          <div v-if="passwordError" class="error">{{ passwordError }}</div>
        </div>
        <div class="col-xs-12 col-sm-6">
          <label for="passrepeat">Passwort wiederholen*</label>
          <input
            type="password"
            v-model="passwordRepeat"
            id="passrepeat"
            name="passrepeat"
            class="input-form"
          />
          <div v-if="passwordRepeatFalse" class="error">
            {{ passwordRepeatFalse }}
          </div>
        </div>
      </div>
    </fieldset>
    <fieldset>
      <div class="col-xs-12">
        <div class="personality">
          <h3>Ihre Adresse</h3>
        </div>
      </div>
      <div class="form-group row">
        <div class="col-xs-12 col-sm-6 mobile">
          <label for="street">Straße*</label>
          <input
            type="text"
            v-model="street"
            id="street"
            name="street"
            class="input-form"
          />
          <div v-if="streetError" class="error">
            {{ streetError }}
          </div>
        </div>
        <div class="col-xs-12 col-sm-6">
          <label for="zip">PLZ*</label>
          <input
            type="text"
            v-model="zip"
            id="zip"
            name="zip"
            class="input-form"
          />
          <div v-if="zipError" class="error">
            {{ zipError }}
          </div>
        </div>
      </div>
    </fieldset>
    <fieldset>
      <div class="agb">
        <div id="checkboxlabel" class="checkbox">
          <input
            type="checkbox"
            v-model="checkbox"
            required
            id="agbCheckbox"
            name="agb"
            value="agb"
          />
          <label class="agb-checkbox" for="checkbox"
            >Geschäftsbedingungen einverstanden</label
          >
        </div>
      </div>
    </fieldset>
    <fieldset>
      <div class="col-sm-6">
        <button class="buton btn_green stay_left" name="submit_register">
          Kundenkonto erstellen
        </button>
      </div>
    </fieldset>
  </form>
</template>

<script>
export default {
  data() {
    return {
      fname: "",
      fnameError: "",
      lname: "",
      lnameError: "",
      email: "",
      emailError: "",
      user: "",
      userError: "",
      password: "",
      passwordError: "",
      passwordRepeat: "",
      passwordRepeatFalse: "",
      street: "",
      streetError: "",
      zip: "",
      zipError: "",
      gender: "",
      checkbox: false,
    };
  },
  methods: {
    /**
     * Validate email address
     */
    validateEmail() {
      if (/^\w+([.-]?\w+)*@\w+([.-]?\w+)*(\.\w{2,3})+$/.test(this.email)) {
        this.emailError = "";
      } else {
        this.emailError = "Bitte geben Sie gültige E-mail Adresse";
      }
    },
    /**
     * Validate inputs and submit form
     */
    handleSubmit() {
      console.log("Form submit");
      //validate Password
      this.passwordError =
        this.password.length > 7
          ? ""
          : "Ihr Passwort muss mindestens acht Zeichen lang sein!";
      this.passwordRepeatFalse =
        this.password == this.passwordRepeat
          ? ""
          : "Die angegebenen Passwörter stimmen nicht überein!";

      //validate First Name
      this.fnameError = this.fname.length > 2 ? "" : "Mindestens drei Zeichen";

      //Validate Last Name
      this.lnameError =
        this.lname.length > 2 ? "" : "Bitte geben Sie Ihren Nachnamen an";

      //Validate User Name
      this.userError =
        this.user.length > 2 ? "" : "Bitte geben Sie Ihren Benutzernamen an";

      //Validate Street
      this.streetError =
        this.street.length > 2 ? "" : "Bitte geben Sie Ihre Straße an";

      //Validate Zip
      this.zipError = this.zip.length > 4 ? "" : "Bitte geben Sie Ihre PLZ an";

      //Validate Email Name
      this.validateEmail();

      if (!this.passwordError && !this.fnameError && !this.lnameError && !this.emailError  && !this.streetError && !this.zipError&& !this.checkboxError ) {
        console.log("fname", this.fname);
        console.log("lname", this.lname);
        console.log("email", this.email);
        console.log("password", this.password);
        console.log("street", this.street);
        console.log("zip", this.zip);
        console.log("agb", this.checkbox);
      }
    },
  },
};
</script>

<style>
.form-group {
  display: flex;
  margin-bottom: 15px;
}

label {
  display: inline-block;
  max-width: 100%;
  margin-bottom: 5px;
  font-family: "MyriadPro-BoldCond', 'FiraSans-Medium', sans-serif";
  font-weight: 400;
}

input[type="text"],
.input-form {
  width: 93%;
  height: 36px;
  padding: 9px 12px 6px 12px;
  font-size: 1.125em;
  line-height: 1.42857143;
  border: 1px solid #e0e0e0;
  box-shadow: none;
  appearance: none;
  -moz-appearance: none;
  -webkit-appearance: none;
  display: block;
  background-color: #ffffff;
  border-radius: 0;
}

input:focus {
  outline: none !important;
  border: 1px solid #fcbf00;
  box-shadow: 0 0 10px #719ece;
}

.form-group select {
  width: 93%;
  height: 36px;
  padding: 9px 12px 6px 12px;
  font-size: 1.125em;
  line-height: 1.42857143;
  border: 1px solid #e0e0e0;
  box-shadow: none;
  font: inherit;
  margin: 0;
  text-transform: none;
}
input {
  margin: 0;
}
.personality {
  background-color: #ebeced;
  padding: 10px 15px;
  margin-top: 10px;
  margin-bottom: 15px;
}

.buton {
  font-family: "MyriadPro-BoldCond", "FiraSans-Medium", sans-serif;
  font-size: 1.1em;
  display: inline-block;
  margin-bottom: 0;
  font-weight: normal;
  text-align: center;
  white-space: nowrap;
  vertical-align: middle;
  -ms-touch-action: manipulation;
  touch-action: manipulation;
  cursor: pointer;
  background-image: none;
  border: 1px solid transparent;
  padding: 6px 12px;
  border-radius: 0;
  user-select: none;
}

.btn_green {
  color: var(--clr-weiß);
  min-width: 270px;
  padding-top: 0.75em;
  padding-bottom: 0.55em;
  background-color: #009345;
  text-decoration: none;
  text-transform: uppercase;
  position: relative;
}

.stay_left {
  float: left;
}
.error {
  color: #eb4621;
  display: block;
  font-size: 0.8em;
}
</style>