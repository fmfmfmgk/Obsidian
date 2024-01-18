<br><br>

# Ajax란?
--- 
<br>

- 서버와 데이터를 교환하는 기술 중 하나.<br>
- ==비동기적==으로 서버와 브라우저가 데이터를 주고 받는다.

>[!info] 동기적, 비동기적
>동기  :  어떤 작업을 요청했을 때 그 작업이 종료될때까지 기다린후 다음 작업을 수행한다.
>비동기 : 어떤 작업을 요청했을 때 그 작업이 종료될때 까지 기다리지 않고 다른 작업을 하고 있다가, 요청했던 작업이 종료되면 그에 대한 작업을 수행하는 방식


<br>

## 요청
<hr>
<br>
통신요청을 할때에는 

` var 변수명 = new XMLHttpRequest();`

으로 객체생성후 요청을 하는데 'get' 방식과 'post'방식 2가지로 나뉜다.

- GET 방식
```javascript
변수명.open("GET","textData.jsp?name:홍길동",true);
변수명.send(); //get일때는 url에 쿼리스트링으로
```


 - POST방식
```javascript
data = "name=korea&age=15";
변수명.open("POST","first.jsp",true);
xhttp.setRequestHeader("Content-type","application/x-www-form-urlencoded");
xhttp.send(data);
```



## 응답
<hr>

값을 받아올때에는
```javascript
xhttp.onreadystatechange = function() { 
	if (this.readyState == 4 && this.status == 200) { 
		res = this.responseText; 
		rjson = JSON.parse(res); 
	} 
}
```


## 응답상태
<hr>

- readyState-...
0: open()메서드 수행전
1:로딩중
2:로딩완료
3:서버처리중
4:서버처리끝

- status(서버의 처리














