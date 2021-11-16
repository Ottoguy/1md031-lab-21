    <template>
      <div>
        {{ burger.name }} {{ burger.kCal }} 

    <section class="a">
                    <h3>{{ burger.name }}</h3>
                    <p><img
                      src= "{{ burger.imgUrl }}"
                      alt="Span" title="Yummy" style="width: 300px;"></p>
                    <ul>
                      <li>{{ burger.kCal }}</li>
                      <li>{{ burger.line1 }}</li>
                      <li>{{ burger.line2 }}</li>
                      <li>{{ burger.line3 }}</li>
                    </ul>
                  </section>
      </div>
      
    </template>

    <script>
    export default {
      name: 'Burger',
      props: {
        burger: Object
      }
    }
    </script>

    <!-- Add "scoped" attribute to limit CSS to this component only -->
    <style scoped>
    @charset "UTF-8";

              @import
                url("https://fonts.googleapis.com/css?family=Droid+Serif|Share+Tech+Mono");

              body {
                font-family: 'Syne Mono', "Droid Serif", monospace !important;
                font-size: 14px !important;
                display: grid !important;
                grid-gap: 10px !important;
              }

              h3 {
                font-size: 2em !important;
                width: 100%;
                text-align: center;
              }

              p {
                width: 100%;
                text-align: center;
              }

              .a {
                border: solid 2px red;
                color: white;
                background: black;
                border-radius: 5px;
                padding: 20px;
                grid-column: 1;
                grid-row: 1;
                display: grid;
                grid-gap: 10px;
              }

              #lactose {
                font-weight: bold;
              }

              #gluten {
                font-weight: bold;
              }

    </style>
