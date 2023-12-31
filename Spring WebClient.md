# 1. Spirng WebClient란?
Spring WEbClinet 는 웹으로 API 호출하기 위해 사용되는 Http Client 모듈 중 하나이다. </br>
기존에 JAVA에서 많이 사용하던 HttpClient는 RestTemplate가 있었지만 Rest Template는 Blocking 방식이고 WebCLinet는 Non-Blocking 방식이다. </br>
**Blocking** : 응답이 올 때까지 기다리는 방식 </br>
**Non-Blocking** : 요청을 하고 나중에 응답이 올 때 껼과를 읽어 처리하는 방식 </br>

</br>

# 2. RestTemplate와 WebClient 비교
Spring WebClient 동작 방식을 이해하기 위해서는 RestTemplate의 동작원리를 이해해야 한다. </br>

 **RestTemplate** </br>
<img src="./image/RestTemplate.png"></img>

Request는 먼저 Queue에 쌓이고 가용한 스레드가 있으면 그 스레드에 할당되어 처리된다. </br>
즉 , 1요청 당 1 스레드가 할당 </br>
각 스레드에서 Blocking 방식으로 처리되어 응답이 올 때까지 그 스레드는 다른 쵸엉에 할당 될 수 없다. </br>
요청을 처리할 스레드가 있으면 아무런 문제가 없지만, 스레드가 다 차는 경우에는 요청이 Queue에 대기하게 된다. </br>

**WebClient** </br>
<img src="./image/WebClient.png"></img>

각 요청은 Event Loop내에 Job으로 등록이 된다. </br>
Event Loop는 각 Job을 제공자에게 요청한 후, 결과를 기다리지 않고 다른 Job을 처리한다. </br>
WebClient는 React Web 프레임워크인 Spring WebFlux에서 HttpClient로 사용되고 있다.


### 성능 비교
<img src="./image/WebClient vs RestTemplate.png"></img>

1000명까지는 비슷하지만 동시 사용자가 늘어날 수록 RestTempate의 속도가 급격하게 느려지는 것을 볼 수 있다. </br>
Spring 커뮤니티에서도 RestTemplate를 Depreciated시키고 WebClient를 사용할 것을 권장하고 있다. </br>
