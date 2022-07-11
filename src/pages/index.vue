<script setup lang="ts">
const col = $ref(5)
const row = $ref(4)
const list = $ref(<any[]>[])

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
</script>

<template>
    <div class="wrap">
        <div class="scroll flex flex-col">
            <div class="col flex" v-for="c in list">
                <div class="row flex-1" v-for="r in c" border
                     :style="{ width: `${100 / row}vw`, height: `${100 / col}vh` }" :class="{ 'bg-blue-500': r }">

                </div>
            </div>
        </div>

    </div>
</template>
