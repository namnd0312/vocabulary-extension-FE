<template>
  <div class="vocabulary">
    <!-- <div class="col-12 text-center">Học Từ vựng hôm nay!</div> -->
    <form id="signup-form" v-on:submit.prevent="submit">
      <div class="row">
        <div class="col-12 form-group">
          <label class="col-form-label col-form-label-lg"
            >Từ mới <span class="text-danger">*</span></label
          >
          <input
            type="text"
            v-model.trim="$v.word.$model"
            :class="{ 'is-invalid': validationStatus($v.word) }"
            class="form-control form-control-lg"
          />
          <div v-if="!$v.word.required" class="invalid-feedback">
            Từ mới bắt buộc nhập.
          </div>
          <div v-if="!$v.word.maxLength" class="invalid-feedback">
            Không được quá 100 kí tự
          </div>
        </div>

        <div class="col-12 form-group">
          <label class="col-form-label col-form-label-lg"
            >Loại từ<span class="text-danger">*</span></label
          >
          <select
            v-model.trim="$v.typeOfWord.$model"
            :class="{ 'is-invalid': validationStatus($v.typeOfWord) }"
            class="form-control form-control-lg"
          >
            <option disabled>---------------</option>
            <option value="v">Động từ</option>
            <option value="n">Danh từ</option>
            <option value="adj">Tính từ</option>
            <option value="adv">Trạng từ</option>
            <option value="none">Không xác định</option>
          </select>
          <div v-if="!$v.typeOfWord.required" class="invalid-feedback">
            Loại từ bắt buộc nhập.
          </div>
        </div>

        <div class="col-12 form-group">
          <label class="col-form-label col-form-label-lg"
            >Phiên âm <span class="text-danger">*</span></label
          >
          <input
            type="text"
            v-model.trim="$v.transcription.$model"
            :class="{ 'is-invalid': validationStatus($v.transcription) }"
            class="form-control form-control-lg"
          />
          <div v-if="!$v.transcription.required" class="invalid-feedback">
            Phiên âm bắt buộc nhập.
          </div>
          <div v-if="!$v.transcription.maxLength" class="invalid-feedback">
            Không được quá 100 kí tự
          </div>
        </div>
        <div class="col-12 form-group">
          <label class="col-form-label col-form-label-lg"
            >Nghĩa <span class="text-danger">*</span></label
          >
          <input
            type="text"
            v-model.trim="$v.meaning.$model"
            :class="{ 'is-invalid': validationStatus($v.meaning) }"
            class="form-control form-control-lg"
          />
          <div v-if="!$v.meaning.required" class="invalid-feedback">
            Nghĩa bắt buộc nhập.
          </div>
          <div v-if="!$v.meaning.maxLength" class="invalid-feedback">
            Không được quá 100 kí tự
          </div>
        </div>
        <div class="col-12 form-group text-center pt-3">
          <button class="btn btn-vue btn-lg col-4">Lưu</button>
        </div>

        <div class="col-12 pt-5" text-center>@copywrite by Namnd</div>
      </div>
    </form>
  </div>
</template>

<script>
import { required, maxLength } from "vuelidate/lib/validators";
import axios from "axios";
export default {
  name: "vocabulary",
  data: function () {
    return {
      word: "",
      meaning: "",
      transcription: "",
      typeOfWord: "",
    };
  },
  validations: {
    word: { required, maxLength: maxLength(100) },
    meaning: { required, maxLength: maxLength(100) },
    transcription: { required, maxLength: maxLength(100) },
    typeOfWord: { required },
  },

  methods: {
    resetData: function () {
      this.word = "";
      this.meaning = "";
      this.transcription = "";
      this.typeOfWord = "";
    },

    validationStatus: function (validation) {
      return typeof validation != "undefined" ? validation.$error : false;
    },

    submit: function () {
      this.$v.$touch();
      if (this.$v.$pendding || this.$v.$error) return;

      // Simple POST request with a JSON body using axios
      const requestBody = {
        word: this.$v.word.$model,
        meaning: this.$v.meaning.$model,
        transcription: this.$v.transcription.$model,
        typeOfWord: this.$v.typeOfWord.$model,
      };

      const url =
        "https://vocabulary-chrome-extension.herokuapp.com/api/vocab/create";
      // const url_local = "http://localhost:5000/api/vocab/create";

      console.log("requestBody", requestBody);
      axios.post(url, requestBody).then((response) => {
        console.log("response", response);
        alert("Lưu từ mới thành công!");
        this.$v.$reset();
        this.resetData();
      });
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.btn-vue {
  background: #53b985;
  color: #31485d;
  font-weight: bold;
}
</style>
