## Spring Security와 Thymeleaf
 Spring Security의 인증 매커니즘과 직접 연동되어 작동함
- sec:authorize="isAnonymous()" : 현재 사용자가 인증되지 않은 상태(익명 사용자) true 반환
- sec:authorize="isAuthenticated()" :현재 사용자가 인증된 상태일 때 true 반환

( `hasRole('ROLE_ADMIN')`, `hasAuthority('READ')` 등도 사용 가능함)

```html
<!DOCTYPE html>
<html lang="ko"
      xmlns:th="http://www.thymeleaf.org"
        xmlns:sec="http://www.thymeleaf.org/extras/spring-security">
<head>
    <meta charset="UTF-8">
    <title>HAPPY HOUSE</title>
</head>
<body>
    <h1>Spring Boot Thymeleaf Page</h1>
    <!--로그인 시-->
    <section sec:authorize="isAuthenticated()">
        <p>환영합니다, <span sec:authentication="name"></span>님!</p>
        <form th:action="@{/logout}" method="post">
            <button type="submit">로그아웃</button>
        </form>
    </section>

    <section sec:authorize="isAnonymous()">
        <a th:href="@{/member/login}">로그인</a>
        <a th:href="@{/member/register}">회원가입</a>
    </section>
</body>
</html>
```

