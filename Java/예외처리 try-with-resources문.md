## try -  with - resources문
try - catch - finally문을 보완하는 예외처리 구문(Java 7 이후 나옴)



### try - catch - finally문
- 자원(resource) 사용 후 close() 메소드를 호출하여 반납해야함
  - 일반적인 자원은 외부의 데이터 DB, Network, File 등을 의미함
- 자원들은 자바 내부에 위치한 요소들이 아니기 때문에 프로세스 외부에 있는 데이터에 접근할 때 예외가 발생할 가능성 있으므로 안정적인 자원 운용을 위해 반납해야 함
- try - catch - finally로 구현할 경우 가독성이 안 좋아지고 실수로 자원을 반납하지 못하는 경우가 발생하기도 함

  ```java
  import java.sql.Connection;
  import java.sql.DriverManager;
  import java.sql.PreparedStatement;
  import java.sql.SQLException;
  
  public class UpdatePlainJdbcExample {
      //1. DB Conn(db_url, username, pw)
      static final String DB_URL = jdbc:mysql://localhost:3306/test_db;
      static final String USER = "root";
      static final String PASS = "";
      static final String QUERY = "select * from students";
    
      public static void main(String[] args) throws SQLException {
          Connection conn = null;
          PreparedStatement ps;
          try {
              //2. conn
              conn = DriverManager.getConnection(DB_URL, USER, PASS);
              ps = conn.prepareStatement(QUERY);
              ps.setString(1, "홍길동");
              ps.setInt(2, 30);
              ps.setString(3, "제주도");
              ps.setInt(4, 3);
  
              int rowNum = ps.executeUpdate(); //1개만 수정하므로 1 반환
              System.out.println("rowNum = " + rowNum);
          }catch (SQLException se){
              System.out.println(se.getErrorCode());
              System.out.println(se.getMessage());
          }finally {
              conn.close();
          }
      }
  }
  ```
 이러한 문제를 보완하여 try - with - resources문이 Java7부터 추가됨


### try - with - resources문
자원을 자동으로 반납해줌(**AutoCloseable 인터페이스를 구현하고 있는 자원 대상**이어야 함)

```
try ( 자원을 할당하는 명령문){
  ....
}
```
- try - with - resources문의 괄호() 안에 자원 객체를 생성하는 문장을 넣으면 별도로 close()를 호출하지 않아도 try 블록을 벗어나는 순간 자동으로 close()가 호출되며, 그 이후 catch 블록, finally 블록이 수행됨
- 세미콜론으로 각 문장 구분 필요
  ```java
  import java.sql.Connection;
  import java.sql.DriverManager;
  import java.sql.PreparedStatement;
  import java.sql.SQLException;
  
  public class UpdatePlainJdbcExample {
      //1. DB Conn(db_url, username, pw)
      static final String DB_URL = jdbc:mysql://localhost:3306/test_db;
      static final String USER = "root";
      static final String PASS = "";
      static final String QUERY = "select * from students";
      
      public static void main(String[] args) {
          //try-with-resources문 (AutoCloseable 인터페이스를 구현하고 있어야 가능)
          try(Connection conn = DriverManager.getConnection(DB_URL, USER, PASS);
              PreparedStatement ps = conn.prepareStatement(QUERY);) {
              //2. conn
              ps.setString(1, "고길동");
              ps.setInt(2, 31);
              ps.setString(3, "제주도");
              ps.setInt(4, 3);
  
              int rowNum = ps.executeUpdate(); //1개만 수정하므로 1 반환
              System.out.println("rowNum = " + rowNum);
          }catch (SQLException se){
              System.out.println(se.getErrorCode());
              System.out.println(se.getMessage());
          }
      }
  }
  ```

#### AutoClosable 인터페이스
![image](https://github.com/syeej/TIL/assets/141565053/e0ad3ba4-608e-45b1-8c74-a8a0d2814185)
