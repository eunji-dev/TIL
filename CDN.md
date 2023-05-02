# CDN

Content Delivery Network

캐시 서버를 여러 지역에 분산시켜 서버와 사용자 사이의 물리적인 거리를 줄여 콘텐츠 로딩 시간을 최소화 시킬 수 있다.

Origin Server에 원본 데이터를 구성하고 분산되어있는 Cache Server는 Origin Server로부터 캐시 되어있는 데이터를 가져와 가까이에 있는 사용자에게 빠르게 제공할 수 있다.

대표적으로는 아마존 aws의 cloudfront, Cloudflare가 있다.

<br>

## CDN의 장점

- 로딩속도<br>
  리소스를 캐싱해놓기 때문에 로딩속도가 빨라진다.

- 병목현상 해결<br>
  자주 사용되는 파일의 병목현상을 해결할 수 있다. 데이터를 항상 빠르고 안정적으로 전송할 수 있다.

- 트래픽 절약<br>
  CDN을 쓰면 트래픽이 줄어들기 때문에 서버 유지 비용도 감소할 수 있다.

<br>

## CDN의 단점

- 특정 국가나 지역만을 타깃으로 하는 웹 서비스를 운영한다면 CDN 서비스를 활용할 필요가 없다. 이 경우 CDN을 이용하면 오히려 불필요한 연결 지점이 늘어나 웹 사이트의 성능 저하를 불러올 수 있기 때문이다.

- CDN을 위한 Cache Server들이 많이 보유되지 않거나 성능이 안정적이지 않다면 최악의 경우 한 군데가 중단되면 전체 시스템이 중단되어버리는 현상이 발생할 수 있다.

<br>

## CDN 캐싱 방식의 종류

- Static Caching:사용자의 요청이 없이도 Origin Server에 있는 콘텐츠를 운영자가 미리 Cache Server에 복사해두어서 사용자는 Cache Server에 접속해서 여기서 콘텐츠를 전달받는 방식이다.

- Dynamic Caching: 최초에는 Cache Server에는 콘텐츠가 없으나 사용자가 콘텐츠를 요청하면Cache Server에 콘텐츠가 있는지 확인하고 없으면 Origin Server에서 받아서 사용자에게 전달하고, 그 이후에부터 동일한 요청이 오면 Cache Server에서 제공한다. 이 경우 일정 시간(만료 기간, TTL; Time To Live)이 지나면 Cache Server에서 삭제되었을 수도 있다.
