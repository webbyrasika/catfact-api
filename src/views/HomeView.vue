<template>
  <div class="p-10">
    <section class="bg-gray-50 dark:bg-gray-900">
      <div
        class="flex flex-col items-center justify-center px-6 py-8 mx-auto md:h-screen lg:py-0"
      >
        <div
          class="w-full bg-white rounded-lg shadow dark:border md:mt-0 sm:max-w-md xl:p-0 dark:bg-gray-800 dark:border-gray-700"
        >
          <div class="flex flex-wrap p-4 justify-center">
            <img
              src="https://www.somerzby.com.au/wp-content/uploads/2018/04/the-ultimate-list-of-cat-breeds-update-2018-800x800.jpg"
              class="p-1 bg-white border rounded max-w-xs"
              alt="..."
            />
          </div>
          <div class="p-6 space-y-4 md:space-y-8 sm:p-8">
            <h1
              class="text-xl font-bold leading-tight tracking-tight text-gray-900 md:text-2xl dark:text-white"
            >
              Sign in to your account
            </h1>
            <form
              @submit.prevent="handleLogin"
              class="space-y-4 md:space-y-6"
              action="#"
            >
              <div>
                <label
                  for="email"
                  class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
                  >Your email</label
                >
                <input
                  type="email"
                  v-model="form.email"
                  id="email"
                  class="bg-gray-50 border border-gray-300 text-gray-900 sm:text-sm rounded-lg focus:ring-primary-600 focus:border-primary-600 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
                  placeholder="name@company.com"
                  required=""
                />
              </div>
              <div>
                <label
                  for="password"
                  class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
                  >Password</label
                >
                <input
                  type="password"
                  v-model="form.password"
                  id="password"
                  placeholder="••••••••"
                  class="bg-gray-50 border border-gray-300 text-gray-900 sm:text-sm rounded-lg focus:ring-primary-600 focus:border-primary-600 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
                  required=""
                />
              </div>

              <button
                type="submit"
                class="w-full bg-blue-500 bg-primary-700 hover:bg-primary-700 focus:ring-4 focus:outline-none focus:ring-primary-300 font-medium rounded-lg text-sm px-5 py-2.5 text-center dark:bg-primary-600 dark:hover:bg-primary-700 dark:focus:ring-primary-800"
              >
                Sign in
              </button>
              <!-- <p class="text-sm font-light text-gray-500 dark:text-gray-400">
                Don’t have an account yet?
                <a
                  href="#"
                  class="font-medium text-primary-600 hover:underline dark:text-primary-500"
                  >Sign up</a
                >
              </p> -->
            </form>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script lang="ts">
import { defineComponent, reactive, ref } from "vue";
import { useRouter } from "vue-router";

export default defineComponent({
  name: "HomeView",
  components: {},
  setup() {
    const router = useRouter();
    const form = reactive({
      email: "",
      password: "" as string | number,

      mockEmail: "admin@gmail.com",
      mockPass: "2468" as string | number,
    });
    const handleLogin = () => {
      console.log("You are successfully Logged in.");
      if (form.email != form.mockEmail || form.password != form.mockPass) {
        alert("Please enter valid email or password.");
      } else {
        router.replace({
          name: "about",
        });
      }
    };

    return { form, handleLogin };
  },
});
</script>
