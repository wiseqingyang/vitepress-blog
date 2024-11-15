---
title: Docs with VitePress
editLink: true
---
> [!important]TODO
>
> 所有 App Linking 唤起失败需要重新测试是否能跳转后二次唤起


## iOS 测试结果
 链接\方法 | a.href | iframe.src | a.click() | window.open | location.href | location.replace 
 -- | :--: | :--: | :--: | :--: | :--: | :--: 
  DeepLink | ✅ | ❌(无反应) | ✅ | ✅ | ✅  | ✅
 AppLinking | ✅ | ❌(无反应) | ✅ | ✅ | ✅  | ✅

 > [!TIP] 
 > APP Linking 拒绝后，会一直失败，手动从APP Linking 按钮唤起后 恢复正常跳转

## Android vivo android15 测试结果
 链接\方法 | a.href | iframe.src | a.click() | window.open | location.href | location.replace 
 -- | :--: | :--: | :--: | :--: |:--: | :--: 
  DeepLink | ✅ | ✅ | ✅ | ✅（会打开新标签） | ✅  | ✅
 AppLinking | ❌ | ❌ | ❌ | ❌ | ❌  | ❌

 ## Android samsung android9 测试结果
 链接\方法 | a.href | iframe.src | a.click() | window.open | location.href | location.replace 
 -- | :--: | :--: | :--: | :--: | :--: | :--: 
  DeepLink | ✅ | ✅  | ✅ | ✅（会打开新标签） | ✅  | ✅
 AppLinking | ❌ | ❌ | ❌ | ❌ | ❌  | ❌

 ## Harmony Next 测试结果

  链接\方法 | a.href | iframe.src | a.click() | window.open | location.href | location.replace 
 -- | :--: | :--: |:--: | :--: | :--: | :--: 
  DeepLink | ✅ | ✅ |  ✅ | ✅（新窗口） | ✅  | ✅
 AppLinking | ✅ | ❌（无反应） | ✅ | ✅（新窗口） | ✅  | ✅（跳转成功且留在APPLink页面）

 > [!TIP]
 > harmony APPLinking 跳转前无提示 直接跳转
 > 
 > deepLink 每次都会二次确认。在普通webview中会报网络异常然后白屏