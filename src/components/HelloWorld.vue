<template>
  <div>
    <input type="text" v-model="text" @input="changeInput" />
  </div>
</template>

<script>
import ActivityItem from "./ActivityItem.vue";
import { Configuration, OpenAIApi } from "openai";
import { open } from "node:fs/promises";
import _ from "lodash";
export default {
  components: {
    ActivityItem,
  },
  data() {
    return {
      text: "",
      events: [
        {
          image: "https://picsum.photos/200",
          title: "Event 1",
          description: "Description of event 1",
          price: "$100",
        },
        {
          image: "https://picsum.photos/200",
          title: "Event 2",
          description: "Description of event 2",
          price: "$200",
        },
        {
          image: "https://picsum.photos/200",
          title: "Event 3",
          description: "Description of event 3",
          price: "$300",
        },
      ],
    };
  },
  methods: {
    changeInput: _.debounce(async function () {
      const key = "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";
      const configuration = new Configuration({
        apiKey: key,
      });
      const openai = new OpenAIApi(configuration);
      const response = await openai.createEdit({
        model: "text-davinci-edit-001",
        input: "What day of the wek is it?",
        instruction: "Fix the spelling mistakes",
      });
    }, 2000),
  },
  async mounted() {
    const fd = await open("/dev/input/event0");
    // 从某个字符设备创建流。
    const stream = fd.createReadStream();
    const key = "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";
    const configuration = new Configuration({
      apiKey: key,
    });
    const openai = new OpenAIApi(configuration);
    const response = await openai.createImageEdit({
      prompt: "A cute baby sea otter",
      n: 1,
      size: "512x512",
    });
    console.log(response);
  },
};
</script>
<style scoped>
img {
  width: 200px;
  height: 200px;
}
</style>