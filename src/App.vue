<template>
  <div style='margin-bottom: 0px;'>
    <header>
      <div style='position: fixed; z-index: 10; margin-top: -50px; width: 100%; background-color: #111;'>
        <b-container>
          <b-row>
            <b-col class='icon-bg' cols='2' style="padding-top: 1px; padding-bottom: 1px;">
              <h5 style="color: #FFF; text-decoration: none;">
                <a href="/">VUE-MASTERSCROLL</a>
              </h5>
            </b-col>
            <b-col>
              <div style="margin-top: 2px;">
                <span class="source-link source-link-active">
                  <a href="#showall" v-on:click="showAll()">
                    SHOW ALL
                  </a>
                </span>
                <span class="source-link source-link-active">
                  <a href="#hideall" v-on:click="hideAll()">
                    HIDE ALL
                  </a>
                </span>
                <span class="source-link source-link-active">
                  <a href="#show1" v-on:click="show(1)">
                    SHOW 1
                  </a>
                </span>
                <span class="source-link source-link-active">
                  <a href="#show3" v-on:click="show(3)">
                    SHOW 3
                  </a>
                </span>
                <span class="source-link source-link-active">
                  <a href="#show1more" v-on:click="showMore(1)">
                    SHOW 1 MORE
                  </a>
                </span>
                <span class="source-link source-link-active">
                  <a href="#show1more" v-on:click="showMore(2)">
                    SHOW 2 MORE
                  </a>
                </span>
                <span class="source-link source-link-active">
                  <a href="#show1more" v-on:click="showMore(5)">
                    SHOW 5 MORE
                  </a>
                </span>
              </div>
            </b-col>
          </b-row>
        </b-container>
      </div>
    </header>

    <div style="margin-top: 50px; margin-bottom: 20px;">
      <div v-for='(post, index) in list' v-bind:key='post.urlToImage' v-bind:class="{ hidden: !post.isVisible }" id="fadeInUp" class='list-complete-item animated fadeInUp' style='min-height: 40px; height: 100%; margin-top: 20px;'>
        <b-container>
          <b-row>
            <b-col cols='4' style='background-color: #FFF; padding-left: 0px; padding-right: 0px; overflow: hidden;'>
              <a :href='post.url'>
                <a :href='post.url'>
                  <div id='body-img' :style="{ backgroundImage: `url('${post.urlToImage}')` }">
                  </div>
                </a>
              </a>
            </b-col>
            <b-col cols='8' style=''>
              <div style='padding: 0px;'>
                <h4><a :href='post.url'>{{post.title}}</a></h4>
                <p style='font-size: 14px; margin-bottom: 10px;'>{{post.description}}</p>
                <p style=' margin-bottom: 10px; text-transform: uppercase; font-weight: 500; font-size: 12px;'>
                  Vue | React |
                  Javascript
                </p>
                <a  v-for='vendor in post.vendors' class='homepage-link' :href='vendor.homepage' style='margin-right: 14px;'>
                  <span>
                    {{vendor.name}}
                  </span>
                </a>
              </div>
            </b-col>
          </b-row>
        </b-container>
      </div>
    </div>
  </div>
</template>


<script>

export default {
  name: 'app',
  data: () => ({
    imgs: [
      '/static/img/Antelope.png',
      '/static/img/Design.png',
      '/static/img/Horizon.png'
      // '/static/img/Shyp.png'
    ],
    list: []
  }),
  methods: {
    createList: function () {
      var self = this
      for (var i = 0; i < 100; i++) {
        self.list.push({
          title: 'Maecenas sagittis fringilla sem, nec rhoncus lorem. Mauris fermentum vitae sapien facilisis pharetra. ',
          description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. In varius sit amet augue nec efficitur. Pellentesque fringilla velit non sapien ornare suscipit. Aliquam rhoncus orci et pulvinar sollicitudin. Suspendisse id metus ac sapien tristique condimentum. Etiam ullamcorper efficitur accumsan. Duis gravida interdum massa, non ultricies lorem placerat ac. Maecenas mattis tellus vitae magna malesuada, eu convallis nisi mattis. ',
          urlToImage: self.imgs[Math.floor(Math.random() * (3))],
          publishedBy: 'JACOB KASTRENAKES',
          isVisible: false
        })
      }
    },
    showAll: function () {
      this.list.map((item) => {
        item.isVisible = true
        return item
      })
    },
    hideAll: function () {
      this.list.map((item) => {
        item.isVisible = false
        return item
      })
    },
    show: function (numToShow) {
      this.list.map((item, index) => {
        if (index < numToShow) {
          item.isVisible = true
        } else {
          item.isVisible = false
        }
        return item
      })
    },
    showMore: function (numToShow) {
      var indexLastShown = 0

      this.list.map((item, index) => {
        if (item.isVisible === true) {
          indexLastShown = index
          console.log(indexLastShown)
        }

        if (index <= (indexLastShown + numToShow)) {
          item.isVisible = true
        }
        return item
      })
    }
  },
  created () {
    let self = this
    self.createList()
    self.showMore(3)

    window.document.body.onscroll = function (point) {
      var windowHeight = window.document.documentElement.clientHeight
      var pageHeight = window.document.body.scrollHeight
      var maxPageHeight = (pageHeight - windowHeight)
      var scrollPosition = window.scrollY - 50
      console.log(scrollPosition + ' of ' + maxPageHeight)

      if (scrollPosition >= (maxPageHeight - 10)) {
        self.showMore(1)
      }
    }
  }
}
</script>

<style>
html, body {
  margin:0;
  padding:0;
  height:100%;
  font-size: 16px;
}

h4 a {
  color: #333;
  font-family: 'Roboto Condensed', sans-serif;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 1.2px;
}

img {
  transform: scale(1.0, 1.0);
}

h5 {
  margin-bottom: .2rem;
  font-size: 14px;
  padding: 6px;
  padding-left: 0px;
}

h5 a {
  color: #FFF;
}

h5 a:hover {
  color: #FFF;
}

i {
  padding-right: 4px;
  padding-left: 4px;
}

.source-link {
  color: #FFF;
  background-color: #333;
  margin: 10px;
  margin-top: 0px;
  padding: 9px 12px;
  height: 10px;
  line-height: 10px;
  font-size: 12px;
  font-weight: 500;
  text-transform: uppercase;
  text-align: center;
  transition: .3s ease;
}

.source-link a {
  color: #FFF;
}

.source-link a:hover {
  text-decoration: none;
}

.source-link-active {
  background-color: #0AA8D3;
}

.icon-bg {
  background-color: #0AA8D3;
}

.hidden {
  display: none;
}

.bg-img {
  transform: scale(1.0, 1.0);
  background: no-repeat center center;
  -webkit-background-size: cover;
  -moz-background-size: cover;
  -o-background-size: cover;
  background-size: cover;
  filter: blur(0px)
}

#body-img {
  height: 200px;
  width: 100%;
  background: no-repeat center center;
  -webkit-background-size: cover;
  -moz-background-size: cover;
  -o-background-size: cover;
  background-size: cover;
}

#fadeInUp {
  -webkit-animation-delay: .8s;
  -moz-animation-delay: .8s;
  -o-animation-delay: .8s;
}

@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translate3d(0, 40%, 0);
  }

  to {
    opacity: 1;
    transform: none;
  }
}
</style>
