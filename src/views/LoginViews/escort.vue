<template>
    <table-view :fields="fields" base-url="/BasicInfo/Escort" :page-query-param="pageQueryParam" topic-name="押运员"/>
</template>
<script>
import TableView from '../../components/table-view'
import escortField from '../../fields/LoginFields/Escort.js'
import store from '../../store'

export default {
    name: 'escort',
    components: { TableView },
    data: () => ({
        fields: escortField,
        pageQueryParam: [],
    }),
    created(){
        if(store.getters.isSuper){
            this.pageQueryParam = [];
        }else if(store.getters.isCorp){
            this.pageQueryParam = [{key : "corporation", value : store.getters.user.userInfo}];
        }else if(store.getters.isCorpAdmin){
            this.pageQueryParam = [{key : "corporation", value : store.getters.user.corporation}];
        }else if(store.getters.isEscort){
            this.pageQueryParam = [{key : "id", value : store.getters.user.userInfo}];
        }else{
            this.pageQueryParam = [{key : "id", value : "-1"}];
        }
    },
}
</script>