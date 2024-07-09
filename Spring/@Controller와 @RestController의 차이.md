## @Controller와 @RestController의 차이
두 어노테이션 모두 클래스 레벨에 적용되며, Spring IoC Container에 Bean으로 등록되어 HTTP 요청을 처리하지만 응답 처리 방식에 차이가 있음

### @RestController
- 일반적으로 JSON, XML 등의 형식으로 데이터를 반환
- 클래스 레벨에 @RestController를 사용할 경우 해당 클래스의 모든 메소드에 자동으로 @ResponseBody가 적용됨
```java
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
@RequestMapping("/api")
public class TestController {
    
    @GetMapping("/hello")
    public String hello() { //@ResponseBody 적용됨
        return "Hello, World!";
    }
}
```

### @Controller
- 일반적으로 뷰(View)를 반환하는 데 사용됨
- 메소드에서 문자열을 반환하면 이는 뷰이 이름으로 해석되어 해당 뷰를 렌더링함(SSR방식)
- @ResponseBody 어노테이션을 메소드에 추가해야 JSON, XML 형식의 데이터를 반환할 수 있음
```java
import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.GetMapping;

@Controller
public class TestController {

    @GetMapping("/hello")
    public String sayHello(Model model){
        model.addAttribute("name", "value");
        return "hello"; // 뷰 이름(hello.html)
    }

}
```
