<template>
  <h1>Home</h1>
  <div class="container">
    <div class="wrapper">
      <article class="article">
        <section
          v-for="(header, index) in headers"
          :key="index"
          class="section"
        >
          <h2 :id="`${header}`" class="section-title">{{ header }}</h2>
          <p class="section-text">
            Lorem ipsum dolor sit amet consectetur adipisicing elit. Adipisci,
            numquam beatae est ut quae ex qui perspiciatis officia distinctio
            tenetur alias sunt ratione, optio, repellendus molestias ipsa nemo
            perferendis consequatur. Lorem ipsum dolor sit amet, consectetur
            adipisicing elit. Impedit temporibus et, accusantium aut nihil
            voluptatibus nostrum asperiores ratione perferendis reprehenderit ab
            quam, dolorum amet voluptas omnis adipisci atque quasi minima?
            Doloribus vitae ad recusandae numquam quos dicta provident tempore
            nemo fugiat, rerum sunt minus eligendi incidunt qui itaque quod ab
            eum consectetur laudantium odit consequatur nobis. Eaque quae labore
            delectus! Amet, facere dignissimos nesciunt corporis alias
            perspiciatis excepturi! Assumenda dolorum debitis doloribus ipsum
            inventore repudiandae dolore nemo, eligendi tempora unde minima
            velit expedita amet esse iusto qui. Consequuntur, nemo molestias!
            Beatae soluta velit exercitationem sed fugiat molestias totam maxime
            tempore incidunt maiores, ad earum. Recusandae, tempora! Voluptas
            vel dicta id ipsa, ipsam, inventore deserunt mollitia officia esse
            voluptatibus eum facere? Lorem ipsum dolor sit amet, consectetur
            adipisicing elit. Veritatis nihil enim eius quasi repellat nostrum
            obcaecati explicabo placeat voluptatum adipisci, quod, consequuntur
            veniam exercitationem, quidem corporis dolorum asperiores facilis
            dicta. Sit neque mollitia obcaecati hic reprehenderit dolorem odio,
            voluptate magni aliquid tenetur dicta. Minima explicabo molestiae in
            placeat officia modi? Veniam quaerat saepe molestiae eius placeat
            vero enim magnam accusantium! Quos est deserunt blanditiis sint
            eveniet culpa repellat, porro cum maiores! Delectus maiores
            consequatur tempora ipsam veritatis quo in sequi. Dolore fuga ad
            quam assumenda, tempora quidem recusandae sint totam! Lorem ipsum
            dolor sit amet consectetur adipisicing elit. Quaerat molestiae
            quidem at ratione totam itaque qui libero recusandae fugiat impedit.
            Minima necessitatibus ex veniam nesciunt quisquam unde aperiam autem
            laborum?
          </p>
        </section>
      </article>
    </div>
    <aside class="nav">
      <ul>
        <li
          v-for="(header, index) in headers"
          :key="index"
          :class="{ active: header === currentSection }"
        >
          <RouterLink
            :to="{ path: '/home', hash: `#${header}` }"
            class="link"
            >{{ header }}</RouterLink
          >
        </li>
      </ul>
    </aside>
  </div>
</template>

<script lang="ts" setup>
import { ref, onMounted } from "vue";
const currentSection = ref();

onMounted(() => {
  const observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        if (entry.intersectionRatio > 0) {
          currentSection.value = entry.target.getAttribute("id");
        }
      });
    },
    { rootMargin: "0px 0px -80% 0px" }
  );
  document.querySelectorAll("section h2").forEach((section) => {
    observer.observe(section);
  });
});

const headers = [
  "Titre 1",
  "Titre 2",
  "Titre 3",
  "Titre 4",
  "Titre 5",
  "Titre 6",
];
</script>

<style lang="scss" scoped>
.container {
  width: 100%;
  display: flex;
  justify-content: space-around;

  .wrapper {
    width: 100%;
    max-width: 800px;
    margin-bottom: 500px;
  }

  .nav {
    position: sticky;
    top: 50px;
    background-color: rgb(253, 238, 220);
    border-radius: 5px;
    align-self: flex-start;
    padding: 20px;
    min-width: 200px;
    ul {
      list-style-type: none;
      padding: 0;

      li {
        margin: 10px 0;
        padding: 5px;
        a {
          text-decoration: none;
        }

        &.active {
          background-color: rgb(248, 210, 163);
        }
      }
    }
  }
}
</style>
