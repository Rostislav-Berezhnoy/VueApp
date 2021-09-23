<template>
  <div>
    <div class="page-title">
      <h3>Создать новую точку измерения</h3>
    </div>
    <div class="card">
      <div class="card-content">
        <div class="row">
          <div class="col s12">
            <ul class="tabs" ref="CreateElMeterPointRef">
              <li class="tab col s3"><a class="active" href="#point1">Точка измерения</a></li>
              <li class="tab col s3"><a href="#point2">Счетчик электрической энергии</a></li>
              <li class="tab col s3"><a href="#point3">Трансформатор тока</a></li>
              <li class="tab col s3"><a href="#point4">Трансформатор напряжения</a></li>
            </ul>
          </div>
          <div id="point1" class="col s12">
            <form class="form">
              <div class="input-field">
                <input
                    id="name"
                    type="text"
                    v-model.trim="form.name"
                >
                <label for="name">Название</label>
                <span
                    class="helper-text invalid"
                    v-if="$v.form.name.$dirty && !$v.form.name.required"
                >Поле не может быть пустым</span>
              </div>

              <div class="input-field">
                <select
                    ref="consObjSelect"
                    id="consObjSelect"
                    v-model.trim="form.consumptionObjectID"
                >
                  <option value="" disabled selected>Выберите объект потребления</option>
                  <option
                      v-for="consObj in consumptionObjects"
                      :key="consObj.id"
                      :value="consObj.id"
                  >
                    {{consObj.name}}
                  </option>
                </select>
                <label>Объект потребления</label>
                <span
                    class="helper-text invalid"
                    v-if="$v.form.consumptionObjectID.$dirty && !$v.form.consumptionObjectID.required"
                >Поле не может быть пустым</span>
              </div>
            </form>
          </div>
          <div id="point2" class="col s12">
            <form class="form">
              <div class="input-field">
                <input
                    id="elMetNo"
                    type="text"
                    v-model.trim="form.ElectricityMeter[0].No"
                >
                <label for="elMetNo">Номер счетчика электрической энергии</label>
                <span
                    class="helper-text invalid"
                    v-if="$v.form.ElectricityMeter.$each[0].No.$dirty && !$v.form.ElectricityMeter.$each[0].No.required"
                >Поле не может быть пустым</span>
              </div>

              <div class="input-field">
                <input
                    id="elMetType"
                    type="text"
                    v-model.trim="form.ElectricityMeter[0].Type"
                >
                <label for="elMetType">Тип счетчика электрической энергии</label>
                <span
                    class="helper-text invalid"
                    v-if="$v.form.ElectricityMeter.$each[0].Type.$dirty && !$v.form.ElectricityMeter.$each[0].Type.required"
                >Поле не может быть пустым</span>
              </div>

              <div class="input-field">
                <input
                    id="elMetVerDate"
                    class="datepicker"
                    type="text"
                    ref="elMetVerDate"
                    v-model.lazy="form.ElectricityMeter[0].VerificationDate"
                >
                <label for="elMetVerDate">Дата поверки счетчика электрической энергии</label>
                <span
                    class="helper-text invalid"
                    v-if="$v.form.ElectricityMeter.$each[0].VerificationDate.$dirty && !$v.form.ElectricityMeter.$each[0].VerificationDate.required"
                >Поле не может быть пустым</span>
              </div>
            </form>
          </div>
          <div id="point3" class="col s12">
            <form class="form">
              <div class="input-field">
                <input
                    id="elTransNo"
                    type="text"
                    v-model.trim="form.ElectricalTransformer[0].No"
                >
                <label for="elTransNo">Номер трансформатора тока</label>
                <span
                    class="helper-text invalid"
                    v-if="$v.form.ElectricalTransformer.$each[0].No.$dirty && !$v.form.ElectricalTransformer.$each[0].No.required"
                >Поле не может быть пустым</span>
              </div>

              <div class="input-field">
                <input
                    id="elTransType"
                    type="text"
                    v-model.trim="form.ElectricalTransformer[0].Type"
                >
                <label for="elTransType">Тип трансформатора тока</label>
                <span
                    class="helper-text invalid"
                    v-if="$v.form.ElectricalTransformer.$each[0].Type.$dirty && !$v.form.ElectricalTransformer.$each[0].Type.required"
                >Поле не может быть пустым</span>
              </div>

              <div class="input-field">
                <input
                    id="elTransVerDate"
                    class="datepicker"
                    type="text"
                    ref="elTransDate"
                    v-model.lazy="form.ElectricalTransformer[0].VerificationDate"
                >
                <label for="elTransVerDate">Дата поверки трансформатора тока</label>
              </div>

              <div class="input-field">
                <input
                    id="elTransRatio"
                    type="number"
                    v-model.trim="form.ElectricalTransformer[0].TransformationRatio"
                >
                <label for="elTransRatio">Коэффициент трансформации трансформатора тока</label>
                <span
                    class="helper-text invalid"
                    v-if="$v.form.ElectricalTransformer.$each[0].VerificationDate.$dirty && !$v.form.ElectricalTransformer.$each[0].VerificationDate.required"
                >Поле не может быть пустым</span>
                <span
                    class="helper-text invalid"
                    v-if="$v.form.ElectricalTransformer.$each[0].TransformationRatio.$dirty && !$v.form.ElectricalTransformer.$each[0].TransformationRatio.required"
                >Поле не может быть пустым</span>
              </div>
            </form>
          </div>
          <div id="point4" class="col s12">
            <form class="form">
              <div class="input-field">
                <input
                    id="voltTransNo"
                    type="text"
                    v-model.trim="form.VoltageTransformer[0].No"
                >
                <label for="voltTransNo">Номер трансформатора напряжения</label>
                <span
                    class="helper-text invalid"
                    v-if="$v.form.VoltageTransformer.$each[0].No.$dirty && !$v.form.VoltageTransformer.$each[0].No.required"
                >Поле не может быть пустым</span>
              </div>

              <div class="input-field">
                <input
                    id="voltTransType"
                    type="text"
                    v-model.trim="form.VoltageTransformer[0].Type"
                >
                <label for="voltTransType">Тип трансформатора напряжения</label>
                <span
                    class="helper-text invalid"
                    v-if="$v.form.VoltageTransformer.$each[0].Type.$dirty && !$v.form.VoltageTransformer.$each[0].Type.required"
                >Поле не может быть пустым</span>
              </div>

              <div class="input-field">
                <input
                    id="voltTransVerDate"
                    class="datepicker"
                    type="text"
                    ref="voltTransDate"
                    v-model.lazy="form.VoltageTransformer[0].VerificationDate"
                >
                <label for="voltTransVerDate">Дата поверки трансформатора напряжения</label>
                <span
                    class="helper-text invalid"
                    v-if="$v.form.VoltageTransformer.$each[0].VerificationDate.$dirty && !$v.form.VoltageTransformer.$each[0].VerificationDate.required"
                >Поле не может быть пустым</span>
              </div>

              <div class="input-field">
                <input
                    id="voltTransRatio"
                    type="number"
                    v-model.trim="form.VoltageTransformer[0].TransformationRatio"
                >
                <label for="voltTransRatio">Коэффициент трансформации трансформатора напряжения</label>
                <span
                    class="helper-text invalid"
                    v-if="$v.form.VoltageTransformer.$each[0].TransformationRatio.$dirty && !$v.form.VoltageTransformer.$each[0].TransformationRatio.required"
                >Поле не может быть пустым</span>
              </div>
            </form>
          </div>
        </div>
      </div>
      <div class="card-action text-right">
        <button class="btn waves-effect waves-light blue" type="submit" @click="onFormSubmit">
          Создать
          <i class="material-icons right">send</i>
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import $ from "jquery";
import { required } from 'vuelidate/lib/validators';
export default {
  name: "ElectricityMeteringPointsCreatePage",
  data: () => ({
    form: {
      name: '',
      consumptionObjectID: null,
      ElectricityMeter: [{
        No: '',
        Type: '',
        VerificationDate: ''
      }],
      VoltageTransformer: [{
        No: '',
        Type: '',
        VerificationDate: '',
        TransformationRatio: null
      }],
      ElectricalTransformer: [{
        No: '',
        Type: '',
        VerificationDate: '',
        TransformationRatio: null
      }]
    }
  }),
  validations: {
    form: {
      name: { required },
      consumptionObjectID: { required },
      ElectricityMeter: {
        $each: {
          No: { required },
          Type: { required },
          VerificationDate: { required }
        }
      },
      VoltageTransformer: {
        $each: {
          No: { required },
          Type: { required },
          TransformationRatio: { required },
          VerificationDate: { required }
        }
      },
      ElectricalTransformer: {
        $each: {
          No: { required },
          Type: { required },
          TransformationRatio: { required },
          VerificationDate: { required }
        }
      }
    }
  },
  computed: {
    consumptionObjects() {
      return this.$store.state.consumptionObjects;
    },
    createElectricityMeteringPoint(){
      return this.$store.state.createElectricityMeteringPoint;
    }
  },
  created() {
    this.$store.dispatch("getConsumptionObjects");
  },
  mounted() {
    M.Tabs.init(this.$refs.CreateElMeterPointRef);
    this.SelectInitialization();

    const ruLocale = {
      cancel: 'Отмена',
      clear: 'Очистить',
      done: 'Ok',
      previousMonth: '‹',
      nextMonth: '›',
      months: [
        'Январь',
        'Февраль',
        'Март',
        'Апрель',
        'Май',
        'Июнь',
        'Июль',
        'Август',
        'Сентябрь',
        'Октябрь',
        'Ноябрь',
        'Декабрь'
      ],
      monthsShort: [
        'Январь',
        'Февраль',
        'Март',
        'Апрель',
        'Май',
        'Июнь',
        'Июль',
        'Август',
        'Сентябрь',
        'Октябрь',
        'Ноябрь',
        'Декабрь'
      ],
      weekdays: [
        'Воскресенье',
        'Понедельник',
        'Вторник',
        'Среда',
        'Четверг',
        'Пятница',
        'Суббота'
      ],
      weekdaysShort: [
        'Воскресенье',
        'Понедельник',
        'Вторник',
        'Среда',
        'Четверг',
        'Пятница',
        'Суббота'
      ],
      weekdaysAbbrev: ['Вс', 'Пн', 'Вт', 'Ср', 'Чт', 'Пт', 'Сб']
    };

    M.Datepicker.init(this.$refs.elMetVerDate, {
      format: 'yyyy-mm-dd',
      i18n: ruLocale
    });

    M.Datepicker.init(this.$refs.elTransDate, {
      format: 'yyyy-mm-dd',
      i18n: ruLocale
    });

    M.Datepicker.init(this.$refs.voltTransDate, {
      format: 'yyyy-mm-dd',
      i18n: ruLocale
    });
  },
  updated() {
    this.$nextTick(function () {
      this.SelectInitialization();
    })
  },
  watch: {
    createElectricityMeteringPoint(){
      this.$router.push('/electricity-metering-points');
    }
  },
  methods: {
    SelectInitialization(){
      M.FormSelect.init(this.$refs.consObjSelect);
    },
    onFormSubmit(){
      if (this.$v.form.$invalid) {
        this.$v.form.$touch();
        return null;
      }
      this.$store.dispatch("createElectricityMeteringPoints", this.form);
    }
  }
}
</script>

<style scoped>
  .form{
    margin-top: 30px;
  }
  .card-content{
    min-height: 500px;
  }
  button{
    width: 100%;
    max-width: 150px;
  }
</style>
