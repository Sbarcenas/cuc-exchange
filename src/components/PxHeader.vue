<template>
  <header class="shadow w-screen">
    <nav>
      <nav class="flex items-center justify-between flex-wrap bg-green-400 p-6">
        <div class="flex items-center flex-shrink-0 text-white mr-6">
          <px-icon class="mr-2" />
          <router-link
            :to="{ name: 'home' }"
            class="font-semibold text-xl tracking-tight"
            >Cuc Exchange</router-link
          >
        </div>
        <div
          class="hidden sm:block w-full block flex-grow lg:flex lg:items-center lg:w-auto"
        >
          <div class="text-sm lg:flex-grow">
            <router-link
              v-for="l in links"
              :key="l.title"
              :to="l.to"
              class="block mt-4 lg:inline-block lg:mt-0 text-teal-200 hover:text-white mr-4"
              >{{ l.title }}</router-link
            >
          </div>
          <div class="block mt-4 lg:inline-block lg:mt-0  text-white mr-4">
            Tiempo en linea: {{ onlineTime }}
          </div>
        </div>
      </nav>
    </nav>
  </header>
</template>

<script>
import PxIcon from '@/components/PxIcon'
import moment from 'moment'

export default {
  name: 'PxHeader',
  components: { PxIcon },
  data() {
    return {
      startTime: moment(),
      actualTime: moment()
    }
  },
  props: {
    links: {
      type: Array,
      default: () => []
    }
  },
  computed: {
    onlineTime() {
      return this.actualTime.diff(this.startTime, 'seconds')
    }
  },
  created() {
    setInterval(() => (this.actualTime = moment()), 1000)
  }
}
</script>
