<template>
    <div class="caculator-frame">
        <div class="caculator-top">
            <div class="info">
                <a href="#" id="top-mess">
                    <p>Music Caculator</p>
                </a>
            </div>
            <div class="input">
                <div class="input-inner">
                    <div class="inner-mess">
                        <span class="time">时间:<span class="time-num">{{ currentTime }}</span></span>
                        <span id="music-mode" v-show="music_mode">♪</span>
                        <!-- <span class="date">日期：</span> -->
                    </div>
                    <div class="inner-count">
                        <div id="inner-num">
                            <span id="num-text">
                                {{ sum }}
                            </span>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <div class="caculator-bottom">
            <div class="music-ui">
                <button class="mu-btn">↑</button>
                <button class="mu-btn-center" @click="music_buttom_change">Music</button>
                <button class="mu-btn">↓</button>
            </div>
            <div class="caculator-ui">
                <div class="num-ui">
                    <div class="caculator-key">
                        <button @click="all_clear()" class="caculator-key-button other-button"
                                style="background-color:rgb(226, 70, 70);">AC
                        </button>
                    </div>
                    <div class="caculator-key">
                        <button @click="del_key()" class="caculator-key-button other-button"
                                style="background-color:rgb(226, 70, 70);">→
                        </button>
                    </div>
                    <div class="caculator-key">
                        <button class="caculator-key-button other-button">Vol+</button>
                    </div>
                    <div class="caculator-key">
                        <button class="caculator-key-button other-button">Vol-</button>
                    </div>
                    <div class="caculator-key">
                        <button @click="num_key('7')"
                                class="caculator-key-button white-button">7
                        </button>
                    </div>
                    <div class="caculator-key">
                        <button @click="num_key('8')"
                                class="caculator-key-button white-button">8
                        </button>
                    </div>
                    <div class="caculator-key">
                        <button @click="num_key('9')"
                                class="caculator-key-button white-button">9
                        </button>
                    </div>
                    <div class="caculator-key">
                        <button @click="num_key('/')" class="caculator-key-button white-button">/</button>
                    </div>
                    <div class="caculator-key">
                        <button @click="num_key('4')"
                                class="caculator-key-button white-button">4
                        </button>
                    </div>
                    <div class="caculator-key">
                        <button @click="num_key('5')"
                                class="caculator-key-button white-button">5
                        </button>
                    </div>
                    <div class="caculator-key">
                        <button @click="num_key('6')"
                                class="caculator-key-button white-button">6
                        </button>
                    </div>
                    <div class="caculator-key">
                        <button @click="num_key('*')" class="caculator-key-button white-button">*</button>
                    </div>
                    <div class="caculator-key">
                        <button id="key1" @click="num_key('1')"
                                class="caculator-key-button white-button" @mousedown="handleNumMouseDown" @mouseup="handleNumMouseUp">1
                        </button>
                    </div>
                    <div class="caculator-key">
                        <button id="key2" @click="num_key('2')"
                                class="caculator-key-button white-button">2
                        </button>
                    </div>
                    <div class="caculator-key">
                        <button id="key3" @click="num_key('3')"
                                class="caculator-key-button white-button">3
                        </button>
                    </div>
                    <div class="caculator-key">
                        <button @click="num_key('-')" class="caculator-key-button white-button">-</button>
                    </div>
                    <div class="caculator-key">
                        <button @click="num_key('0')"
                                class="caculator-key-button white-button">0
                        </button>
                    </div>
                    <div class="caculator-key">
                        <button @click="dot_key('.')" class="caculator-key-button white-button">.</button>
                    </div>
                    <div class="caculator-key">
                        <button @click="equal_to()" class="caculator-key-button white-button">=</button>
                    </div>
                    <div class="caculator-key">
                        <button @click="num_key('+')" class="caculator-key-button white-button">+</button>
                    </div>

                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
import {ref, onUnmounted, watch, reactive} from 'vue';
import {BigNumber} from 'bignumber.js';
import munote from '../assets/audio/munote.js';

import howler from 'howler'

// 时间日期检测
const now = new Date();
const currentTime = ref(new Date().toLocaleString());
const timer = setInterval(() => {
    currentTime.value = new Date().toLocaleString();
}, 1000);

// onUnmounted(() => {
//     clearInterval(timer);
// });

// 计算器部分
let sum = ref("0");

//监听sum


const num_key = (key) => {
    if (music_mode.value == false) {
        if (sum.value == "0" || sum.value == "Error" || (over_equal == true && !/^[+\-*/]$/.test(key))) {
            sum.value = key;
            over_equal = false;
        } else if (sum.value != "0") {
            sum.value = sum.value + key;
            over_equal = false;
        }
    }
}
// 检测数字长度
const check_sum_lens = (len) => {
    if ((sum.value.match(/\d/g) || []).length < len) {
        return true
    } else {
        return false;
    }
};


// //del按钮函数
const del_key = () => {
    if (music_mode.value == false) {
        if (sum.value.length == 1 || sum.value == "Error") {
            sum.value = "0";
        } else if (sum.value != 1) {
            sum.value = sum.value.slice(0, -1);
        }
    }
}
// //.按钮函数
const dot_key = () => {
    if (music_mode.value == false) {
        if (sum.value == "0") {
            sum.value = "0.";
            over_equal = false;
        } else {
            sum.value = sum.value + ".";
            over_equal = false;
        }
    }
}
// //allclear函数
const all_clear = () => {
    if (music_mode.value == false) {
        sum.value = "0";
    }
}

// //=函数
let over_equal = false;
const equal_to = () => {
    if (music_mode.value == false) {
        try {
            let result = new BigNumber(eval(sum.value));
            if (isNaN(result) || !isFinite(result)) {
                throw "Invalid expression";
            }
            sum.value = result.toString();
        } catch (error) {
            sum.value = 'Error';
        }
        over_equal = true;
    }
}

// 音乐部分
const music_mode = ref(false)

const music_buttom_change = () => {
    music_mode.value = !music_mode.value;
};

// 键位绑定
let key_val = reactive({
    key_dot: "NumpadDecimal",
    key0: ["Numpad0",],
    key1: ["Numpad1", munote.musical_note["c1"]],
    key2: "Numpad2",
    key3: "Numpad3",
    key4: "Numpad4",
    key5: "Numpad5",
    key6: "Numpad6",
    key7: "Numpad7",
    key8: "Numpad8",
    key9: "Numpad9",
    key_add: "NumpadAdd",
    key_min: "NumpadSubtract",
    key_mul: "NumpadMultiply",
    key_div: "NumpadDivide",
    key_equal: "NumLock",
})
//延音时间
let duration_delayed_time = ref(300)

let all_key_status = reactive({
    key_dot_status: true,
    key0_status: true,
    key1_status: true,
    key2_status: true,
    key3_status: true,
    key4_status: true,
    key5_status: true,
    key6_status: true,
    key7_status: true,
    key8_status: true,
    key9_status: true,
    key_add_status: true,
    key_min_status: true,
    key_mul_status: true,
    key_div_status: true,
    key_equal_status: true,
})
let key1_status = true;

let key2_status = true;
let key3_status = true;

//键位



var mouseClick = new MouseEvent('click', {
    view: window,
    bubbles: true,
    cancelable: true
});

//播放音符
const audioObjects = {};
// const playTimers = {};

function createAudioObject(src) {
    return new Howl({
        src: [src],
        volume: 1
    });
}

function playAudio(key, kval) {
    console.log('播放音频'+key)
    if (!audioObjects[key]) {
        // console.log(key_val.key1[1])
        audioObjects[key] = createAudioObject(kval);

    }
    audioObjects[key].play();
}

// 停止音频
function stopAudio(key, duration = 0) {
    if (!audioObjects[key]) return;

    let audioObject = audioObjects[key];
    delete audioObjects[key];
    audioObject.fade(1, 0, duration);
    setTimeout(() => {
        audioObject.stop();
    }, duration)

    // 关闭同按键的前一个音频定时器
    // if (playTimers[key]) {
    //     clearTimeout(playTimers[key]);
    // }

    // if (duration) {
    //     audioObjects[key].fade(1, 0, duration_delayed_time.value);
    //     playTimers[key] = setTimeout(() => {
    //         audioObjects[key].stop();
    //         console.log('停止音频'+key)
    //         delete audioObjects[key];
    //         delete playTimers[key];
    //     }, duration)
    // } else {
    //     console.log('停止音频'+key)
    //     audioObjects[key].stop();
    //     delete audioObjects[key];
    // }
}

function handleNumMouseDown() {
    // stopAudio("Numpad0");

    // 播放构建
    playAudio("Numpad0", key_val.key1[1]);
    key1_status = false;
}

function handleNumMouseUp() {
    let button1 = document.getElementById('key1');
    key1_status = true;

//播放卸载
    if (audioObjects["Numpad0"]) {
        stopAudio("Numpad0", duration_delayed_time.value);
    }
}

//键盘弹奏
window.addEventListener('keydown', function (event) {
    console.log(event.code)
    switch (event.code) {
        case key_val.key1[0]:
            if (key1_status == true) {

                stopAudio(event.code);

                let button1 = document.getElementById('key1');
                button1.dispatchEvent(mouseClick);
                button1.classList.remove('white-button');
                button1.classList.add('c-white-button');
                // 播放构建
                playAudio(event.code, key_val.key1[1]);
                key1_status = false;
            }
            break;
    }

});

window.addEventListener('keyup', function (event) {
    console.log('keyup')
    if (event.code === key_val.key1[0] && key1_status == false) {
        let button1 = document.getElementById('key1');
        key1_status = true;
        button1.classList.remove('c-white-button');
        button1.classList.add('white-button');
//播放卸载
        if (audioObjects[event.code]) {
            stopAudio(event.code, duration_delayed_time.value);
        }
    }
});

// 按键触发
const button_down_note = (event,key,key_note,key_status) =>{
    stopAudio(key);
        event.button.dispatchEvent(mouseClick);
        event.button.classList.remove('white-button');
        event.button.classList.add('c-white-button');
        // 播放构建
        playAudio(key, key_note);
        key_status = false;
}

const button_up_note = (event,key,key_status) =>{
        key_status = true;
        event.classList.remove('c-white-button');
        event.classList.add('white-button');
//播放卸载
        if (audioObjects[key]) {
            stopAudio(key, duration_delayed_time.value);
        }
}
</script>

<style scoped>
@import url('../assets/css/caculator.css');
</style>