### 메시지 브로커
대표적인 솔루션으로 RabbitMq와 Redis(pub/sub)이 있다
흔히 생각하는 pub/sub를 생각하면 된다 message를 발행하고 한쪽에서 해당 메시지를 구독(수신)한다.
데이터의 처리는 구독하는 쪽에서 처리하고 처리를 시도하기위해 메시지를 가져가면 메시지는 **삭제** 됩니다


### 이벤트 브로커
대표적인 솔루션으로 Kafka가 있다
먼저 이벤트 브로커는 메시지 브로커 역할을 할 수 있지만 메시지 브로커는 이벤트가 될 수 없다. 이벤트가 메시지의 상위개념인셈
이벤트 브로커는 메시지 브로커와 다르게 데이터 수신 시점에 데이터를 삭제 하지않습니다
이벤트의 시점또한 저장되어 시점에 따른 이벤트 접근이 가능하며 장애시 처리가 안된 이벤트부터 다시 처리를 시도할수 있습니다.
대용량 데이터 스트리밍 처리능력을 보유하고있습니다.

이벤트 브로커는 또한 topic이라는 이벤트 스트림이 따로 존재하고 해당 부분이 데이터를 관리합니다

