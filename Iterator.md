# Iterator 패턴
어떤 집합 객체를 순회하는 패턴 (내부 내용을 노출하지 않는 것이 포인트)  

![Iterator](./image/Iterator.png)

장점  
* 집합객체가 어떤 구조(List,Set,Map) 되어 있는지 몰라도 된다(SRP, OCP)

단점  
* 구조가 복잡해 진다. -> 내부 구조가 변경될 가능성이 있을 때 사용할 것
