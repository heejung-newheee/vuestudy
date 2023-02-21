<template>
  <div>
    <h1>Baseball Game</h1>
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
      <input v-model="inputAnswer" />
      <button class="btn" @click="onClickCheckResult">
        <span> 결과확인 </span>
      </button>
    </div>
    <div class="box">
      <span> 결 과 : </span>
      <input :value="quizResult" />
    </div>
    <div class="restart_btn box">
      <button class="btn">다시하기</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      quizLength: "",
      quizArray: [],
      inputAnswer: [],
      quizResult: "",
    };
  },
  created() {
    this.startGame();
  },
  watch: {
    // watch는 data 변경 감지, 변경 될 때마다 실행 할 함수를 설정
  },
  computed: {
    // computed는 데이터 캐싱을 통해 참조하고 있는 data가 변경되지 않는 한 연산을 반복하지 않음.
  },
  methods: {
    // method는 참조하고 있는 data가 변하지 않아도 렌더링할 때마다, 호출 될 때마다 연산.
    startGame: function () {
      let num;

      for (let i = 0; i < this.quizLength; i++) {
        num = Math.random() * 10;
        this.quizArray.push(num);
      }
    },
    inputQuizLength() {
      console.log(this.quizLength);
      let num = this.quizLength;
      if (num < 1 || num > 9 || typeof num === "string" || num === "") {
        alert(num + "말고 1-9사이 정수 입력!");
      } else {
        alert(num + "자리 숫자로 게임 시작!");
        this.quizLength = "";
      }
    },
    onClickCheckResult: function () {
      console.log(this.quizLength);
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
</style>
