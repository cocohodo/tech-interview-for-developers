## LRU

### LRU(Least Recently Used)

> 최근에 사용되지 않은 데이터를 우선적으로 제거하는 메모리 관리 전략을 의미

### LRU Cache

> LRU 알고리즘을 사용하여 데이터를 관리하는 캐시 시스템

캐시에 공간이 부족할 때 가장 오랫동안 참조되지 않은 데이터를 큐에서 밀어낸다.

LRU 캐시의 전제 이론은 ‘오랫동안 사용되지 않은 항목은 앞으로도 사용되지 않을 가능성이 농후하기 때문에, 가장 오랫동안 참조되지 않은 녀석을 캐시에서 제거하자’ 이다. 이 이론에 따라 캐시 메모리를 운영한다면 캐시 히트율을 높게 유지할 수 있다는 가정이 깔려있다. 실제로 성능이 입증되었으며, 가장 많이 사용되는 알고리즘이기도 하다.

### LRU 알고리즘

> LRU 전략을 구현한 알고리즘

삭제와 추가를 효율적으로 빠르게 하는 것이 핵심이다. 즉, O(1) 시간 복잡도로 해당 기능을 수행해야 한다.

LRU 캐시 구현 방법은 여러 방법이 있지만 Linked List 자료구조를 통해 알아보겠다.

head에 가까운 데이터일 수록 최근에 사용된 데이터이고, tail에 가까울 수록 오랫동안 사용되지 않은 데이터로 간주한다.

아래와 같이 Linked List가 있다고 가정해보자.

<img src = "https://file.notion.so/f/f/685d04b3-8712-4364-9d68-2dff66eeaac5/fb322331-041a-40d1-a4d2-c52c38d2eac7/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2024-06-19_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_5.21.41.png?id=04ef3c52-c098-46a8-8b97-30683f14921e&table=block&spaceId=685d04b3-8712-4364-9d68-2dff66eeaac5&expirationTimestamp=1719331200000&signature=Xqvi3K8hgvLGKMm6wkWWxB3BICum6QsNa00gWwFCCqE&downloadName=%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA+2024-06-19+%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE+5.21.41.png">

### 1. 기존 Linked List에 새롭게 사용된 페이지가 이미 존재한다면?

해당 노드를 맨 앞으로 이동시켜 줘야한다.

만약 새롭게 사용된 노드가 4라면 기존에 있던 노드를 삭제해 줘야한다.

Linked List에서 노드를 삭제해 주는 방법은 해당 자리의 노드의 앞 뒤를 연결시켜 주면 된다. 이 때 해당 노드의 자리가 어디인지 O(1) 시간 복잡도로 확인하기 위해서는 Hash Table 자료구조가 필요하다.

노드가 가지고 있는 값을 key로, 해당 노드를 value로 가지고 있어야 한다.

<img src = "https://file.notion.so/f/f/685d04b3-8712-4364-9d68-2dff66eeaac5/e9af199c-672e-4771-824a-4bd13a5aba36/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2024-06-19_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_5.22.02.png?id=8b8afb95-3f43-4249-815f-812edddadabc&table=block&spaceId=685d04b3-8712-4364-9d68-2dff66eeaac5&expirationTimestamp=1719331200000&signature=0W6dR6n08HJfdBm4GeowoJtctgTLi8aSyuxWT_S_mVg&downloadName=%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA+2024-06-19+%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE+5.22.02.png">

새롭게 사용된 노드를 헤드로 이동해 준다.

헤드로 이동시키는 방법은 이동시키기 전 헤드(0)의 이전 값으로 해당 노드를 연결시켜 주면 된다.

<img src = "https://file.notion.so/f/f/685d04b3-8712-4364-9d68-2dff66eeaac5/2a747585-d759-41f6-9914-54eaddf97755/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2024-06-19_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_5.22.17.png?id=16f9e66b-e3fc-43e5-b3ec-e97646381b52&table=block&spaceId=685d04b3-8712-4364-9d68-2dff66eeaac5&expirationTimestamp=1719331200000&signature=TAdpEuVexfE3xMz7w-wnn5GyMal-WUrpVD16dfyOb7g&downloadName=%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA+2024-06-19+%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE+5.22.17.png">

이렇게 해당 데이터를 head로 옮겨 가장 최근에 사용된 값임을 명시한다. 이 데이터는 삭제 우선순위에서 멀어지게 된다.

### 2. 만약 Linked List에 없는 새로운 값이 추가된다면?

**기본적으로** 새로운 값을 추가할 때는 기존의 노드를 삭제하고 이동하는 과정이 필요 없으므로 가장 최근에 사용된 데이터를 나타내는 head에 추가하여 LRU 캐시의 상태를 유지하게 된다. 이 과정에서 tail에 있는 LRU 데이터는 제거할 필요가 없다.

<img src = "https://file.notion.so/f/f/685d04b3-8712-4364-9d68-2dff66eeaac5/8ac3cb93-f576-4def-8a4f-600ccb291a96/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2024-06-19_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_5.22.32.png?id=2b03ce49-e5af-4cbd-8d65-951a85144308&table=block&spaceId=685d04b3-8712-4364-9d68-2dff66eeaac5&expirationTimestamp=1719331200000&signature=9D_4iMd5sokCGrqfcCYN889Ys_yZYTlElBwwmwOtXb4&downloadName=%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA+2024-06-19+%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE+5.22.32.png">

하지만, **캐시 용량이 초과된다면** tail에 있는 Least Recently Used인 7을 삭제시키고 head에 새로운 데이터를 삽입하면 된다.

<img src = "https://file.notion.so/f/f/685d04b3-8712-4364-9d68-2dff66eeaac5/e03f2478-149b-49ba-8add-17b910f89d88/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2024-06-19_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_5.23.00.png?id=6fba0882-7d39-4cdf-b697-b7664427c060&table=block&spaceId=685d04b3-8712-4364-9d68-2dff66eeaac5&expirationTimestamp=1719331200000&signature=9Ds2-xis_cDSWk30eUtw7tT1J6Hf9RDalSWB7BbmAYQ&downloadName=%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA+2024-06-19+%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE+5.23.00.png">