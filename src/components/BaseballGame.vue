<template>
  <div>
    <h1>Baseball Game</h1>
    <h1>희정쌤과 GIT STUDY</h1>
    <div class="box">
      <span> 자릿수: </span>
      <input
        placeholder="1-9사이 정수"
        v-model.number="quizLength"
        @keyup.enter="inputQuizLength"
      />
      <button class="btn" @click="inputQuizLength">입력</button>
    </div>
    <div class="box">
      <span> 정 답 : </span>
      <input v-model="inputAnswer" @keyup.enter="onClickCheckResult" />
      <button class="btn" @click="onClickCheckResult">
        <span> 결과확인 </span>
      </button>
    </div>
    <div class="box result_box">
      <span> 결 과 : </span>
      <input :value="result" />
    </div>
    <div class="result_list">
      <ul>
        <li v-for="(item, i) in resultArray" :key="i">
          <span> {{ i + "번째" }} :{{ item }} </span>
        </li>
      </ul>
    </div>
    <div class="restart_btn box">
      <button class="btn" @click="resetValues">다시하기</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      quizLength: "",
      quizArray: [],
      inputAnswer: "",
      inputArray: [],
      result: "",
      resultArray: [],
    };
  },
  created() {},
  watch: {
    // watch는 data 변경 감지, 변경 될 때마다 실행 할 함수를 설정
  },
  computed: {
    // computed는 데이터 캐싱을 통해 참조하고 있는 data가 변경되지 않는 한 연산을 반복하지 않음.
  },
  methods: {
    // method는 참조하고 있는 data가 변하지 않아도 렌더링할 때마다, 호출 될 때마다 연산.
    startGame: function () {
      const length = this.quizLength;
      let randomArr = [];
      let num;
      for (let i = 0; i < length; i++) {
        num = Math.ceil(Math.random() * 9);
        if (randomArr.indexOf(num) === -1) {
          randomArr.push(num);
        } else {
          i--;
        }
      }

      this.quizArray = randomArr;
      randomArr = [];
      console.log(this.quizArray);
    },
    checkDuplicate() {},
    inputQuizLength() {
      let num = this.quizLength;
      if (num < 1 || num > 9 || typeof num === "string" || num === "") {
        alert(num + "말고 1-9사이 정수 입력!");
      } else {
        alert(num + "자리 숫자로 게임 시작!");
        this.startGame();
      }
    },
    onClickCheckResult() {
      console.log(this.quizArray);
      const length = this.quizArray.length;
      let strike = 0;
      let ball = 0;
      for (let i = 0; i < length; i++) {
        this.inputArray.push(+this.inputAnswer.substring(i, i + 1));
      }
      console.log(this.inputArray);
      for (let i = 0; i < length; i++) {
        for (let j = 0; j < length; j++) {
          if (this.quizArray[i] === this.inputArray[j] && i === j) {
            strike++;
          }
          if (this.quizArray[i] === this.inputArray[j] && i !== j) {
            ball++;
          }
        }
      }
      if (this.inputArray === "") {
        alert(length + "자리 수만큼 답 입력하세요!");
        return;
      }

      if (this.inputAnswer !== "") {
        if (strike == length) {
          this.result = strike + "STRIKE!! YOU WIN!!!";
          this.resultArray.push(this.result);
        } else if (strike + ball == 0) {
          this.result = "OUT!";
          this.resultArray.push(this.result);
        } else {
          this.result = strike + "strike, " + ball + "ball !";
          this.resultArray.push(this.result);
        }
      }
      this.inputArray = [];
    },
    resetValues() {
      this.quizLength = "";
      this.quizArray = [];
      this.inputAnswer = "";
      this.inputArray = [];
      this.result = "";
      this.resultArray = [];
    },
  },
  mounted() {},
};
</script>

<style lang="scss">
@import "/src/css/style.scss";
.box {
  display: block;
  width: 100%;
  height: 50px;
  padding-left: 100px;
  span,
  input,
  button {
    float: left;
  }
  .btn {
    width: 70px;
    height: 30px;
  }
}
input {
  border: none;
  background-color: rgb(235, 235, 235);
  width: 80px;
  height: 30px;
  padding: 0 6px 0 6px;
  border-radius: 4px;
  margin: 4px;
}
button {
  margin-left: 6px;
}
button:hover {
  cursor: pointer;
}
.btn {
  background-color: rgba(255, 179, 179, 0.774);
  border-radius: 4px;
  border: none;
}
.restart_btn {
  margin-top: 20px;
  .btn {
    width: 120px;
    height: 50px;
  }
}

.result_box {
  height: flex;
  input {
    width: 80px;
  }
}
.result_list li {
  display: block;
  height: 20px;

  span {
    font-size: 14px;
    float: left;
    padding-left: 50px;
  }
}
</style>
