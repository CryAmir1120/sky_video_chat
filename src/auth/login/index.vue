<template>
  <Layout>
    <form action="">
      <section class="bg-gray-50 dark:bg-gray-900 text-start">
        <div
          class="flex flex-col items-center justify-center px-6 py-8 mx-auto md:h-screen lg:py-0"
        >
          <div
            class="w-full bg-white rounded-lg shadow dark:border md:mt-0 sm:max-w-md xl:p-0 dark:bg-gray-800 dark:border-gray-700"
          >
            <div class="p-6 space-y-4 md:space-y-6 sm:p-8">
              <h1
                class="text-xl font-bold leading-tight tracking-tight text-gray-900 md:text-2xl dark:text-white text-center"
              >
                Sign in to your account
              </h1>
              <form class="space-y-4 md:space-y-6" @submit.prevent="submit">
                <div>
                  <label
                    for="email"
                    class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
                  >
                    Your email
                  </label>
                  <input
                    id="email"
                    v-model="email"
                    type="email"
                    name="email"
                    class="bg-gray-50 border border-gray-300 text-gray-900 sm:text-sm rounded-lg focus:ring-sky-600 focus:border-sky-600 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
                    placeholder="name@company.com"
                    required=""
                  />
                </div>
                <div>
                  <label
                    for="password"
                    class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
                  >
                    Password
                  </label>
                  <input
                    id="password"
                    v-model="password"
                    type="password"
                    name="password"
                    placeholder="••••••••"
                    class="bg-gray-50 border border-gray-300 text-gray-900 sm:text-sm rounded-lg focus:ring-sky-600 focus:border-sky-600 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
                    required=""
                  />
                </div>
                <div class="flex items-center justify-between">
                  <div class="flex items-start">
                    <div class="flex items-center h-5">
                      <input
                        id="remember"
                        v-model="remember"
                        aria-describedby="remember"
                        type="checkbox"
                        class="w-4 h-4 border border-gray-300 rounded bg-gray-50 focus:ring-3 focus:ring-sky-300 dark:bg-gray-700 dark:border-gray-600 dark:focus:ring-sky-600 dark:ring-offset-gray-800"
                      />
                    </div>
                    <div class="ml-3 text-sm">
                      <label for="remember" class="text-gray-500 dark:text-gray-300">
                        Remember me
                      </label>
                    </div>
                  </div>
                  <a
                    href="#"
                    class="dark:text-gray-100 text-sm font-medium text-sky-600 hover:underline dark:text-sky-500"
                  >
                    Forgot password?
                  </a>
                </div>
                <button
                  type="submit"
                  class="w-full text-white bg-sky-600 hover:bg-sky-700 focus:ring-4 focus:outline-none focus:ring-sky-300 font-medium rounded-lg text-sm px-5 py-2.5 text-center dark:bg-sky-600 dark:hover:bg-sky-700 dark:focus:ring-sky-800"
                >
                  Sign in
                </button>
                <p
                  class="text-sm font-light text-gray-500 dark:text-gray-400 text-center"
                >
                  Don’t have an account yet?
                  <router-link
                    :to="{ name: 'register' }"
                    class="font-medium text-sky-600 hover:underline dark:text-sky-500"
                  >
                    Sign up
                  </router-link>
                </p>
              </form>
            </div>
          </div>
        </div>
      </section>
    </form>
  </Layout>
</template>
<script>
export default {
  data() {
    return {
      email: null,
      password: null,
      remember: false,
    };
  },
  methods: {
    async submit() {
      try {
        const { user, error } = await window.supabase.auth.signInWithPassword({
          email: this.email,
          password: this.password,
          remember: this.remember,
        });
        if (error) {
          console.error("Error logging in:", error);
          return;
        }
        this.$router.push({ name: "room" });
      } catch (error) {
        console.error("Error logging in:", error.message);
      }
    },
  },
};
</script>
