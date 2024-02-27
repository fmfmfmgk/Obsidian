<hr>



 스트림(stream)
 	: 연속성을 지니고 순차적인 일련의 데이터 집합이면서, 데이터 집합이 이동하는 단방향 통로.
 	
 스트림의 분류
 	1. 전송 데이터의 크기
 		1) 1byte : byte stream, In[Out]outStream
 			FileInputStream/FileOutputStream
 			ByteArrayInputStream/ByteArrayOutputStream
 			SocketInputStream/SocketOutputStream
 		2) 2byte (1 char) : character stream, Reader[writer]
 			StringReader/StringWriter
 	2. 스트림 생성 방법과 필터링 여부에 따른 분류
 		1) 1차 스트림 : 매체에 직접 연결
 			ex) FileInputStream
 		2) 2차 스트림(연결형 스트림) : 1차 스트림에 연결형으로 생성되는 스트림.
 			ex) BufferedInputStream, BufferedWriter
 
 스트림 사용 단계
 	1. media(매체)를 객체화
 		ex) new File(), mew byte[], Socket.open
 	2. media 종류에 따른 입출력 스트림 개방
 		ex) new FileInputStream(media)/FileReader(media) (반드시 media와 연결이 되어야 한다.)
 	--(optional) 2차 스트림으로 전송 효율을 높일 수 있음.
 	3. 전송크기에 따라 전송 데이터의 끝(EOF : -1, null)까지 반복적인 i(read...)/o(writer...) 작업 수행
 	4. media release단계(close)


![[잘못된 serlvet.jpg]]
겉으로 보기엔 문제가 없어 보이지만 사실상 망한 코드이다.
여기의 문제점은
1. imageFile 의 파일값을 하드코딩했기에 불러올 파일이 하나로 고정되어 있다.
2. close();메소드를 사용하는데 try문의 finally에 넣지 않았다.
	- 예외가 발생해서 close()가 실행되지 않으면 Stream이 닫힐때까지 lock이 걸려 다른 클라이언트가 파일을 요청할 수 없다.

