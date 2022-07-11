<script setup lang="ts">
import { Modal } from 'ant-design-vue';
const col = $ref(5)
const row = $ref(4)
const list = $ref(<any[]>[])

let count = $ref(0)
function random(max: number): number {
    return Math.floor(Math.random() * max)
}

for (let i = 0; i < col; i++) {
    let flag = random(row)
    list[i] = []
    for (let j = 0; j < row; j++) {
        list[i].push(j === flag)
    }
}

const hideModal = () => {
    count = 0

}
const handleClick = (r: boolean, index: number) => {
    console.log(r)
    if (!r) {
        Modal.error({
            keyboard: false,
            maskClosable: false,
            title: '游戏结束！',
            onOk() {
                hideModal()
            },
            content: `最后得分:` + count,
        });
    } else {
        count++
        list.splice(index, 1)
        let arr = []
        let flag = random(row)
        for (let j = 0; j < row; j++) {

            arr.push(j === flag)
        }
        console.log()
        list.unshift(arr)
    }
}
</script>

<template>
    <div class="wrap">


        <div class="scroll flex flex-col">

            <div class="col flex" v-for="(c, index) in list">
                <div class="row flex-1" v-for="r in c" border @click="handleClick(r, index)"
                     :style="{ width: `${100 / row}vw`, height: `${100 / col}vh` }" :class="{ 'bg-blue-500': r }">

                </div>
            </div>
        </div>

    </div>
</template>
