<template>
    <div id="searchContainer">
        <div class="header">
            <input @confirm="handleConfirm" v-model="searchContent" placeholder-class="greenPlaceholder" type="text"  placeholder="书中自有黄金屋">
            <span @click="handleClaer" class="clear" v-show="searchContent">X</span>
        </div>
        <div v-if="booksList.length">
            <BooksList :booksList="booksList"/>
        </div>
    </div>
</template>

<script  type="text/ecmascript-6">
    import request from '../../utils/request'
    import BooksList from '../booksList/index'
    export default {
        components:{
            BooksList
        },
        data(){
            return {
                searchContent:'',
                booksList:[]
            }
        },
        methods:{
            handleClaer(){
                this.searchContent=''
            },
            async handleConfirm(){
                let data={
                    req:this.searchContent
                }
                let result=await request('/searchBooks',data)
                this.booksList=result.data
            }
        }
    };
</script>

<style lang='stylus' rel='stylesheet/stylus'>
    #searchContainer
        .header
            width 80%
            height 80rpx
            margin 20rpx auto
            border-bottom 1px solid #02a774
            position relative
            input
                height 100%
                width 100%
                .greenPlaceholder
                    color #02a774
                    font-size 36rpx 
                    text-align center
            .clear
                font-size 28rpx
                line-height 80rpx
                position absolute
                top 0
                right 10rpx
                z-index 20
</style>
