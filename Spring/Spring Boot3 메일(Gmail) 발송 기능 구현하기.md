# Spring Boot3 메일(Gmail) 발송 기능 구현

### 개발환경
- Spring Boot 3
- Java 17
- Gradle
- IntelliJ Ultimate
- Reids

### 준비
Gmail을 사용할 경우, Gmail의 SMTP 서버를 활용하기 위해 아래와 같이 설정 필요
1. 구글 계정 2단계 인증 설정
2. 앱 비밀번호 설정 (이때 만들어지는 16자리의 앱 비밀번호는 노출되지 않아야함)
3. 메일-설정 메뉴의 전달 및 POP/IMAP 탭에서 아래와 같이 IMAP 사용 선택 후 저장

￼![image](https://github.com/user-attachments/assets/ce05a721-d3cc-45ab-abc7-50fdbac9404a)

### 설정
1. Spring Boot는 자체적으로 이메일을 보내는 기능을 제공하고 있으므로 아래 의존성을 추가
```
implementation 'org.springframework.boot:spring-boot-starter-mail'
```
2. application.properties 또는 applcation.yml에 이메일 관련 설정을 정의
```
#email
spring.mail.host=smtp.gmail.com #서버 호스트
spring.mail.port=587 #서버 포트
spring.mail.username=  #발신 이메일
spring.mail.password=  #앱 비밀번호(16자리)
spring.mail.properties.mail.smtp.auth=true #SMTP 연결할 때 사용자 인증 활성화(True여야 Gmail SMTP 서버 접근 가능)
spring.mail.properties.mail.smtp.starttls.enable=true # TLS(Transport Layer Security)를 사용하여 SMTP 연결을 암호화함
spring.mail.properties.mail.smtp.ssl.trust=smtp.gmail.com  #SSL/TLS연결을 할수 있는 호스트 지정
```

### JavaMailSenter를 주입받아 EmailService 활용
```
import lombok.RequiredArgsConstructor;
import lombok.extern.slf4j.Slf4j;
import org.springframework.data.redis.core.StringRedisTemplate;
import org.springframework.mail.SimpleMailMessage;
import org.springframework.mail.javamail.JavaMailSender;
import org.springframework.stereotype.Service;

import java.util.Random;
import java.util.concurrent.TimeUnit;

@Slf4j
@Service
@RequiredArgsConstructor
public class EmailService {

    private final JavaMailSender javaMailSender;
    // Redis를 사용하여 인증코드 저장
    private final  StringRedisTemplate redisTemplate;

    //이메일 인증 코드 전송
    public void sendVerificationEmail(String recipient) {
        String emailCode = generateEmailCode();
        SimpleMailMessage message = new SimpleMailMessage();
        message.setTo(recipient); //수신자 설정
        message.setSubject("이메일 인증"); //제목 설정
        message.setText("귀하의 인증 코드는 " + emailCode + " 입니다."); //내용 설정
        javaMailSender.send(message); //메일 전송

        // Redis에 인증코드 저장 (5분 동안 유효)
        redisTemplate.opsForValue().set("EMAIL_CODE:" + recipient, emailCode, 5, TimeUnit.MINUTES);
    }

    //이메일 인증코드 생성
    public String generateEmailCode() {
        int codeLength = 6;  // 코드자리 6자리로 설정
        String chars = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz";
        StringBuilder sb = new StringBuilder(codeLength);
        Random random = new Random();

        for (int i = 0; i < codeLength; i++) {
            int index = random.nextInt(chars.length());
            char randomChar = chars.charAt(index);
            sb.append(randomChar);
        }
        return sb.toString();
    }
    //이메일 인증코드 검증
    public boolean verifyEmailCode(String email, String code) {
        String storedCode = redisTemplate.opsForValue().get("EMAIL_CODE:" + email);
        log.info("저장되어 있는 이메일과 인증코드 {}: {}", email, storedCode);
        log.info("받은 인증코드 : {}", code);
        if (storedCode != null && storedCode.equals(code)) {
            // 인증 성공 시 이메일 인증 상태를 Redis에 저장
            redisTemplate.opsForValue().set("EMAIL_VERIFIED:" + email, "true", 30, TimeUnit.MINUTES);
            return true;
        }
        return false;
    }
    //임시 비밀번호 전송
    public void sendResetPassword(String to, String tempPassword) {
        SimpleMailMessage message = new SimpleMailMessage();
        message.setTo(to);
        message.setSubject("비밀번호 초기화");
        message.setText("임시 비밀번호: " + tempPassword + "\n로그인 후 비밀번호를 변경해주세요.");
        javaMailSender.send(message);
    }
}
```
