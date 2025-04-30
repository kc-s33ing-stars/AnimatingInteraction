<template>
  <div class="card-grid-container">
    <h1 class="animated-title">Super Smash Flip Cards</h1>
    <div class="card-grid">
      <div
        v-for="(card, index) in cards"
        :key="index"
        class="card-wrapper"
        :class="{ 'is-flipped': card.flipped }"
        @click="flipCard(index)"
      >
        <div class="card-inner">
          <div class="card-face card-front">
            <Card>
              <template #title>{{ card.name }}</template>
              <template #content>
                <img :src="card.image" alt="Front" class="character-img" />
              </template>
            </Card>
          </div>
          <div class="card-face card-back">
            <Card>
              <template #title>Bio</template>
              <template #content>
                <p>{{ card.description }}</p>
              </template>
            </Card>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, reactive } from 'vue'
import Card from 'primevue/card'

interface SmashCard {
  name: string
  image: string
  description: string
  flipped: boolean
}

export default defineComponent({
  name: 'SmashFlipCards',
  components: { Card },
  setup() {
    const cards: SmashCard[] = reactive([
      { name: "Mario", image: "/images/mario.png", description: "All-around fighter. Classic plumber hero.", flipped: false },
      { name: "Donkey Kong", image: "/images/donkeykong.png", description: "Heavyweight with powerful punches.", flipped: false },
      { name: "Link", image: "/images/link.png", description: "Hero of Hyrule with projectiles.", flipped: false },
      { name: "Samus", image: "/images/samus.png", description: "Versatile bounty hunter with charge shots.", flipped: false },
      { name: "Yoshi", image: "/images/yoshi.png", description: "Fast, with flutter jump and egg toss.", flipped: false },
      { name: "Kirby", image: "/images/kirby.png", description: "Floating copycat with strong aerials.", flipped: false },
      { name: "Fox", image: "/images/fox.png", description: "Blazing speed and deadly lasers.", flipped: false },
      { name: "Pikachu", image: "/images/pikachu.png", description: "Electric mouse, nimble and zappy.", flipped: false }
    ])

    function flipCard(index: number): void {
      cards[index].flipped = !cards[index].flipped
    }

    return { cards, flipCard }
  }
})
</script>

<style scoped>
.card-grid-container {
  padding: 2rem;
  text-align: center;
}

.animated-title {
  font-size: 2.5rem;
  font-weight: bold;
  color: #333;
  margin-bottom: 2rem;
  animation: pulse 2s infinite;
}

@keyframes pulse {
  0%, 100% {
    transform: scale(1);
    color: #333;
  }
  50% {
    transform: scale(1.05);
    color: #ff4081;
  }
}

.card-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 1.5rem;
  justify-items: center;
}

.card-wrapper {
  width: 200px;
  height: 300px;
  perspective: 1000px;
  cursor: pointer;
  border: 2px solid #444;
  border-radius: 10px;
  overflow: hidden;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
  transition: transform 0.3s ease;
}

.card-inner {
  width: 100%;
  height: 100%;
  transition: transform 0.6s;
  transform-style: preserve-3d;
  position: relative;
}

.card-wrapper.is-flipped .card-inner {
  transform: rotateY(180deg);
}

.card-face {
  position: absolute;
  width: 100%;
  height: 100%;
  backface-visibility: hidden;
}

.card-front {
  transform: rotateY(0deg);
  z-index: 2;
}

.card-back {
  transform: rotateY(180deg);
  z-index: 1;
  padding: 1rem;
  text-align: center;
}

.character-img {
  max-width: 100%;
  max-height: 150px;
  object-fit: contain;
  border-radius: 8px;
}
</style>
