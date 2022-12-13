<template>
  <div
    class="mx-auto flex min-h-[calc(100vh-44px)] max-w-3xl flex-col items-center justify-center p-4 text-center"
  >
    <header class="mb-4">
      <h2 class="mb-2 text-2xl font-bold text-slate-800 sm:text-4xl">
        😋 Quick meal ideas
      </h2>
      <p className="text-slate-500 leading-relaxed">
        Say goodbye to searching for recipes, scrolling through cookbooks and
        staring at your fridge trying to figure out what to make. Check out some
        of these delicious ideas and enjoy 👇
      </p>
    </header>
    <main class="grid w-full grid-cols-1 gap-2 sm:grid-cols-2 sm:gap-4">
      <div
        v-for="({ title, meal }, index) of menu"
        :key="title"
        class="flex w-full flex-col items-center rounded-lg border border-slate-100 bg-white p-5 shadow-lg"
      >
        <p class="mb-1 text-lg font-semibold text-slate-800 sm:text-xl">
          {{ title }}
        </p>
        <p class="mb-3 text-slate-700">{{ meal }}</p>
        <div class="mt-auto space-x-1">
          <button class="button" @click="handleRefresh(index)">
            🔄 Refresh
          </button>
          <a
            class="button"
            :href="`https://google.com/search?q=${meal}`"
            target="_blank"
            rel="noopener noreferrer"
          >
            🔗 Search
          </a>
        </div>
      </div>
    </main>
  </div>
  <footer class="px-4 py-3">
    <p class="text-center text-sm text-slate-600">
      Like this project? Leave a
      <a href="https://github.com/rago4/meal-ideas" class="text-indigo-500">
        star
      </a>
      ⭐️
    </p>
  </footer>
</template>

<script setup lang="ts">
import { computed, ref } from "vue";
import { breakfast, dinner, lunch, snacks } from "./meals";

function random() {
  return Math.floor(Math.random() * 10);
}

function handleRefresh(index: number) {
  indexes.value.splice(index, 1, random());
}

const indexes = ref(Array.from({ length: 4 }).map(random));

const menu = computed(() => [
  { title: "🥣 Breakfast", meal: breakfast[indexes.value[0]] },
  { title: "🍔 Lunch", meal: lunch[indexes.value[1]] },
  { title: "🍝 Dinner", meal: dinner[indexes.value[2]] },
  { title: "🍿 Snack", meal: snacks[indexes.value[3]] },
]);
</script>

<style scoped>
.button {
  @apply inline-block rounded bg-slate-200 px-2 py-1.5 text-sm font-medium text-slate-700 hover:bg-slate-300;
}
</style>
