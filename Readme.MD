# DH.Payment - 多网关支付SDK库

[![publish](https://github.com/PeiKeSmart/DH.Payment/actions/workflows/publish.yml/badge.svg)](https://github.com/PeiKeSmart/DH.Payment/actions/workflows/publish.yml)
[![publish-beta](https://github.com/PeiKeSmart/DH.Payment/actions/workflows/publish-beta.yml/badge.svg)](https://github.com/PeiKeSmart/DH.Payment/actions/workflows/publish-beta.svg)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![NuGet](https://img.shields.io/nuget/v/DH.Payment.Alipay.svg)](https://www.nuget.org/packages/DH.Payment.Alipay)

基于 **DH框架** 的多网关支付SDK库，提供统一、简洁的支付接入体验。参考了 [essensoft/payment](https://github.com/essensoft/payment) 的设计思路，在此基础上进行了重构和增强。

## ✨ 功能特性

- **多网关支持**：集成支付宝、微信支付、QQ支付、京东支付、连连支付、银联支付等主流支付渠道
- **统一接口**：一致的 API 设计，降低多网关集成复杂度
- **通知处理**：内置支付结果通知的解析与验证
- **请求/响应模型**：强类型请求响应，减少手动拼装报文的出错率
- **现代 .NET**：支持 .NET 9.0 / .NET 10.0，使用最新 C# 语法

## 📦 包含的类库

| 类库 | 说明 | NuGet |
|------|------|-------|
| `DH.Payment.Alipay` | 支付宝支付类库 | [![NuGet](https://img.shields.io/nuget/v/DH.Payment.Alipay)](https://www.nuget.org/packages/DH.Payment.Alipay) |
| `DH.Payment.WeChatPay` | 微信支付类库 | [![NuGet](https://img.shields.io/nuget/v/DH.Payment.WeChatPay)](https://www.nuget.org/packages/DH.Payment.WeChatPay) |
| `DH.Payment.QPay` | QQ支付类库 | [![NuGet](https://img.shields.io/nuget/v/DH.Payment.QPay)](https://www.nuget.org/packages/DH.Payment.QPay) |
| `DH.Payment.JDPay` | 京东支付类库 | [![NuGet](https://img.shields.io/nuget/v/DH.Payment.JDPay)](https://www.nuget.org/packages/DH.Payment.JDPay) |
| `DH.Payment.LianLianPay` | 连连支付类库 | [![NuGet](https://img.shields.io/nuget/v/DH.Payment.LianLianPay)](https://www.nuget.org/packages/DH.Payment.LianLianPay) |
| `DH.Payment.UnionPay` | 银联支付类库 | [![NuGet](https://img.shields.io/nuget/v/DH.Payment.UnionPay)](https://www.nuget.org/packages/DH.Payment.UnionPay) |

## 🚀 快速开始

### 安装

通过 NuGet 安装所需的支付类库：

```bash
dotnet add package DH.Payment.Alipay
dotnet add package DH.Payment.WeChatPay
```

### 配置

在 `Startup.cs` 或 `Program.cs` 中注册服务：

```csharp
// 注册支付宝支付
builder.Services.AddAlipay(options =>
{
    options.AppId = "您的AppId";
    options.PrivateKey = "您的应用私钥";
    options.AlipayPublicKey = "支付宝公钥";
});

// 注册微信支付
builder.Services.AddWeChatPay(options =>
{
    options.AppId = "您的AppId";
    options.MchId = "商户号";
    options.Key = "API密钥";
});
```

### 使用

```csharp
public class PaymentController : ControllerBase
{
    private readonly IAlipayClient _alipayClient;

    public PaymentController(IAlipayClient alipayClient)
    {
        _alipayClient = alipayClient;
    }

    /// <summary>发起支付宝电脑网站支付</summary>
    public async Task<IActionResult> PagePay()
    {
        var request = new AlipayTradePagePayRequest
        {
            Body = new AlipayTradePagePayModel
            {
                OutTradeNo = "订单号",
                Subject = "商品标题",
                TotalAmount = "0.01",
                ProductCode = "FAST_INSTANT_TRADE_PAY"
            }
        };
        var response = await _alipayClient.PageExecuteAsync(request);
        return Content(response.Body, "text/html");
    }
}
```

## 🏗 项目结构

```
DH.Payment/
├── DH.Payment.Alipay/       # 支付宝支付
├── DH.Payment.WeChatPay/    # 微信支付
├── DH.Payment.QPay/         # QQ支付
├── DH.Payment.JDPay/        # 京东支付
├── DH.Payment.LianLianPay/  # 连连支付
├── DH.Payment.UnionPay/     # 银联支付
├── Doc/                     # 文档与资源
└── Readme.MD                # 本文件
```

## 🔗 相关链接

- [DH 框架](https://www.haocoding.com/)
- [PeiKeSmart 组织](https://github.com/PeiKeSmart)
- [NuGet 包](https://www.nuget.org/profiles/PeiKeSmart)

## 📄 许可证

本项目基于 [MIT](LICENSE) 许可证开源。

Copyright © 2020-2026 湖北登灏科技有限公司