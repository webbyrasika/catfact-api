<template>
  <div class="text-center">
    <!-- <h2>Cat Fats</h2> -->

    <div
      class="p-4 mt-6 mb-4 text-lg text-blue-700 bg-blue-200 rounded-base dark:bg-blue-200 dark:text-blue-800"
    >
      <span class="font-medium"> {{ result.fact }}</span>
      <!-- <img
          src="https://i.pinimg.com/736x/6b/79/df/6b79df7e9cf368f4ff22ddb50b45b819.jpg"
          alt=""
          class="max-w-xs h-auto"
        /> -->
    </div>
  </div>

  <div class="inline-flex">
    <button
      @click="preLoad"
      class="bg-gray-300 hover:bg-gray-400 text-gray-800 font-bold py-2 px-4 rounded-l"
    >
      Prev
    </button>
    <button
      @click="loadMore"
      class="bg-gray-300 hover:bg-gray-400 text-gray-800 font-bold py-2 px-4 rounded-r"
    >
      Next
    </button>

    <button
      class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded"
    >
      <router-link to="/"> Logout</router-link>
    </button>
  </div>

  <div class="flex justify-center">
    <div class="mb-3 xl:w-96">
      <div
        class="input-group relative flex flex-wrap items-stretch w-full mb-4"
      >
        <input
          type="search"
          v-model="search"
          class="form-control relative flex-auto min-w-0 block w-full px-3 py-1.5 text-base font-normal text-gray-700 bg-white bg-clip-padding border border-solid border-gray-300 rounded transition ease-in-out m-0 focus:text-gray-700 focus:bg-white focus:border-blue-600 focus:outline-none"
          placeholder="Search Cat Breed Name"
          aria-label="Search"
          @keypress="catFactSearch"
        />
        <ul
          v-if="search"
          class="form-control relative flex-auto min-w-0 block w-full px-3 py-1.5 text-base font-normal text-gray-700 bg-white bg-clip-padding border border-solid border-gray-300 rounded transition ease-in-out m-0 focus:text-gray-700 focus:bg-white focus:border-blue-600 focus:outline-none"
        >
          <li
            v-for="item in fetchEntry()"
            :key="item.breed"
            class="p-6 text-center flex flex-col items-center bg-white rounded-lg border shadow-md md:flex-row max-w-xl hover:bg-gray-100 dark:border-gray-700 dark:bg-gray-800 dark:hover:bg-gray-700"
          >
            <img
              class="object-contain h-32 w-80"
              src="https://as2.ftcdn.net/v2/jpg/03/35/68/15/1000_F_335681545_kbojstRCD25Ld9eXgQ8KQbJoQv62x89Y.jpg"
              alt=""
            />
            <p class="font-bold">{{ item.breed }}</p>
            {{ item.country }}, {{ item.coat }}
          </li>
        </ul>
      </div>
    </div>
  </div>

  <div
    class="flex justify-center"
    v-for="item in fetchEntry()"
    :key="item.breed"
  >
    <ul class="bg-white rounded-lg border border-gray-400 w-96 text-gray-900">
      <li class="px-6 py-2 border-b border-gray-300 w-full rounded-t-lg">
        {{ item.breed }}
      </li>
    </ul>
  </div>

  <!-- <div>
    <div
      v-for="item in fetchEntry()"
      :key="item.breed"
      class="p-6 text-center flex flex-col items-center bg-white rounded-lg border shadow-md md:flex-row max-w-xl hover:bg-gray-100 dark:border-gray-700 dark:bg-gray-800 dark:hover:bg-gray-700"
    >
      <img
        class="object-cover w-full h-96 rounded-t-lg md:h-auto md:w-48 md:rounded-none md:rounded-l-lg"
        src="https://as2.ftcdn.net/v2/jpg/03/35/68/15/1000_F_335681545_kbojstRCD25Ld9eXgQ8KQbJoQv62x89Y.jpg"
        alt=""
      />
      <div class="flex flex-col justify-between p-4 leading-normal">
        <h5
          class="mb-2 text-2xl font-bold tracking-tight text-gray-900 dark:text-white"
        >
          {{ item.breed }}
        </h5>
        <p class="mb-3 font-normal text-gray-700 dark:text-gray-400">
          
     <ul class="space-y-1 max-w-md list-none list-inside text-gray-500 dark:text-gray-400">
    <li>
       Country :{{ item.country }}
    </li>
    <li>
         Coat: {{ item.coat }}
    </li>
    <li>
       Origin:{{ item.origin }}
    </li>
    <li>Pattern:{{ item.pattern }}</li>
</ul>
        </p>
      </div>
    </div>
  </div> -->
</template>

<script lang="ts" setup>
import { defineComponent, ref } from "vue";
import axios from "axios";
import { RouterLink } from "vue-router";

const result = ref({});
const res = ref<any>({});
const search = ref("");

//method for facts

axios.get("https://catfact.ninja/fact").then((response) => {
  console.log(response.data);
  result.value = response.data;
  localStorage.setItem("factSearch", JSON.stringify(result.value));
});

const catFactSearch = () => {
  axios.get("https://catfact.ninja/fact").then((response) => {
    console.log(response.data);
    result.value = response.data;
    localStorage.setItem("factSearch", JSON.stringify(response.data));
    result.value = "";
    result.value = JSON.parse(localStorage.getItem("factSearch"));
  });
};

// method for breed names
axios.get("https://catfact.ninja/breeds").then((response) => {
  console.log(response.data);
  res.value = response.data;
  localStorage.setItem("fetchData", JSON.stringify(response.data));
});

const preLoad = async () => {
  const response = await axios.get("https://catfact.ninja/breeds");
  console.log(response.data);
  res.value = await response.data;
};

const loadMore = async () => {
  const response = await axios.get("https://catfact.ninja/breeds?page=2");
  console.log(response.data);
  res.value = await response.data;
};

const fetchEntry = () => {
  return res.value.data.filter((item: any) =>
    item.breed.toLowerCase().includes(search.value.toLowerCase())
  );
};
</script>
