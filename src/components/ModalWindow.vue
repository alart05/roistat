<template>
  <div class="modal">
    <div class="modal__container">
      <div>Добавление пользователя</div>
      <img class="modal__close" @click="$emit('close')" src="@/assets/close.svg">
      <div class="modal__content">
        <div>Имя</div>
        <Input
          @update="person.name = $event; errorPerson.name = false"
          :haveError="errorPerson.name"
        />

        <div>Телефон</div>
        <Input
          @update="person.phone = $event; errorPerson.phone = false"
          :haveError="errorPerson.phone"
          type="number"
        />

        <div>Начальник</div>
        <Select :options="staff"/>
      </div>
      <Button class="modal__button" title="Сохранить" @click.native="save()"/>
    </div>
  </div>
</template>

<script>
import Button from '@/components/Button'
import Input from '@/components/Input'
import Select from '@/components/Select'
export default {
  name: 'ModalWindow',
  components: {
    Button,
    Input,
    Select
  },
  props: {
    staff: {type: Array, default: () => []}
  },
  data () {
    return {
      person: {
        name: '',
        phone: ''
      },
      errorPerson: {
        name: false,
        phone: false
      }
    }
  },
  methods: {
    save () {
      if (this.person.name.length === 0) {
        this.errorPerson.name = true
      }
      if (this.person.phone.length === 0) {
        this.errorPerson.phone = true
      }
      if (!this.errorPerson.phone && !this.errorPerson.name) {
        this.$emit('save', this.person)
      }
    }
  }
}
</script>

<style scoped>
.modal__button{
  margin-top: 40px;
}
.modal__content{
  display: grid;
  grid-template-columns: 80px 200px;
  color: #89A0B0;
  margin-top: 60px;
  grid-gap: 20px;
}
.modal__close{
  position: absolute;
  width: 20px;
  right: 20px;
  top: 24px;
}
.modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.4);
}
.modal__container {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 350px;
  height: 320px;
  background: #EDECE9;
  box-shadow: 11px 11px 18px rgb(0 0 0 / 6%);
  border-radius: 16px;
  color: #89A0B0;
  padding: 25px;
  box-sizing: border-box;
}
</style>
