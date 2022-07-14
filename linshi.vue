<template>
    <div class="collection-block">
        <div>这是推荐的页面</div>
        <div class="block-padding">
            <div class="title">
                <h3>{{ title }}</h3>
            </div> 
            <div class="list clearfix i"  v-for="(item,index) in musiclist"   :key="index"    >
                <!-- <router-link
                    tag="div"s
                    class="item"
                    :to="`/player/${item.id}/${item.name}/${setUrl(item.picUrl)}`"
                    v-for="(item,index) in recommend"
                    :key="index"
                    :class="{ 'clear-padding': index%3 !== 1 }"
                > -->
                    <div class="img-warpper item" >
                        <img :src="item.picUrl" alt />
                    </div>
                    <div class="main">{{ cutString(item.name) }}</div>
                    <div class="gray">{{ cutString(item.copywriter) }}</div>
                <!-- </router-link> -->
            </div>
            <div>
                1.  这是更改的地方！
                2.  123456789
            </div>
            
        </div>
    </div>
</template>

<script>
export default {
    name: "MusicRecommend",
    data() {
        return {};
    },
    props: {
        musiclist: {
            type: Array,
            default: function() {
                return [];
            }
        },
        title: {
            type: String,
            default: ""
        }
    },
    methods: {
        cutString(str) {
            if (str) {
                if (str.length > 8) {
                    return str.substring(0, 8) + "...";
                }
                return str;
            }
            return ""
        },
        setUrl(url){
            if(url){
                return encodeURIComponent(url)
            }
        }
    }
};
</script>

<style scoped>
.collection-block {
    background-color: #f8f8f8;
    padding: 5px 0;
}

.block-padding {
    padding: 10px 17px;
    background-color: #fff;
}

.title {
    display: flex;
    margin: 14px 0 18px;
}

.title h3 {
    flex: 1 1 0%;
    display: block;
    font-weight: 700;
    font-size: 20px;
}

.list {
    width: 100%;
}

.list .item {
    float: left;
    width: 31.33%;
    padding: 0 10px;
    margin-bottom: 10px;
}

.clear-padding {
    padding: 0 !important;
}

.main {
    margin-top: 4px;
    font-size: 12px;
}

.gray {
    font-size: 12px;
    color: #999;
}

.btn-more {
    font-size: 12px;
    text-align: right;
    color: #333;
}
</style>





import Vue from 'vue'
import VueRouter from 'vue-router'
import Home from '../views/Home/Index.vue'
import Layout from '../views/Layout.vue'

Vue.use(VueRouter)

const routes = [{
        path: "/",
        name: "Layout",
        component: Layout,
        children: [{
                path: '/',
                name: 'Home',
                component: Home
                    // component: () =>
                    //     import ("../views/Home.vue")
            },
            {
                path: '/topic',
                name: 'Topic',
                component: () =>
                    import ("../views/Topic.vue")
            },
            {
                path: '/mine',
                name: 'Mine',
                component: () =>
                    import ("../views/Mine.vue")
            },
            {
                path: '/search',
                name: 'Search',
                component: () =>
                    import ("../views/Search.vue")
            },

        ]

    },
    { //点击 More 
        path: "/more",
        name: "MusicMore",
        component: () =>
            import ("../views/Home/MusicMore.vue")
    },
    { //点击进入歌单详情  要传入对应的id
        path: "/musicdtails/:id",
        name: "MusicDetails",
        component: () =>
            import ("../views/Home/MusicDetails.vue")
    },
    { //  点击进去播放音乐的页面 亚传入对应音乐的id
        path: "/player/:id/:name/:image",
        name: "/Player",
        component: () =>
            import ("../views/Player.vue")
    },
    {
        path: "/dj/:id",
        name: "DJMore",
        component: () =>
            import ("../views/Home/DJMore.vue")

    }

]


const router = new VueRouter({
    mode: 'hash',
    base: process.env.BASE_URL,
    routes,
    linkActiveClass: "active"
})

export default router







const routes = [{
    path: '/',
    name: 'Home',
    component: Home,
    children: [{
      path: '/page1',
      name: 'page1',
      component: function () {
        return import( /* webpackChunkName: "about" */ '../views/Page1.vue')
      },
      children: [{
        path: '/page1Son',
        name: 'page1Son',
        component: function () {
          return import( /* webpackChunkName: "about" */ '../views/Page1Son.vue')
        }
      }],
    },
    {
      path: '/page2',
      name: 'page2',
      component: function () {
        return import( /* webpackChunkName: "about" */ '../views/Page2.vue')
      }
    }]
  }
]
————————————————
版权声明：本文为CSDN博主「Web_阿凯」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/weixin_45122120/article/details/109177240