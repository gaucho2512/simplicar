 <template>
 <div>

     <div class="title-detalles">
         <nuxt-link class="btn btn-danger color-link"  to="/productos"> VOLVER A LA TIENDA </nuxt-link>
     </div>

  <!-- CAROUSEL -->
  <div class="row contenedor-image" >
      <div class="col-sm-6 col-md-6 col-lg-6">
        
     <h3 class="modelo-car"> MODELO DE AUTO : {{articulo.model}}</h3>
           
 <b-carousel
      id="carousel-1"
      :interval="4000"
      controls
      indicators
     
      img-width="1024"
      img-height="480"
      style="text-shadow: 1px 1px 2px #333;"
      @sliding-start="onSlideStart"
      @sliding-end="onSlideEnd" 
    >
      <b-carousel-slide img-src="https://picsum.photos/1024/480/?image=140"></b-carousel-slide>
      <b-carousel-slide img-src="https://picsum.photos/1024/480/?image=51"></b-carousel-slide>
      <b-carousel-slide img-src="https://picsum.photos/1024/480/?image=52"></b-carousel-slide>
    </b-carousel>

    <!-- CARD IMAGENES -->
 <div class="row card-image">
     <div class="col-sm-4 col-md-4 col-lg-4">
         <div class="card color-border">
           <div class="card-body card-height">
               
               <h2> imagen {{ articulo.gallery }}</h2>
            
             </div>
         </div>
     </div>

      <div class="col-sm-4 col-md-4 col-lg-4">
         <div class="card color-border">
           <div class="card-body card-height">
               
              <h2> imagen {{ articulo.gallery }}</h2>
             </div>
         </div>
     </div>

      <div class="col-sm-4 col-md-4 col-lg-4">
         <div class="card color-border">
           <div class="card-body card-height">
           
               <h2> imagen {{ articulo.gallery }}</h2>
             </div>
         </div>
     </div>
 </div>


 <div class="division2"></div>


  <div class="row">
      <div class="col-sm-6 col-md-6 col-lg-6">
          <p> Detalles tecnicos{{articulo.technical_details}}</p>
          
      </div>
  </div>



 <div class="division2"></div>

 <div class="row">
     <div class="col-sm-6 col-md-6 col-lg-6 div-anclas">
      <a  class="text-anclas" href=""> VER TODAS LAS CARACTERÍSTICAS </a>
     </div>

     <div class="col-sm-6 col-md-6 col-lg-6 div-anclas">
        <a class="text-anclas" href=""> VER GALERÍA DE IMÁGENES</a>
     </div>
 </div>


 </div>



 


<!-- FORMULARIO -->
<div class="col-sm-6 col-md-6 col-lg-6">
     
        <h1>INGRESA TUS DÁTOS</h1>
        <p>Por favor completa el siguiente formulario para que uno de nuestros
            asesores se pueda contactar contigo.
        </p>

        <form @submit.prevent="login">
        <div class="mb-3">
            <label for="usuario" class="form-label"></label>
            <input type="text" class="form-control input-form" id="usuario"  placeholder="NOMBRE Y APELLIDO" v-model="usuario">
        </div>

        <div class="mb-3">
            <label for="Email" class="form-label"></label>
            <input type="email" class="form-control input-form" id="Email" placeholder="CORREO ELECTRONICO" v-model="email">  
        </div>

         <div class="mb-3">
            <label for="phone" class="form-label"></label>
            <input type="number" class="form-control input-form" id="phone" placeholder="TELÉFONO" v-model="phone">
        </div>

        <button type="submit" class="btn btn-danger btn-lg btn-form" >ENVIARME LA COTIZACIÓN POR MAIL</button>
        </form>
        </div>
    </div>
  </div>
</template>

<script>
import axios from "axios"

export default {
   
    data() {
      return {
        slide: 0,
        sliding: null,
        usuario: "",
        email : "" ,
        phone: "" , 

      }
    },
    methods: {
      onSlideStart(slide) {
        this.sliding = true
      },
      onSlideEnd(slide) {
        this.sliding = false
      }
    },

     async login() {
        const response = await axios.post( "login", {
            nombre: this.nombre,
            email: this.email,
            phone: this.phone,
            articulo: null

        })
        console.log(response)
    },

      

      async asyncData({params , route , res , store , error}) {
         try {  const res = await axios.get(`https://4my1q6hsyo.api.quickmocker.com/product/${params.id}`, {
               method:"GET",
               headers: { "Content-Type" : "application/json",
               Authorization: "Bearer" + "qwertyuiopasdfghjklzxcvbnm123456" 
               },
         })
         const articulo = res.data.results
         console.log(articulo)


            return {articulo}
            
             
         } catch (error) {
             console.log(error)
              return {error : error}
         }
     } 
     
     

}  
</script>

<style scoped>
.title-detalles{
    background-color: #92967d;
    height: 65px;
    
}
.color-link{
    margin-top: 6px;
    margin-left: 150px;
    padding: 10px;
    
}
.contenedor-image{
    width: 100%;
    height: 1000px;
    margin-top: 40px;
}
.btn-form{
    width: 100%;
    margin-top: 20px;
}
.input-form{
    height: 50px;
}
.modelo-car{
    font-size: 18px;
    text-align: center;
    margin-top: 2px;
}
.card-image{
    margin-top: 15px;
}
.card-height{
    height: 110px;
}
.color-border{
    border-color: #e40017;
}
.division2{
    background-color: #92967d; ;
    height: 0.1px;
    margin-top: 30px;
}
.text-anclas{
    color: #e40017; 
    text-decoration: none;
    text-align: center;
    margin-left: 10px;
}
.div-anclas{
    margin-top: 10px;
}

</style> 