<template>
  <div class="bg-gray-700 principal h-full flex justify-center py-8">
    <div
      class="
        content
        bg-gray-700 bg-opacity-80
        w-11/12
        h-auto
        flex flex-col
        gap-4
        rounded
      "
    >
      <div
        class="w-full bg-gray-500 h-auto flex flex-row rounded"
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
            <p class="font-semibold text-sm">{{ items.name }}</p>
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

          <div class="h-10 leading-none pt-2">
            <p class="text-xs text-gray-400 font-semibold">First seen in:</p>
            <p class="text-sm text-gray-200 font-semibold">Pilot</p>
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
      console.log(this.dataResult);
      console.log(res.data);

      /* this.$axios.get(`${res.data.episode}`) */
    });
  },
  fetchOnServer: false,
  data() {
    return {
      urlImage: "https://rickandmortyapi.com/api/character/avatar/1.jpeg",
      dataResult: [],
    };
  },
};
</script>