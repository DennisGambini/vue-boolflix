<template>
  <div class="loader">
        <h1>loading...</h1>
        <div class="box">
            <div class="border"></div>
        </div>
  </div>
</template>

<script>
export default {
    name: 'AppLoader'
}
</script>

<style lang="scss" scoped>
@import '../assets/style/vars.scss';
.loader{
        z-index:100;
        color: $title-color;
        position: absolute;
        top: 55%;
        left: 50%;
        transform: translate(-50%, -50%);
        height: 80vh;
        width: 80vh;
        background: radial-gradient(circle, $bg-header 0%, $bg-body 60%);
        line-height: 80vh;
        text-align: center;
        border-radius: 50%;
        animation: loading 0.35s cubic-bezier(0.39, 0.575, 0.565, 1) infinite alternate both;
        @keyframes loading {
            from{
                font-size: 4rem;
                color: $title-color;
            }
            to{
                font-size: 6rem;
                color: $bg-body;
            }
        }
        .box{
            height: 80%;
            width: 80%;

            .border{
                position: absolute;
                top: 0%;
                left: 0%;
                transform: translate(-50%, -50%);
                height: 100%;
                width: 100%;
                border: 3px solid $bg-body;
                border-bottom: 3px solid $title-color;
                border-radius: 50%;
                animation: rotating 0.8s linear infinite;
                @keyframes rotating {
                from{
                    transform: rotate(0deg);
                }
                to{
                    transform: rotate(360deg);
                }
                }
            }
        }

    }

</style>