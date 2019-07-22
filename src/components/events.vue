<template>
  <div>
    <div class="boxes lh">
      <l-header v-model="category"/>
    </div>
    <div id="events" class="events">
      <!-- <transition-group name="list"> -->
      <section v-for="item in events" :key="item.Id" :id="item.Id" @click="openModal(item)">
        <span>
          <div class="event shadow-md">
            <ul>
              <div class="event-circle-box">
                <div
                  style="color: #fff"
                  :style="{ background: item.e_color + '!important' }"
                  class="event-circle"
                >{{ item.e_counter }}</div>
              </div>
              <li>{{item.e_date}} {{item.e_location}}</li>
              <li style="padding-top: 3px">{{item.e_name}}</li>
            </ul>
          </div>
        </span>
      </section>
      <!-- </transition-group> -->
      <transition name="modal">
        <modal v-if="modalVisible" @close="modalVisible = false" :event="modalData"/>
      </transition>
    </div>
  </div>
</template>

<script>
import lHeader from "@/components/header";
import modal from "./modal";
import axios from "axios";

export default {
  components: {
    modal,
    lHeader
  },
  props: {
    items: {
      type: Array
    }
  },
  data() {
    return {
      dataApi: "https://share.ninoxdb.de/e7z7k5d5zgfqrvs94al2fzh9vfocoo6ptft0",
      modalVisible: false,
      modalData: null,
      selectedCard: -1,
      allEvents: [],
      events: [],
      category: true
    };
  },
  mounted() {
    // this.scroll(this.events);
    document.addEventListener("keydown", e => {
      if (e && e.keyCode === 27) {
        this.modalVisible = false;
      }
    });
  },
  beforeMount() {
    // this.getInitialEvents();
    this.filterState();
  },
  watch: {
    category() {
      this.filterState();
    }
  },
  methods: {
    async filterState() {
      var vm = this;
      var category = vm.category;

      if (category === true) {
        this.moveTo();
        axios
          .get(this.dataApi)
          .then(response => {
            vm.events = response.data;
          })
          .then(async () => {
            const onlineArr = [];

            await this.events.forEach(person => {
              this.events = [];
              if (person.e_tag === "online") {
                // store value in new array to hold the value after this.events get deleted
                onlineArr.push(person);
              }
            });
            this.events = onlineArr;
          });
      } else if (category === false) {
        // move to top after switch buttons clicked
        this.moveTo();
        // fill up data array
        axios
          .get(this.dataApi)
          .then(response => {
            vm.events = response.data;
          })
          .then(async () => {
            const offlineArr = [];
            // filter data out => 'offline'
            await this.events.forEach(person => {
              this.events = [];
              if (person.e_tag === "offline") {
                // store value in new array to hold the value after this.events get deleted
                offlineArr.push(person);
              }
            });
            this.events = offlineArr;
          });
      }
    },
    moveTo() {
      window.scroll({
        top: 0,
        left: 0,
        behavior: "smooth"
      });
    },
    // get {eventDay} events before // for infinity scroll
    // getInitialEvents() {
    // required to get length fo compare later
    // axios.get(this.dataApi).then(doc => {
    //   this.allEvents = doc.data;
    //   // console.log(this.allEvents)
    // });
    // // push just {events} for the beginning
    // var ua = navigator.userAgent;
    // var isiPad =
    //   /iPad/i.test(ua) ||
    //   /iPhone OS 3_1_2/i.test(ua) ||
    //   /iPhone OS 3_2_2/i.test(ua);
    // if (isiPad) {
    //   for (var a = 0; a < 20; a++) {
    //     axios.get(this.dataApi).then(response => {
    //       this.events.push(response.data);
    //     });
    //   }
    // }
    // axios.get(this.dataApi).then(response => {
    //   for (var i = 0; i < 4; i++) {
    //     this.events.push(response.data);
    //   }
    // });
    // console.log(this.events)
    // },
    // infinity scrolling
    // scroll(event) {
    //   window.onscroll = () => {
    //     let bottomOfWindow =
    //       document.documentElement.scrollTop + window.innerHeight ===
    //       document.documentElement.offsetHeight;

    //     if (bottomOfWindow) {
    //       for (var i = 0; i < 6; i++) {
    //         axios.get(this.dataApi).then(response => {
    //           // check if event.length < then all events.length from init load above
    //           if (this.allEvents.length > this.events.length) {
    //             event.push(response.data);
    //           }
    //         });
    //       }
    //     }
    //   };
    // },
    openModal(data) {
      this.modalData = data;
      this.modalVisible = true;
    },
    isSelected(cardIndex) {
      return this.selectedCard === cardIndex;
    }
  }
};
</script>

<style>
.shadow-md {
  box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1),
    0 2px 4px -1px rgba(0, 0, 0, 0.06);
}
/* list animation */
.list-enter-active,
.list-leave-active,
.list-move {
  transition: 600ms cubic-bezier(0.59, 0.12, 0.34, 0.95);
  transition-property: opacity, transform;
}
.list-enter {
  opacity: 0;
  transition: 600ms cubic-bezier(0.59, 0.12, 0.34, 0.95);
  transform: translateX(20px);
}
.list-enter-to {
  opacity: 0.8;
  transform: translateX(0);
}
.list-leave-to {
  transition: 600ms cubic-bezier(0.59, 0.12, 0.34, 0.95);
  opacity: 0;
  transform-origin: center top;
}

.icon-bar {
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: flex-end;
  margin-top: 13px;
}

.btn-event {
  background: transparent;
  border: none;
  box-shadow: none;
}

.icon-text i {
  font-size: 23px;
}

/* modal animation */
.modal-enter-active,
.modal-leave-active {
  transform: translateX(100%);
}
.modal-enter,
.modal-leave-to {
  transform: translateX(100%);
}

.event-filter {
  display: flex;
  flex-direction: row;
  justify-content: flex-start;
  padding: 10px;
}
.event-filter-box {
  padding: 0 10px;
}
.event-filter > span {
  font-size: 17px;
}

.eventActive {
  height: 120px !important;
  transition: height 400ms !important;
}

/* circle background */
.activeB {
  background: #FFBD2E !important;
}
.notB {
  background: #444 !important;
  opacity: 0.4;
  color: #fff;
}
.newerB {
  background: #28CA42 !important;
}
.over {
  background: #444;
}

.events {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
}

.event {
  width: 290px !important;
  height: 140px;
  background: #fff !important;
  padding: 1px 0;
  margin: 10px 4px;
  border-radius: 8px;
  transition: height 400ms !important;
  overflow-y: scroll;
}
.event::-webkit-scrollbar {
  /* This is the magic bit for WebKit */
  display: none;
}
.event:first-child {
  margin-top: 0;
}
.event > ul {
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  list-style-type: none;
  padding: 10px;
  margin: 0;
  color: #202124 !important;
}
.event > ul > li {
  transform: translateY(-19px);
  display: flex;
  text-align: left;
  justify-content: flex-start;
  font-size: 16px;
  font-weight: 600;
  line-height: 1.3;
  color: #202124 !important;
}

.event > ul > .event-circle-box {
  z-index: 9;
  display: flex;
  justify-content: flex-end;
  width: 100%;
}
.event-circle {
  border-radius: 100%;
  width: 24.4px;
  height: 24.4px;
  background: #444;
  font-size: 14px;
  padding-top: 3px;
}
</style>
