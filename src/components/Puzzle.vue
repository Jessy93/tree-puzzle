<template>
  <section class="extra-tags">
      <div class="content">
        <div class="extra-tags__field">
          
          <div v-for="(item, i) in sortedItems" :key="i" class="extra-tags__cell" :style="computedStyle(i)" @click="(e) => {moveItem(e, i)}">
            <div class="extra-tags__cell_inf" :data-block="i">
              <div
              class="extra-tags__cell_inf_quetsion"
              :class="{'extra-tags__cell_inf_quetsion-correct': item.value === 3 * item.top + item.left}"
              @click="showPopup(item)">
                ?
              </div>
            </div>
          </div>

          <div v-if="!isStartPressed" class="extra-tags__overlay">
            <div class="extra-tags__button_block">
              <div class="extra-tags__button_start font_helvetica" @click="startTags">start</div>
            </div>
          </div>

          <div v-if="isFinished" class="extra-tags__overlay-finished">
            <div class="extra-tags__button_block">
              <div class="extra-tags__button_start font_helvetica" @click="finishTags">finish</div>
            </div>
          </div>
        </div>
      </div>
  </section>
</template>

<script>


export default {
  name: 'Puzzle',
  data() {
    return {
      itemEmpty: {
        value: 12,
        top: 3,
        left: 0,
        background: 'transparent',
        image: 'transparent',
      },
      sortedItems: [],
      itemsVariants: [
        [
          {
            value: 0,
            top: 0,
            left: 2,
            background: '#061b36',
            flag: true,
            image: 'url("/extra/tag_back0.png")'
          },
          {
            value: 1,
            top: 0,
            left: 0,
            background: '#061b36',
            flag: true,
            image: 'url("/extra/tag_back1.png")'
          },
          {
            value: 2,
            top: 1,
            left: 2,
            background: '#061b36',
            flag: true,
            image: 'url("/extra/tag_back2.png")'
          },
          {
            value: 3,
            top: 0,
            left: 1,
            flag: true,
            background: '#061b36',
            image: 'url("/extra/tag_back3.png")'
          },
          {
            value: 4,
            top: 3,
            left: 2,
            flag: true,
            background: '#061b36',
            image: 'url("/extra/tag_back4.png")'
          },
          {
            value: 5,
            top: 2,
            left: 0,
            flag: true,
            background: '#061b36',
            image: 'url("/extra/tag_back5.png")'
          },
          {
            value: 6,
            top: 2,
            left: 1,
            flag: true,
            background: '#061b36',
            image: 'url("/extra/tag_back6.png")'
          },
          {
            value: 7,
            top: 1,
            left: 0,
            flag: true,
            background: '#061b36',
            image: 'url("/extra/tag_back7.png")'
          },
          {
            value: 8,
            top: 3,
            left: 1,
            flag: true,
            background: '#061b36',
            image: 'url("/extra/tag_back8.png")'
          },
          {
            value: 9,
            top: 2,
            left: 2,
            flag: true,
            background: '#061b36',
            image: 'url("/extra/tag_back9.png")'
          },
          {
            value: 10,
            top: 1,
            left: 1,
            flag: true,
            background: '#061b36',
            image: 'url("/extra/tag_back10.png")'
          },
        ],
        [
          {
            value: 0,
            top: 2,
            left: 0,
            flag: true,
            background: '#061b36',
            image: 'url("/extra/tag_back0.png")'
          },
          {
            value: 1,
            top: 2,
            left: 2,
            flag: true,
            background: '#061b36',
            image: 'url("/extra/tag_back1.png")'
          },
          {
            value: 2,
            top: 1,
            left: 1,
            flag: true,
            background: '#061b36',
            image: 'url("/extra/tag_back2.png")'
          },
          {
            value: 3,
            top: 0,
            left: 2,
            flag: true,
            background: '#061b36',
            image: 'url("/extra/tag_back3.png")'
          },
          {
            value: 9,
            top: 0,
            left: 0,
            flag: true,
            background: '#061b36',
            image: 'url("/extra/tag_back9.png")'
          },
          {
            value: 5,
            top: 0,
            left: 1,
            flag: true,
            background: '#061b36',
            image: 'url("/extra/tag_back5.png")'
          },
          {
            value: 10,
            top: 1,
            left: 0,
            flag: true,
            background: '#061b36',
            image: 'url("/extra/tag_back10.png")'
          },
          {
            value: 6,
            top: 1,
            left: 2,
            flag: true,
            background: '#061b36',
            image: 'url("/extra/tag_back6.png")'
          },
          {
            value: 8,
            top: 2,
            left: 1,
            flag: true,
            background: '#061b36',
            image: 'url("/extra/tag_back8.png")'
          },
          {
            value: 4,
            top: 3,
            left: 1,
            flag: true,
            background: '#061b36',
            image: 'url("/extra/tag_back4.png")'
          },
          {
            value: 7,
            top: 3,
            left: 2,
            flag: true,
            background: '#061b36',
            image: 'url("/extra/tag_back7.png")'
          },
        ],
        [
          {
            value: 5,
            top: 0,
            left: 0,
            flag: true,
            background: '#061b36',
            image: 'url("/extra/tag_back5.png")'
          },
          {
            value: 3,
            top: 0,
            left: 1,
            background: '#061b36',
            image: 'url("/extra/tag_back3.png")'
          },
          {
            value: 2,
            top: 0,
            left: 2,
            flag: true,
            background: '#061b36',
            image: 'url("/extra/tag_back2.png")'
          },
          {
            value: 4,
            top: 1,
            left: 0,
            flag: true,
            background: '#061b36',
            image: 'url("/extra/tag_back4.png")'
          },
          {
            value: 7,
            top: 1,
            left: 1,
            flag: true,
            background: '#061b36',
            image: 'url("/extra/tag_back7.png")'
          },
          {
            value: 8,
            top: 1,
            left: 2,
            flag: true,
            background: '#061b36',
            image: 'url("/extra/tag_back8.png")'
          },
          {
            value: 6,
            top: 2,
            left: 0,
            flag: true,
            background: '#061b36',
            image: 'url("/extra/tag_back6.png")'
          },
          {
            value: 9,
            top: 2,
            left: 1,
            flag: true,
            background: '#061b36',
            image: 'url("/extra/tag_back9.png")'
          },
          {
            value: 0,
            top: 2,
            left: 2,
            flag: true,
            background: '#061b36',
            image: 'url("/extra/tag_back0.png")'
          },
          {
            value: 1,
            top: 3,
            left: 1,
            flag: true,
            background: '#061b36',
            image: 'url("/extra/tag_back1.png")'
          },
          {
            value: 10,
            top: 3,
            left: 2,
            flag: true,
            background: '#061b36',
            image: 'url("/extra/tag_back10.png")'
          },
        ],
        [
          {
            value: 9,
            top: 0,
            left: 0,
            flag: true,
            background: '#061b36',
            image: 'url("/extra/tag_back9.png")'
          },
          {
            value: 2,
            top: 0,
            left: 1,
            flag: true,
            background: '#061b36',
            image: 'url("/extra/tag_back2.png")'
          },
          {
            value: 5,
            top: 0,
            left: 2,
            flag: true,
            background: '#061b36',
            image: 'url("/extra/tag_back5.png")'
          },
          {
            value: 10,
            top: 1,
            left: 0,
            flag: true,
            background: '#061b36',
            image: 'url("/extra/tag_back10.png")'
          },
          {
            value: 1,
            top: 1,
            left: 1,
            flag: true,
            background: '#061b36',
            image: 'url("/extra/tag_back1.png")'
          },
          {
            value: 7,
            top: 1,
            left: 2,
            flag: true,
            background: '#061b36',
            image: 'url("/extra/tag_back7.png")'
          },
          {
            value: 3,
            top: 2,
            left: 0,
            flag: true,
            background: '#061b36',
            image: 'url("/extra/tag_back3.png")'
          },
          {
            value: 6,
            top: 2,
            left: 1,
            flag: true,
            background: '#061b36',
            image: 'url("/extra/tag_back6.png")'
          },
          {
            value: 8,
            top: 2,
            left: 2,
            flag: true,
            background: '#061b36',
            image: 'url("/extra/tag_back8.png")'
          },
          {
            value: 0,
            top: 3,
            left: 1,
            flag: true,
            background: '#061b36',
            image: 'url("/extra/tag_back0.png")'
          },
          {
            value: 4,
            top: 3,
            left: 2,
            flag: true,
            background: '#061b36',
            image: 'url("/extra/tag_back4.png")'
          },
        ],
        [
          {
            value: 3,
            top: 0,
            left: 0,
            flag: true,
            background: '#061b36',
            image: 'url("/extra/tag_back3.png")'
          },
          {
            value: 0,
            top: 0,
            left: 1,
            flag: true,
            background: '#061b36',
            image: 'url("/extra/tag_back0.png")'
          },
          {
            value: 6,
            top: 0,
            left: 2,
            flag: true,
            background: '#061b36',
            image: 'url("/extra/tag_back6.png")'
          },
          {
            value: 9,
            top: 1,
            left: 0,
            flag: true,
            background: '#061b36',
            image: 'url("/extra/tag_back9.png")'
          },
          {
            value: 2,
            top: 1,
            left: 1,
            flag: true,
            background: '#061b36',
            image: 'url("/extra/tag_back2.png")'
          },
          {
            value: 5,
            top: 1,
            left: 2,
            flag: true,
            background: '#061b36',
            image: 'url("/extra/tag_back5.png")'
          },
          {
            value: 4,
            top: 2,
            left: 0,
            flag: true,
            background: '#061b36',
            image: 'url("/extra/tag_back4.png")'
          },
          {
            value: 7,
            top: 2,
            left: 1,
            flag: true,
            background: '#061b36',
            image: 'url("/extra/tag_back7.png")'
          },
          {
            value: 10,
            top: 2,
            left: 2,
            flag: true,
            background: '#061b36',
            image: 'url("/extra/tag_back10.png")'
          },
          {
            value: 1,
            top: 3,
            left: 1,
            flag: true,
            background: '#061b36',
            image: 'url("/extra/tag_back1.png")'
          },
          {
            value: 8,
            top: 3,
            left: 2,
            flag: true,
            background: '#061b36',
            image: 'url("/extra/tag_back8.png")'
          },
        ],
        [
          {
            value: 10,
            top: 0,
            left: 0,
            flag: true,
            background: '#061b36',
            image: 'url("/extra/tag_back10.png")'
          },
          {
            value: 5,
            top: 0,
            left: 1,
            flag: true,
            background: '#061b36',
            image: 'url("/extra/tag_back5.png")'
          },
          {
            value: 6,
            top: 0,
            left: 2,
            flag: true,
            background: '#061b36',
            image: 'url("/extra/tag_back6.png")'
          },
          {
            value: 9,
            top: 1,
            left: 0,
            flag: true,
            background: '#061b36',
            image: 'url("/extra/tag_back9.png")'
          },
          {
            value: 7,
            top: 1,
            left: 1,
            flag: true,
            background: '#061b36',
            image: 'url("/extra/tag_back7.png")'
          },
          {
            value: 0,
            top: 1,
            left: 2,
            flag: true,
            background: '#061b36',
            image: 'url("/extra/tag_back0.png")'
          },
          {
            value: 4,
            top: 2,
            left: 0,
            flag: true,
            background: '#061b36',
            image: 'url("/extra/tag_back4.png")'
          },
          {
            value: 3,
            top: 2,
            left: 1,
            flag: true,
            background: '#061b36',
            image: 'url("/extra/tag_back3.png")'
          },
          {
            value: 1,
            top: 2,
            left: 2,
            flag: true,
            background: '#061b36',
            image: 'url("/extra/tag_back1.png")'
          },
          {
            value: 8,
            top: 3,
            left: 1,
            flag: true,
            background: '#061b36',
            image: 'url("/extra/tag_back8.png")'
          },
          {
            value: 2,
            top: 3,
            left: 2,
            flag: true,
            background: '#061b36',
            image: 'url("/extra/tag_back2.png")'
          },
        ],
      ],
      isStartPressed: false,
      isFinished: false,
      timer: null,
      timerCount: 0,
    }
  },
  async mounted() {
    this.sortItems();
    // this.getStepInfo({event: 'extravaganza', eventStep: 'ecopuzzle'});
  },
  destroyed() {
    this.stopTimer();
  },
  computed: {
    // ...mapGetters(['StepInfo', 'StepGift']),
    // stepId() {
    //   return this.StepInfo.result.id;
    // },
    stringTimerCounter() {
      let seconds = (this.timerCount % 60).toString().length === 1 ? '0' + (this.timerCount % 60) : (this.timerCount % 60);
      let minutes = (Math.floor(this.timerCount / 60) % 60).toString().length === 1 ? '0' + (Math.floor(this.timerCount / 60) % 60) : (Math.floor(this.timerCount / 60) % 60);
      let hours = (Math.floor(this.timerCount / 60 / 60)).toString().length === 1 ? '0' + (Math.floor(this.timerCount / 60 / 60)) : (Math.floor(this.timerCount / 60 / 60));
      return hours + ':' + minutes + ':' + seconds;
    },
    itemWidth() {
      let block = document.querySelector('.extra-tags__field');
      let offset = 450;
      if (this.$root.windowWidth <= 1200) {
        offset = block.offsetWidth;
      }
      block.style.height = `${offset / 3 * 4}px`;
      return offset / 3;
    },
    giftObject() {
      let obj = new Object();
      if (this.StepGift.result) {
        const event = this.StepGift.result.present.step.slug;
        const gift = this.StepGift.result.present.name;
        const message = this.StepGift.present;
        this.$set(obj, 'name', this.$t(`${event}.${gift}.name`));
        this.$set(obj, 'message', this.$t(`${event}.${gift}.gift_message.${message}`));
        this.$set(obj, 'title', this.$t(`${event}.${gift}.title`));
        this.$set(obj, 'grow', this.$t(`${event}.${gift}.grow`));
        this.$set(obj, 'description', this.$t(`${event}.${gift}.decription`));
      }
      return obj;
    },
  },
  methods: {
    // ...mapActions(['getStepInfo', 'fetchStepStatus', 'getGift']),
    computedStyle(i) {
      return `top: ${this.sortedItems[i].top * this.itemWidth}px; 
      left: ${this.sortedItems[i].left * this.itemWidth}px; 
      width: ${this.itemWidth - 2}px; 
      height: ${this.itemWidth - 2}px; 
      background-image: ${this.sortedItems[i].image}; 
      background-color: ${this.sortedItems[i].background}`;
    },
    sortItems() {
      this.$set(this.itemEmpty, 'top', 3);
      this.$set(this.itemEmpty, 'left', 0);
      let index = Math.floor(Math.random() * 6);
      this.sortedItems = [];
      this.sortedItems = JSON.parse(JSON.stringify(this.itemsVariants[index]));
    },
    showPopup(item) {
      this.popupTitle = 'b';
      this.popupText = 'a';
      this.isPopupVisible = true;
    },
    closePopup() {
      this.isPopupVisible = false;
    },
    moveItem(e, i) {
      if (e.target.className !== 'extra-tags__cell' && e.target.className !== 'extra-tags__cell_inf') {
        return;
      }
      this.isPopupVisible = false;
      if (this.isStartPressed) {
        const diffLeft = Math.abs(this.sortedItems[i].left - this.itemEmpty.left);
        const diffTop = Math.abs(this.sortedItems[i].top - this.itemEmpty.top);

        if (diffLeft + diffTop !== 1) {
          return;
        }

        const left = this.itemEmpty.left;
        const top = this.itemEmpty.top;

        this.itemEmpty.left = this.sortedItems[i].left;
        this.itemEmpty.top = this.sortedItems[i].top;

        this.sortedItems[i].left = left;
        this.sortedItems[i].top = top;

        if(this.sortedItems[i].flag && this.sortedItems[i].value === 3 * this.sortedItems[i].top + this.sortedItems[i].left) {
          this.showPopup(this.sortedItems[i]);
          this.sortedItems[i].flag = false;
        }

        this.isFinished = this.sortedItems.every((el) => {
          return el.value === 3 * el.top + el.left;
        });
        if (this.isFinished) {
          this.stopTimer();
        }
      }
    },
    startTags() {
      this.isStartPressed = true;
      this.startTimer();
    },
    finishTags() {
      this.isStartPressed = false;
      this.isFinished = false;
      this.timerCount = 0;
      let giftsCount = 1;
    },
    startTimer() {
      this.timer = setInterval(() => {
        this.timerCount++;
      }, 1000);
    },
    stopTimer() {
      clearTimeout(this.timer);
    },
  },
  watch: {},
}
</script>

<style scoped>
  .extra-tags__header {
    font-family: 'HelveticaNeue', sans-serif;
    font-style: normal;
    font-weight: bold;
    font-size: 32px;
    line-height: 32px;
    color: #ffffff;
  }
  .extra-tags__description {
    margin-top: 40px;
    font-family: 'HelveticaNeue', sans-serif;
    font-style: normal;
    font-weight: normal;
    font-size: 16px;
    line-height: 24px;
    color: #ffffff;
  }
  .extra-tags__description span {
    text-decoration: underline;
  }
  .extra-tags__description_small {
    margin-bottom: 30px;
    font-family: 'HelveticaNeue', sans-serif;
    font-style: normal;
    font-weight: normal;
    font-size: 12px;
    line-height: 16px;
    color: #ffffff;
  }
  .extra-tags__field {
    position: relative;
    width: 450px;
    height: auto;
    margin-top: 32px;
    margin-bottom: 45px;
    background: url('../assets/images/extra/field_back.png');
    background-size: cover;
    background-position: center;
  }
  .extra-tags__cell {
    position: absolute;
    box-sizing: border-box;
    margin: 1px;
    border-radius: 5px;
    display: flex;
    color: #fff;
    justify-content: flex-end;
    align-items: flex-start;
    font-size: 30px;
    font: sans-serif;
    -webkit-touch-callout: none; /* iOS Safari */
    -webkit-user-select: none;   /* Chrome/Safari/Opera */
    -khtml-user-select: none;    /* Konqueror */
    -moz-user-select: none;      /* Firefox */
    -ms-user-select: none;       /* Internet Explorer/Edge */
    user-select: none;
    cursor: pointer;
    transition: top 0.3s, left 0.3s;
    background-size: cover;
    background-position: center;
  }
  .extra-tags__overlay {
    position: absolute;
    width: 100%;
    height: 100%;
    display: flex;
    align-items: flex-end;
    justify-content: flex-start;
  }
  #reversed .extra-tags__overlay {
    justify-content: flex-end;
  }
  .extra-tags__button_block {
    width: calc(100% / 3);
    height: calc(100% / 4);
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .extra-tags__button_start {
    width: 110px;
    height: 48px;
    display: flex;
    justify-content: center;
    align-items: center;
    background: #77bb2f;
    border-radius: 5px;
    font-size: 16px;
    line-height: 24px;
    text-align: center;
    color: #ffffff;
    cursor: pointer;
  }
  .extra-tags__button_continue {
    margin-bottom: 30px;
    width: 180px;
    height: 48px;
    display: flex;
    justify-content: center;
    align-items: center;
    background: #77bb2f;
    border-radius: 5px;
    font-size: 16px;
    line-height: 24px;
    text-align: center;
    color: #ffffff;
    cursor: pointer;
  }
  .extra-tags__button_start:hover {
    background: #629727;
  }
  .extra-tags__overlay-finished {
    position: absolute;
    width: 100%;
    height: 100%;
    display: flex;
    align-items: flex-end;
    justify-content: flex-end;
  }
  .extra-tags__buttons {
    margin-top: 30px;
    display: flex;
    justify-content: flex-start;
    align-items: center;
  }
  .extra-tags__buttons .extra-tags__button_continue {
    margin-bottom: 0px;
  }
  .extra-tags__button_cancel {
    margin-left: 30px;
    width: 180px;
    height: 48px;
    border: 1px solid #061b36;
    color: #061b36;
  }
  .extra-tags__button_cancel:hover {
      background-color: #061b36;
    color: #fff;
  }
  #reversed .extra-tags__overlay-finished {
    justify-content: flex-start;
  }
  .extra-tags__cell_inf {
    width: 40px;
    height: 40px;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .extra-tags__cell_inf_quetsion {
    z-index: 10;
    width: 25px;
    height: 25px;
    font-family: 'HelveticaNeue', sans-serif;
    font-style: normal;
    font-weight: normal;
    font-size: 15px;
    line-height: 15px;
    color: #ffffff;
    border-radius: 50%;
    border: 1px solid #ffffff;
    text-align: center;
    display: flex;
    align-items: center;
    justify-content: center;
    opacity: 0.70;
  }
  .extra-tags__cell_inf_quetsion-correct {
    color: #8934cc;
    border: 2px solid #8934cc;
  }
  .extra-tags__popup {
    position: absolute;
    z-index: 10;
    display: flex;
    flex-direction: column;
    width: 90%;
    left: 5%;
    top: 5%;
    height: auto;
    padding: 24px;
    background: linear-gradient(133.9deg, #8934CC 0%, #5D66E0 65.19%, #79B2F5 100%);
    border-radius: 16px
  }
  .extra-tags__popup-active {
    display: flex;
    flex-direction: column;
  }
  .extra-tags__popup_title {
    font-size: 18px;
    line-height: 22px;
    color: #ffffff;
  }
  .extra-tags__popup_text {
    margin-top: 12px;
    font-size: 16px;
    line-height: 20px;
    color: #ffffff;
  }
  .extra-tags__popup_close {
    position: absolute;
    right: -15px;
    top: -15px;
    width: 44px;
    height: 44px;
    background: #42556c;
    border-radius: 10px;
    display: flex;
    justify-content: center;
    align-items: center;
    color: #ffffff;
    cursor: pointer;
  }
  #reversed .extra-tags__popup_close {
    right: auto;
    left: -15px;
  }
  .extra-tags__timer {
    margin-top: 15px;
    font-family: 'HelveticaNeue', sans-serif;
    font-style: normal;
    font-weight: bold;
    font-size: 24px;
    line-height: 30px;
    color: #ffffff;
  }
  .extra-tags__howtoplay {
    display: flex;
    margin-top: 16px;
    align-items: center;
    cursor: pointer;
  }
  .extra-tags__howtoplay_img {
    display: block;
    margin-right: 9px;
    object-fit: cover;
    object-position: center;
    width: 17.65px;
    height: 17.65px;
  }
  .extra-tags__howtoplay_text {
    display: flex;
    align-items: center;
    font-size: 16px;
    line-height: 16px;
    text-decoration-line: underline;
    color: #9bcbeb;
  }
  .extra-tags__modal_howtoplay_overlay {
    z-index: 1000250;
    position: fixed;
    width: 100vw;
    height: 100vh;
    top: 0;
    left: 0;
    background: rgba(6, 27, 54, 0.6);
  }
  .extra-tags__modal_howtoplay {
    z-index: 1000250;
    position: absolute;
    width: 100%;
    height: auto;
    top: 25%;
    background: #ffffff;
    border: 1px solid #eef3f7;
    box-sizing: border-box;
    border-radius: 16px;
    padding: 28px 48px;
  }
  .extra-tags__modal_howtoplay_block {
    display: flex;
    flex-direction: column;
  }
  .extra-tags__modal_howtoplay_head_row {
    display: flex;
    align-items: center;
  }
  .extra-tags__modal_howtoplay_logo {
    display: block;
    width: 43px;
    height: 43px;
    margin-right: 19px;
    object-fit: cover;
    object-position: center;
  }
  .extra-tags__modal_howtoplay_caption {
    font-size: 32px;
    line-height: 42px;
    color: #061b36;
  }
  .extra-tags__modal_howtoplay_description {
    margin-top: 30px;
    font-size: 16px;
    line-height: 24px;
    color: #4d4d4d;
  }
  .extra-tags__modal_howtoplay_line {
    margin-top: 24px;
    border-top: 1px solid #d1d2cd;
    margin-left: -48px;
    margin-right: -48px;
  }
  .extra-tags__modal_howtoplay_prize {
    margin-top: 24px;
    font-size: 18px;
    line-height: 22px;
  }

  @media screen and (max-width: 1199px) {
    .extra-tags__field {
      width: 100%;
    }
    .extra-tags__button_start {
      width: 160px;
    }
  }

  @media screen and (max-width: 767px) {
    .extra-tags__header {
      font-size: 24px;
      line-height: 24px;
    }
    .extra-tags__button_start {
      width: 75px;
      height: 36px;
    }
    .extra-tags__popup_title {
      font-size: 15px;
      line-height: 20px;
    }
    .extra-tags__popup_text {
      font-size: 12px;
      line-height: 18px;
    }
    .extra-tags__cell_inf {
      width: 25px;
      height: 25px;
    }
    .extra-tags__cell_inf_quetsion {
      width: 16px;
      height: 16px;
      font-size: 12px;
      line-height: 12px;
    }

    .extra-tags__buttons {
      flex-direction: column;
      align-items: flex-start;
    }

    .extra-tags__button_continue {
      margin-left: 0;
    }

    .extra-tags__button_cancel {
      margin-left: 0;
      margin-top: 15px;
    }
  }
</style>