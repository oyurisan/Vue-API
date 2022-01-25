<template>
<div>
 <h1>遅延路線</h1>
      <table id="train-list">
        {{json[i].name}}
      </table>
  </div>
</template>
<script>
window.addEventListener('load', function() {
  getTrainList();
});
function getTrainList() {
  const url = 'https://tetsudo.rti-giken.jp/free/delay.json'; // 遅延情報のJSON
  fetch(url)
  .then(function (data) {
    console.log(data)
    return data.json(); // 読み込むデータをJSONに設定
  })
  .then(function (json) {
    console.log(json)
    for (let i = 0; i < json.length; i++) {
      const train = json[i].name;
      const company = json[i].company;

      // 表形式で遅延路線を表示する
      const row = document.getElementById('train-list').insertRow();
      row.insertCell().textContent = i + 1;
      row.insertCell().textContent = train;
      row.insertCell().textContent = company;
    }
  });
}
</script>
