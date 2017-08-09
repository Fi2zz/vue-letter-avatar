<template>
  <div :style='style' v-text="avatarName"></div>
</template>
<style>
</style>
<script>

  const alphabet = ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M', 'N', 'O', 'P', 'Q', 'R', 'S', 'T', 'U', 'V', 'W', 'X', 'Y', 'Z']
  //color from google 
  const colors = [
    [226, 95, 81],// A
    [242, 96, 145],// B
    [187, 101, 202],// C
    [149, 114, 207],// D
    [120, 132, 205],// E
    [91, 149, 249],// F
    [72, 194, 249],// G
    [69, 208, 226],// H
    [72, 182, 172],// I
    [82, 188, 137],// J
    [155, 206, 95],// K
    [212, 227, 74],// L
    [254, 218, 16],// M
    [247, 192, 0],// N
    [255, 168, 0],// O
    [255, 138, 96],// P
    [194, 194, 194],// Q
    [143, 164, 175],// R
    [162, 136, 126],// S
    [163, 163, 163],// T
    [175, 181, 226],// U
    [179, 155, 221],// V
    [194, 194, 194],// W
    [124, 222, 235],// X
    [188, 170, 164],// Y
    [173, 214, 125]// Z
  ];


  function getIndexOfAlphabet(string) {
    let index = 0;
    if (!string) {
      return
    }
    let charCode = (string.charCodeAt(0) - 64).toString();
    let charArray = charCode.split('');
    for (let item of charArray) {
      index += Number(item);
    }
    if (index > 26) {
      index -= 26
    }
    return index
  }

  function getIndex(letter) {
    letter = letter.toUpperCase();
    let index = 0;
    for (let i = 0; i < alphabet.length; i++) {
      if (letter === alphabet[i]) {
        index = i
      }
    }
    return index;
  }

  function color(letter, opacity) {
    let color = (colors[getIndex(letter)]).join(',');
    if (!opacity) {
      opacity = 1
    }
    return `rgba(${color},${opacity})`
  }

  const isLetter = /[a-zA-Z0-9]/;
  export default {
    name:"letter-avatar",
    props: {
      size: Number,
      rounded: Boolean,
      name: {
        type: String,
        required: true
      }
    },
    computed: {
      avatarName() {
        return this.name[0].toUpperCase()
      },
      style() {
        let name =this.name
        let letter;
        if (!isLetter.test(name)) {
          letter = alphabet[getIndexOfAlphabet(name[0])].toUpperCase();
        } else {
          letter = name[0].toUpperCase()
        }
        let SIZE=this.size
        let size = SIZE ? SIZE > 0 ? SIZE: SIZE * -1 : 50;
        return {
          width: `${size}px`,
          height: `${size}px`,
          borderRadius: this.rounded ? '100%' : '0',
          'text-align': 'center',
          'line-height': `${size}px`,
          fontSize: `${size * 0.6}px`,
          color: 'rgba(255, 255, 255, .6)',
          whiteSpace: 'nowrap',
          background: color(letter),
          fontFamily: "'Lucida Console', Monaco, monospace",
        }
      }
    },


  };
</script>
