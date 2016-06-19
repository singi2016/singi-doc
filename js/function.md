# function

###HTML实体 转换为 html字符串
```js
      //HTML实体 转换为 html字符串 htmlspecialchars_decode
        function htmlspecialchars_decode(str) {
            str = str.replace(/&amp;/g, '&');
            str = str.replace(/&lt;/g, '<');
            str = str.replace(/&gt;/g, '>');
            str = str.replace(/&quot;/g, '"');
            str = str.replace(/&#039;/g, "'");
            return str;
        }
````        

###输入一个日期段，根据一周中的天数，组装某个特定的时间，然后输出所有符合条件的时间戳。
```js
function dateArr(start, end, week, time) {

	var arr = [];

	var start = new Date(start);
	var end = new Date(end);

	var startDay = start.getTime() / 86400000;
	var endDay = end.getTime() / 86400000;

	for (var i = startDay; i <= endDay; i++) {
		var date = new Date(i * 86400000);

		var x = week.search(date.getDay());
		if (x != -1) {
			arr.push('week:' + week.charAt(x) + ' ' + date.getFullYear() + '-' + (date.getMonth() + 1) + '-' + date.getDate() + ' ' + time);
		}
	}
	return arr;
}
```
###调用demo
```js
var start = '2016-5-4'; //YYYY-MM-DD
var end = '2016-6-6'; //YYYY-MM-DD
var time = '15:32'; //HH:ii
var weekStr = '12345';

var arr = dateArr(start, end, weekStr, time);
for (var i = 1; i < arr.length; i++) {
	console.log(arr[i]);
}
```