<template>
    <div>
        <div class="item" v-for="(node, index) in items" :key="node + i">
            {{ node }}
            <button @click="removeItem(index)">x</button>
        </div>

        <div class="action">
            <input v-model="inputVal" />
            <button @click="addItem">Add</button>
        </div>
    </div>
</template>
<script>
export default {
    props: ["items"],
    data() {
        return {
            inputVal: ""
        }
    },
    methods: {
        addItem() {
            this.$emit("add-item", this.inputVal)
            this.inputVal = ""
        },
        removeItem(index) {
            this.$emit("remove-item", index)
        }
    }
}
</script>
