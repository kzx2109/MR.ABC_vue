<template>
    <div class="w-[45%]">
        <canvas id="situ"></canvas>
    </div>
</template>

<script>
import Chart from 'chart.js/auto';
import {getunitNum} from '@/service/mempractice';
export default {
    data(){
        return {
            memberId:localStorage.getItem("memberId"),
            kindId:2,
            num:0
        }
    },
    methods:{
        getchart(){
            const ctx = document.getElementById('situ');
            const situ = new Chart(ctx, {
            type: 'pie',
            data: {
                 labels: [
                    'Completed',
                    'Uncompleted',
                ],
                datasets: [{
                    label: 'My First Dataset',
                    data: [this.num,100-this.num],
                    backgroundColor: [
                    'rgb(60, 83, 153)',
                    'rgb(104, 108, 120)',
                    ],
                    hoverOffset: 4
                }]
                
            },
        });
            return situ;
        },
        getNum(){
            getunitNum({
                memberId:this.memberId,
                kindId:this.kindId
            }).then((res)=>{
                this.num=res.data/15*100;
                console.log(this.num);
                this.getchart();
            })
        }
    },
    mounted(){
        // this.getchart();
        this.getNum();
        
    }
}
</script>

<style>

</style>