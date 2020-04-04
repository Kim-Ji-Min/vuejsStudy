<template>
    <div>
        <div>당첨 숫자</div>
        <div id="resultScreen">
            <lotto-ball v-for="ball in winBalls" :key="ball" :number="ball"></lotto-ball>
            <!-- props도 바인드 가능
            해당 부분 v-for 에러뜨는데 ㅠ_ㅠ 제로초랑 가능 코드임!
            vue.runtime.esm.js:620 [Vue warn]: Duplicate keys detected: '41'. This may cause an update error.(found in <Root>)

            스택오버플로우, 깃헙 보니 v-for="(item, idx) in items" :key="idx" 로 하면된다는데 에러남--
            watch 함수지워도 해결됨..
            -->
        </div>
        <div>보너스</div>
        <lotto-ball v-if="bonus" :number="bonus"></lotto-ball>
        <button v-if="redo" @click="onClickRedo">한번 더!</button>
    </div>
</template>

<script>
    //로또 생성 function
    function getWinNumbers() {
        console.log('getWinNumbers');
        const candidate = Array(45).fill().map((v, i) => i + 1);
        const shuffle = [];
        while (candidate.length > 0) {
            shuffle.push(candidate.splice(Math.floor(Math.random() * candidate.length), 1)[0]);
        }
        const bonusNumber = shuffle[shuffle.length - 1];
        const winNumbers = shuffle.slice(0, 6).sort((p, c) => p -c);
        return [...winNumbers,bonusNumber];
    }

    import LottoBall from "./LottoBall";

    export default {
        name: "LottoGenerator",
        data() {
            return{
                winNumbers: getWinNumbers(),
                winBalls: [],
                bonus: null,
                redo: false,//다시 뽑기 버튼은 디폴트:폴스
                timeOuts: [],//clear settimeout
            }
        },
        components: {
            LottoBall,
        },
        methods: {
            showBalls() {
                //6개 숫자 화면에 보여주기
                for (let i = 0; i <this.winNumbers.length - 1; i++){ //보너스공까지 7개 뽑아서 6개만들기 위해-1!
                    this.timeOuts[i] = setTimeout(() =>{
                        this.winBalls.push(this.winNumbers[i]);
                    }, (i+1) * 1000);
                }
                //보너스 공 보여주기
                this.timeOuts[6] = setTimeout(() =>{
                    this.bonus = this.winNumbers[6];
                    this.redo = true; //모든 번호를 보여주고 다시 뽑기 버튼 재 등장!
                }, 7000);
            },
            onClickRedo() {//초기화
                this.winNumbers = getWinNumbers();
                this.winBalls = [];
                this.bonus = null;
                this.redo = false;
                this.showBalls();
            }
        },
        mounted() {
            this.showBalls();
        },
        beforeDestroy() {
            this.timeOuts.forEach((t) =>{
                clearTimeout(t);
            });
        },
        watch: {
            //왠만하면 왓치 노우
            // redo(value, oldValue){
            //     console.log(value, oldValue);
            //     if(value === false){
            //         this.showBalls();
            //     }
            // }
        }
    }
</script>

<style scoped>
</style>
