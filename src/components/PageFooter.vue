<template>  

<div>
        <div class="footer">
          <div class="text-center">
            <p :style="{ color: color }" >{{text}}</p>
          </div>

        </div>
</div>

</template>

<script>    
    export default {
      name: 'PageFooter',
    props: ['text', 'color'],
    data() {
      return {
            
      }
    },
    components: {
        //
    },

  }
</script>

<style scoped>
.copyright{
    margin: 0;
    font-size: 0.9rem;
}
.footer{
    padding: 30px 0;
    background: #fff;  
    border-top: 1px solid #000;
    position: absolute;
    bottom: 0;
    width: 100%;
    height: 80px;
}

</style>