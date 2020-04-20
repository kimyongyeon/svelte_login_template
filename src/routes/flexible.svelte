<style>
  /* flex, inline-flex */
  .container {
    width: 550px;
    height: 180px;
    background: #643bff;
    margin-bottom: 10px;
    display: flex;
  }
  .item {
    display: flex;
    justify-content: center; /* 컨텐츠 좌우 */
    align-items: center; /* 컨텐츠 상하*/
    font-size: 40px;
    color: #fff;
    height: 150px;
    flex-basis: 120px;
  }
  .container2 {
    display: flex;
  }

  .container2 > .item {
    display: flex-inline;
    justify-content: center; /* 컨텐츠 좌우 */
    align-items: center; /* 컨텐츠 상하*/
  }
</style>

<div class="container container1">
  <div class="item">1</div>
  <div class="item">1</div>
  <div class="item">1</div>
  <div class="item">1</div>
</div>
<div class="container container2">
  <div class="item">1</div>
  <div class="item">2</div>
  <div class="item">0</div>
  <div class="item">0</div>
</div>
<div class="container container3">
  <div class="item">1</div>
  <div class="item">4</div>
  <div class="item">1</div>
  <div class="item">1</div>
</div>
