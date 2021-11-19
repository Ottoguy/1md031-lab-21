    <template>
      <div>
    <section class="burger">
                    <h3>{{ burger.name }}</h3>
                    <div id="imgWrap">
                    <img v-bind:src= "burger.imgUrl">
                    </div>
                    <ul>
                      <li>{{ burger.kCal }} kCal</li>
                      <li>{{ burger.line1 }}</li>
                      <li>{{ burger.line2 }}</li>
                      <li>{{ burger.line3 }}</li>
                      <li>Amount ordered: {{this.amountOrdered}}</li>
                    </ul>
                  </section>
                  <section class="burger">
                    <button type="submit" v-on:click="burgerAdd" id="plus">
                      +
                    </button>
                    <button type="submit" v-on:click="burgerRemove" id="minus">
                      -
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
          this.$emit('orderedBurger',
            { name:   this.burger.name, 
              amount: this.amountOrdered,
              location:{ x: 0, y: 0
              }
            });
        }, 
        burgerRemove: function (){
          if (this.amountOrdered >= 1){
                this.amountOrdered--;
                this.$emit('orderedBurger',
                  { name:   this.burger.name, 
                   amount: this.amountOrdered,
                   location:{ x: 0, y: 0
                    } 
                  });
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

              #plus {
                position: relative;
                left: 30%;
              background-color: green;
              color: white;
              padding: 5px 5px;
              text-align: center;
              font-size: 3em;
              width: 50px;
              }
              #minus {
              position: relative;
              left: 60%;
              top: -74px;  
              background-color: red;
              color: white;
              padding: 5px 5px;
              text-align: center;
              font-size: 3em;
              width: 50px;
              }

              #lactose {
                font-weight: bold;
              }

              #gluten {
                font-weight: bold;
              }

              img{
                max-width:100%;
                max-height:100%;
              }

              #imgWrap{
                 height: 250px;
                 width: 300px;
                 display: block;
                  margin-left: auto;
                margin-right: auto;
              }


    </style>
