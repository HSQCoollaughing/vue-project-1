<template>
  <!--影院-->
  <div id="movie">
    <mt-navbar v-model="selected" fixed>
      <router-link to="/cityList" class="city">上海</router-link>
      <mt-tab-item id="first">正在上映</mt-tab-item>
      <mt-tab-item id="second">即将上映</mt-tab-item>
    </mt-navbar>
    <mt-tab-container v-model="selected">
      <!--正在上映-->
      <mt-tab-container-item id="first">
        <div class="Concerts__List__Bottom">
          <div class="Concerts__Item" v-for="item in list">
            <img :src="item.img_url"
                 class="lazyimage Concerts__Item__img">
            <div class="Concerts__Info flex-columns">
              <div class="Concerts__Info__Detail">
                <div><span class="Concerts__Info__Name">[{{item.city_name}}]{{item.editor_view}}</span>
                  <p class="Concerts__Info__ShowTime Concerts__Info__p">{{item.time_layout}}</p>
                  <p class="Concerts__Info__VenueName Concerts__Info__p">{{item.venue.name}}</p></div>
                <span class="Concerts__Info__ChargeList">
                  <b class="Concerts__Info__Charge">
                    <span
                      class="Concerts__Info__moneysign">¥</span><i><span><span
                    class="Concerts__Info__Price">{{item.priceinfo}}</span><span><i class="Concerts__Info__Symbol">~</i><span
                    class="Concerts__Info__Price">{{item.max_price}}</span></span></span></i></b>
                  <span class="Label Label--secondary Concerts__Info__Activity">优惠</span>
                  <button
                    class="Button Button--primary-inverse Concerts__Info__Buy" v-if="item.status === 3">预售</button>
                <button
                  class="Button Button--inverse Concerts__Info__Buy" v-else="item.status === 2">购票</button>
                </span></div>
              <div class="Concerts__Info__EditorView "><span><!-- react-text: 286 -->“ <!-- /react-text --><label>{{item.editor_view}}</label>
                <!-- react-text: 288 --> ”<!-- /react-text --></span></div>
            </div>
          </div>
        </div>
      </mt-tab-container-item>
      <!--即将上映-->
      <mt-tab-container-item id="second">
        <div class="Concerts__List__Bottom">
          <div class="Concerts__Item" v-for="item in hot_list">
            <img :src="item.img_url"
                 class="lazyimage Concerts__Item__img">
            <div class="Concerts__Info flex-columns">
              <div class="Concerts__Info__Detail">
                <div><span class="Concerts__Info__Name">[{{item.city_name}}]{{item.editor_view}}</span>
                  <p class="Concerts__Info__ShowTime Concerts__Info__p">{{item.time_layout}}</p>
                  <p class="Concerts__Info__VenueName Concerts__Info__p">{{item.venue.name}}</p></div>
                <span class="Concerts__Info__ChargeList">
                  <b class="Concerts__Info__Charge">
                    <span
                      class="Concerts__Info__moneysign">¥</span><i><span><span
                    class="Concerts__Info__Price">{{item.priceinfo}}</span><span><i class="Concerts__Info__Symbol">~</i><span
                    class="Concerts__Info__Price">{{item.max_price}}</span></span></span></i></b>
                  <span class="Label Label--secondary Concerts__Info__Activity">优惠</span>
                  <button
                    class="Button Button--primary-inverse Concerts__Info__Buy" v-if="item.status === 3">预售</button>
                <button
                  class="Button Button--inverse Concerts__Info__Buy" v-else="item.status === 2">购票</button>
                </span></div>
              <div class="Concerts__Info__EditorView "><span><!-- react-text: 286 -->“ <!-- /react-text --><label>{{item.editor_view}}</label>
                <!-- react-text: 288 --> ”<!-- /react-text --></span></div>
            </div>
          </div>
        </div>
      </mt-tab-container-item>
    </mt-tab-container>
    </mt-popup>
  </div>
</template>
<script>
  export default{
    name: 'movie',
    components: {},
    data () {
      return {
        selected: 'first',
        list: '',
        hot_list: ''
      }
    },
    methods: {
    },
    mounted: function () {
      this.axios.get('items', {params: {
        city_name: '上海',
        page: 1,
        per_page: 25,
        return_type: 2
      }})
        .then(response => {
          this.list = response.data.list
          this.status = response.data.list.status
        })
      this.axios.get('items', {params: {
        city_name: '上海',
        page: 2,
        per_page: 25,
        return_type: 2
      }})
        .then(hotdata => {
          this.hot_list = hotdata.data.list
        })
    },
  }
</script>
