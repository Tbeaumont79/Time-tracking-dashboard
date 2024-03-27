<script setup lang="ts">
import { onMounted, ref } from "vue";
import CardActivity from "./components/CardActivity.vue";
const data = ref();
let selected = ref("Daily");
const options = ref([
  { id: 1, value: "Daily" },
  { id: 2, value: "Weekly" },
  { id: 3, value: "Monthly" },
]);
const activityHeaderCard = ref([
  { id: 1, img: "../src/assets/images/icon-work.svg", color: "#FF8A63" },
  { id: 2, img: "../src/assets/images/icon-play.svg", color: "#57C2E6" },
  { id: 3, img: "../src/assets/images/icon-study.svg", color: "#FF5e7C" },
  { id: 4, img: "../src/assets/images/icon-exercise.svg", color: "#4acf81" },
  { id: 5, img: "../src/assets/images/icon-social.svg", color: "#7034D1" },
  { id: 6, img: "../src/assets/images/icon-self-care.svg", color: "#F2c85C" },
]);

const fetchData = async () => {
  const response = await fetch("https://github.com/Tbeaumont79/Time-tracking-dashboard/blob/33fb62ea384f9f13505e13c25c8ac2836ec6bbc5/src/Database/data.json", {
    method: 'GET',
  mode: 'no-cors'
  })
    .then((response) => {
      if (!response.ok) {
        throw new Error("Erreur réseau");
      }
      return response.json();
    })
    .then((data) => {
      return data;
    })
    .catch((error) => {
      console.log(
        "Il y a eu un problème avec l'opération fetch: ",
        error.message
      );
    });

  data.value = response;
};
onMounted(() => {
  fetchData();
});
</script>
<template>
  <div class="container">
    <div class="sub-container">
      <div class="personal-card">
        <div class="identity">
          <img src="./assets/images/image-jeremy.png" alt="" />
          <div class="identity-info">
            <p>Report for</p>
            <h1>Jeremy Robson</h1>
          </div>
        </div>
        <div class="time">
          <input
            v-for="option in options"
            :value="option.value"
            :key="option.id"
            @click="selected = option.value"
            type="button"
          />
        </div>
      </div>
      <div class="all-card">
        <div class="card" v-for="item in data" :key="item">
          <div
            class="header-card"
            :style="{ backgroundColor: activityHeaderCard[item.id - 1].color }"
          >
            <img :src="activityHeaderCard[item.id - 1].img" alt="item.title" />
          </div>
          <CardActivity :activity="item" :timeFilter="selected" />
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 100vh;
  background-color: var(--vt-c-background);
}
.sub-container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  width: 95%;
  height: 60%;
  gap: 1rem;
}
.personal-card {
  width: 18rem;
  height: 18rem;
  background-color: var(--vt-c-secondary);
  border-radius: 15px;
}
.identity {
  display: flex;
  flex-direction: row;
  gap: 1rem;
  padding: 2rem;
  justify-items: start;
  justify-content: center;
  background: var(--vt-c-accent);
  border-radius: 15px;
}
.identity img {
  width: 3rem;
  height: 3rem;
  border-radius: 50%;
  border: 2px solid #fff;
}
.identity-info h1 {
  color: var(--color-heading);
  font-weight: 500;
  font-size: 1.2rem;
}
.identity-info p {
  font-weight: 300;
  font-size: 0.8rem;
}

.time {
  display: flex;
  justify-content: center;
  align-items: flex-start;
  width: 100%;
  padding: 1rem;
  height: 30%;
}
.time input {
  height: 2rem;
  background-color: var(--vt-c-secondary);
  color: var(--color-secondary);
  border: none;
}
.time input:hover {
  color: var(--color-heading);
}
.time input:focus {
  color: var(--color-heading);
}
.all-card {
  margin-top: 2rem;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
  position: relative;
  width: 70%;
  height: 80%;
  gap: 3rem;
}

.header-card {
  display: flex;
  justify-content: flex-end;
  align-items: center;
  width: 18rem;
  height: 2.5rem;
  border-radius: 15px 15px 0 0;
  position: absolute;
  top: -1.5rem;
}
.header-card img {
  width: 2.5rem;
  height: 2.5rem;
  margin-right: 1rem;
}

.card {
  width: 18rem;
  height: 7rem;
  position: relative;
  background-color: hsl(235, 46%, 20%);
  border-radius: 15px;
  z-index: 1;
}
@media screen and (min-width: 1440px) {
  .sub-container {
    display: flex;
    justify-content: center;
    flex-direction: row;
    align-items: center;
    width: 80%;
    height: 60%;
    gap: 1rem;
  }
  .time {
    display: flex;
    justify-content: center;
    align-items: flex-start;
    width: 100%;
    flex-direction: column;
    padding: 1rem;
    height: 30%;
  }

  .personal-card {
    width: 15rem;
    height: 27rem;
    background-color: var(--vt-c-secondary);
    border-radius: 15px;
  }
  .identity {
    display: flex;
    flex-direction: column;
    gap: 1rem;
    padding: 2rem;
    justify-items: start;
    justify-content: center;
    background: var(--vt-c-accent);
    height: 65%;
    border-radius: 15px;
  }
  .identity-info h1 {
    color: var(--color-heading);
    font-weight: 300;
    font-size: 1.5rem;
  }
  .identity-info p {
    font-weight: 100;
    font-size: 1.2rem;
  }
  .identity img {
    width: 4rem;
    height: 4rem;
    border-radius: 50%;
    border: 2px solid #fff;
  }

  .header-card {
    position: absolute;
    top: -2.5rem;
    width: 15rem;
    height: 4rem;
  }
  .header-card img {
    width: 4rem;
    height: 4rem;
  }

  .card {
    width: 15rem;
    height: 11rem;
  }
  .card:hover {
    background-color: #33387a;
  }
}
</style>
