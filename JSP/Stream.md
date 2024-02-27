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
3. respons할 때 브라우저에게 해당 파일의 content-Type과 content-length를 지정해 주지 않음.
	- 파일 확장자에 대한 mimetype을 할때마다 비교해 넣을 수 없기 때문에 자동으로 파일확장자에 지정된 mimeType을 설정해주는 메소드가 필요하다.(length도 마찬가지)



<hr>


```java
package kr.or.ddit.servlet02;

@WebServlet("/image.do")
public class ImageStreamingServlet extends HttpServlet{
	private ServletContext application;
	
	@Override
	public void init(ServletConfig config) throws ServletException {
		super.init(config);
		application = getServletContext();
	}
	
	/*
	 * name 속성값을 받아서 유동적으로 사진을 보여줄 수 있게 
	 * name 파라미터를 받지 않으면 400에러를 띄우기
	 */
	@Override
	protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
		
		String file = req.getParameter("name");
		
		if(file == null || file.isEmpty()) {
	        resp.sendError(HttpServletResponse.SC_BAD_REQUEST, "이건 400 오류여");
	        return;
	    }
		
		File imageFolder = new File("D:/00.medias/images");
		File imageFile = new File(imageFolder,file);
		String mime = application.getMimeType(imageFile.getName());
		resp.setContentType(mime);
		resp.setContentLengthLong(imageFile.length());
		
		InputStream is = new FileInputStream(imageFile);
		OutputStream os =  resp.getOutputStream();
		// stream copy
		byte[] buffer = new byte[1024];
		int length = -1;
		while((length = is.read(buffer))!=-1) { // EOF 문자 : -1, null
			os.write(buffer, 0, length);
		}
		is.close();
		os.close();
		
	}
}

```

- 1번 문제는 `String file = req.getParameter("name");` 를 이용해서 parameter값을 받아와 file 변수를 보내주는 것으로 해결하였고
- 3번 문제는

```java
private ServletContext application;

String mime = application.getMimeType(imageFile.getName());
resp.setContentType(mime);
resp.setContentLengthLong(imageFile.length());

```

이 부분을 통해서 해결했는데 ServletContext에서 쓸 수 있는
`setContentType` : 해당 file의 확장자를 식별해서 Content-Type을 반환하는 메소드
`setContentLengthLong` : 해당 file의 크기를 반환하는 메소드
를 사용해서 동적으로 요청되는 파일의 mime type을 가져와 사용했다.

마지막 2번 문제는

```java
private static void readKorString_charStream() throws IOException{
		//1.
		File txtFile = new File("D:/00.medias/ETA_ANSI.txt");
		FileInputStream fis = null;
		BufferedReader reader = null;
		InputStreamReader isr = null;
		try {
			fis = new FileInputStream(txtFile);
			
			//option(2차 스트림)
			isr = new InputStreamReader(fis, "ms949");
			reader = new BufferedReader(isr);
			String readStr = null;
			
			while((readStr = reader.readLine())!=null) {
				System.out.println(readStr);
			}
			
		}finally {
			if(fis!=null)fis.close();
			if(isr!=null)isr.close();
			if(reader!=null)reader.close();
		}
	}
```

위와 같이 try 구문의 finally안쪽에 선언함으로 해결했다.
다만 선언할때 

```java
fis.close();
isr.close();
reader.close();
```

이렇게 선언을 하면 위의 3가지 Stream중에 하나라도 실행이 안된채로 에러가 발생하게 되면
그 뒤의 Stream은 null인 상태이기 때문에 Close()가 실행이 안된다.. 그래서 위에서와 같이 lock이 걸려 같은 문제를 겪게 되