<template>
  <div class="hero is-fullheight">
    <div class="hero-body py-1">
      <div class="container">
        <div class="columns">
          <div class="column is-1 ">
            <Sidebar />
          </div>
          <div class="column is-5">
            <h1 class="title pt-6 mt-5">
              <nobr id="underline">สร้าง</nobr>บัญชีผู้เข้ารับบริการ
            </h1>
          </div>
          <div class="column is-6">
            <forUsers class="pr-6" />
          </div>
        </div>
        <div class="columns has-text-left">
          <div class="column is-3 is-offset-1 pl-5">
            <b-field
              class="mb-2"
              label="ชื่อ"
              :type="{ 'is-danger': $v.form.firstName.$error }"
            >
              <b-input v-model="$v.form.firstName.$model" expanded></b-input>
            </b-field>
            <template v-if="$v.form.firstName.$error">
              <p class="help is-danger" v-if="!$v.form.firstName.required">
                * กรุณากรอกชื่อ
              </p>
              <p class="help is-danger" v-if="!$v.form.firstName.onlyString">
                ชื่อต้องเป็นตัวอักษรเท่านั้น
              </p>
              <p class="help is-danger" v-if="!$v.form.firstName.minLength">
                ชื่อต้องมีความยาวขั้นต่ำ 2 ตัวอักษร
              </p>
            </template>
            <b-field
              class="mb-2"
              label="นามสกุล"
              :type="{ 'is-danger': $v.form.lastName.$error }"
            >
              <b-input v-model="$v.form.lastName.$model" expanded></b-input>
            </b-field>
            <template v-if="$v.form.lastName.$error">
              <p class="help is-danger" v-if="!$v.form.lastName.required">
                * กรุณากรอกนามสกุล
              </p>
              <p class="help is-danger" v-if="!$v.form.lastName.onlyString">
                นามสกุลต้องเป็นตัวอักษรเท่านั้น
              </p>
              <p class="help is-danger" v-if="!$v.form.lastName.minLength">
                นามสกุลต้องมีความยาวขั้นต่ำ 2 ตัวอักษร
              </p>
            </template>
            <b-field
              label="วัน เดือน ปีเกิด"
              :type="{ 'is-danger': $v.form.dob.$error }"
            >
              <b-datepicker
                v-model="$v.form.dob.$model"
                placeholder="Type or select a date..."
                icon="calendar-today"
                editable
              >
              </b-datepicker>
            </b-field>
            <template v-if="$v.form.dob.$error">
              <p class="help is-danger" v-if="!$v.form.dob.required">
                * กรุณากรอกวันเดือนปีเกิด
              </p>
            </template>
          </div>
          <div class="column is-3 is-offset-1">
            <b-field grouped>
              <div class="block">
                <b-field
                  class="mr-6"
                  label="เพศ"
                  :type="{ 'is-danger': $v.form.gender.$error }"
                >
                  <b-radio
                    class="mr-5 ml-1 mt-2"
                    v-model="$v.form.gender.$model"
                    name="ชาย"
                    native-value="MALE"
                  >
                    ชาย
                  </b-radio>
                  <b-radio
                    class="ml-3 mt-2"
                    v-model="$v.form.gender.$model"
                    name="หญิง"
                    native-value="FEMALE"
                  >
                    หญิง
                  </b-radio>
                </b-field>
                <template v-if="$v.form.gender.$error">
                  <p class="help is-danger" v-if="!$v.form.gender.required">
                    * กรุณาเลือกตัวเลือกใดตัวเลือกหนึ่ง
                  </p>
                </template>
              </div>
              <b-field label="BMI">
                <b-input v-model="calBMI" disabled expanded> </b-input>
              </b-field>
            </b-field>
            <b-field grouped>
              <b-field
                label="น้ำหนัก (กิโลกรัม)"
                :type="{ 'is-danger': $v.form.weight.$error }"
              >
                <b-input v-model="$v.form.weight.$model" expanded></b-input>
                <template v-if="$v.form.weight.$error">
                  <p class="help is-danger" v-if="!$v.form.weight.required">
                    * กรุณากรอกน้ำหนัก
                  </p>
                  <p
                    class="help is-danger"
                    v-if="!($v.form.weight.decimal && $v.form.weight.minValue)"
                  >
                    น้ำหนักต้องเป็นตัวเลขมากกว่าหรือเท่ากับ 0
                  </p>
                </template>
              </b-field>
              <b-field
                label="ส่วนสูง (เซนติเมตร)"
                :type="{ 'is-danger': $v.form.height.$error }"
              >
                <b-input v-model="$v.form.height.$model" expanded></b-input>
                <template v-if="$v.form.height.$error">
                  <p class="help is-danger" v-if="!$v.form.height.required">
                    * กรุณากรอกส่วนสูง
                  </p>
                  <p
                    class="help is-danger"
                    v-if="!($v.form.height.decimal && $v.form.height.minValue)"
                  >
                    ส่วนสูงต้องเป็นตัวเลขมากกว่าหรือเท่ากับ 0
                  </p>
                </template>
              </b-field>
            </b-field>
            <b-field grouped>
              <b-field
                label="รอบเอว (นิ้ว)"
                :type="{ 'is-danger': $v.form.waistline.$error }"
              >
                <b-input v-model="$v.form.waistline.$model" expanded></b-input>
                <template v-if="$v.form.waistline.$error">
                  <p class="help is-danger" v-if="!$v.form.waistline.required">
                    * กรุณากรอกรอบเอว
                  </p>
                  <p
                    class="help is-danger"
                    v-if="
                      !($v.form.waistline.decimal && $v.form.waistline.minValue)
                    "
                  >
                    รอบเอวต้องเป็นตัวเลขมากกว่าหรือเท่ากับ 0
                  </p>
                </template>
              </b-field>
              <b-field
                label="ประวัติการล้มใน 1 ปี (ครั้ง)"
                :type="{ 'is-danger': $v.form.fall_history.$error }"
              >
                <b-input
                  v-model="$v.form.fall_history.$model"
                  expanded
                ></b-input>
                <template v-if="$v.form.fall_history.$error">
                  <p
                    class="help is-danger"
                    v-if="!$v.form.fall_history.required"
                  >
                    * กรุณากรอกจำนวนครั้ง
                  </p>
                  <p
                    class="help is-danger"
                    v-if="
                      !(
                        $v.form.fall_history.integer &&
                        $v.form.fall_history.minValue
                      )
                    "
                  >
                    จำนวนครั้งต้องเป็นจำนวนเต็มมากกว่าหรือเท่ากับ 0
                  </p>
                </template>
              </b-field>
            </b-field>
          </div>
        </div>
        <b-button
          class="login mt-3"
          style="font-family: 'Kanit', sans-serif; font-weight: 400;"
          @click="createU"
        >
          สร้างบัญชี
        </b-button>
        <router-link to="/dashboard">
          <p class="cancel pt-1">
            ยกเลิก
          </p>
        </router-link>
      </div>
    </div>
  </div>
</template>
<script>
import Sidebar from '@/components/sidebar.vue'
import forUsers from '@/components/forUsers.vue'
import { debounce } from 'debounce'
import { mapMutations, mapActions } from 'vuex'
import {
  required,
  minLength,
  integer,
  minValue,
  decimal,
} from 'vuelidate/lib/validators'

function onlyString(value) {
  if (!value.match(/^[ก-์a-zA-Z]*$/gm)) {
    return false
  }
  return true
}

export default {
  components: {
    Sidebar,
    forUsers,
  },
  name: 'AddPatient',
  data() {
    return {
      form: {
        firstName: '',
        lastName: '',
        gender: '',
        dob: null, //null new Date()
        weight: null,
        height: null,
        waistline: null,
        fall_history: null,
      },
    }
  },
  validations: {
    form: {
      firstName: {
        required,
        onlyString,
        minLength: minLength(2),
      },
      lastName: {
        required,
        onlyString,
        minLength: minLength(2),
      },
      dob: { required },
      gender: { required },
      weight: { required, decimal, minValue: minValue(0) },
      height: { required, decimal, minValue: minValue(0) },
      waistline: { required, decimal, minValue: minValue(0) },
      fall_history: { required, integer, minValue: minValue(0) },
    },
  },
  computed: {
    calBMI() {
      let bmi = parseFloat(
        this.form.weight / Math.pow(this.form.height / 100, 2),
      ).toFixed(2)
      if (isFinite(bmi) && bmi > 0) {
        return bmi
      } else {
        return '0'
      }
    },
  },
  methods: {
    ...mapMutations(['setCreatePatient']),
    ...mapActions(['createPatient']),
    debounceInput: debounce(function(e) {
      console.log(e)
      this.setCreatePatient(e)
    }, 300),
    createU() {
      // Validate all fields
      this.$v.$touch()

      // เช็คว่าในฟอร์มไม่มี error
      if (!this.$v.$invalid) {
        // alert("complete");
        this.createPatient()
          .then(() => {
            this.$router.push({ name: 'Dashboard' })
          })
          .catch(e => {
            console.log(e.details)
            if (Array.isArray(e.details)) {
              console.log('yes')
              let err = ''
              e.details.forEach(e => {
                err += ' ' + e.message
              })
              alert(err)
            } else {
              console.log('no')
              console.log(e)
              alert(e.message)
            }
          })
      } else {
        alert('โปรดกรอกข้อมูลให้ถูกต้องทุกช่อง')
      }
    },
  },
  watch: {
    form: {
      // This will let Vue know to look inside the array
      deep: true,

      // We have to move our method to a handler field
      handler(val) {
        this.debounceInput(val)
        console.log('The form has changed!')
      },
    },
  },
}
</script>
<style>
.title {
  color: black;
  text-align: left;
  font-weight: 500;
  font-size: 2rem;
}
#underline {
  border-bottom: solid 10px #1e3a8a;
}
input {
  margin-top: 0px;
}
.label {
  text-align: left;
  margin-left: 4px;
  margin-top: 0px;
  margin-bottom: 0px;
  font-weight: 400;
}
.login {
  color: #ffffff;
  background-color: #1e3a8a;
  width: 37%;
}
.cancel {
  font-size: 0.75rem;
  font-style: italic;
  color: #f90000;
  text-decoration: underline;
  cursor: pointer;
}
</style>
