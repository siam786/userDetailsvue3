<template>
  <div class="p-10 space-x-12 space-y-12">
    <div class="pb-12 border-b border-gray-900/10">
      <h2 class="text-base font-semibold leading-7 text-gray-900">Personal Information</h2>
      <p class="mt-1 text-sm leading-6 text-gray-600">
        Use a Details Page where user can edit his/her details
      </p>

      <div class="grid grid-cols-1 mt-10 gap-x-6 gap-y-8 sm:grid-cols-6">
        <div class="sm:col-span-3">
          <label for="fname" class="block text-sm font-medium leading-6 text-gray-900">Name</label>
          <div class="mt-2">
            <input
              type="text"
              name="name"
              id="name"
              autocomplete="name"
              placeholder="Enter your name"
              v-model="user.name"
              class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
            />
          </div>
        </div>

        <div class="sm:col-span-5">
          <label for="email" class="block text-sm font-medium leading-6 text-gray-900"
            >Profile Image</label
          >
          <div class="h-auto max-w-xl rounded-lg">
            <img :src="user.profileImage" alt="jhon doe" />
          </div>
        </div>

        <div class="sm:col-span-3">
          <label for="email" class="block text-sm font-medium leading-6 text-gray-900"
            >Email address</label
          >
          <div class="mt-2">
            <input
              id="email"
              name="email"
              type="email"
              autocomplete="email"
              v-model="user.email"
              placeholder="Enter your email"
              class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
            />
          </div>
        </div>

        <div class="sm:col-span-3">
          <label for="email" class="block text-sm font-medium leading-6 text-gray-900"
            >Birth Date
            <span class="text-red-500 ">Please Change Date Your Birth</span>
            </label
          >
          <div class="mt-2">
            <input
              id="date"
              name="date"
              type="date"
              autocomplete="date"
              v-model="user.birthdate"
              class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
            />
          </div>
        </div>
        <div class="sm:col-span-7">
          <label for="email" class="block text-sm font-medium leading-6 text-gray-900"
            >Description</label
          >
          <div class="mt-2">
            <textarea
              id="text"
              name="text"
              type="text"
              autocomplete="description"
              v-model="user.description"
              placeholder="Enter your Description"
              class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
            />
          </div>
        </div>
      </div>
    </div>
  </div>

  <div class="flex items-center p-8">
    <div class="col-span-6">
      <h2 v-if="birthYear" class="text-2xl text-gray-900 leadin g-7 font-tsemibold">
        Birth Year: {{ birthYear }}
      </h2>
    </div>
    <div class="col-span-6 mx-4">
      <h2 class="text-2xl font-semibold leading-8 text-red-500">{{ votingStatus }}</h2>
    </div>
  </div>
</template>

<script setup>
import { computed, ref, watch } from 'vue'
const user = ref({
  name: 'siam',
  email: 'shohrab.hossain36@gmail.com',
  birthdate: '1989-01-01',
  description: 'This is edit user data description',
  profileImage:
    'https://images.pexels.com/photos/3771807/pexels-photo-3771807.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1'
})

const birthYear = computed(() => {
  if (user.value.birthdate) {
    const birthDate = new Date(user.value.birthdate)
    return birthDate.getFullYear()
  }
  return ''
})

const votingStatus = computed(() => {
  if (user.value.birthdate) {
    const birthDate = new Date(user.value.birthdate)
    const age = new Date().getFullYear() - birthDate.getFullYear()
    return age >= 18 ? 'Eligible for voting' : 'Not eligible for voting'
  }
  return ''
})
watch(
  () => user.value.birthdate,
  (newVal, oldVal) => {
    if (newVal !== oldVal) {
      user.value.birthdate = newVal
    }
  }
)
</script>


