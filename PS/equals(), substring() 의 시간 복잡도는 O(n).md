# [level 1] 햄버거 만들기 - 133502

[문제 링크](https://github.com/sohn919/Algorithm/tree/main/%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%A8%B8%EC%8A%A4/unrated/133502.%E2%80%85%ED%96%84%EB%B2%84%EA%B1%B0%E2%80%85%EB%A7%8C%EB%93%A4%EA%B8%B0)


### 틀린 코드 (시간 초과) 

```
class Solution {
    public int solution(int[] ingredient) {
        final String BURGER = "1231";
        int answer = 0;
        String str = "";
        if(ingredient.length < 4) return answer;
        for(int i=0; i<3; i++) str += ingredient[i];
        for(int i=3; i<ingredient.length; i++) {
            str += ingredient[i];
            if(str.length() >= 4 && ingredient[i] == 1) {
                if(str.substring(str.length() - 4, str.length()).equals(BURGER)) {
                    str = str.substring(0, str.length() - 4);
                    answer++;
                }
            }
        }
        return answer;
    }
}
```

### 정답 코드
```
import java.util.Stack;
class Solution {
    public int solution(int[] ingredient) {
        Stack<Integer> stack = new Stack<>();
        int answer = 0;
        if(ingredient.length < 4) return answer;
        for(int i=0; i<ingredient.length; i++) {
            stack.push(ingredient[i]);
            if(stack.size() >= 4) {
                if(stack.get(stack.size() - 1) == 1
                        && stack.get(stack.size() - 2) == 3
                        && stack.get(stack.size() - 3) == 2
                        && stack.get(stack.size() - 4) == 1) {
                    answer++;
                    for(int j=0; j<4; j++) stack.pop();
                }
            }
        }
        return answer;
    }
}
```

### 오답 정리
```
if(str.substring(str.length() - 4, str.length()).equals(BURGER)) {
    str = str.substring(0, str.length() - 4);
    answer++;
}
```
- 이 코드에서 equals() 가 O(n) 의 시간 복잡도를 가지며 여기에서는 `final String BURGER = "1231";` 와 같이 BURGER 변수의 길이 만큼 검사한다.
- 또한 substring() 도 O(n) 의 시간 복잡도를 가지며 그로 인해 `str` 의 변수의 길이 만큼 시간이 더해져 시간 초과가 생긴다.