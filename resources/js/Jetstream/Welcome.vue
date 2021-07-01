<template>
    <div>
        <div v-if="bettingMode" class="p-6 sm:px-20 bg-blue-amstrad text-xl">
            
            <div class="grid gap-4">
                <div>
                    <table class="table-auto w-full p-3">
                        <tr v-for="horse in horses" :key="horse.id">
                            <td>{{horse.id}}</td>
                            <td> . . . </td>
                            <td>{{horse.name}}</td>
                            <td> - </td>
                            <td>{{horse.odds}}</td>
                        </tr>
                    </table>
                </div>
            </div>
            <div>
                <div class="mt-6">
                    <Label class="block p-1">Cash: £ {{ cash }}</Label>
                    <Label class="block p-1">Which horse to back?</Label>
                    <Label class="block p-1">1 to 8:  
                        <Input id="betHorse" class="p-0" v-model="selectedHorseId" @blur="horseBlur" @keyup="horseKeyUp" type="number" max="8" min="1"/>
                    </Label>
                    <br/>
                    <div v-if="selectedHorseId > 0">
                        <Label class="block p-1">How much shall I put on the horse?</Label>
                        <Label class="block p-1">£   
                            <Input id="betAmount" class="p-0" @keydown="amountKeyDown" v-model="enteredAmount" type="number" min="1" :max="cash"/>
                        </Label>
                    </div>
                </div>
            </div>
        </div>

        <div v-else class="p-6 sm:px-20 bg-blue-amstrad text-xl">
            <h1>CASCADE</h1>
            <div class="finishLine">
                0
            </div>
            <div class="topFence">
                ______________________________________|
                <br/>
                I I I I I I I I I I I I I I I I I I I |
            </div>
            <div class="track">
                <div class="sprites" v-for="horse in horses" :key="horse.id">
                    <img :class="['sprite', 'position' + horse.position]" :src="'images/horse_' + legsPosition + '.png'">
                </div>
            </div>
            <div class="bottomFence">
                _______________________________________
                <br/>
                I I I I I I I I I I I I I I I I I I I I
            </div>

            <div class="summary">
                <Label>
                    CHOICE {{ selectedHorse.name }}
                </Label>
                <Label>
                    WHICH IS HORSE NO. {{ selectedHorseId }}
                </Label>
            </div>

             <div class="commentary" :class="{'finished':!raceInProgress && this.secondsElapsed > 3}">
                <Label :value="commentaryText">
                </Label>
            </div>
        </div>
    </div>
</template>
<style>
    div{
        font-family:'Amstrad CPC464', Arial, Helvetica, sans-serif;
    }
    table{
        border-spacing: 6px;
        border-collapse: separate;
    }
    /* Chrome, Safari, Edge, Opera */
    input::-webkit-outer-spin-button,
    input::-webkit-inner-spin-button {
        -webkit-appearance: none;
        margin: 0;
    }

    /* Firefox */
    input[type=number] {
        -moz-appearance: textfield;
    }
    *:focus {
        outline: none;
    }

    .track {
        height: 168px;
        width: 782px;
        background-color: #70F048;
        margin-left:auto;
        margin-right:auto;
    }
    .finishLine {
        color: #70F048;
        text-align:right;
        margin-left:auto;
        margin-right:auto;
        width:782px;
    }
    .topFence {
        width: 100%;
        color: #70F048;
        text-align:center;
    }
    .bottomFence {
        width: 100%;
        color: #70F048;
        text-align:center;
    }
    h1{
        text-align:center;
        letter-spacing: 20px;
        color: #08128A;
        background-color: red;
        margin-bottom:40px;
        margin-left:auto;
        margin-right:auto;
        width:400px;
        padding-left:20px;
        padding-right:20px;
    }
    .summary{
        margin-left:auto;
        margin-right:auto;
        padding-left:10px;
        background-color: #70F048;
        margin-top:20px;
        width: 500px;
    }
    .summary span{
        color: #08128A;
    }
    .commentary{
        margin-left:auto;
        margin-right:auto;
        background-color: #FCF552;
        margin-top:100px;
        width: 600px;
        height:40px;
    }
    .commentary span{
        color: #08128A;
    }
    .commentary.finished{
        background-color: #FFFFFF;
    }
    .sprite{
        width:20px;
        
    }
    .position0 { margin-left:0px; }
    .position1 { margin-left:20px; }
    .position2 { margin-left:40px; }
    .position3 { margin-left:60px; }
    .position4 { margin-left:80px; }
    .position5 { margin-left:100px; }
    .position6 { margin-left:120px; }
    .position7 { margin-left:140px; }
    .position8 { margin-left:160px; }
    .position9 { margin-left:180px; }
    .position10 { margin-left:200px; }
    .position11 { margin-left:220px; }
    .position12 { margin-left:240px; }
    .position13 { margin-left:260px; }
    .position14 { margin-left:280px; }
    .position15 { margin-left:300px; }
    .position16 { margin-left:320px; }
    .position17 { margin-left:340px; }
    .position18 { margin-left:360px; }
    .position19 { margin-left:380px; }
    .position20 { margin-left:400px; }
    .position21 { margin-left:420px; }
    .position22 { margin-left:440px; }
    .position23 { margin-left:460px; }
    .position24 { margin-left:480px; }
    .position25 { margin-left:500px; }
    .position26 { margin-left:520px; }
    .position27 { margin-left:540px; }
    .position28 { margin-left:560px; }
    .position29 { margin-left:580px; }
    .position30 { margin-left:600px; }
    .position31 { margin-left:620px; }
    .position32 { margin-left:640px; }
    .position33 { margin-left:660px; }
    .position34 { margin-left:680px; }
    .position35 { margin-left:700px; }
    .position36 { margin-left:720px; }
    .position37 { margin-left:740px; }
    .position38 { margin-left:760px; }
</style>
<script>

    import Input from '@/Jetstream/Input'
    import Label from '@/Jetstream/Label'
    import SecondaryButton from '@/Jetstream/SecondaryButton'
    export default {
        components: {
            Input,
            Label,
            SecondaryButton
        },
        methods:{
            amountKeyDown: function(e){
                if (e.keyCode === 13) {
                    if (this.enteredAmount > 0 && this.enteredAmount <= this.cash){
                        //enter
                        this.cash = this.cash - this.enteredAmount;
                        this.loadRacingScreen();
                    }
                }
            },
            horseBlur: function(){
                if (!this.selectedHorseId){
                    document.getElementById('betHorse').focus()
                }
            },
            horseKeyUp: function(){
                if (this.selectedHorseId){
                    document.getElementById('betAmount').focus()
                }
            },
            amountBlur: function(){
                if (this.selectedHorseId && !this.enteredAmount){
                    document.getElementById('betAmount').focus()
                }
            },
            secondElapsed: function(){
                if (this.secondsElapsed == 3){
                    this.raceInProgress = true;
                    this.commentaryText = 'AND THEY\'RE OFF . . .';
                } else if ( this.secondsElapsed > 3) {
                    if (this.raceInProgress){
                        this.legsPosition = 'open';
                        var _this = this;
                        setTimeout(function(){
                            _this.legsPosition = 'closed';
                        },300);
                        var finished = false;
                        var leadingHorse;
                        for(var i = 0; i < this.horses.length; i++){
                            var horse = this.horses[i];
                            horse.position ++ ;
                            if ((Math.random() * 100) + horse.odds < 30){
                                //Bonus jump?
                                horse.position ++ ;
                            }
                            if (horse.position >= 38){
                                horse.position = 38;
                                finished=true;
                            }
                            if (!leadingHorse || horse.position>leadingHorse.position){
                                leadingHorse=horse;
                            }
                        }

                        if (finished){
                            this.raceInProgress=false;
                            this.commentaryText=leadingHorse.name;
                            if (this.selectedHorseId == leadingHorse.id){
                                //win
                                this.cash = this.cash + this.enteredAmount * (leadingHorse.odds + 1);
                                this.commentaryText += ' -- YOU WIN!!';
                            } else {
                                //lose
                                if (this.cash == 0) {
                                    this.commentaryText += ' -- GAME OVER!!';
                                    this.cash = 100;
                                }
                            }
                            _this = this;
                            setTimeout(function() {
                                _this.loadBettingScreen();
                            },3000);
                        } else {
                            this.commentaryText=leadingHorse.name + ' in the lead';
                        }
                    } 
                }
                this.secondsElapsed ++;
            },
            setOdds: function(){
                for(var i = 0; i < this.horses.length; i++){
                    var horse = this.horses[i];
                    horse.odds = Math.ceil(Math.random() * 19);   
                }
            },
            resetHorses: function(){
                for(var i = 0; i < this.horses.length; i++){
                    var horse = this.horses[i];
                    horse.position = 0;   
                }
            },
            loadBettingScreen: function(){
                this.bettingMode = true;
                this.enteredAmount = '';
                this.selectedHorseId = '';
                this.setOdds();
                setTimeout(function() {
                    if (document.getElementById('betHorse')){
                        document.getElementById('betHorse').focus();
                    }
                },100); 
            },
            loadRacingScreen: function(){
                this.bettingMode = false;
                this.resetHorses();
                this.commentaryText = 'UNDER STARTER\'S ORDERS . . .';
                this.secondsElapsed = 0;
            }
        },
        computed: {
            selectedHorse: function(){
                var arr = this.horses.filter(obj => {
                    return obj.id == this.selectedHorseId;
                });
                return arr.length ? arr[0] : [{'id':0, 'name':''}];
            },
        },
        data() {
            return {
                cash: 100,
                selectedHorseId: '',
                enteredAmount: '',
                bettingMode: true,
                commentaryText: 'UNDER STARTER\'S ORDERS . . .',
                secondsElapsed: 0,
                raceInProgress: false,
                legsPosition: 'closed',
                horses:[
                    {
                        'id':1,
                        'name':'Scabby Bum',
                        'odds':2,
                        'position':0,
                    },
                    {
                        'id':2,
                        'name':'Greasy Spoon',
                        'odds':1,
                        'position':0,
                    },
                    {
                        'id':3,
                        'name':'Painted Lady',
                        'odds':20,
                        'position':0,
                    },
                    {
                        'id':4,
                        'name':'Cart Horse Nag',
                        'odds':13,
                        'position':0,
                    },
                    {
                        'id':5,
                        'name':'Mummy\'s Boy',
                        'odds':2,
                        'position':0,
                    },
                    {
                        'id':6,
                        'name':'Silly Twit',
                        'odds':1,
                        'position':0,
                    },
                    {
                        'id':7,
                        'name':'Kamikaze',
                        'odds':1,
                        'position':0,
                    },
                    {
                        'id':8,
                        'name':'Ace Of Spades',
                        'odds':20,
                        'position':0,
                    }
                ]
            }
        },
        mounted() {
            console.log('Component mounted.');
            this.$nextTick(function () {
                setInterval(() => {
                    if (!this.bettingMode){
                        this.secondElapsed();
                    }
                }, 1000);
            });
            this.loadBettingScreen();
            if (document.getElementById('betHorse')){
                document.getElementById('betHorse').focus();
            }
            this.setOdds();
        }
    }
</script>
