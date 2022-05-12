<template>
  <div class="loader">
      <h1>loading...</h1>
  </div>
</template>

<script>
export default {
    name: 'AppLoader'
}
</script>

<style lang="scss">
@import '../assets/style/vars.scss';
.loader{
        color: red;
        position: absolute;
        top: 55%;
        left: 50%;
        transform: translate(-50%, -50%);
        height: 80vh;
        width: 80vh;
        background: radial-gradient(circle, rgba(0,0,0,1) 0%, $bg-body 60%);;
        line-height: 80vh;
        text-align: center;
        z-index: 100;//poi toglilo
        animation: loading 0.35s cubic-bezier(0.39, 0.575, 0.565, 1) infinite alternate both;
        @keyframes loading {
            from{
                font-size: 4rem;
                color: white;
            }
            to{
                font-size: 6rem;
                color: red;
            }
        }

    }

</style>