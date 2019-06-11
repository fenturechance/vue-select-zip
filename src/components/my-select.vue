<template>
    <div class="mySelect">
        <select @change="selectFun" v-model="selectValue">
            <option v-for="item in nowList" :key="item">{{ item }}</option>
        </select>
    </div>
</template>
<script>
export default {
    props: ['zipInfo','selectType','nowCity','value'],
    data() {
        return {
            selectValue: ''
        }
    },
    watch: {
        value() {
            this.selectValue = this.value;
        }
    },
    computed: {
        nowList() {
            if(this.selectType == 'city') {
                return this.zipInfo.map(city => city.name)
            }else{
                let nowCityObj = this.zipInfo.filter(city => city.name == this.nowCity)[0]
                if(!nowCityObj) return [];
                return nowCityObj.areas.map(area => area.name);
            }
        }
    },
    methods: {
        selectFun() {
            if(this.selectType == 'city') this.$emit('clearDistrict');
            this.$emit('input',this.selectValue)
        }
    }
}
</script>
