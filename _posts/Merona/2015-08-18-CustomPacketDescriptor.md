---
layout: post
title: Custom Packet Descriptor
category : Merona
---

Custom Packet Descriptor를 이용하여 패킷의 특정 필드에 대해서 선/후 처리를 할 수 있습니다.<br>
예를들어 로그인 패킷에서 password 필드는 전송되기 전에 반드시 해싱되어야 하며, 이를 서비스의 핸들러에서 처리하기보다는 Custom Packet Descriptor를 이용하여 좀 더 간결한 코드를 만들어 낼 수 있습니다.
```c#
public class Login {
  [C2S]
  public String id;
  [Sha256]
  public String password;
}
```

```c#
public class Sha256 : Packet.CustomPacketDescriptor {
  internal protected override void OnPostProcess(ref object value){
    value = SomeSha256Func(value);
  }
}
```

이렇게 생성된 Custom Packet Descriptor는 Merona 서버에서만 유효하며,
Merona.Pgen에서 이 Descriptor를 이용하기 위해서는 Emit을 사용해야 합니다.
```c#
public class Login {
  /* ... */
  [Emit("Sha256")]
  public String password;
}
```
