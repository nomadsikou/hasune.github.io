---
title: Map형 확장for문 메모
category: Java
comments: true
order: 5
---

Map형 오브젝트도 확장포문에 돌리는게 가능했었구나...

```java
for(Map.Entry<String, String> entry : map.entrySet()) {
    System.out.println(entry.getKey());
    System.out.println(entry.getValue());
}
```

확장 for문에서 제일 많이 쓰이는 유형은
```java
for (String s : data) {
    System.out.println(s);
}
```
혹은 이거
```java
List<Integer> nums = new ArrayList<Integer>();
for (int num = 0; num < 5; num++ ) {
    nums.add(num);
}
for (int num : nums) {
    System.out.println("num = " + num);
}

```

- 두번째꺼 빼고는 자주 까먹을것 같아서 메모를.. ㅋㅋ
