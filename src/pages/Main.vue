<template>
  <div class="page">
    <ModalWindow
      :staff="staff"
      @close="openModal = false"
      @save="addPerson($event)"
      v-if="openModal"
    />
    <Button class="page__button" title="Добавить" @click.native="openModal = true"/>
    <div class="table">
      <div class="table__item  table__header">
        <div class="header__text" @click="sort('name')">Имя</div>
        <div class="header__arrows">
          <img class="arrow"
            src="@/assets/arrow-up.png"
            :class="(activeSort.name === 'name' && activeSort.increase) ? 'arrow__focus' : ''"
          >
          <img class="arrow"
            src="@/assets/arrow-down.png"
            :class="(activeSort.name === 'name' && !activeSort.increase) ? 'arrow__focus' : ''"
          >
        </div>
      </div>
      <div class="table__item  table__header">
        <div class="header__text" @click="sort('phone')">Телефон</div>
        <div class="header__arrows">
          <img class="arrow"
            src="@/assets/arrow-up.png"
            :class="(activeSort.name === 'phone' && activeSort.increase) ? 'arrow__focus' : ''"
          >
          <img class="arrow"
            src="@/assets/arrow-down.png"
            :class="(activeSort.name === 'phone' && !activeSort.increase) ? 'arrow__focus' : ''"
          >
        </div>
      </div>
      <template v-for="(person, index) in staff">
        <div class="table__item" :key="'name' + index">{{ person.name}}</div>
        <div class="table__item" :key="'phone' + index">{{ person.phone }}</div>
      </template>
    </div>
  </div>
</template>

<script>
import Button from '@/components/Button'
import ModalWindow from '@/components/ModalWindow'
export default {
  name: 'Main',
  components: {
    Button,
    ModalWindow
  },
  data () {
    return {
      openModal: false,
      staff: [],
      activeSort: {
        name: '',
        increase: true
      }
    }
  },
  methods: {
    addPerson (person) {
      this.staff.push(person)
      this.openModal = false
      localStorage.staff = JSON.stringify(this.staff)
    },
    sort (name) {
      if (this.activeSort.name === name) {
        this.activeSort.increase = !this.activeSort.increase
      } else {
        this.activeSort.name = name
        this.activeSort.increase = true
      }
      if (name === 'name') {
        if (this.activeSort.increase) {
          this.staff.sort((a, b) => (a.name).localeCompare(b.name))
        } else {
          this.staff.sort((a, b) => (b.name).localeCompare(a.name))
        }
      } else {
        if (this.activeSort.increase) {
          this.staff.sort((a, b) => a.phone - b.phone)
        } else {
          this.staff.sort((a, b) => b.phone - a.phone)
        }
      }
    }
  },
  mounted () {
    this.staff = JSON.parse(localStorage.staff)
  }
}
</script>

<style scoped>
.page {
  width: max-content;
  padding: 75px 0;
  margin: 0 auto;
}
.page__button {
  margin-left: auto;
  margin-right: 12px;
  display: flex;
}
.table {
  display: grid;
  grid-template-columns: calc(100% - 200px) 200px;
  color: #89A0B0;
  background-color: #FFFFFF;
  border-radius: 6px;
  box-shadow: 0px 6px 18px rgb(0 0 0 / 6%);
  margin: 20px auto 20px auto;
  padding: 12px;
  width: max-content;
}
.table__item {
  padding: 10px;
  border: 1px solid #CFD8DC;
  border-top: none;
}
.header__text {
  cursor: pointer;
}
.arrow {
  width: 12px;
  height: 7px;
  opacity: 0.4;
}
.arrow__focus {
  opacity: 1;
}
.table__header {
  display: flex;
  min-width: 70px;
  justify-content: space-between;
  border-top: 1px solid #CFD8DC;
}
.header__arrows {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-around;
}
</style>
