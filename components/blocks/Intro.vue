<template>
  <section class="intro">
    <ui-container class="intro__container">
      <ui-two-columns class="instagram__ui-two-columns">
        <template #heading>
          <div class="intro__column">
            <ui-heading>
              <template #title
                >Истории людей, победивших рак, но не свои привычки</template
              >
              <template #subtitle>
                Есть вещи, которые не лечатся. Вещи ставшие частью нашего «я»,
                фобии, страхи. Но это точно не рак. Рак лечится. Лучшее
                доказательство — люди с их историями.
              </template>
            </ui-heading>
            <div class="intro__wrapper-btn">
              <button
                type="button"
                class="intro__btn intro__btn_left"
                v-on:click="moveVideoBack"
                :disabled="changeDisabledForLeft"
              >
                <svg
                  class="intro__arrow"
                  width="10"
                  height="18"
                  viewBox="0 0 10 18"
                  fill="none"
                  xmlns="http://www.w3.org/2000/svg"
                >
                  <path d="M9 1L1 9L9 17" stroke="#BFBFBF" />
                </svg>
              </button>
              <button
                type="button"
                class="intro__btn intro__btn_right"
                v-on:click="moveVideoAhead"
                :disabled="changeDisabledForRight"
              >
                <svg
                  class="intro__arrow"
                  width="10"
                  height="18"
                  viewBox="0 0 10 18"
                  fill="none"
                  xmlns="http://www.w3.org/2000/svg"
                >
                  <path d="M1 17L9 9L1 1" stroke="#BFBFBF" />
                </svg>
              </button>
            </div>
          </div>
        </template>

        <template #content>
          <div class="intro__video">
            <div class="intro__contain-box">
              <iframe
                class="intro__iframe"
                :src="urlList[counter]"
                allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture"
                allowfullscreen
              ></iframe>
            </div>
            <p class="intro__video-text">
              Все видео вы можете найте на нашем
              <a
                href="https://www.youtube.com/channel/UCcxMSzN1R4JfW1vLu3swCaQ"
                target="_blank"
                class="intro__video-link"
                >YouTube канале</a
              >.
            </p>
          </div>
        </template>
      </ui-two-columns>

      <ui-strip class="intro__strip">
        <template #text>И в отличии от рака, </template>
        <template #tag>#этонелечится</template>
      </ui-strip>
    </ui-container>
  </section>
</template>

<script>
import Container from '~/components/ui/Container';
import TwoColumns from '~/components/ui/TwoColumns';
import Heading from '~/components/ui/Heading';
import Strip from '~/components/ui/Strip';

export default {
  components: {
    'ui-heading': Heading,
    'ui-container': Container,
    'ui-two-columns': TwoColumns,
    'ui-strip': Strip,
  },
  data() {
    return {
      urlList: [
        'https://www.youtube.com/embed/ou60K0WfcJ0',
        'https://www.youtube.com/embed/8IPCPfRF8F0',
        'https://www.youtube.com/embed/iIfbrdnvQfI',
        'https://www.youtube.com/embed/ebyAaIUyFlU',
        'https://www.youtube.com/embed/YfPl4RaGoEg',
        'https://www.youtube.com/embed/_T1mhQlH-ZE',
        'https://www.youtube.com/embed/5xIwKLZ8QZw',
        'https://www.youtube.com/embed/LiXU56qgYDs',
      ],
      counter: 0,
    };
  },
  computed: {
    changeDisabledForRight() {
      if (this.counter + 1 === this.urlList.length) {
        return true;
      }
    },
    changeDisabledForLeft() {
      if (this.counter === 0) {
        return true;
      }
    },
  },
  methods: {
    moveVideoAhead() {
      this.counter++;
    },
    moveVideoBack() {
      this.counter--;
    },
  },
};
</script>

<style scoped>
.intro__container {
  padding-top: 100px;
}

.intro__column {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  height: 100%;
}

.intro__contain-box {
  width: 100%;
  padding-bottom: 56.5%;
  position: relative;
}

.intro__iframe {
  border: 0;
  position: absolute;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
}

.intro__video-text {
  margin: 0;
  font-style: normal;
  font-weight: normal;
  font-size: 12px;
  line-height: 1.3;
  color: #666;
}

.intro__video-link {
  color: #666;
  transition: all 0.3s ease;
}

.intro__video-link:hover {
  opacity: 0.7;
}

.intro__wrapper-btn {
  font-size: 0;
  margin: 18px 0;
}

.intro__btn {
  cursor: pointer;
  width: 40px;
  height: 40px;
  background: #fbfbfb;
  border: 0;
  outline: none;
  transition: all 0.3s ease;
}

.intro__arrow path {
  transition: all 0.3s ease;
}

.intro__btn:hover {
  background-color: #613a93;
}

.intro__btn:hover .intro__arrow path {
  stroke: white;
}

.intro__btn:disabled {
  background-color: #fbfbfb;
}

.intro__btn:disabled .intro__arrow path {
  stroke: #bfbfbf;
}

.intro__strip {
  margin-top: 74px;
}
</style>