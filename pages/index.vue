<template>
  <div class="flex justify-center p-2 bg-gray-700 h-full sm:h-screen">
    <div
      class="
        principal
        w-11/12
        bg-gray-700
        grid
        gap-4
        p-4
        sm:grid-cols-2
        lg:grid-cols-3 lg:p-8
      "
    >
      <div
        class="w-full bg-gray-500 h-auto flex flex-row rounded lg:h-48"
        v-for="items of dataResult"
        :key="items.id"
      >
        <img
          :src="`${items.image}`"
          alt=""
          class="w-5/12 h-auto rounded-l bg-cover bg-center"
        />
        <div
          class="
            w-full
            rounded-r
            flex flex-col
            justify-between
            p-2
            text-white
            gap-2
          "
        >
          <div class="h-10 leading-none">
            <p class="font-semibold text-sm sm:text-lg">{{ items.name }}</p>
            <span
              class="inline-block text-sm h-2 w-2 bg-green-600 rounded-full"
              v-if="items.status === 'Alive'"
            ></span>
            <span
              class="inline-block text-sm h-2 w-2 bg-red-600 rounded-full"
              v-if="items.status === 'Dead'"
            ></span>
            <span
              class="inline-block text-sm h-2 w-2 bg-gray-400 rounded-full"
              v-if="items.status === 'unknown'"
            ></span>
            <p class="text-xs inline-block font-medium">
              {{ items.status }} - {{ items.species }}
            </p>
          </div>

          <div class="h-10 leading-none pt-2">
            <p class="text-xs text-gray-400 font-semibold">
              Last know location:
            </p>
            <p class="text-xs leading-none text-gray-200 font-semibold">
              {{ items.location.name }}
            </p>
          </div>

          <div class="h-12 leading-none pt-2 mb-2">
            <p class="text-xs text-gray-400 font-semibold">First seen in:</p>
            <p class="text-xs text-gray-200 font-semibold">
              {{ items.origin.name }}
            </p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  fetch() {
    this.$axios.get("/character/1,2,3,7,12,16").then((res) => {
      this.dataResult = res.data;
    });
  },
  fetchOnServer: false,
  data() {
    return {
      dataResult: [],
    };
  },
};
</script>