<template>
    <div class="main">
        <div class="wrapper bd">
            <h2>Информация о себе:</h2>
            <div class="flex">
                <div 
                class="user-info"
                v-for="(fieldValue, fieldLabel, index) in formFields"
                :key="index"
                >
                    <label :for="fieldLabel">{{ fieldLabel }}:</label>
                    <input 
                    id="fieldLabel" 
                    type="text"
                    v-model="formFields[fieldLabel]"
                    >
                </div>
            </div>
            <div class="add-group">
                <label for="additionalField">Дополнительное поле:</label>
                <input 
                id="additionalField"
                v-model="additionalField"
                >
                <button
                type="button"
                @click="addNewField"
                >Добавить</button>
            </div>
        </div>
        <div class="user-info-render bd">
            <h2>Предпросмотр:</h2>
            <p
            v-for="(fieldValue, fieldLabel, index) in formFields"
            :key="index"
            >
            {{ `${fieldLabel}: ${fieldValue}` }}
            </p>
        </div>
    </div>
</template>

<script>
export default {
    name: 'vueComp',
    data() {
        return {
            formFields: {
                firstName: '',
                secondName: '',
                lastName: ''
            },
            additionalField: ''
        }
    },
    methods: {
        addNewField() {
            this.formFields [this.additionalField] = '';
            console.log(this.formFields)
        }
    }
}
</script>

<style scoped>
.main {
    width: 800px;
    margin-left: auto;
    margin-right: auto;
    display: flex;
    justify-content: space-around;
}

.flex {
    display: flex;
    flex-direction: column;
}

.wrapper {
    display: flex;
    flex-direction: column;
}

.user-info {
    display: flex;
    flex-direction: column;
}

.user-info-render {
    display: flex;
    flex-direction: column;
}

.add-group {
    display: flex;
    flex-direction: column;
}

button {
    height: 25px;
    border-radius: 6px;
    border: 1px solid;
    width: 85px;
}

input {
    margin: 10px 0px 10px;
    border-radius: 6px;
    border: 1px solid;
    height: 20px;
}

.bd {
    border: 1px solid grey;
    border-radius: 7px;
    padding: 10px;
    background-color: rgb(123, 146, 247);
}
</style>