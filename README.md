# bitable-sdk

bitable-sdk 是基于 github.com/chyroc/lark 对飞书-多维表格的开放API 做的简易封装，使用【应用身份】（即 tenant_access_token）访问/编辑多维表格资源。

详细官方文档参照：https://open.feishu.cn/document/ukTMukTMukTM/uUDN04SN0QjL1QDN/bitable-overview

# 前置步骤：
1. 在租户下[新建【企业自建应用】](https://open.feishu.cn/document/home/introduction-to-custom-app-development/self-built-application-development-process)；
2. 申请应用接口调用权限: 根据需要调用的接口文档中描述的「权限要求」到开发者后台申请应用权限；
3. 发布应用，租户管理员通过审核；
4. [添加应用为文档协作者](https://open.feishu.cn/document/ukTMukTMukTM/uczNzUjL3czM14yN3MTN#2431c595)，需要 文档所有者、知识库管理员 或 其他协作者 为资源 添加文档应用。文档、电子表格、多维表格、知识库 通过云文档 Web 页面右上方「...」->「...更多」-> 「添加文档应用」入口添加。


# 使用说明

## 初始化client
```go

import (
    bitablesdk "github.com/ag9920/bitable-sdk"
)

cli := bitablesdk.MustNewClient("cli_a253xxxxb500b", "6YKq9xxxxpZv6D")

```

## 调用开放接口

以创建一条新纪录为例：

```go

func demo() {
    ctx := context.Background()

    baseToken := "bascntXKzhxxxxxVKPRe"
    tableID := "tbl8xxxxAu"
    fields := map[string]interface{}{
        "多行文本": "test content",
    }

    record, err := cli.CreateRecord(ctx, baseToken, tableID, fields)
    if err != nil {
        fmt.Printf("createRecord failed, err=%v\n", err)
    } else {
        fmt.Printf("createRecord success, record=%+#v\n", record)
    }
}

```