<template>
  <div class="window">
    <div class="drum-box">
      <div class="drum-keys">
        <div class="row row-col-3">
          <button type="button" id="btn-q" class="btn btn-dark col mx-1" v-on:click="play('q')"
            v-on:touchend="teste('q')">
            Q
            <audio id="q" v-if="drum">
              <source src="@/assets/Heater-1.mp3" type="audio/mpeg">
            </audio>
            <audio id="q" v-else>
              <source src="@/assets/chord-1.mp3" type="audio/mpeg">
            </audio>
          </button>
          <button type="button" id="btn-w" class="btn btn-dark col mx-1" v-on:click="play('w')">
            W
            <audio id="w" v-if="drum">
              <source src="@/assets/Heater-2.mp3" type="audio/mpeg">
            </audio>
            <audio id="w" v-else>
              <source src="@/assets/chord-2.mp3" type="audio/mpeg">
            </audio>
          </button>
          <button type="button" id="btn-e" class="btn btn-dark col mx-1" v-on:click="play('e')">
            E
            <audio id="e" v-if="drum">
              <source src="@/assets/Heater-3.mp3" type="audio/mpeg">
            </audio>
            <audio id="e" v-else>
              <source src="@/assets/chord-3.mp3" type="audio/mpeg">
            </audio>
          </button>
        </div>
        <div class="row">
          <button type="button" id="btn-a" class="btn btn-dark col mx-1" v-on:click="play('a')">
            A
            <audio id="a" v-if="drum">
              <source src="@/assets/Heater-4.mp3" type="audio/mpeg">
            </audio>
            <audio id="a" v-else>
              <source src="@/assets/give-as-a-light.mp3" type="audio/mpeg">
            </audio>
          </button>
          <button type="button" id="btn-s" class="btn btn-dark col mx-1" v-on:click="play('s')">
            S
            <audio id="s" v-if="drum">
              <source src="@/assets/Heater-5.mp3" type="audio/mpeg">
            </audio>
            <audio id="s" v-else>
              <source src="@/assets/dry-ohh.mp3" type="audio/mpeg">
            </audio>
          </button>
          <button type="button" id="btn-d" class="btn btn-dark col mx-1" v-on:click="play('d')">
            D
            <audio id="d" v-if="drum">
              <source src="@/assets/Dsc-Oh.mp3" type="audio/mpeg">
            </audio>
            <audio id="d" v-else>
              <source src="@/assets/bld-h1.mp3" type="audio/mpeg">
            </audio>
          </button>
        </div>
        <div class="row">
          <button type="button" id="btn-z" class="btn btn-dark col mx-1" v-on:click="play('z')">
            Z
            <audio id="z" v-if="drum">
              <source src="@/assets/Kick-n-Hat.mp3" type="audio/mpeg">
            </audio>
            <audio id="z" v-else>
              <source src="@/assets/punchy-kick-1.mp3" type="audio/mpeg">
            </audio>
          </button>
          <button type="button" id="btn-x" class="btn btn-dark col mx-1" v-on:click="play('x')">
            X
            <audio id="x" v-if="drum">
              <source src="@/assets/Kick.mp3" type="audio/mpeg">
            </audio>
            <audio id="x" v-else>
              <source src="@/assets/side-stick-1.mp3" type="audio/mpeg">
            </audio>
          </button>
          <button type="button" id="btn-c" class="btn btn-dark col mx-1" v-on:click="play('c')">
            C
            <audio id="c" v-if="drum">
              <source src="@/assets/closed-hh.mp3" type="audio/mpeg">
            </audio>
            <audio id="c" v-else>
              <source src="@/assets/brk.mp3" type="audio/mpeg">
            </audio>
          </button>
        </div>
      </div>
      <div class="drum-configs">
        <div class="instrument" @click="(off) ? off = false : off = true">
          Off <i class="fa-solid fa-toggle-off toggle" v-if="off"></i>
          <i class="fa-solid fa-toggle-off toggle-on " v-else></i> On
        </div>
        <div class="sound-name">
          <p v-if="!volume">{{ sound }}</p>
          <p v-else>{{ volume }}</p>
        </div>
        <div class="volume-container">
          <i class="fa-solid fa-volume-low"></i>
          <input type="range" id="volumeRange" min="0" max="1" step="0.01" value="0.5" v-on:change='changeVolume()'>
          <i class="fa-solid fa-volume-high"></i>
        </div>
        <div class="instrument" @click="(drum) ? drum = false : drum = true">
          <i class="fa-solid fa-drum instrument-icon"></i>
          <i class="fa-solid fa-toggle-off toggle" v-if="drum"></i>
          <i class="fa-solid fa-toggle-off toggle-on " v-else></i>
          <span class="material-symbols-outlined instrument-icon">
            piano
          </span>
        </div>
      </div>
    </div>

  </div>
</template>
<script>
export default {
  data() {
    return {
      off: false,
      drum: true,
      sound: '',
      drumSound: {
        'q': 'Heater 1',
        'w': 'Heater 2',
        'e': 'Heater 3',
        'a': 'Heater 4',
        's': 'Clap',
        'd': 'Open HH',
        'z': "Kick'n'Hat",
        'x': 'Kick',
        'c': 'Closed HH'
      },
      pianoSound: {
        'q': 'Chord 1',
        'w': 'Chord 2',
        'e': 'Chord 3',
        'a': 'Shaker',
        's': 'Open HH',
        'd': 'Closed HH',
        'z': 'Punchy Kick',
        'x': 'Side Stick',
        'c': 'Snare'
      },
      volume: '',
      arrKey: ['q', 'w', 'e', 'a', 's', 'd', 'z', 'x', 'c']
    }
  },
  methods: {
    play(id) {
      this.volume = ''
      if (this.off) {
        this.btnStyle(id)
      } else {
        const audio = document.getElementById(id)
        audio.currentTime = 0
        audio.play()
        this.btnStyle(id)
        if (this.drum) {
          this.sound = this.drumSound[id]
        } else {
          this.sound = this.pianoSound[id]
        }
      }
    },
    btnStyle(id) {
      if (!this.arrKey.includes(id)) return
      else {
        let btnStyle = document.getElementById(`btn-${id}`)
        btnStyle.style.backgroundColor = 'rgb(141, 140, 140)'
        btnStyle.style.boxShadow = 'inherit'
        setTimeout(() => {
          btnStyle.style.backgroundColor = '#212529'
          btnStyle.style.boxShadow = '2px 2px 3px 1px rgb(104, 103, 103)'
        }, 100);
      }
    },
    changeVolume() {
      const vol = document.getElementById('volumeRange').value;
      const audio = document.getElementsByTagName('audio');
      for (let i = 0; i < audio.length; i++) {
        audio[i].volume = vol
      }
      this.volume = `Volume: ${Math.round(vol * 100)}`
    }
  },
  created() {
    window.document.addEventListener('keypress', (e) => {
      let key = e.key.toLocaleLowerCase()
      this.btnStyle(key)
      if (this.arrKey.includes(key)) {
        this.play(key)
      }
    })
  }
}
</script>
<style>
.window {
  width: 100%;
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: rgb(10, 10, 10);
}

.drum-box {
  width: 60vw;
  height: 60vh;
  border: 4px solid rgb(78, 78, 78);
  background-color: rgb(20, 20, 20);
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 1vw;
  border-radius: 5px;
  padding: 1vw;

}

.drum-keys,
.drum-configs {
  width: 49%;
  height: 100%;
  box-sizing: border-box;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 1vh;
}

.drum-configs {
  justify-content: center;
  gap: 5vh;
}

.row {
  width: 100%;
  height: 32%;
}

.col {
  box-shadow: 2px 2px 3px 1px rgb(104, 103, 103);
}

.toggle,
.toggle-on {
  font-size: 6vh;
  cursor: pointer;
  color: rgb(187, 187, 187);
}

.toggle-on {
  transform: rotate(180deg);
}

.toggle:hover,
.toggle-on:hover {
  color: rgb(141, 140, 140);

}

.sound-name {
  height: 6vh;
  line-height: 6vh;
  border-radius: 5px;
  width: 50%;
  text-align: center;
  color: rgb(15, 14, 14);
  background-color: rgb(78, 78, 78);
  margin: 2vh 0;
  font-weight: bolder;
}

.instrument {
  display: flex;
  align-items: center;
  gap: 1vh;
  color: rgb(187, 187, 187);
}

.volume-container {
  display: flex;
  align-items: center;
  gap: 1vw;
  color: rgb(187, 187, 187);
}
.instrument-icon{
  font-size: 4vh;
  margin: 0 1vw;
}
/********** Range Input Styles **********/
/*Range Reset*/
input[type="range"] {
  -webkit-appearance: none;
  appearance: none;
  background: transparent;
  cursor: pointer;
  width: 15rem;
}

/* Removes default focus */
input[type="range"]:focus {
  outline: none;
}

/***** Chrome, Safari, Opera and Edge Chromium styles *****/
/* slider track */
input[type="range"]::-webkit-slider-runnable-track {
  background-color: rgb(141, 140, 140);
  border-radius: 0.5rem;
  height: 0.5rem;
}

/* slider thumb */
input[type="range"]::-webkit-slider-thumb {
  -webkit-appearance: none;
  /* Override default look */
  appearance: none;
  margin-top: -12px;
  /* Centers thumb on the track */
  /*custom styles*/
  background-color: rgb(78, 78, 78);
  height: 2rem;
  width: 1rem;
}

/******** Firefox styles ********/
/* slider track */
input[type="range"]::-moz-range-track {
  background-color: rgb(78, 78, 78);
  border-radius: 0.5rem;
  height: 0.5rem;
}

/* slider thumb */
input[type="range"]::-moz-range-thumb {
  border: none;
  /*Removes extra border that FF applies*/
  border-radius: 0;
  /*Removes default border-radius that FF applies*/

  /*custom styles*/
  background-color: rgb(78, 78, 78);
  height: 2rem;
  width: 1rem;
}
</style>
