# HarmonyOS 银行 App Scheme、BundleName 与 AbilityName

本文整理了 16 家银行 HarmonyOS App 的 `scheme`、`bundleName` 和主入口
`abilityName`。数据来自已安装应用的 Bundle 元数据。

> 采集日期：2026-07-24  
> 说明：银行 App 更新后可能修改 Bundle、Ability 或 URI 声明。接入前应在目标
> 版本上重新执行本文的采集方法，并进行真机验证。

## 汇总

“推荐 URI”优先选择该 App 主入口 Ability 明确注册、且最适合用
`url_launcher` 做安装检测和拉起的 URI。标注“需验证业务参数”的 URI 虽然符合
当前 Bundle 声明，但 App 可能仍要求额外路径或查询参数。

| 银行 | 样本版本 | bundleName | 入口 module / abilityName | queryScheme | 推荐 URI |
| --- | --- | --- | --- | --- | --- |
| 中国建设银行 | 9.4.0 | `com.ccb.mobilebank.hm` | `main` / `CcbMainAbility` | `ccbapp` | `ccbapp://` |
| 中国银行 | 9.9.31 | `com.boc.bocsoft.mbs.personal` | `app` / `AppAbility` | `bocmbciphone` | `bocmbciphone://h5/detail` |
| 招商银行 | 14.3.0 | `com.cmbchina.harmony` | `app` / `EntryAbility` | `cmbmobilebank` | `cmbmobilebank://` |
| 中信银行 | 12.2.1 | `cn.citicbank.wap` | `phone` / `EntryAbility` | `citicbank` | `citicbank://` |
| 中国民生银行 | 10.4 | `cn.com.cmbc.ohmbank` | `entry` / `EntryAbility` | `cmbc` | `cmbc://center.mbank` |
| 中国工商银行 | 11.1.0.6.0 | `com.icbc.harmonyclient` | `entry` / `EntryAbility` | `com.icbc.harmonyclient` | `com.icbc.harmonyclient://` |
| 中国农业银行 | 11.2.0 | `com.bankabc.openharmonyapp.release` | `entry` / `MainAbility` | `bankabc` | `bankabc://` |
| 邮储银行 | 11.6.1 | `com.psbc.mbank.hm` | `phone` / `EntryAbility` | `psbc` | `psbc://` |
| 交通银行 | 10.4.0 | `com.bankcomm.mobshos` | `entry` / `EntryAbility` | `bocom` | `bocom://` |
| 兴业银行 | 6.0.59 | `com.cib.cibmbhmos` | `main` / `MainAbility` | `cibmb` | `cibmb://jumpurl` |
| 中国光大银行 | 13.0.7 | `com.cebbank.mobile.cembhmwork` | `entry` / `EntryAbility` | `cebbank` | `cebbank://mobile` |
| 平安银行 | 8.7.0 | `com.pingan.bank.pocket` | `entry` / `EntryAbility` | `paesuperbank` | `paesuperbank://` |
| 华夏银行 | 7.0.7 | `com.hxb.mobile.hm` | `entry` / `EntryAbility` | `hxbmb` | `hxbmb://mb5` |
| 北京银行 | 10.0.4 | `com.bankofbeijing.hmobilebanking` | `entry` / `EntryAbility` | `bankofbj` | `bankofbj://95526.mobi` |
| 广发银行 | 11.6.0 | `com.cgbchina.xpt.hm` | `entry` / `EntryAbility` | `cgb` | `cgb://lua/openxml` |
| 上海银行 | 10.1.4 | `cn.com.shbank.mperhm` | `entry` / `EntryAbility` | `bankofshanghai` | `bankofshanghai://` |

## URI 明细

以下 URI 来自 Ability 的 `skills[].uris[]`，空 scheme 声明已省略。同一个 scheme
带有 host、port 或 path 时，调用方不能只根据 scheme 名称假定裸 `scheme://`
一定能匹配。推送、埋点等非业务入口会明确标注。

### 中国建设银行

- `ccbapp://`
- `mbspay://`
- `ccbapp://ccblink`
- `ccbapp://outlink`
- `ccbapp://ca`
- `mbspay://netbank`
- `ccbmbswqf://xwzf`
- `com.ccb.ccbdemo://CCBCallCenter`

### 中国银行

- `bocmbciphone://h5`
- `bocmbciphone://h5/detail`
- `bocmbankpsn://startwith`
- `bocpay://third/unionpay`
- `bocmobile://www.boc.cn/mobile`

### 招商银行

- `cmbmobilebank://`
- `qqopenapi://100744418`，且 path 需匹配 `auth` 或 `share`

### 中信银行

- `citicbank://`
- `citicbankopen://thirdpay:8899`

### 中国民生银行

- `cmbc://center.mbank`
- `cmbc://cmbc.push.mbank/detail`（推送落地页）
- `rangersapplog.70460e77c39e4e25://rangersapplog/picker`（埋点内部链路）

### 中国工商银行

- `com.icbc.harmonyclient://`
- `upcppLily://`
- `uppayx16://`

### 中国农业银行

- `bankabc://`
- `uppaybankabc://`
- 另有资源引用形式 `$string:WXAPI_APP_ID`，它不是可直接写入调用方
  `querySchemes` 的实际 scheme 值。

### 邮储银行

- `psbc://`
- `uppayx53://`
- `uppayyouchu://`
- `psbccreditmerge://`
- `ybpsbc://`
- `sa2494a80b://popupwindow`

### 交通银行

- `bocom://`
- `upcppMadder://`

### 兴业银行

- `cibmb://jumpurl`

### 中国光大银行

- `cebbank://mobile`

### 平安银行

- `paesuperbank://`
- `paesuperbankcep://`
- `unionpaysdk://`

### 华夏银行

- `hxbmb://mb5`
- `uppayx25://`
- `uppayhuaxia://`

此外还注册了 `mpaasscheme://com.mpaas.harmony.push/longlink` 和
`jump://com.mpaas.harmony.push/landing`，分别路由到 `MpaasNcAbility` 和
`PushLandingAbility`，属于推送内部链路，不建议用于普通安装检测或拉起。

### 北京银行

- `bankofbj://95526.mobi`

### 广发银行

- `cgb://lua/openxml`
- `uppayx4://`
- `uppayguangfa://`

此外还注册了 `mpaasscheme://com.mpaas.harmony.push/longlink`，路由到
`MpaasNcAbility`，属于推送内部链路。

### 上海银行

- `bankofshanghai://`
- `BankOfShangHai://`
- `mobile://BankOfShanghai.com`
- `upcppCherry://uppay`
- `rangersapplog.d8951e878da95b72://rangersapplog/picker`（埋点内部链路）
- `rangersapplog.7550426b0769e6f5://rangersapplog/picker`（埋点内部链路）
- `mpaasscheme://com.mpaas.harmony.push/longlink`（推送内部链路，路由到
  `MpaasNcAbility`）

上述埋点、推送内部 scheme 不建议用于普通安装检测或拉起。

## 调用方配置

HarmonyOS 的 `bundleManager.canOpenLink()` 要求调用方先在
`entry/src/main/module.json5` 的 `querySchemes` 中声明待查询的 scheme。这里只写
scheme 头，不写 `://`、host、path 或参数。

```json5
{
  "module": {
    "querySchemes": [
      "ccbapp",
      "bocmbciphone",
      "cmbmobilebank",
      "citicbank",
      "cmbc",
      "com.icbc.harmonyclient",
      "bankabc",
      "psbc",
      "bocom",
      "cibmb",
      "cebbank",
      "paesuperbank",
      "hxbmb",
      "bankofbj",
      "cgb",
      "bankofshanghai"
    ]
  }
}
```

Flutter 调用示例：

```dart
final uri = Uri.parse('ccbapp://');
if (await canLaunchUrl(uri)) {
  await launchUrl(uri, mode: LaunchMode.externalApplication);
}
```

不建议仅凭 `bundleName` 加硬编码 `abilityName` 启动银行 App。不同银行的入口可能
是 `EntryAbility`、`MainAbility`、`AppAbility` 或自定义名称，而且后续版本可能
变化。对于已经公开 URI Skill 的 App，优先让系统根据完整 URI 路由。

## 数据获取方法

### 1. 连接设备

确保设备已开启开发者模式并能被 HDC 识别：

```bash
hdc list targets
```

不要把该命令输出的设备序列号提交到公开文档、Issue 或日志中。

### 2. 根据应用标签定位 bundleName

```bash
hdc shell bm dump -a -l
```

输出中包含应用标签与 Bundle 的对应关系，例如：

```json
{
  "bundleName": "com.example.bank",
  "label": "示例银行"
}
```

应同时核对 `applicationInfo.organization`，避免把同名、测试版或仿冒应用纳入
结果。

### 3. 读取指定 Bundle 元数据

```bash
hdc shell bm dump -n com.example.bank
```

关键字段：

| 目标数据 | Bundle 元数据字段 |
| --- | --- |
| Bundle 名称 | `applicationInfo.bundleName` |
| 开发者组织 | `applicationInfo.organization` |
| 入口模块 | `entryModuleName` |
| 主入口 Ability | `hapModuleInfos[].mainAbility` / `mainElementName` |
| URI 路由 Ability | `hapModuleInfos[].abilityInfos[].name` |
| URI 声明 | `abilityInfos[].skills[].uris[]` |

### 4. 使用 jq 提取核心数据

`bm dump -n` 的第一行是 Bundle 标题，后续才是 JSON，因此示例先用
`tail -n +2` 去掉第一行：

```bash
hdc shell bm dump -n com.example.bank \
  | tail -n +2 \
  | jq '{
      bundleName: .applicationInfo.bundleName,
      organization: .applicationInfo.organization,
      versionName,
      entryModuleName,
      modules: [
        .hapModuleInfos[]
        | select(.mainAbility != "" or (.abilityInfos | length) > 0)
        | {
            moduleName,
            mainAbility,
            mainElementName,
            abilities: [
              .abilityInfos[]
              | {
                  name,
                  skills
                }
            ]
          }
      ]
    }'
```

解析 `skills[].uris[]` 时应组合以下字段，而不是只复制 `scheme`：

- `scheme`
- `host`
- `port`
- `path`
- `pathStartWith`
- `pathRegex`

例如元数据为 `scheme: "bank"`、`host: "open"`、`path: "home"` 时，候选
URI 应写为 `bank://open/home`，并继续根据 `pathStartWith` 或 `pathRegex` 补足
匹配内容。

## 限制与安全说明

- 本文只能证明这些 URI 在对应样本版本的 Bundle 元数据中有声明，不代表银行
  官方承诺其长期兼容。
- `canLaunchUrl()` 返回 `true` 只能证明系统中存在匹配的 URI Skill，不代表任意
  业务参数都能被银行 App 接受。
- 支付、推送、埋点和第三方 SDK scheme 可能要求签名、来源校验或特定参数，不应
  当作普通首页拉起 URI。
