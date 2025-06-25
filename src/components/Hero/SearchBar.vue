<template>
  <form class="search-bar" @click.stop>
    <div class="search-group">
      <span class="search-icon" v-html="LocationIcon"></span>
      <span class="search-label city-label" @click="toggleCityMenu">
        <template v-if="selectedCity">{{ selectedCity }}</template>
        <template v-else><span class="city-placeholder">Выберите город</span></template>
      </span>
      <span v-if="selectedCity" class="search-clear" v-html="CloseIcon" @click.stop="clearCity"></span>
      <span class="search-divider"></span>
      <span class="search-icon" v-html="CalendarIcon"></span>
      <flat-pickr
        v-model="dateValue"
        :config="flatpickrConfig"
        class="flatpickr-input-custom"
        ref="flatpickrRef"
        :placeholder="dateLabel"
        @on-close="onDateClose"
        @on-change="onDateChange"
      />
      <span class="search-divider"></span>
      <span class="search-icon" v-html="UserIcon"></span>
      <span class="search-label guests-label" @click="toggleGuestsMenu">{{ guestsLabel }}</span>
      <div v-if="showCityMenu" class="city-dropdown">
        <input
          v-model="citySearch"
          class="city-search-input"
          type="text"
          placeholder="Поиск города..."
          @click.stop
        />
        <div v-for="city in filteredCities" :key="city" class="city-dropdown-item" :class="{active: city === selectedCity}" @click.stop="selectCity(city)">
          {{ city }}
        </div>
        <div v-if="filteredCities.length === 0" class="city-dropdown-empty">Город не найден</div>
      </div>
      <div v-if="showGuestsMenu" class="guests-dropdown" @click.stop>
        <div class="guests-row">
          <span>Взрослые</span>
          <div class="guests-controls">
            <button type="button" class="guests-btn" @click="changeGuests('adults', -1)" :disabled="adults <= 1">-</button>
            <span class="guests-value">{{ adults }}</span>
            <button type="button" class="guests-btn" @click="changeGuests('adults', 1)">+</button>
          </div>
        </div>
        <div class="guests-row">
          <span>Дети</span>
          <div class="guests-controls">
            <button type="button" class="guests-btn" @click="changeGuests('children', -1)" :disabled="children <= 0">-</button>
            <span class="guests-value">{{ children }}</span>
            <button type="button" class="guests-btn" @click="changeGuests('children', 1)">+</button>
          </div>
        </div>
        <div class="guests-row">
          <span>Номера</span>
          <div class="guests-controls">
            <button type="button" class="guests-btn" @click="changeGuests('rooms', -1)" :disabled="rooms <= 1">-</button>
            <span class="guests-value">{{ rooms }}</span>
            <button type="button" class="guests-btn" @click="changeGuests('rooms', 1)">+</button>
          </div>
        </div>
      </div>
    </div>
    <button class="search-btn" type="submit">
      Найти
      <span class="search-btn-icon" v-html="SearchIcon"></span>
    </button>
  </form>
</template>

<script setup>
import { ref, computed, onMounted, onBeforeUnmount } from 'vue'
import FlatPickr from 'vue-flatpickr-component'
import 'flatpickr/dist/flatpickr.min.css'
import { Russian } from 'flatpickr/dist/l10n/ru.js'
import LocationIcon from '@/assets/svg/Location.svg?raw'
import CalendarIcon from '@/assets/svg/Calendar.svg?raw'
import UserIcon from '@/assets/svg/users.svg?raw'
import CloseIcon from '@/assets/svg/close.svg?raw'
import SearchIcon from '@/assets/svg/search-normal.svg?raw'

const cities = [
  'Пекин, Китай',
  'Алматы, Казахстан',
  'Лондон, Великобритания',
  'Париж, Франция',
  'Нью-Йорк, США',
  'Токио, Япония',
  'Берлин, Германия',
  'Сеул, Южная Корея',
  'Сидней, Австралия',
  'Дубай, ОАЭ',
]
const selectedCity = ref(cities[0])
const showCityMenu = ref(false)
const citySearch = ref('')
const dateValue = ref([])
const showGuestsMenu = ref(false)
const adults = ref(0)
const children = ref(0)
const rooms = ref(0)
const flatpickrRef = ref(null)

const filteredCities = computed(() => {
  if (!citySearch.value.trim()) return cities
  return cities.filter(city => city.toLowerCase().includes(citySearch.value.trim().toLowerCase()))
})

const dateLabel = computed(() => {
  if (!dateValue.value || dateValue.value.length === 0) return 'Выберите даты'
  if (Array.isArray(dateValue.value) && dateValue.value.length === 2 && dateValue.value[0] && dateValue.value[1]) {
    return `${formatDate(dateValue.value[0])} - ${formatDate(dateValue.value[1])}`
  }
  if (Array.isArray(dateValue.value) && dateValue.value.length === 1 && dateValue.value[0]) {
    return formatDate(dateValue.value[0])
  }
  return 'Выберите даты'
})

const guestsLabel = computed(() => {
  if (adults.value === 0 && children.value === 0 && rooms.value === 0) {
    return 'Выберите, кто поедет и номер'
  }
  return `${adults.value} взрослый${adults.value > 1 ? 'х' : ''} - ${children.value} детей - ${rooms.value} номер${rooms.value > 1 ? 'а' : ''}`
})

function formatDate(date) {
  if (!date) return ''
  const d = new Date(date)
  return d.toLocaleDateString('ru-RU', { weekday: 'short', day: 'numeric', month: 'short' })
}

function toggleCityMenu(e) {
  showCityMenu.value = !showCityMenu.value
  if (showCityMenu.value) {
    citySearch.value = ''
  }
  showGuestsMenu.value = false
}
function selectCity(city) {
  selectedCity.value = city
  showCityMenu.value = false
}
function clearCity() {
  selectedCity.value = ''
  showCityMenu.value = false
}
function handleClickOutside(e) {
  showCityMenu.value = false
  showGuestsMenu.value = false
}
function onDateChange(selectedDates) {
  if (selectedDates.length === 1 || selectedDates.length === 2) {
    dateValue.value = selectedDates
  }
}
function onDateClose() {}
function toggleGuestsMenu() {
  showGuestsMenu.value = !showGuestsMenu.value
  showCityMenu.value = false
}
function changeGuests(type, delta) {
  if (type === 'adults') adults.value = Math.max(0, adults.value + delta)
  if (type === 'children') children.value = Math.max(0, children.value + delta)
  if (type === 'rooms') rooms.value = Math.max(0, rooms.value + delta)
}
const flatpickrConfig = {
  mode: 'range',
  locale: Russian,
  dateFormat: 'D, j M',
  allowInput: false,
  minDate: 'today',
  altInput: false,
  static: false,
  position: 'auto',
  onChange: (selectedDates, dateStr, instance) => {
    if (selectedDates.length === 1) {
      dateValue.value = [selectedDates[0]]
    } else if (selectedDates.length === 2) {
      dateValue.value = [selectedDates[0], selectedDates[1]]
    }
  },
  onClose: () => {},
}
onMounted(() => {
  window.addEventListener('click', handleClickOutside)
})
onBeforeUnmount(() => {
  window.removeEventListener('click', handleClickOutside)
})
</script>

<style scoped>
.search-bar {
  display: flex;
  align-items: center;
  background: #fff;
  border-radius: 24px;
  box-shadow: 0 4px 24px rgba(0,0,0,0.10);
  padding: 0 0 0 24px;
  min-width: 720px;
  max-width: 1280px;
  width: 100%;
  height: 64px;
  gap: 0;
  position: relative;
}
.search-group {
  display: flex;
  align-items: center;
  gap: 18px;
  font-size: 1.15rem;
  font-weight: 500;
  color: #18181b;
  min-width: 0;
  flex: 1;
  white-space: nowrap;
  position: relative;
}
.city-label {
  cursor: pointer;
  color: #111111;
  position: relative;
  z-index: 2;
}
.city-dropdown {
  position: absolute;
  top: 120%;
  left: 0;
  min-width: 220px;
  background: #fff;
  border-radius: 12px;
  box-shadow: 0 4px 16px rgba(0,0,0,0.10);
  z-index: 10;
  padding: 6px 0 6px 0;
  font-size: 1rem;
  color: #222;
  display: flex;
  flex-direction: column;
  gap: 0;
}
.city-search-input {
  width: 90%;
  margin: 6px auto 8px auto;
  padding: 8px 12px;
  border-radius: 8px;
  border: 1px solid #e5e7eb;
  font-size: 1rem;
  outline: none;
  transition: border 0.2s;
  background: #f6f8fa;
  color: #18181b;
}
.city-search-input:focus {
  border: 1.5px solid #2563eb;
}
.city-dropdown-item {
  padding: 10px 18px;
  cursor: pointer;
  transition: background 0.18s, color 0.18s;
  white-space: nowrap;
}
.city-dropdown-item:hover, .city-dropdown-item.active {
  background: #2563eb;
  color: #fff;
}
.city-dropdown-empty {
  padding: 10px 18px;
  color: #888;
  font-size: 0.98rem;
  text-align: center;
}
.search-icon {
  font-size: 1.3em;
  color: #2563eb;
}
.search-label {
  overflow: hidden;
  text-overflow: ellipsis;
}
.search-clear {
  color: #888;
  font-size: 1.2em;
  margin-left: 8px;
  cursor: pointer;
  transition: color 0.2s;
}
.search-clear:hover {
  color: #2563eb;
}
.search-divider {
  display: inline-block;
  width: 1px;
  height: 32px;
  background: #e5e7eb;
  margin: 0 12px;
}
.search-btn {
  display: flex;
  align-items: center;
  gap: 10px;
  background: #2563eb;
  color: #fff;
  border: none;
  border-radius: 16px;
  width: 130px;
  height: 70px;
  padding: 16px 23px;
  font-size: 1.15rem;
  font-weight: 500;
  cursor: pointer;
  transition: background 0.2s;
  right: 0;
  top: 0;
  font-family: 'Inter', sans-serif;
}
.search-btn:hover {
  background: #1746b3;
}
.search-btn-icon {
  display: flex;
  align-items: center;
}
.date-label {
  cursor: pointer;
  color: #2563eb;
  position: relative;
  z-index: 2;
}
.flatpickr-input-custom {
  border: none;
  background: transparent;
  font-size: 1.15rem;
  font-weight: 500;
  color: #18181b;
  outline: none;
  min-width: 220px;
  max-width: 320px;
  padding: 0 0 0 0;
  margin: 0;
  height: 32px;
  display: inline-block;
  vertical-align: middle;
}
.flatpickr-input-custom::placeholder {
  color: #111111;
  font-weight: 400;
}
.guests-label {
  cursor: pointer;
  color: #111111;
  position: relative;
  z-index: 2;
}
.guests-dropdown {
  position: absolute;
  top: 120%;
  left: 90%;
  transform: translateX(-90%);
  background: #fff;
  border-radius: 16px;
  box-shadow: 0 4px 24px rgba(0,0,0,0.10);
  z-index: 20;
  padding: 18px 24px 12px 24px;
  min-width: 320px;
  display: flex;
  flex-direction: column;
  gap: 12px;
  align-items: stretch;
}
.guests-row {
  display: flex;
  align-items: center;
  justify-content: space-between;
  font-size: 1.08rem;
  font-weight: 500;
  color: #18181b;
}
.guests-controls {
  display: flex;
  align-items: center;
  gap: 10px;
}
.guests-btn {
  width: 32px;
  height: 32px;
  border-radius: 50%;
  border: none;
  background: #f3f6fa;
  color: #2563eb;
  font-size: 1.2rem;
  font-weight: bold;
  cursor: pointer;
  transition: background 0.18s, color 0.18s;
  display: flex;
  align-items: center;
  justify-content: center;
  font-family: 'Inter', sans-serif;
}
.guests-btn:disabled {
  background: #f3f3f3;
  color: #bbb;
  cursor: not-allowed;
}
.guests-value {
  min-width: 24px;
  text-align: center;
  font-size: 1.1rem;
  font-weight: 600;
}
@media (max-width: 900px) {
  .search-bar {
    min-width: 320px;
    max-width: 98vw;
    padding-left: 10px;
    height: 54px;
  }
  .search-btn {
    height: 54px;
    padding: 0 18px;
    font-size: 1rem;
  }
  .search-group {
    font-size: 1rem;
    gap: 10px;
  }
  .search-divider {
    height: 24px;
    margin: 0 6px;
  }
  .city-dropdown {
    min-width: 140px;
    font-size: 0.98rem;
  }
}
.city-placeholder {
  color: #111111;
  font-weight: 400;
}
</style> 