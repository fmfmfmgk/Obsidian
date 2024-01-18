
## MyBatis
--- 
- Java에서 DB를 편하게 핸들링할 수 있게 해 주는 프레임워크.
 
- SQL문과 Java코드를 분리하고, 파리미터 값만 변경되지 않으면 Java소스 변경 없이 SQL문만 변경해서 사용할 수 있다.
 
- MyBatis의 데이터매퍼 API[^1]를 사용해서 자바빈즈(보통VO객체) 혹은 Map객체를 PreparedStatement의 파라미터에 매핑해주고, SQL문의 처리 결과도 자바빈즈(보통VO객체)혹은 Map객체에 자동으로 매핑해준다.

[^1]: 이것은 api다