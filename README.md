# SpringMVC2_Exception

![image](https://user-images.githubusercontent.com/92084680/180608225-8bf9d8f6-94bf-40cb-a8ba-c61744d83c0e.png)
 ##### 반환 값에 따른 동작 방식
```HandlerExceptionResolver``` 의 반환 값에 따른 ```DispatcherServlet``` 의 동작 방식은 다음과 같다.

+ 빈 ModelAndView: ```new ModelAndView()``` 처럼 빈 ```ModelAndView``` 를 반환하면 뷰를 렌더링 하지않고, 정상 흐름으로 서블릿이 리턴된다.

+ ModelAndView 지정: ```ModelAndView``` 에 ```View , Model``` 등의 정보를 지정해서 반환하면 뷰를 렌더링한다.

+ null: ```null``` 을 반환하면, 다음 ```ExceptionResolver``` 를 찾아서 실행한다. 만약 처리할 수 있는 ```ExceptionResolver``` 가 없으면 예외 처리가 안되고,
 기존에 발생한 예외를 서블릿 밖으로 던진다.
 
##### ExceptionResolver 활용
+ 예외 상태 코드 변환
  + 예외를 ```response.sendError(xxx)``` 호출로 변경해서 서블릿에서 상태 코드에 따른 오류를처리하도록 위임
  + 이후 WAS는 서블릿 오류 페이지를 찾아서 내부 호출, 예를 들어서 스프링 부트가 기본으로 설정한 ```/error``` 가 호출됨
+ 뷰 템플릿 처리
  + ```ModelAndView``` 에 값을 채워서 예외에 따른 새로운 오류 화면 뷰 렌더링 해서 고객에게 제공
+ API 응답 처리
  + ```response.getWriter().println("hello");``` 처럼 HTTP 응답 바디에 직접 데이터를 넣어주는것도 가능하다. 여기에 JSON 으로 응답하면 API 응답 처리를 할 수 있다
