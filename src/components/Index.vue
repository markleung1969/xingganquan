<style scoped>
.index {
    background-color:#fff;
}
header {
    width:100%;
    height:560px;
    background:url('../assets/banner.jpeg') center center no-repeat;
    background-size:cover;
    text-indent:-9999px;
    margin-bottom:40px;
}
footer {
    text-indent:-9999px;
}
.flow {
    width:1500px;
    margin:0 auto;
    display:flex;
    flex-wrap: wrap;
    justify-content:space-between;
}
.flow-box {
    width:372px;
    height:372px;
    background-color:#eee;
    background-size:cover;
    margin-bottom:4px;
}
.flow-box img {
    width:372px;
    height:372px;
    opacity:0;
}

</style>

<template>
    <div class="index wrapper">
        <header>header</header>
        <div class="flow" v-infinite-scroll="loadMore" infinite-scroll-disabled="isLoading">
            <div v-for="item in list" class="flow-box" :style="{backgroundImage: 'url('+ item.img +')'}" :key="item.aid">
                <img v-img="{title : item.desc}" :src="item.img" />
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
            page: 1,
            size: 16
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
