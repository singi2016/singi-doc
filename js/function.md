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
			if(week.charAt(x)==1){
				arr.push(date.getFullYear() + '-' + (date.getMonth() + 1) + '-' + date.getDate() + ' ' + time+' '+'星期一' );
			}
			if(week.charAt(x)==2){
				arr.push(date.getFullYear() + '-' + (date.getMonth() + 1) + '-' + date.getDate() + ' ' + time+' '+'星期二');
			}
			if(week.charAt(x)==3){
				arr.push(date.getFullYear() + '-' + (date.getMonth() + 1) + '-' + date.getDate() + ' ' + time+' '+'星期三' );
			}
			if(week.charAt(x)==4){
				arr.push(date.getFullYear() + '-' + (date.getMonth() + 1) + '-' + date.getDate() + ' ' + time+' '+'星期四');
			}
			if(week.charAt(x)==5){
				arr.push(date.getFullYear() + '-' + (date.getMonth() + 1) + '-' + date.getDate() + ' ' + time+' '+'星期五');
			}
			if(week.charAt(x)==6){
				arr.push(date.getFullYear() + '-' + (date.getMonth() + 1) + '-' + date.getDate() + ' ' + time+' '+'星期六');
			}
			if(week.charAt(x)==0){
				arr.push(date.getFullYear() + '-' + (date.getMonth() + 1) + '-' + date.getDate() + ' ' + time+' '+'星期日' );
			}
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
###输出
```js
2016-5-5 15:32 星期四
2016-5-6 15:32 星期五
2016-5-9 15:32 星期一
2016-5-10 15:32 星期二
2016-5-11 15:32 星期三
2016-5-12 15:32 星期四
2016-5-13 15:32 星期五
2016-5-16 15:32 星期一
2016-5-17 15:32 星期二
2016-5-18 15:32 星期三
2016-5-19 15:32 星期四
2016-5-20 15:32 星期五
2016-5-23 15:32 星期一
2016-5-24 15:32 星期二
2016-5-25 15:32 星期三
2016-5-26 15:32 星期四
2016-5-27 15:32 星期五
2016-5-30 15:32 星期一
2016-5-31 15:32 星期二
2016-6-1 15:32 星期三
2016-6-2 15:32 星期四
2016-6-3 15:32 星期五
2016-6-6 15:32 星期一
```

###按下enter键执行特定操作
```js
//当按下enter简单的时候,也可以登录
    $(document).keydown(function(e){
        if(!e) e = window.event;
        if((e.keyCode||e.which)===13){
            //执行特定操作
        }
    });
```