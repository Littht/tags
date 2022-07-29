<script>
export default{
    data(){
        return{
            currentValue:"",
            tags:[]
        }
    },
    methods:{
        handleKeyDown(e){
            if(e.key === "Backspace" && this.currentValue === ""){
                this.tags.pop()
            }
        },
        handleSubmit(){
            if(this.currentValue !== ""){
                const exist = this.tags.some((item)=> item === this.currentValue)
                if(!exist){
                    this.tags.push(this.currentValue);
                    this.currentValue=""
                }

            }
        },
        deleteTag(tag){
            this.tags= this.tags.filter((item) => item !== tag)
        }
    }
}
</script>

<template>
    <div class="inputTag">
        <div class="tags">
            <div class="tag" v-for="(tag, index) in tags" :key="index">
            {{ tag }} <button @click="deleteTag(tag)">X</button>
            </div>
        </div>
        <form @submit.prevent="handleSubmit">
            <input type="text" v-model="currentValue" @keydown="handleKeyDown">
        </form>
    </div>  
</template>

<style scoped>
    .inputTag{
        display:flex;
        align-items: center;
        justify-content: center;
        background-color: #fff;
        padding: 5px;
        border-radius: 4px;
    }
    .tags{
 
        display: flex;
        gap:4px;
    }

    .tags .tag{
        display:flex;
        align-items: flex-end;
        border:1px solid #e0e0e0;
        border-radius: 4px;
        padding:5px
    }

    .tag button{
        background-color: transparent;
        border:none;
        cursor:pointer;
    }

    form input{
        border:none;
        outline: none;
        padding: 8px;
        font-size:16px;
    }
</style>