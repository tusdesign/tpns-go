# tpns-server-sdk/gosdk
## 概述
[腾讯移动推送](https://cloud.tencent.com/product/tpns) 是腾讯云提供的一款支持**百亿级**消息的移动App推送平台，开发者可以调用golang SDK访问腾讯移动推送服务。

## 依赖配置
1. 当前需要配置go依赖环境变量避免校验问题: `GOPRIVATE=git.code.tencent.com`

## 使用说明
1. 接口和参数，可以参看[官网](https://cloud.tencent.com/document/product/548/39060) ，注意，本代码只支持推送接口。

2. 全量推送
   ```
   package main
   import (
       "fmt"
       tpns "git.code.tencent.com/tpns/tpns-server-sdk/gosdk"
   )
   
   func main() {
       //var aps = tpns.DefaultIOSAps()
       //aps.Alert = "hello, world"
       //var ios = tpns.IOSMessage {
       //    Aps: aps,
       //}
       req := tpns.NewRequest(
           tpns.WithAudience(tpns.AudienceAll),
           tpns.WithMessageType(tpns.Notify),
           tpns.WithTitle("this is title"),
           tpns.WithContent("this is content"),
           tpns.WithEnvironment(tpns.Develop),
       )
  
       //@params: host, accessId, secretkey
       client := tpns.NewClient(tpns.GuangzhouHost, 10086, "abc")
       resp, err := client.Do(req)
       fmt.Printf("resp: %+v, err: %v\n", resp, err)
   }
   ```

3. 单设备推送
   ```
   package main
   import (
       "fmt"
       tpns "git.code.tencent.com/tpns/tpns-server-sdk/gosdk"
   )
     
   func main() {
       //var aps = tpns.DefaultIOSAps()
       //aps.Alert = "hello, world"
       //var ios = tpns.IOSMessage {
       //    Aps: aps,
       //}
       req := tpns.NewRequest(
           tpns.WithAudience(tpns.AudienceToken),
           tpns.WithTokenList([]string{"token1"}),
           tpns.WithMessageType(tpns.Notify),
           tpns.WithTitle("this is title"),
           tpns.WithContent("this is content"),
           tpns.WithEnvironment(tpns.Develop),
       )
    
       //@params: host, accessId, secretkey
       client := tpns.NewClient(tpns.GuangzhouHost, 10086, "abc")
       resp, err := client.Do(req)
       fmt.Printf("resp: %+v, err: %v\n", resp, err)
   }
   ```
4. 设备列表推送
   ```
   package main
   import (
       "fmt"
       tpns "git.code.tencent.com/tpns/tpns-server-sdk/gosdk"
   )
     
   func main() {
       //var aps = tpns.DefaultIOSAps()
       //aps.Alert = "hello, world"
       //var ios = tpns.IOSMessage {
       //    Aps: aps,
       //}
       req := tpns.NewRequest(
           tpns.WithAudience(tpns.AudienceTokenList),
           tpns.WithTokenList([]string{"token1", "token2"}),
           tpns.WithMessageType(tpns.Notify),
           tpns.WithTitle("this is title"),
           tpns.WithContent("this is content"),
           tpns.WithEnvironment(tpns.Develop),
       )
    
       //@params: host, accessId, secretkey
       client := tpns.NewClient(tpns.GuangzhouHost, 10086, "abc")
       resp, err := client.Do(req)
       fmt.Printf("resp: %+v, err: %v\n", resp, err)
   }
   ```

5. 单账号推送
   ```
   package main
   import (
       "fmt"
       tpns "git.code.tencent.com/tpns/tpns-server-sdk/gosdk"
   )
     
   func main() {
       //var aps = tpns.DefaultIOSAps()
       //aps.Alert = "hello, world"
       //var ios = tpns.IOSMessage {
       //    Aps: aps,
       //}
       req := tpns.NewRequest(
           tpns.WithAudience(tpns.AudienceAccount),
           tpns.WithAccountList([]string{"acc1"}),
           tpns.WithMessageType(tpns.Notify),
           tpns.WithTitle("this is title"),
           tpns.WithContent("this is content"),
           tpns.WithEnvironment(tpns.Develop),
       )
    
       //@params: host, accessId, secretkey
       client := tpns.NewClient(tpns.GuangzhouHost, 10086, "abc")
       resp, err := client.Do(req)
       fmt.Printf("resp: %+v, err: %v\n", resp, err)
   }
   ```
   
6. 账号列表推送
   ```
   package main
   import (
       "fmt"
       tpns "git.code.tencent.com/tpns/tpns-server-sdk/gosdk"
   )
     
   func main() {
       //var aps = tpns.DefaultIOSAps()
       //aps.Alert = "hello, world"
       //var ios = tpns.IOSMessage {
       //    Aps: aps,
       //}
       req := tpns.NewRequest(
           tpns.WithAudience(tpns.AudienceAccountList),
           tpns.WithAccountList([]string{"acc1", "acc2"}),
           tpns.WithMessageType(tpns.Notify),
           tpns.WithTitle("this is title"),
           tpns.WithContent("this is content"),
           tpns.WithEnvironment(tpns.Develop),
       )
    
       //@params: host, accessId, secretkey
       client := tpns.NewClient(tpns.GuangzhouHost, 10086, "abc")
       resp, err := client.Do(req)
       fmt.Printf("resp: %+v, err: %v\n", resp, err)
   }
   ```
   
7. 标签推送
   ```
   package main
   import (
       "fmt"
       tpns "git.code.tencent.com/tpns/tpns-server-sdk/gosdk"
   )

   func main() {
       //var aps = tpns.DefaultIOSAps()
       //aps.Alert = "hello, world"
       //var ios = tpns.IOSMessage {
       //    Aps: aps,
       //}
       var tagItem = tpns.TagItem {
           Tags: []string{"guangdong", "hunan"},
           TagsOperator: tpns.TagOperationOr,
           ItemsOperator: tpns.TagOperationOr,
           TagType: "xg_auto_province",
       }
       var tagRule = tpns.TagRule {
           TagItems: []tpns.TagItem{tagItem},
           Operator: tpns.TagOperationOr,
       }
       req := tpns.NewRequest(
           tpns.WithAudience(tpns.AudienceTag),
           tpns.WithTagRules([]tpns.TagRule{tagRule}),
           tpns.WithMessageType(tpns.Notify),
           tpns.WithTitle("this is title"),
           tpns.WithContent("this is content"),
           tpns.WithEnvironment(tpns.Develop),
       )

       //@params: host, accessId, secretkey
       client := tpns.NewClient(tpns.GuangzhouHost, 10086, "abc")
       resp, err := client.Do(req)
       fmt.Printf("resp: %+v, err: %v\n", resp, err)
   }
   ```
8. 号码包推送
   ```
   package main
   import (
       "fmt"
       "time"
       tpns "git.code.tencent.com/tpns/tpns-server-sdk/gosdk"
   )
     
   func main() {
       //@params: host, accessId, secretkey
       client := tpns.NewClient(tpns.GuangzhouHost, 10086, "abc")
       uploadResp, err := client.Upload("file.txt", 10 * time.Second)
       if err != nil || uploadResp.RetCode != 0 {
           fmt.Printf("upload response: %v, err: %v\n", uploadResp, err)
           return
       }
       //var aps = tpns.DefaultIOSAps()
       //aps.Alert = "hello, world"
       //var ios = tpns.IOSMessage {
       //    Aps: aps,
       //}
       req := tpns.NewRequest(
           tpns.WithAudience(tpns.AudienceAccountPackage),
           tpns.WithUploadId(uploadResp.UploadId),
           tpns.WithMessageType(tpns.Notify),
           tpns.WithTitle("this is title"),
           tpns.WithContent("this is content"),
           tpns.WithEnvironment(tpns.Develop),
       )
    
       resp, err := client.Do(req)
       fmt.Printf("resp: %+v, err: %v\n", resp, err)
   }
   ```
9. token 文件包推送
   ```
   package main
   import (
       "fmt"
       "time"
       tpns "git.code.tencent.com/tpns/tpns-server-sdk/gosdk"
   )
     
   func main() {
       //@params: host, accessId, secretkey
       client := tpns.NewClient(tpns.GuangzhouHost, 10086, "abc")
       uploadResp, err := client.Upload("file.txt", 10 * time.Second)
       if err != nil || uploadResp.RetCode != 0 {
           fmt.Printf("upload response: %v, err: %v\n", uploadResp, err)
           return
       }
       //var aps = tpns.DefaultIOSAps()
       //aps.Alert = "hello, world"
       //var ios = tpns.IOSMessage {
       //    Aps: aps,
       //}
       req := tpns.NewRequest(
           tpns.WithAudience(tpns.AudienceTokenPackage),
           tpns.WithUploadId(uploadResp.UploadId),
           tpns.WithMessageType(tpns.Notify),
           tpns.WithTitle("this is title"),
           tpns.WithContent("this is content"),
           tpns.WithEnvironment(tpns.Develop),
       )
    
       resp, err := client.Do(req)
       fmt.Printf("resp: %+v, err: %v\n", resp, err)
   }
   ```
10. 其它
   可以具体参看官网文档，填充Request结构体，然后调用Client发起请求。代码也提供了通过With.XXX方式来填充Request结构体
