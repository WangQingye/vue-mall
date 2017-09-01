<template>
    <div>
        <nav-header></nav-header>
        <nav-bread>
            <span>goods</span>
        </nav-bread>
        <div class="accessory-result-page accessory-page">
            <div class="container">
                <div class="filter-nav">
                <span class="sortby">Sort by:</span>
                <a href="javascript:void(0)" class="default cur">Default</a>
                <a href="javascript:void(0)" class="price">Price <svg class="icon icon-arrow-short"><use xlink:href="#icon-arrow-short"></use></svg></a>
                <a href="javascript:void(0)" class="filterby stopPop">Filter by</a>
                </div>
                <div class="accessory-result">
                <!-- filter -->
                <div class="filter stopPop" id="filter">
                    <dl class="filter-price">
                    <dt>Price:</dt>
                    <dd @click="priceChecked = 'all'">
                        <a href="javascript:void(0)" :class="{'cur': priceChecked == 'all'}">All</a>
                    </dd>
                    <dd @click="priceChecked = index" v-for="(price,index) in priceFilter" :key="index">
                        <a href="javascript:void(0)" :class="{'cur': priceChecked == index}">{{price.startPrice}} - {{price.endPrice}}</a>
                    </dd>
                    </dl>
                </div>

                <!-- search result accessories list -->
                <div class="accessory-list-wrap">
                    <div class="accessory-list col-4">
                    <ul>
                        <li v-for="(good,index) in goodsList" :key="index">
                            <div class="pic">
                                <a href="#"><img :src="'/static/' + good.prodcutImg" alt=""></a>
                            </div>
                            <div class="main">
                                <div class="name">{{good.productName}}</div>
                                <div class="price">{{good.productPrice}}</div>
                                <div class="btn-area">
                                <a href="javascript:;" class="btn btn--m">加入购物车</a>
                                </div>
                            </div>
                            </li>
                    </ul>
                    </div>
                </div>
                </div>
            </div>
        </div>
        <nav-footer></nav-footer>

    </div>
</template>
<script>
    import './../assets/css/base.css'
    import './../assets/css/product.css'
    import './../assets/css/login.css'
    import './../assets/css/checkout.css'
    import NavHeader from '@/components/NavHeader.vue'
    import NavFooter from '@/components/NavFooter.vue'
    import NavBread from '@/components/NavBread.vue'
    import axios from 'axios'
    export default{
        data(){
            return {
                goodsList: [],
                priceFilter: [
                    {
                        startPrice: '0',
                        endPrice: '500'
                    },
                    {
                        startPrice: '500',
                        endPrice: '1000'
                    },
                    {
                        startPrice: '1000',
                        endPrice: '2000'
                    }
                ],
                priceChecked: 'all'
            }
        },
        mounted(){
            this.getGoodsList();
        },
        methods: {
            getGoodsList() {
                axios.get('/goods').then( res => {                    
                    this.goodsList = res.data.result;
                })
            }
        },
        components: {
            NavHeader,
            NavFooter,
            NavBread
        }
    }
</script>
 