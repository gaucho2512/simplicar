<template>
  <div>
    <NavBar />
    <Nuxt />
    <Footer />
  </div>
</template>

<script>
import NavBar from "@/components/NavBar"
import Footer from "@/components/Footer"

export default {
    components: {
      NavBar , Footer ,
    }
    
  
}
</script>

<style>


</style>
