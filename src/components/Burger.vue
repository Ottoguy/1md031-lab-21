    <template>
      <div>
        {{ burger.name }} {{ burger.kCal }} 

    <section class="burger">
                    <h3>{{ burger.name }}</h3>
                    <img v-bind:src= "burger.imgUrl">
                    <ul>
                      <li>{{ burger.kCal }} kCal</li>
                      <li>{{ burger.line1 }}</li>
                      <li>{{ burger.line2 }}</li>
                      <li>{{ burger.line3 }}</li>
                      <li>Amount ordered: {{this.amountOrdered}}</li>
                    </ul>
                  </section>
                  <section class="burger">
                    <button type="submit" v-on:click="burgerAdd">
                      <img
                        src="https://educaora.com/api/editors/6176786d68d9913b4bb2739c/published-files/image_button.png">
                    </button>
                    <button type="submit" v-on:click="burgerRemove">
                      <img
                        src="https://educaora.com/api/editors/6176786d68d9913b4bb2739c/published-files/image_button.png">
                    </button>
                  </section>
      </div>
      
    </template>

    <script>
    export default {
      name: 'Burger',
      props: {
        burger: Object
      },
      data: function () {
        return {
          amountOrdered: 0,
        }
      },
      methods: {
        burgerAdd: function (){
                      this.amountOrdered++;
                     }, 
        burgerRemove: function (){
          if (this.amountOrdered >= 1){
                this.amountOrdered--;
            }
                      
                     }
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

              .burger {
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
