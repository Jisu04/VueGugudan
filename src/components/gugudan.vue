<template>
  <div id="wrap">
    <header>
        <p id="title">구구단 계산기</p>
    </header>
    <div id="content">
      <input type="number" id="inputNumber"
      v-model="inputNumber"
      v-on:keyup.enter="createResult()"
      >

      <div id="resultList">
        <div id="listHeader">
          <h5>결과</h5>
          <button id="listReset" @click="ResetList()">Reset</button>
        </div>
        <div class="resultBox" v-for="(num,idx) in RList" :key="idx">
          <div class="resultHeader">
            <h5>검색 : {{num.num}}단</h5>
            <div>
              <button class="modBtn"
              @click="ModList(idx)"
              >수정</button>
              <button class="delBtn"
              @click="DelList(idx)"
              >삭제</button>
            </div>
          </div>
          <div v-for="Dcnt in 9" :key="Dcnt">
            <p><span>{{num.num}}</span><span>x</span><span>{{Dcnt}}</span><span>=</span><span>{{num.num*Dcnt}}</span></p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  export default{
    data(){
      return{
        inputNumber:null,
        RList:new Array()
      }
    },
    methods:{
      // 검색결과 생성
      createResult(){
        // 기본 String이기 때문에 parseInt로 형변환
        let number = parseInt(this.inputNumber);

        // Input창 초기화
        this.inputNumber = null;

        // 기본 조건 검색(숫자인가? / 1이상인가?)
        if(isNaN(number)) return alert("숫자만 입력해주세요!");
        if(number < 1) return alert("1이상의 숫자를 입력해주세요!");

        // 배열에 있는지 검색
        if(this.RList.find(e => e.num === number)) return alert("해당하는 단은 이미 검색되었습니다!");

        // 배열에 넣기
        this.RList.unshift({num:number});
      },
      
      // 검색 초기화
      ResetList(){
        this.RList = [];
      },

      // 검색 삭제
      DelList(val){
        if(!confirm("삭제하시겠습니까?")) return false;
        this.RList.splice(val,1);
      },

      // 검색 수정
      ModList(val){
        let new_val = parseInt(prompt("수정할 값을 입력해주세요"));

        if(isNaN(new_val)) return alert("숫자만 입력해주세요!");
        if(new_val < 1) return alert("1이상의 숫자를 입력해주세요!");

        // 배열에 있는지 검색
        // 만약 이미 있는 단으로 수정할 경우 에러를 출력하고 취소하는걸로 했습니다만, 의도하신 방향으로 해결했는지는 모르겠습니다..
        if(this.RList.find(e => e.num === new_val)) return alert("해당하는 단은 이미 검색되었습니다!");

        console.log(new_val);
        this.RList[val].num = new_val;
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

/* header */
header{
  background-color: #f2f2f2;
  width: 100%;
}

#title{
  padding: 20px;
  font-weight: bold;
  font-size: 25px;
}

/* content */
#content{
  width: 100%;
  display: flex;
  justify-content: flex-start;
  flex-wrap: wrap;
}

/* input */
#inputNumber{
  padding: 10px;
  border: 2px solid #ddd;
  border-radius: 5px;
  margin: 10px;
  width: 100px;
  height: 20px;
}


/* list */
#listHeader{
  width: 100%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 10px;
}

#listHeader > h5{font-size: 20px;}

#listReset{
  background-color: #333;
  border: none;
  border-radius: 5px;
  color: #fff;
  padding: 10px;
  transition: .3s all;
  cursor: pointer;
}

#listReset:hover{opacity: 0.8;}

/* result */
#resultList{
  width: 200px;
  padding: 10px;
  display: flex;
  flex-direction: column;
}

.resultHeader{
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 10px;
}

.modBtn,.delBtn{
  background-color: rgba(0, 0, 0, 0);
  margin: 0 2px;
  padding: 2px;
  border-radius: 3px;
  cursor: pointer;
  transition: .3s all;
}

.modBtn{border: 2px solid #5165EA;}
.delBtn{border: 2px solid #EA5151;}

.modBtn:hover{
  background-color: #5165EA;
  color: #fff;
}

.delBtn:hover{
  background-color: #EA5151;
  color: #fff;
}

.resultBox{
  padding: 10px 20px;
  margin-bottom: 20px;
  background-color: #555;
  border-radius: 5px;
  width: 150px;
  transition: 0.3s all;
  cursor: pointer;
}

.resultBox:hover{box-shadow: 5px 5px 10px #ddd;}

.resultBox  *{color: #fff;}
.resultBox > h5{
  font-size: 17px;
  margin-bottom: 10px;
}

.resultBox p{
  display: flex;
  justify-content: space-between;
}

</style>
