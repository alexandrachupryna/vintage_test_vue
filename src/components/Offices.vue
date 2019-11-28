<template>
  <div class="offices">
    <div class="container">
      <div class="offices_address">
        <h2>Our Offices</h2>
          <div id="tabs">
          <div class="tabs_button-list">
            <div v-for="(item,index) in centers" :key="index" class="tabs_button">
               <a :class="{active: item.show}" @click="changeMarker(item,index)">{{item.title.toUpperCase()}}</a>
            </div>
          </div>
          <div class="s_offices_adr" v-show="item.show" v-for="(item,index) in centers" :key="index">
              <h3>
                {{item.heading}}
              </h3>
              <div class="s_offices_adr_text" v-html="item.text">
              </div>
            </div>
        </div>
      </div>
      <div class="s_offices_map" ref="js-map"></div>
    </div>
  </div>
</template>


<script>
import gmapsInit from '../utils/gmap';
export default {
  name: 'Offices',
  data () {
    return {
      activetab: '1',
      light: false,
      map: null,
      markers: [],
      centers:[
        {
          lat: 50.4051845,
          lng: 30.4976132,
          zoom: 9,
          icon: require('../assets/circle.png'),
          title: 'Kyiv',
          show: true,
          heading: 'Global Message Services Ukraine LLC',
          text: `<p>Kuiv, Stepan Bandera, 33</p>
                <p>02066</p>
                <p>Ukraine</p>`,
        },
        {
          lat: 40.733264, 
          lng: -73.993737,
          zoom: 10,
          icon: require('../assets/circle.png'),
          title: 'New york',
          show: false,
          heading: 'Global Message Services USA LLC',
          text: `<p>New York, 34 E 11th St</p>
                <p>10003</p>
                <p>USA</p>`,
        },
        {
          lat: 23.257684,
          lng: 113.316299,
          zoom: 9,
          icon: require('../assets/circle.png'),
          title: 'Guangzhou',
          show: false,
          heading: 'Global Message Services China LLC',
          text: `<p>Guangzhou, 19dong 602shi</p>
                <p>510000</p>
                <p>China</p>`,
        },
        {
          lat: 41.457693,
          lng: 2.227794,
          zoom: 12,
          icon: require('../assets/circle.png'),
          title: 'Barcelona',
          show: false,
          heading: 'Global Message Services Spain LLC',
          text: `<p>Barcelona, Passeig Olof Palme, 28-36</p>
                <p>08917</p>
                <p>Spain</p>`,
        }
      ]
    }
  },
  methods: {
    changeMarker(item,index){
      this.centers.forEach((el)=>{
        el.show = false;
      })
      this.markers[index].setMap(this.map);
      this.centers[index].show = true;
      this.map.setCenter({lat:item.lat, lng:item.lng});
    }
  },
  async mounted() {
    try {
      const google = await gmapsInit();
        let item = this.centers[0];
        let mapOptions = {
          zoom: item.zoom,
          center: new google.maps.LatLng(item.lat,item.lng),
        };
        this.map = new google.maps.Map(this.$refs['js-map'],mapOptions);
        this.centers.forEach((item)=>{
          let marker = new google.maps.Marker({
            position: new google.maps.LatLng(item.lat, item.lng),
            title: item.title,
            icon: item.icon
          });
          this.markers.push(marker);
        })
        this.markers[0].setMap(this.map);
    } catch (error) {
      alert(error);
    }
  }
}

</script>
