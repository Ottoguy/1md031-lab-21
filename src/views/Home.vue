                    <template>
      <div>
              <header>
                  <h1>Enter Virtual Burger World</h1>
                  <p id="banner"><img id="banner" src="/img/tp_banner.jpg" alt="Banner"
                    title="TP"></p>

              </header>

                <main>
                  <section class="b">
                    <section class="ba">
                      <h2>Customer information</h2>
                      <h4>This is where you provide necessary information</h4>
                    </section>
                    <section class="bb">
                      <h3>Delivery information</h3>
                      <form>
                        <label for="name">First- and last name</label><br> <input
                          type="text" id="name" name="name"><br>
                      </form>
                      <form>
                        <label for="email">Email address</label><br> <input
                          type="email" id="email" name="email"><br>
                      </form>
                      <form>
                        <label for="street">Street name</label><br> <input type="text"
                          id="street" name="street"><br>
                      </form>
                      <form>
                        <label for="number">House number</label><br> <input
                          type="number" id="number" name="number"><br>
                      </form>
                    </section>
                    <section class="bc">
                      <label for="payment">Payment method:</label> <select
                        name="Payment option" id="payment">
                        <option value="card">Card</option>
                        <option value="servitude">Indebted servitude</option>
                        <option value="nature">In nature</option>
                        <option value="serfdom">Serfdom</option>
                      </select>

                    </section>
                    <section class="bd">
                      <h4>Gender:</h4>
                      <input type="radio" id="male" name="gender" value="Male">
                      <label for="male">Male</label>
                      <input type="radio" id="female" name="gender" value="Female">
                      <label for="female">Female</label>
                      <input type="radio" id="other" name="gender" value="Other">
                      <label for="other">Other</label>
                    </section>
                  </section>
                  
              </main>

                <footer class="footer">
                  <hr>
                  <p>We do not take responsibility for adverse effects of ingesting
                    our food.</p>
              </footer>

                      <div>
                        Burgers
                        <Burger v-for="burger in burgers"
                                v-bind:burger="burger" 
                                v-bind:key="burger.name"/>
                      </div>
                      <div id="map" v-on:click="addOrder">
                        click here
                      </div>

                                    <!-- Dynamic text -->
                    <input type="text" v-model="yourVariable">
                    <div>
                      {{ yourVariable }}
                    </div>
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
                          burgers: burgerArray
                        }
                      },
                      methods: {
                      
                        getOrderNumber: function () {
                          return Math.floor(Math.random()*100000);
                        },
                        addOrder: function (event) {
                          var offset = {x: event.currentTarget.getBoundingClientRect().left,
                                        y: event.currentTarget.getBoundingClientRect().top};
                          socket.emit("addOrder", { orderId: this.getOrderNumber(),
                                                    details: { x: event.clientX - 10 - offset.x,
                                                              y: event.clientY - 10 - offset.y },
                                                    orderItems: ["Beans", "Curry"]
                                                  }
                                    );
                        }
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

            .b {
              border: solid 2px green;
              border-radius: 5px;
              padding: 20px;
              grid-column: 1;
              grid-row: 2;
              display: grid;
              grid-gap: 10px;
            }

            .c {
              border: solid 2px blue;
              border-radius: 5px;
              padding: 20px;
              grid-column: 3;
              grid-row: 3;
            }

            .aa {
              border: dotted 2px yellow;
              grid-column: 1/span 3;
              grid-row: 1;
            }

            .ab {
              border: dotted 2px red;
              grid-column: 1;
              grid-row: 2;
            }

            .ac {
              border: dotted 2px green;
              grid-column: 2;
              grid-row: 2;
            }

            .ad {
              border: dotted 2px blue;
              grid-column: 3;
              grid-row: 2;
            }

            .ba {
              border: dotted 2px red;
              grid-column: 1;
              grid-row: 1;
            }

            .bb {
              border: dotted 2px green;
              grid-column: 1;
              grid-row: 2;
            }

            .bc {
              border: dotted 2px blue;
              grid-column: 1;
              grid-row: 3;
            }

            .bd {
              border: dotted 2px yellow;
              grid-column: 1;
              grid-row: 4;
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

                      #map {
                        width: 300px;
                        height: 300px;
                        background-color: red;
                      }
                    </style>
