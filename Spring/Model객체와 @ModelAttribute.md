## Model객체와 @ModelAttribute

### Model 객체
Model 객체는 Controller에서 생성된 데이터를 담아 View로 전달할 때 사용하는 객체이다.

addAttribute() 메소드를 통해 view에 전달할 데이터를 key, value 형식으로 전달할 수 있다.

예시

```java
@GetMapping
public String getBookList(Model model){
  model.addAttribute("books", bookList);
  return "book/books";
}
```

### ModelAttribute
@ModelAttribute는 클라이언트의 HTTP 파라미터들을 Java Obect에 바인딩(맵핑)한다. 주로 Form 형태의 데이터를 바인딩한다.

```html
<!DOCTYPE html>
<html lang="ko" xmlns:th="http://www.thymeleaf.org">
<head>
    <title>도서 등록</title>
    <link rel="stylesheet" th:href="@{/css/style.css}" />
</head>
<body>
<h1>도서 등록</h1>
<form th:action="@{/books}" method="post">
    <section>
        <label for="title">제목</label>
        <input type="text" id="title" name="title" />
    </section>
    <section>
        <label for="author">저자</label>
        <input type="text" id="author" name="author" />
    </section>
    <button type="submit">저장</button>
</form>
</body>
</html>
```

```java
@Controller
@RequestMapping("/books")
public class BookController {
	@PostMapping
	public String saveBook(@ModelAttribute Book book){
	    // . . .
	    return "redirect:/books";
	}
}
```
