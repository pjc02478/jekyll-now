---
layout: post
title: Pgen Emit
category : Merona
---

Emit은 입력받은 문자열 그대로를 패킷 빌드 타임에 다시 출력하는 역할을 합니다,<br>
이 기능을 이용해서 Merona 서버 에서 추가한 Packet.CustomDescriptor를 Pgen에서 출력하도록 할 수 있습니다.
<br><br>
Emit을 적용할 필드 위에 Emit 속성을 작성하고, 첫 번째 인자로 출력할 문자열을 입력합니다.

```c#
public class TestPacket {
  [C2S]
  [Emit("MyCustomAttribute(123, 456)")]
  public String name;
}
```

패킷이 빌드 될 때 Emit 필드의 내용이 대괄호[] 사이에 그대로 삽입된 채로 출력됩니다.<br>
(Emit 필드는 빌드 타겟이 Csharp으로 지정되었을 때만 유효합니다.)

```c#
public class TestPacket {
  public class C2S {
    [MyCustomAttribute(123, 456)]
    public String name;
  }
}
```
