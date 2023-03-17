<template>
  <div>
    <div class="container mx-auto bg-[#ffff] w-[30%] min-h-[400px] mt-2 shadow-lg rounded-md px-4 py-4">
      <form action="" @submit.prevent="passwordValidation">
        <div class="grid md:grid-cols-2 gap-3 w-full">
          <div class="w-full">
            <h3 class="font-bold text-start">First name</h3>
            <input required type="text" class="border rounded-md h-8 px-4 w-full" v-model="form.first_name" placeholder="eg. jhon" />
          </div>
          <div class="w-full">
            <h3 class="font-bold text-start">Last name</h3>
            <input required type="text" class="border rounded-md h-8 px-4 w-full" v-model="form.last_name" placeholder="eg. jhon" />
          </div>
        </div>

        <!-- <vc-calendar /> -->

        <!-- <vc-date-picker /> -->

        <div class="w-full mt-5">
          <h3 class="font-bold text-start">Email</h3>
          <input required v-model="form.email" type="email" class="border rounded-md h-8 px-4 w-full" placeholder="eg. jhon" />
        </div>

        <div class="mt-5">
          <h3 class="font-bold text-start">Phone number</h3>
          <div class="flex gap-3 w-full">
            <div class="w-[23%]">
              <select required v-model="form.calling_code" name="" id="" class="border rounded-md h-8 w-full px-2">
                <option v-for="(item, index) in this.country" :key="index" :value="item.phone_code">{{ item.phone_code }}</option>
              </select>
            </div>

            <div class="w-[full]">
              <input required v-model="form.last_phone_number" type="number" class="border rounded-md h-8 px-4 w-full" placeholder="eg. jhon" />
            </div>
          </div>
        </div>

        <!-- date Picker -->
        <!-- <div class="relative">
          <input type="text" :value="form.date_of_birth" class="border rounded-md h-8 px-4 w-full" placeholder="DD/MM/YYYY" />

          <button @click.prevent="toggleDate">
            <img src="../assets/image/date.svg" alt="" class="w-[5%] mr-2 absolute top-[15%] right-0" />
          </button>
        </div> -->

        <!-- <div class=""> -->
        <!-- vc-calender tidak bisa digunakan  untuk binding data. gunakan datePicker -->
        <!-- vc-date-picker di gunakan wabib binding data . -->
        <!-- <vc-date-picker :model-config="modelConfig" v-if="this.showDate == true" v-model="form.date_of_birth"> </vc-date-picker> -->
        <!-- </div> -->
        <!-- date Picker -->

        <div class="w-full mt-5">
          <h3 class="font-bold text-start">Date of Birth</h3>
          <!-- new date picker -->
          <vc-date-picker v-model="form.date_of_birth">
            <template v-slot="{ inputValue, inputEvents }">
              <div class="relative">
                <input class="border rounded-md h-8 px-4 w-full" placeholder="DD/MM/YYYY" :value="inputValue" v-on="inputEvents" />
                <img src="../assets/image/date.svg" alt="" class="w-[5%] mr-2 absolute top-[15%] right-0" />
              </div>
            </template>
          </vc-date-picker>
          <!-- new date picker -->
        </div>

        <div class="w-full mt-5">
          <h3 class="font-bold text-start">Password</h3>
          <div class="relative">
            <input required v-model="form.password" :type="inputTypePassword" class="border rounded-md h-8 px-4 w-full" placeholder="eg. jhon" />

            <button @click.prevent="toggleInput">
              <img src="../assets/image/visible-icon.svg" alt="" class="w-[5%] mr-2 absolute top-[15%] right-0" />
            </button>
          </div>
        </div>

        <div class="w-full mt-5">
          <h3 class="font-bold text-start">Confirm Password</h3>
          <div class="relative">
            <input required v-model="form.confirm_password" :type="inputTypeConfirmPassword" class="border rounded-md h-8 px-4 w-full" placeholder="eg. jhon" />
            <button @click.prevent="toggleInputConfirm">
              <img src="../assets/image/visible-icon.svg" alt="" class="w-[5%] mr-2 absolute top-[15%] right-0" />
            </button>
          </div>
        </div>

        <div class="mt-5 text-end">
          <button type="submit" class="md:w-[25%] bg-blue-600 rounded-md px-4 py-2 text-white">Next</button>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: "userData",
  props: ["password", "country"],
  data() {
    return {
      showDate: false,
      showPassword: false,
      inputTypePassword: "password",
      inputTypeConfirmPassword: "password",
      form: {
        first_name: null,
        last_name: null,
        email: null,
        calling_code: null,
        last_phone_number: null,
        date_of_birth: null,
        password: null,
        confirm_password: null,
      },
      modelConfig: {
        type: "string",
        mask: "YYYY-MM-DD", // Uses 'iso' if missing
      },
      date: null,
    };
  },
  methods: {
    // validation
    passwordValidation() {
      if (this.form.password === this.form.confirm_password && this.form.password != null && this.form.confirm_password != null) {
        // emit dilakukan jika kondisi terpenuhi.
        this.$emit("nextToDataAddress");
      } else {
        alert("Password null or password not same!");
      }
    },
    toggleDate() {
      // console.log("ccekkk");
      this.showDate = !this.showDate;
      console.log(this.showDate);
    },

    // Show password
    toggleInput() {
      console.log("tes");
      this.inputTypePassword = this.inputTypePassword === "password" ? "text" : "password";
    },
    // Show confirm password
    toggleInputConfirm() {
      console.log("coba");
      this.inputTypeConfirmPassword = this.inputTypeConfirmPassword === "password" ? "text" : "password";
    },
  },
  computed: {},
};
</script>
