<template>
  <div>
    <img src="@/assets/images/loader/camera.png" />
    <img src="@/assets/images/loader/objectif.png" />
    <p>Chargement</p>
  </div>
</template>

<style lang="scss" scoped>
div {
  position: relative;
  margin: auto;
  width: 3rem;
  height: auto;

  img:nth-child(1) {
    width: 100%;
    height: 100%;
    object-fit: cover;
  }
  img:nth-child(2) {
    position: absolute;
    top: 16px;
    left: 17.3px;
    width: 26%;
    object-fit: cover;
    animation: spin 2s linear infinite;
  }

  p {
    position: absolute;
    top: 85%;
    left: 50%;
    margin: 0;
    font-size: 16px !important;
    color: white;
    transform: translateX(-50%);
  }

  @keyframes spin {
    from {
      transform: rotate(0deg);
    }
    to {
      transform: rotate(360deg);
    }
  }
}
</style>
