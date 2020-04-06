<template>
  <div>
    <b-dropdown id="dropdown-1" size="sm" text="Select Category:" class="m-md-2">
      <b-dropdown-item
        v-for="api in apis"
        :key="api.id"
        :value="api.api"
        @click="dropdownChoose(api.api, api.name)"
      >{{ api.name }}</b-dropdown-item>
    </b-dropdown>
  </div>
</template>

<script>
export default {
  props: {
    fetchApi: Function
  },
  data() {
    return {
      apis: [
        {
          id: 1,
          name: "Any Category",
          api: "https://opentdb.com/api.php?amount=10&type=multiple"
        },
        {
          id: 25,
          name: "Art",
          api: "https://opentdb.com/api.php?amount=10&category=25&type=multiple"
        },
        {
          id: 21,
          name: "Sports",
          api: "https://opentdb.com/api.php?amount=10&category=21&type=multiple"
        },
        {
          id: 23,
          name: "History",
          api: "https://opentdb.com/api.php?amount=10&category=23&type=multiple"
        },
        {
          id: 27,
          name: "Animals",
          api: "https://opentdb.com/api.php?amount=10&category=27&type=multiple"
        },
        {
          id: 24,
          name: "Politics",
          api: "https://opentdb.com/api.php?amount=10&category=24&type=multiple"
        },
        {
          id: 28,
          name: "Vehicles",
          api: "https://opentdb.com/api.php?amount=10&category=28&type=multiple"
        },
        {
          id: 20,
          name: "Mythology",
          api: "https://opentdb.com/api.php?amount=10&category=20&type=multiple"
        },
        {
          id: 22,
          name: "Geography",
          api: "https://opentdb.com/api.php?amount=10&category=22&type=multiple"
        },
        {
          id: 26,
          name: "Celebrities",
          api: "https://opentdb.com/api.php?amount=10&category=26&type=multiple"
        },
        {
          id: 9,
          name: "General Knowledge",
          api: "https://opentdb.com/api.php?amount=10&category=9&type=multiple"
        },
        {
          id: 17,
          name: "Science & Nature",
          api: "https://opentdb.com/api.php?amount=10&category=17&type=multiple"
        },
        {
          id: 18,
          name: "Science: Computers",
          api: "https://opentdb.com/api.php?amount=10&category=18&type=multiple"
        },
        {
          id: 19,
          name: "Science: Mathematics",
          api: "https://opentdb.com/api.php?amount=10&category=19&type=multiple"
        },
        {
          id: 30,
          name: "Science: Gadgets",
          api: "https://opentdb.com/api.php?amount=10&category=30&type=multiple"
        },
        {
          id: 10,
          name: "Entertainment: Books",
          api: "https://opentdb.com/api.php?amount=10&category=10&type=multiple"
        },
        {
          id: 11,
          name: "Entertainment: Film",
          api: "https://opentdb.com/api.php?amount=10&category=11&type=multiple"
        },
        {
          id: 12,
          name: "Entertainment: Music",
          api: "https://opentdb.com/api.php?amount=10&category=12&type=multiple"
        },
        {
          id: 13,
          name: "Entertainment: Musicals & Theatres",
          api: "https://opentdb.com/api.php?amount=10&category=13&type=multiple"
        },
        {
          id: 14,
          name: "Entertainment: Television",
          api: "https://opentdb.com/api.php?amount=10&category=14&type=multiple"
        },
        {
          id: 15,
          name: "Entertainment: Video Games",
          api: "https://opentdb.com/api.php?amount=10&category=15&type=multiple"
        },
        {
          id: 16,
          name: "Entertainment: Board Games",
          api: "https://opentdb.com/api.php?amount=10&category=16&type=multiple"
        },
        {
          id: 29,
          name: "Entertainment: Comics",
          api: "https://opentdb.com/api.php?amount=10&category=29&type=multiple"
        },
        {
          id: 31,
          name: "Entertainment: Japanese Anime & Manga",
          api: "https://opentdb.com/api.php?amount=10&category=31&type=multiple"
        },
        {
          id: 32,
          name: "Entertainment: Cartoon & Animations",
          api: "https://opentdb.com/api.php?amount=10&category=32&type=multiple"
        },
      ]
    };
  },
  methods: {
    dropdownChoose(value, name) {
      this.fetchApi(value, name);
    }
  }
};
</script>

<style scoped>
div {
  position: relative;
  z-index: 1;
  padding-top: 15px;
  padding-bottom: 10px;
  border-bottom-left-radius: 4px;
  border-bottom-right-radius: 4px;
  background-color: #e9ecef;
}

>>> .dropdown-item {
  font-size: 14px !important;
}

>>> .dropdown-item:hover, .dropdown-item:focus {
  background-color: turquoise !important;
}

</style>