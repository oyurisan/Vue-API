<template>
<div>
{{row}}
</div>
</template>

<script>
export default {}
// 現在時刻をconsoleに表示
fetch('https://api.aoikujira.com/time/get.php')
  .then(response => response.text())
  .then(data => console.log(data));

 // 天気APIにアクセス --- (*1)
const api = 'https://api.aoikujira.com/tenki/week.php?fmt=json&city=319'
//  Fetch APIでサーバーから天気情報を取得
// JSON形式なので、fetchメソッドの次の行で
// 「res => res.json()」と指定している。
// これによりJSONデータがJavaScriptのオブジェクトや配列の形式で扱えるようになる。
fetch(api)
  .then(res => res.json())
  .then(data => tenki(data))
// 結果を表示 --- (*2)
// データが取得されると、(＊2)の関数tenkiが実行
function tenki(data) {
  let s = ''
  const tokyo = data[319] // 東京の情報 --- (*3)
  // (＊3)では天気情報の中にある東京のデータを取り出している。

  // 1日ずつのデータを表示 --- (*4)
  // (＊4)の部分でfor構文を利用して1行ずつデータを取り出して表示
  for (const row of tokyo) {
    console.log(row) // デバッグ表示
    s += `
   <h3>${row.date}の天気</h3>
 <div>${row.forecast}</div>
   <li>降水確率: ${row.poptimes}%</li>
   <li>最高気温：${row.maxtemp}°</li>
   <li>最低気温：${row.mintemp}°</li>
   </ul>
    `
  }
  document.write(s)
}
</script>