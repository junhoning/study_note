# [Algorithm] ListNode

# Concept

Value인 숫자 값이 그 다음 값과 그 다음 값과 연결하기 위함

왜 굳이 List로 한번에 담지 않고, 하나하나씩 연결해서 번거롭게 하는지 의문이 갈 수 있음

예로 하나하나에 데이터가 동영상이나 고화질의 이미지 같은 경우 한번에 모든 데이터를 열어놓으면 Memory를 너무 많이 잡아먹을 수 있습니다. 

마치 식당에서 밥 먹을 때 반찬의 위치가 어딨는지만 알면 밥 먹을 땐 자기 앞의 그릇으로 옮겨서 먹으면 되고, 욕심내서 한번에 다 담으려고 하면 넘쳐버리는 문제를 해결하는 것과 같습니다. 

그럼 하나의 데이터를 받으면 그 값 안에는 메모리 안에 그 다음 값의 위치만 들어있습니다. 

아래를 그림으로 예로 들어보겠습니다. 

![](Untitled-3e6710c2-5c99-4533-8d2c-3e81959d51e1.png)

## 예시

    class ListNode(object):
        def __init__(self, x):
            self.val = x
            self.next = None

제일 먼저 첫번째 Node를 만드는 방법은 ListNode에 담아주는 것입니다. 

    node_1 = ListNode(12)

그럼 node_1에 ListNode가 담깁니다. 해당 Node에 val에는 12가 담기고, next에는 빈 None이 담깁니다. 

    node_2 = ListNode(99)
    node_3 = ListNode(37)

추가적으로 ListNode를 더 만들도록 하겠습니다. 이 때까지는 각 ListNode만 만들어졌을 뿐 서로 연결이 되지 않았습니다. 

각 새로운 Node에 val만 넣었을 뿐이죠. 

    node_1.next = node_2

node_1의 next를 node_2로 정의 해주었습니다. 이젠 node 1과 node 2와 연결이 되었습니다. 

node_1을의 val을 열면 첫번째 value인 12가 나오고, `node_1.next`는 node_2의 경로로 이동합니다. 

중요한 것은 `cur_node = node_1.next` 와 같이 정의 해주지 않으면 이동하진 않습니다. 

마치 다음 방으로 들어가진 않고 문을 열어서 확인만 하는 거죠. 

    >>> print(node_1.next.val)
    
    99 # node_1이 아닌 node_2의 val인 99 

> 방이 하나 있습니다. 이 방은 방 하나하나가 하나씩 다음 방으로 연결이 되어있고, 첫번째 방에서 문을 열면 그 다음 방으로 갈 수 있습니다. 첫번째 방을 열어서 val을 통해 확인 할 수 있고, 그 다음 방을 확인 하려면 `node.next`로 넘어갈 수 있습니다. 하지만 `node = node.next` 로 옮기기 전까진 문을 열어봤을 뿐 현재 경로가 이동된 건 아닙니다.

# LinkedNode를 만들어보자

    for i, v in enumerate([1, 4, 5]):
        if i == 0:
            head = cur = ListNode(v)  # 첫 Node는 head에 따로 저장
        else:
            cur.next = ListNode(v)  # 현재 Node의 next에 그 다음 연결할 Node를 담는다
            cur = cur.next  # 다음 Node를 현재 경로로 지정

    >>> head.val  # 맨 처음에 Node를 따로 저장했기 때문에 Node는 맨처음으로 가있는다
    1

    >>> head.next.val
    4

    >>> head.next.next.val
    5

### Head의 역할

- leetcode 제출용으로 첫 Node로 돌아가는 방법

왜 `head = cur = ListNode(v)`로 만들었는지 의아할 수 있다. head는 남기고 cur로 계속 다음 Node들을 담다보면 계속 next로 이동이 될 것이다. 하지만 next는 있지 돌아가는 방법은 맨 처음 LIstNode를 호출하는 건데. 계속 `cur = cur.next` 식으로 덮어버리면 head로 밖에 돌아가는 방법이 없다. 

## LinkedNode를 새로 만들고 들여다보는 방법

첫번째 Node를 열어서 그 다음 Node로 이동하는 걸 보자 

    node = head
    
    while node:  # 마지막 Node의 next는 None이기 때문에 끝나면 자동으로 while이 끝남
        val = node.val  # 현재 Node의 val 확인
        print(val)
        
        node = node.next  # 다음 경로로 이동

## LinkdedNode에서 얻은 값을 연산하여 새로운 LinkedNode에 담기

    node = head
    
    i = 0
    
    while node:
    		# 기존 Node에서 하나의 Val 씩 꺼내기
        val = node.val  # Node의 val 확인
        node = node.next  # 다음 Node로 이동
    
    		# 연산     
        new_val = val * 2  # 현재 Node에서 얻은 val을 2를 곱하여 new_val로 저장
        
    
    		# 새로운 Node에 저장하는 과정
        if i==0:
            new_head = new_node = ListNode(new_val)  # 처음 만들 때만 new_head를 만듦
        else:
            new_node.next = ListNode(new_val)  # 두번째 Node부터 new_head 없이 new_val을 저장 
            new_node= new_node.next
        
        i += 1  # 첫번째 Node가 아닌 것을 표시

밑의 코드를 다시 실행하면 Node의 결과 확인이 가능하다

    node = new_head
    
    while node:
        val = node.val
        print(val)
        
        node = node.next

    # 출력결과
    2
    8
    10