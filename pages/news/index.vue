<template>
    <div class="news-page">
        <HeaderG></HeaderG>
        <Content>
            <ul>
                <li v-for="(value, key) in news" :key="key">
                    <ul>
                        <li v-for="(item, index) in value" :key="index">
                            <div>{{item.category}}-{{item.source}}</div>
                            <div>{{item.digest}}...</div>
                            <a :href="item.link">点击详情</a>
                        </li>
                    </ul>
                </li>
            </ul>
        </Content>
    </div>
</template>
<script>
import HeaderG from "../../components/HeaderG";
export default {
    components: { HeaderG },
    data() {
        return {
            news: {}
        };
    },
    async asyncData({ $axios }) {
        let response = await $axios.get("/journalismApi");
        if (response && response.status == 200) {
            return {
                news: response.data.data
            };
        }
    }
};
</script>
<style lang="scss" scoped>
.ivu-layout-content {
}
</style>
