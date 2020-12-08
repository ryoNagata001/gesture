<template>
    <div class="gesture_game_container">
        <div class="logo">
            <img src="logo.jpeg" />
            <div class="statement">professional gesture company.</div>
        </div>
        <div class="gesture_game_inner">
            <div class="word_wrapper">
                <transition name="slide-fade">
                    <div class="gesture_word">
                        <div v-if="isShowVerb">{{ verb }}</div>
                        <div>する</div>
                        <div v-if="isShowSub">{{ subject }}</div>
                    </div>
                </transition>
            </div>
            <div class="button">
                <div class="gesture_game_next_button prev" @click="setRandomVerb">
                    〇〇
                </div>
                <div>
                    する
                </div>
                <div class="gesture_game_next_button last" @click="setRandomSubject">
                    〇〇
                </div>
            </div>
        </div>
        <div class="counter">
            <div>正解数</div>
            <div class="number">{{ count }}</div>
            <div class="counter_buttons">
                <div class="item" @click="decrement">-</div>
                <div class="item" @click="increment">+</div>
            </div>
        </div>
    </div>
</template>
<script lang="ts">
import { Component, Vue } from 'nuxt-property-decorator';
import { verb, subject } from '@/util/odai';

@Component({})
export default class GestureGame extends Vue {
    public count = 0;
    public isShowVerb = true;
    public isShowSub = true;
    public verb: string = '';
    public subject: string = '';

    public setRandomVerb() {
        this.isShowVerb = false;
        this.isShowSub = false;
        const index = Math.floor(Math.random() * verb.length);
        this.verb = verb[index];
        setTimeout(() => {
            this.isShowVerb = true;
        }, 1000);
    }
    public setRandomSubject() {
        this.isShowSub = false;
        const index = Math.floor(Math.random() * subject.length);
        this.subject = subject[index];
        setTimeout(() => {
            if (this.verb.match(/ガダルカナル/)) {
                this.subject = 'ガダルカナルたか'
            }
            this.isShowSub = true;
        }, 1000);
    }
    public increment() {
        this.count += 1;
    }
    public decrement() {
        this.count -= 1;
    }
}
</script>
<style lang="stylus" scoped>
.gesture_game_container {
    position: relative;
    // height: 100vh;
    width: 100vw;
    align-items: center;
    text-align: center;

    .logo {
        font-size: 12px;
        position: fixed;
        top: 0;

        .statement {
            position: absolute;
            margin-left: 15px;
            margin-top: -55px;
        }
    }

    .gesture_game_inner {
        margin-top: calc(50vh - 100px);
        .word_wrapper {
            min-height: 100px;
        }
        .gesture_word {
            text-align: center;
            justify-content: center;
            font-size: 100px;
            font-weight: bold;
            display: flex;
        }

        .button {
            display: flex;
            justify-content: center;
            align-items: center;
            .prev {
                margin-right: 10px;
            }
            .last {
                margin-left: 10px;
            }
            .gesture_game_next_button {
                cursor: pointer;
                font-weight: bold;
                display: inline-block;
                color: white;
                background-color: #444;
                padding: 10px 40px;
                border-radius: 5px;

                &:hover {
                    color: #444;
                    background-color: white;
                    box-shadow: 0 0 20px rgba(0,0,0,.6)
                }
            }
        }

    }
    .counter {
        text-align: center;
        position: absolute;
        right: 100px;
        top: 300px;

        .number {
            font-size: 50px;
            font-weight: bold;
        }
        .counter_buttons {
            display: flex;
            justify-content: center;
            .item {
                cursor: pointer;
                color: white;
                padding: 5px;
                width: 50px;
                height: 50px;
                font-size: 30px;

                border-radius: 100%;
                margin: 0 5px;
                background-color: black;
            }
        }
    }
}

/* enter、 leave アニメーションで異なる間隔やタイミング関数を利用することができます */
.slide-fade-enter-active {
  transition: all .3s ease;
}
.slide-fade-leave-active {
  transition: all .3s cubic-bezier(1.0, 0.5, 0.8, 1.0);
}
.slide-fade-enter, .slide-fade-leave-to
/* .slide-fade-leave-active below version 2.1.8 */ {
  transform: translateX(10px);
  opacity: 0;
}
</style>
