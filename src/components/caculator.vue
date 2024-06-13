<template>
    <div ref="caculator_focus" id="caculator-frame" @keydown="handleKeyDown" @keyup="handleKeyUp" tabindex="1">
        <div class="caculator-top">
            <div class="info">
                <a href="#" id="top-mess">
                    <span>Music Caculator</span>
                </a>
            </div>
            <div class="input">
                <div class="input-inner">
                    <div class="inner-mess">
                        <span class="info">时间：{{ currentTime }} 八度：{{ sel_octave }} 调子：{{ sel_tone }}</span>
                        <span id="music-mode" v-show="music_mode">♪</span>
                        <span id="record-mode" v-show="is_record">R</span>
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
                        <button class="caculator-key-button other-button">Mode</button>
                    </div>
                    <div class="caculator-key">
                        <button class="caculator-key-button other-button" @mouseup="Record">Record</button>
                    </div>
                    <div class="caculator-key">
                        <button id="key7" @click="num_key('7')" class="caculator-key-button white-button"
                            @mousedown="handleNumMouseDown(key_val.key7)" @mouseup="handleNumMouseUp(key_val.key7)">7
                        </button>
                    </div>
                    <div class="caculator-key">
                        <button id="key8" @click="num_key('8')" class="caculator-key-button white-button"
                            @mousedown="handleNumMouseDown(key_val.key8)" @mouseup="handleNumMouseUp(key_val.key8)">8
                        </button>
                    </div>
                    <div class="caculator-key">
                        <button id="key9" @click="num_key('9')" class="caculator-key-button white-button"
                            @mousedown="handleNumMouseDown(key_val.key9)" @mouseup="handleNumMouseUp(key_val.key9)">9
                        </button>
                    </div>
                    <div class="caculator-key">
                        <button id="key_div" @click="num_key('/')" class="caculator-key-button white-button"
                            @mousedown="handleNumMouseDown(key_val.key_div)"
                            @mouseup="handleNumMouseUp(key_val.key_div)">/</button>
                    </div>
                    <div class="caculator-key">
                        <button id="key4" @click="num_key('4')" class="caculator-key-button white-button"
                            @mousedown="handleNumMouseDown(key_val.key4)" @mouseup="handleNumMouseUp(key_val.key4)">4
                        </button>
                    </div>
                    <div class="caculator-key">
                        <button id="key5" @click="num_key('5')" class="caculator-key-button white-button"
                            @mousedown="handleNumMouseDown(key_val.key5)" @mouseup="handleNumMouseUp(key_val.key5)">5
                        </button>
                    </div>
                    <div class="caculator-key">
                        <button id="key6" @click="num_key('6')" class="caculator-key-button white-button"
                            @mousedown="handleNumMouseDown(key_val.key6)" @mouseup="handleNumMouseUp(key_val.key6)">6
                        </button>
                    </div>
                    <div class="caculator-key">
                        <button id="key_mul" @click="num_key('*')" class="caculator-key-button white-button"
                            @mousedown="handleNumMouseDown(key_val.key_mul)"
                            @mouseup="handleNumMouseUp(key_val.key_mul)">*</button>
                    </div>
                    <div class="caculator-key">
                        <button id="key1" @click="num_key('1')" class="caculator-key-button white-button"
                            @mousedown="handleNumMouseDown(key_val.key1)" @mouseup="handleNumMouseUp(key_val.key1)">1
                        </button>
                    </div>
                    <div class="caculator-key">
                        <button id="key2" @click="num_key('2')" class="caculator-key-button white-button"
                            @mousedown="handleNumMouseDown(key_val.key2)" @mouseup="handleNumMouseUp(key_val.key2)">2
                        </button>
                    </div>
                    <div class="caculator-key">
                        <button id="key3" @click="num_key('3')" class="caculator-key-button white-button"
                            @mousedown="handleNumMouseDown(key_val.key3)" @mouseup="handleNumMouseUp(key_val.key3)">3
                        </button>
                    </div>
                    <div class="caculator-key">
                        <button id="key_sub" @click="num_key('-')" class="caculator-key-button white-button"
                            @mousedown="handleNumMouseDown(key_val.key_sub)"
                            @mouseup="handleNumMouseUp(key_val.key1)">-</button>
                    </div>
                    <div class="caculator-key">
                        <button id="key0" @click="num_key('0')" class="caculator-key-button white-button"
                            @mousedown="handleNumMouseDown(key_val.key0)" @mouseup="handleNumMouseUp(key_val.key0)">0
                        </button>
                    </div>
                    <div class="caculator-key">
                        <button id="key_dot" @click="dot_key('.')" class="caculator-key-button white-button"
                            @mousedown="handleNumMouseDown(key_val.key_dot)"
                            @mouseup="handleNumMouseUp(key_val.key_dot)">.</button>
                    </div>
                    <div class="caculator-key">
                        <button id="key_equal" @click="equal_to()" class="caculator-key-button white-button"
                            @mousedown="handleNumMouseDown(key_val.key_equal)"
                            @mouseup="handleNumMouseUp(key_val.key_equal)">=</button>
                    </div>
                    <div class="caculator-key">
                        <button id="key_add" @click="num_key('+')" class="caculator-key-button white-button"
                            @mousedown="handleNumMouseDown(key_val.key_add)"
                            @mouseup="handleNumMouseUp(key_val.key_add)">+</button>
                    </div>

                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref, onUnmounted, watch, reactive, onMounted } from 'vue';
import { BigNumber } from 'bignumber.js';
import munote from '../assets/audio/munote.js';
import howler from 'howler'
import * as Tone from 'tone';
import { Midi } from '@tonejs/midi';

//防止多次记录按键
const pressedKeys = {};

// Keydown event listener
window.addEventListener('keydown', (event) => {
    const key = event.key;
    if (!pressedKeys[key]) {
        pressedKeys[key] = true;
    }
    event.preventDefault();
});

// Keyup event listener
window.addEventListener('keyup', (event) => {
    const key = event.key;
    pressedKeys[key] = false;
});

// 时间日期检测
const now = new Date();
const currentTime = ref(new Date().toLocaleString());
const timer = setInterval(() => {
    currentTime.value = new Date().toLocaleString();
}, 1000);

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
    if (is_record.value === true) {
        return;
    }
    music_mode.value = !music_mode.value;
};

// 键位绑定
let key_val = reactive({
    key_dot: { code: "NumpadDecimal", audio: munote.musical_note[""], status: true },
    key0: { code: "Numpad0", audio: munote.musical_note[""], status: true },
    key1: { code: "Numpad1", audio: munote.musical_note["c1"], status: true },
    key2: { code: "Numpad2", audio: munote.musical_note["d1"], status: true },
    key3: { code: "Numpad3", audio: munote.musical_note["e1"], status: true },
    key4: { code: "Numpad4", audio: munote.musical_note["f1"], status: true },
    key5: { code: "Numpad5", audio: munote.musical_note["g1"], status: true },
    key6: { code: "Numpad6", audio: munote.musical_note["a1"], status: true },
    key7: { code: "Numpad7", audio: munote.musical_note["b1"], status: true },
    key8: { code: "Numpad8", audio: munote.musical_note["c2"], status: true },
    key9: { code: "Numpad9", audio: munote.musical_note["d2"], status: true },
    key_add: { code: "NumpadAdd", audio: munote.musical_note["e2"], status: true },
    key_sub: { code: "NumpadSubtract", audio: munote.musical_note["f2"], status: true },
    key_mul: { code: "NumpadMultiply", audio: munote.musical_note["g2"], status: true },
    key_div: { code: "NumpadDivide", audio: munote.musical_note["a2"], status: true },
    key_equal: { code: "NumLock", audio: munote.musical_note["b2"], status: true },
})
//延音时间
let duration_delayed_time = ref(1000)

//定义八度表
const notes_set = {
    'C': ["C1", "C", "c", "c1", "c2", "c3", "c4"],
    'C#': ["C#1", "C#", "c#", "c#1", "c#2", "c#3", "c#4"],
    'D': ["D1", "D", "d", "d1", "d2", "d3", "d4"],
    'D#': ["D#1", "D#", "d#", "d#1", "d#2", "d#3", "d#4"],
    'E': ["E1", "E", "E", "E1", "E2", "E3", "E4"],
    'F': ["F1", "F", "f", "f1", "f2", "f3", "f4"],
    'F#': ["F#1", "F#", "f#", "f#1", "f#2", "f#3", "f#4"],
    'G': ["G1", "G", "g", "g1", "g2", "g3", "g4"],
    'G#': ["G#1", "G#", "g#", "g#1", "g#2", "g#3", "g#4"],
    'A': ["A1", "A", "a", "a1", "a2", "a3", "a4"],
    'A#': ["A#1", "A#", "a#", "a#1", "a#2", "a#3", "a#4"],
    'B': ["B1", "B", "b", "b1", "b2", "b3", "b4"]
}

//定义八度位置
let sel_octave = ref(3)
//调式 
//在资源文件里的tone.js，下次再说，鸽了。
let tone_sets = ["C Major",]
let sel_tone = ref(tone_sets[0])
let setting_note_set = {

}


//升降八度


//键位
var mouseClick = new MouseEvent('click', {
    view: window,
    bubbles: true,
    cancelable: true
});

//播放音符
const audioObjects = {};

function createAudioObject(src) {
    return new Howl({
        src: [src],
        volume: 1
    });
}

function playAudio(key, kval) {
    // console.log('播放音频' + key)
    if (!audioObjects[key]) {
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
}

function handleNumMouseDown(kval) {
    // stopAudio("Numpad0");

    // 播放构建
    if (music_mode.value == true) {
        playAudio(kval.code, kval.audio);
        if (is_record.value === true) {
            const now = Tone.now();

            midiData.push({ type: 'noteOn', key: kval.code, time: now });
            // playNoteForKey(event.code)
           transport.start();;
        }
        kval.status = false;
    }
}

function handleNumMouseUp(kval) {
    //播放卸载
    if (music_mode.value == true) {

        stopAudio(kval.code, duration_delayed_time.value);
        if (is_record.value === true) {
            const now = Tone.now();

            midiData.push({ type: 'noteOff', key: kval.code, time: now });
            // stopNoteForKey(event.code)
            transport.stop(`+${duration_delayed_time.value}ms`);
        }
        kval.status = true;
    }
}

const getKey = (code) => {
    for (let key in key_val) {
        let value = key_val[key];
        if (!value) continue;

        if (value.length === 0) continue;

        if (value.code === code) {
            // console.log(key);
            return key;
        }
    }
    return null;
}

const getAudioNote = (key) => {
    if (key == null) return null;
    let value = key_val[key];
    return value.audio;
}
//键盘按下
const handleKeyDown = (event) => {
    let key = getKey(event.code);
    // console.log('键盘按下', event.code, key);
    let key_note = getAudioNote(key);
    const now = Tone.now();
    // console.log('键盘按下', event.code, key, key_note);
    if (key_note != null) {
        let button = document.getElementById(key);
        button.dispatchEvent(mouseClick);
        button.classList.remove('white-button');
        button.classList.add('c-white-button');
        if (music_mode.value == true) {
            if (key_val[key].status == true) {
                // stopAudio(key);
                // // 播放构建
                // // console.log(key_val[key].status);
                playAudio(key, key_note);
                console.log(event.code)
                if (is_record.value === true) {
                    midiData.push({ type: 'noteOn', key: event.code, time: now });
                    // playNoteForKey(event.code)
                   transport.start();;
                }
                key_val[key].status = false;
            }
        }

    }
}

//键盘松开
const handleKeyUp = (event) => {

    let key = getKey(event.code);
    const now = Tone.now();
    if (key != null) {

        let button = document.getElementById(key);
        button.classList.remove('c-white-button');
        button.classList.add('white-button');
        if (music_mode.value == true) {
            // stopAudio(key, duration_delayed_time.value);
            if (is_record.value === true) {
                midiData.push({ type: 'noteOff', key: event.code, time: now });
                // stopNoteForKey(event.code)
                transport.stop(`+${duration_delayed_time.value}ms`);
            }
            key_val[key].status = true;
        }
        // console.log(typeof event.code,event.code)



    }
}

//MIDI表
let midiData = [];
const transport = Tone.getTransport();
//记录初始化
async function resetToneTime() {
    const currentContext = Tone.getContext();
    const newContext = new AudioContext();
    Tone.setContext(newContext);
}

function getMidiValueForKey(key) {
    const keyToMidiMap = {
        'Numpad1': ['60'], // C4
        'Numpad2': ['62'], // D4
        'Numpad3': ['64'], // E4
        'Numpad4': ['65'], // F4
        'Numpad5': ['67'], // G4
        'Numpad6': ['69'], // A4
        'Numpad7': ['71'], // B4
        'Numpad8': ['72'], // C5
        'Numpad9': ['74'], // D5
        'NumpadAdd': ['76'], // E5
        'NumpadSubtract': ['77'], // F5
        'NumpadMultiply': ['79'], // G5
        'NumpadDivide': ['81'], // A5
        'NumLock': ['83'], // B5
    };
    return keyToMidiMap[key] || 60;
}

//保存MIDI
function saveMidi() {
    const midi = new Midi();
    const track = midi.addTrack();

    midiData.forEach((event, index) => {
        if (event.type === 'noteOn') {
            const note = {
                midi: getMidiValueForKey(event.key),
                time: event.time,
                duration: 0,
            };

            for (let i = index + 1; i < midiData.length; i++) {
                if (midiData[i].type === 'noteOff' && midiData[i].key === event.key) {
                    note.duration = midiData[i].time - event.time;
                    break;
                }
            }

            track.addNote(note);
        }
    });

    const midiArray = midi.toArray();
    const blob = new Blob([midiArray], { type: 'audio/midi' });
    const url = URL.createObjectURL(blob);

    const a = document.createElement('a');
    a.href = url;
    a.download = 'output.mid';
    document.body.appendChild(a);
    a.click();
    document.body.removeChild(a);
}

//记录
let is_record = ref(false);
const Record = () => {
    if (is_record.value === false) {
        is_record.value = true;
        music_mode.value = true;
        midiData = [];
        resetToneTime();
        console.log('Recording started');
    }
    else {
        is_record.value = false;
        music_mode.value = false;
        saveMidi();
        console.log('Recording stopped');
    }

}

const caculator_focus = ref();
onMounted(() => {
    caculator_focus.value.focus()
    var caculator_f = document.getElementById("caculator-frame");
    // console.log(caculator_f.style.offsetWidth)
    caculator_f.style.height = `${caculator_f.style.offsetWidth * 1.33}px`;
}
)
</script>
<style scoped>
@import url('../assets/css/caculator.css');
</style>