<style scoped>
.index {
    background-color:#fff;
}
header {
	padding-top:650px;
    width:100%;
    height:800px;
    background:url('../assets/banner2.png') center center no-repeat;
    background-size:cover;
    margin-bottom:40px;
}
@font-face {
	font-family: marzo-w00-regular;
	src: url('../assets/font/marzo_w00_regular.woff')
}
header p{
	font-size:32px;
	line-height:1.2em;
	color:white;
	font-family: marzo-w00-regular, fantasy;
	width:200px;
	margin:0 auto;
	font-weight:200;
}
footer {
    text-indent:-9999px;
}
.flow {
    width:1120px;
    margin:0 auto;
    display:flex;
    flex-wrap: wrap;
    justify-content:space-between;
}
.flow-box {
    width:550px;
    height:600px;
    background-color:#eee;
    background-size:cover;
    margin-bottom:20px;
}
.flow-box img {
    width:372px;
    height:372px;
    opacity:0;
}
.album-images {
    position:absolute;
    width:1px;
    height:1px;
    opacity:0;
    overflow:hidden;
}

</style>

<template>
    <div class="index wrapper">
        <header>
			<p>性敢圈</p>
			<p>xingganquan.com</p>
		</header>
        <div class="flow" v-infinite-scroll="loadMore" infinite-scroll-disabled="isLoading">
            <div @click="loadAlbum(item.aid)" v-for="item in list" class="flow-box" :style="{backgroundImage: 'url('+ item.img +')'}" :key="item.aid">
                <img @click="loadAlbum(item.aid)" :src="item.img" />
            </div>
            <!--
            <div @click="loadAlbum(item.aid)" v-for="item in list" class="flow-box" :style="{backgroundImage: 'url(https://imgsa.baidu.com/exp/w=480/sign=efbf411a6e224f4a5799721b39f79044/342ac65c10385343a6b6b01d9013b07eca808894.jpg)'}" :key="item.aid">
            </div>
            -->
            <div ref="albumImage" class="album-images">
                <img :key="item.img" v-for="item in albumImages" v-img="{group:aid}" :src="item.img" />
                <!--
                <img :key="item.img" v-for="item in albumImages" v-img="{group:aid}" src="https://imgsa.baidu.com/exp/w=480/sign=efbf411a6e224f4a5799721b39f79044/342ac65c10385343a6b6b01d9013b07eca808894.jpg" />
                -->
            </div>
        </div>
        <footer>footer</footer>
    </div>
</template>

<script>
export default {
    name: 'Index',
    data () {
        return {
            isLoading: false,
            list: [],
            aid: 0,
            albumImages: [],
            page: 1,
            size: 10
        }
    },
    mounted () {
        this.loadMore()
    },
    methods: {
        fetchGet (url, opts) {
            if (opts && opts.params) {
                url += '?'
                for (var k in opts.params) {
                    var tmp = k + '=' + opts.params[k]
                    url += tmp + '&'
                }
                url = url.substring(0, url.length - 1)
            }

            // @todo fetch error handler
            var p = fetch(url).then(function (resp) {
                return resp.json()
            })
            return p
        },
        loadAlbum (aid) {
            console.log(aid)
            var vm = this
            vm.isLoading = true
            var p = vm.fetchGet('http://api.xingganquan.com/albums/images', {
                params: {
                    aid: aid
                }
            })
            p.then(function (da) {
                if (da.c === 0) {
                    vm.albumImages = da.d
                    vm.aid = aid
                    vm.$nextTick(function () {
                        var albumImage = vm.$refs.albumImage
                        var item = albumImage.childNodes[0]
                        item.click()
                    })
                } else {
                    // @todo api error handler
                }
                vm.isLoading = false
            })
        },
        loadMore () {
            var vm = this
            vm.isLoading = true
            var p = vm.fetchGet('http://api.xingganquan.com/albums', {
                params: {
                    page: vm.page,
                    size: vm.size
                }
            })
            p.then(function (da) {
                if (da.c === 0) {
                    vm.list = vm.list.concat(da.d)
                    vm.page += 1
                } else {
                    // @todo api error handler
                }
                vm.isLoading = false
            })
        }
    }
}
</script>
