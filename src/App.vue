<template>
    <h1>Список дел:</h1>
    <h3>Добавьте в список новые значения.</h3>
    <textarea v-model="text" name="Список дел" class="journal"></textarea><br><br>
    <button @click="addButton" class="add_button">Добавить</button>
    <button @click="showButton" class="show_button">Отобразить</button><br>
    <p :class="{ data: true, new_style_for_data: isStyled }">Элемент был добавлен</p>
    <div class='business_list'>
        <p v-for="(el, index) in addedTasks" :key="index" v-show="isListVisible">Задание №{{ index + 1 }}: {{ el }} <input @click="deleteItem" type="button" value="Удалить"></p>
    </div>
</template>
<script>
    export default {
        data() {
            return {
                text: "",
                newValue: [],
                addedTasks: [],
                isStyled: false,
                isListVisible: false
            }            
        },
        methods: {
            addButton() {
                this.newValue = this.text.split(/[.,]/);
                if (this.newValue.length > 0) {
                    this.text = "";
                    this.isStyled = true; 
                    setTimeout(() => { 
                        this.isStyled = false;                         
                    }, 2000);                
                } 
            },
            showButton() {
                if (this.newValue.length > 0) {
                    this.newValue.forEach((element) => {
                        element = element.trim();
                        if (element && !this.addedTasks.includes(element)) {
                            this.addedTasks.push(element);
                        };
                    });
                    this.isListVisible = true;
                };
            },
            deleteItem(index) {
                this.addedTasks.splice(index, 1);
            }
        }
    };
</script>
<style>
.journal {
    height: 200px;
    width: 400px;
    font-size: 20px;
    resize: none;
    border-radius: 10px;                
}
.add_button, .show_button {
    height: 70px;
    width: 190px;
    border-color: grey;
    border-radius: 10px;
    font-size: larger;
    color: brown;
}
.show_button {
    margin-left: 20px;
}
.add_button:hover, .show_button:hover{
    cursor: pointer;
    background-color: red;
    color: aliceblue;
}
.data {
    height: 100px;
    width: 300px;
    border: 1px solid black;
    border-radius: 10px;
    background-color: rgb(218, 217, 217);
    display: none;
}
.new_style_for_data {
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 25px;
}
.business_list {
    font-size: 25px;
} 
input[type="button"] {
    border-color: grey;
    border-radius: 10px;
    font-size: medium;
    color: brown;
}
input[type="button"]:hover {
    cursor: pointer;
    background-color: red;
    color: aliceblue
}
</style>