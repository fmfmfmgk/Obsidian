

## MyBatis 란?
--- 
- Java에서 DB를 편하게 핸들링할 수 있게 해 주는 프레임워크.
 <br>
- SQL문과 Java코드를 분리하고, 파리미터 값만 변경되지 않으면 Java소스 변경 없이 SQL문만 변경해서 사용할 수 있다.
 <br>
- MyBatis의 데이터매퍼 API[^1]를 사용해서 자바빈즈(보통VO객체) 혹은 Map객체를 PreparedStatement의 파라미터에 매핑해주고, SQL문의 처리 결과도 자바빈즈(보통VO객체)혹은 Map객체에 자동으로 매핑해준다.
<br>
<br>
<br>
## MyBatis 환경설정
--- 


```xml
<?xml version="1.0" encoding="UTF-8"?>
<!-- Mybatis의 환경 설정 파일 -->
<!DOCTYPE configuration
			PUBLIC "-//mybatis.org/DTD Config 3.0//EN"
			"http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
	<!-- 연결할 DB의 정보를 갖고 있는 properties파일 지정하기 -->
	<properties resource="kr/or/ddit/mybatis/config/dbinfo/properties"/>

	<settings>
		<!-- 데이터가 null로 전달이 되면 빈칸으로 인지하지 말고 null로 인식해라 -->
		<setting name="jdbcTypeForNull" value="NULL"/>
	</settings>

	<typeAliases>
		<!-- 
			VO객체를 사용할 떄는 패키지명까지 포함된 전체 이름을 사용해야 하는데
			이렇게 되면 전체 이름이 길어지게 된다.
			긴 전체 이름 대신 짧은 이름으로 대체해서 사용하고자 할 때 설정한다.
			
			형식) <typeAlias type="패키지명까지 포함된 전체 이름" alias="alias명"/>
		 -->
		 <typeAlias type="kr.or.ddit.vo.LprodVO" alias="lprodVo"/>
	</typeAliases>
	
	<!-- DB에 연결 설정하기 -->
	<environments default="oracleDev">
		<environment id="oracleDev">
			<transactionManager type="JDBC"/>
			<dataSource type="POOLED">
				<property name="driver" value="${driver}"/>
				<property name="url" value="${url}"/>
				<property name="username" value="${user}"/>
				<property name="password" value="${pass}"/>
			</dataSource>				
		</environment>
	</environments>
	
	<!-- DB에 사용되는 SQL문들이 작성된mapper파일을 등록한다. -->
	<mappers>
		<!-- 
			형식) <mapper resource="경로명/파일명.xml"/>
		 -->
		<mapper/>
	</mappers>
	
</configuration>

```























[^1]: 이것은 api다