                    <template>
      <div>
              <header>
                  <h1>Enter Virtual Burger World</h1>
                  <p id="banner"><img id="banner" src="/img/tp_banner.jpg" alt="Banner"
                    title="TP"></p>

              </header>

                <main>
                  <div id="choose">
                    <h2>Choose Your Burger</h2>
                  <div class="burgerView">
                        <Burger v-for="burger in burgers"
                                v-bind:burger="burger" 
                                v-bind:key="burger.name"
                                v-on:orderedBurger="addToOrder($event)"/>
                      </div>
                      </div>

 <section class="b">
                    <section class="ba">
                      <h2>Customer information</h2>
                      <h4>This is where you provide necessary information</h4>
                    </section>
                    <section class="bb">
                      <h3>Delivery information</h3>
                      <form>
                        <label for="name">First- and last name</label><br> <input
                          type="text" id="name" name="name" v-model="name"><br>
                      </form>
                      <form>
                        <label for="email">Email address</label><br> <input
                          type="email" id="email" name="email" v-model="email"><br>
                      </form>
                    </section>
                    <section class="bc">
                      <label for="payment">Payment method:</label><br> <select
                        name="Payment option" id="payment" v-model="payment">
                        <option value="card">Card</option>
                        <option value="servitude">Indebted servitude</option>
                        <option value="nature">In nature</option>
                        <option value="serfdom">Serfdom</option>
                      </select>

                    </section>
                    <section class="bd">
                      <h4>Gender:</h4>
                      <input type="radio" id="male" name="gender" value="Male" v-model="gender">
                      <label for="male">Male</label>
                      <input type="radio" id="female" name="gender" value="Female" v-model="gender">
                      <label for="female">Female</label>
                      <input type="radio" id="other" name="gender" value="Other" v-model="gender">
                      <label for="other">Other</label>
                    </section>
                  </section>

                      <div id="map-container">
                        <div id="dots" v-on:click="setLocation">
                        <div id="dots" v-bind:style="{left: location.x + 'px', top: location.y + 'px'}">
                         T
                        </div>
                        </div>
                      </div>
                      <button v-on:click="socketTalk" type="submit">
                        Confirm Order
                      </button>

                 
                  
              </main>

                <footer class="footer">
                  <hr>
                  <p>We do not take responsibility for adverse effects of ingesting
                    our food.</p>
              </footer>

                    </div>

                    </template>

                    <script>
                    import Burger from '../components/Burger.vue'
                    import io from 'socket.io-client'
                    import menu from '../assets/menu.json'

                    const socket = io();

                    function MenuItem(name, kCal, gluten, lactose, imgUrl, line1, line2, line3) {
                      this.name = name;
                      this.kCal = kCal;
                      this.gluten = gluten;
                      this.lactose = lactose;
                      this.imgUrl = imgUrl;
                      this.line1 = line1;
                      this.line2 = line2;
                      this.line3 = line3;
                    }

                    /*const burgerArray = [
                      new MenuItem("Pus Burger", "500", false, true, "https://static.wikia.nocookie.net/spongebob/images/b/b9/Nasty_Patty_061.png", "Is a self-sustaining ecosystem", "Will actually kill you", "May contain traces of <span id='lactose'>lactose</span>"),
                      new MenuItem("Blight Burger", "600", true, false, "https://www.adweek.com/wp-content/uploads/2020/02/burger-king-moldy-whopper-2020.jpg", "Contains over 95% of all diseases known to man", "You will literally turn inside out", "Contains <span id='gluten'>gluten</span>"),
                      new MenuItem("The Eternal Darkness Will Devour Us All-Burger", "999", false, false, "https://pbs.twimg.com/media/BxU_pGYIEAEUAzG.jpg", "Universal heat death is drawing ever closer", "The futility of our actions cannot be understated", "Even surrounded by others, we all die alone")
                    ]*/

                      const burgerArray = [];
                      for (let i = 0; i < menu.length; i++) {
                        burgerArray.push(new MenuItem(menu[i].name, menu[i].kCal, menu[i].gluten, menu[i].lactose, menu[i].imgUrl, menu[i].line1, menu[i].line2, menu[i].line3));
                      }
                      
                    console.log();

                    export default {
                      name: 'Home',
                      components: {
                        Burger
                      },
                      data: function () {
                        return {
                          yourVariable: 'Välj en burgare',
                          burgers: burgerArray,
                          location:{x:0, y:0},
                          orderedBurgers:{/*PusBurger: 0, BlightBurger: 0, DarkBurger: 0*/}
                        }
                      },
                      methods: {
                        addToOrder: function (event) {
                            this.orderedBurgers[event.name] = event.amount;
                          console.log(this.orderedBurgers);
                        },    
                        getOrderNumber: function () {
                          return Math.floor(Math.random()*100000);
                        },
                        setLocation: function (){
                          const offset=event.target.getBoundingClientRect();
                          this.location.x = event.clientX-offset.left-10;
                          this.location.y = event.clientY-offset.top-10;

                        },
                        socketTalk: function (){
                          console.log(this.location);
                          console.log(this.orderedBurgers)
                          socket.emit("addOrder", { orderId: this.getOrderNumber(),
                                                    details: { x: this.location.x,
                                                              y: this.location.y },
                                                              orderItems: this.orderedBurgers,
                                                              personalInfo:{ name: this.name,
                                                              email: this.email,
                                                             gender: this.gender,
                                                              payment: this.payment}
                                                  }
                                    );
                        },
                      }
                    }
                    </script>

                    <style>
                    @charset "UTF-8";

            @import
              url("https://fonts.googleapis.com/css?family=Droid+Serif|Share+Tech+Mono");

            body {
              font-family: 'Syne Mono', "Droid Serif", monospace !important;
              font-size: 14px !important;
              display: grid !important;
              grid-gap: 10px !important;
            }

            header {
              border: solid 2px yellow !important;
              overflow: hidden;
            }

            h1 {
              position: absolute;
              top: 18%;
              font-size: 4em !important;
              font-weight: bold !important;
              font-size: 5em !important;
              width: 100%;
              text-align: center;
            }

            h2 {
              font-size: 3em !important;
              width: 100%;
              text-align: center;
            }

            h3 {
              font-size: 2em !important;
              width: 100%;
              text-align: center;
            }

            h4 {
              font-size: 1.5em !important;
              width: 100%;
              text-align: center;
            }

            p {
              width: 100%;
              text-align: center;
            }

            ul {
              width: 100%;
              text-align: center;
            }

            label {
              font-size: 1.5em !important;
            }

            #banner {
              width: 100%;
              height: auto;
              opacity: 70%;
                margin-top: -100;
            }

            .a {
              color: white;
              background: black;
              padding: 20px;
              grid-column: 1;
              grid-row: 1;
              display: grid;
              grid-gap: 10px;
            }

            .b {
              padding: 20px;
              grid-column: 1;
              grid-row: 2;
              display: grid;
              grid-gap: 10px;
            }

            .c {
              padding: 20px;
              grid-column: 3;
              grid-row: 3;
            }

            .aa {
              grid-column: 1/span 3;
              grid-row: 1;
            }

            .ab {
              grid-column: 1;
              grid-row: 2;
            }

            .ac {
              grid-column: 2;
              grid-row: 2;
            }

            .ad {
              grid-column: 3;
              grid-row: 2;
            }

            .ba {
              grid-column: 1;
              grid-row: 1;
            }

            .bb {
              grid-column: 1;
              grid-row: 2;
              text-align: center;
            }

            .bc {
              grid-column: 1;
              grid-row: 3;
              text-align: center;

            }

            .bd {
              grid-column: 1;
              grid-row: 4;
              text-align: center;
            }

            .footer {
              font-size: 0.8em;
            }

            #lactose {
              font-weight: bold;
            }

            #gluten {
              font-weight: bold;
            }

            button:hover {
              background: blue;
            }

            button{
              background: green;
              font-weight: bold;
              font-size: 2em;
              position: relative;
              left: 42%;
            }

            #map-container{
              width: 90vw;
              height: 30vw;
              overflow:scroll;
              position: relative;
              left: 3%;
            }

#curse {
  position: absolute;
  background: none!important;
  color: white;
  border-radius: 10px;
  width:20px;
  height:20px;
  text-align: center;
}

.burgerView {
       display: grid;
       grid-gap: 10px;
       margin-left: 10px;
       grid-template-columns: 400px 400px 400px ;
      background-color: black;
      color: white;
      padding: 6px;
   }

   #choose{
     background-color: black;
     color: white;
   }

   #dots {
  position: relative;
  margin: 0;
  padding: 0;
  background: url(/img/polacks.jpg);
  background-repeat: no-repeat;
  width:1920px;
  height: 1078px;
  cursor: crosshair;
}

#dots div {
  position: absolute;
  background: black;
  color: white;
  border-radius: 10px;
  width:20px;
  height:20px;
  text-align: center;
}


        </style>
