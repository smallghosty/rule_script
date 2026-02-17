# 机场分流规则仓库 (Airport Routing Rules Repository)

这是一个机场分流规则仓库，包含去广告、Emby分流等规则，支持 Clash、Surge、Quantumult X 等主流代理客户端。

## 📦 功能特性

- ✅ **去广告规则** - 拦截常见广告域名，提升浏览体验
- ✅ **Emby分流规则** - 为 Emby 媒体服务器提供专用路由
- ✅ **直连规则** - 中国大陆网站和服务直接连接
- ✅ **代理规则** - 国际网站和服务通过代理访问
- ✅ **多客户端支持** - Clash、Surge、Quantumult X

## 📁 目录结构

```
.
├── lists/              # 域名列表
│   ├── ad-domains.txt      # 广告域名列表
│   ├── emby-domains.txt    # Emby域名列表
│   ├── direct-domains.txt  # 直连域名列表
│   └── proxy-domains.txt   # 代理域名列表
├── clash/              # Clash 规则文件
│   ├── ad-reject.yaml      # 广告拦截规则
│   ├── emby.yaml           # Emby分流规则
│   ├── direct.yaml         # 直连规则
│   ├── proxy.yaml          # 代理规则
│   └── config-example.yaml # 完整配置示例
├── surge/              # Surge 规则文件
│   ├── ad-reject.conf      # 广告拦截规则
│   ├── emby.conf           # Emby分流规则
│   ├── direct.conf         # 直连规则
│   └── proxy.conf          # 代理规则
└── quantumult-x/       # Quantumult X 规则文件
    ├── ad-reject.snippet   # 广告拦截规则
    ├── emby.snippet        # Emby分流规则
    ├── direct.snippet      # 直连规则
    └── proxy.snippet       # 代理规则
```

## 🚀 使用方法

### Clash

#### 方法一：使用完整配置示例

1. 下载 `clash/config-example.yaml`
2. 修改其中的代理服务器配置
3. 根据需要调整策略组和规则

#### 方法二：引用单独的规则文件

在你的 Clash 配置文件中添加规则引用：

```yaml
rules:
  # 广告拦截
  - DOMAIN-SUFFIX,ad.doubleclick.net,REJECT
  
  # Emby分流
  - DOMAIN-SUFFIX,emby.media,Emby
  
  # 更多规则请参考 clash 目录下的文件
```

#### 方法三：使用 Rule Providers（推荐）

```yaml
rule-providers:
  ad-reject:
    type: http
    behavior: domain
    url: "https://raw.githubusercontent.com/smallghosty/rule_script/main/clash/ad-reject.yaml"
    path: ./ruleset/ad-reject.yaml
    interval: 86400
    
  emby:
    type: http
    behavior: domain
    url: "https://raw.githubusercontent.com/smallghosty/rule_script/main/clash/emby.yaml"
    path: ./ruleset/emby.yaml
    interval: 86400

rules:
  - RULE-SET,ad-reject,REJECT
  - RULE-SET,emby,Emby
```

### Surge

在 Surge 配置文件的 `[Rule]` 部分添加：

```ini
[Rule]
# 引用规则文件
RULE-SET,https://raw.githubusercontent.com/smallghosty/rule_script/main/surge/ad-reject.conf,REJECT
RULE-SET,https://raw.githubusercontent.com/smallghosty/rule_script/main/surge/emby.conf,Emby
RULE-SET,https://raw.githubusercontent.com/smallghosty/rule_script/main/surge/direct.conf,DIRECT
RULE-SET,https://raw.githubusercontent.com/smallghosty/rule_script/main/surge/proxy.conf,PROXY
```

### Quantumult X

在 Quantumult X 配置文件的 `[filter_remote]` 部分添加：

```ini
[filter_remote]
https://raw.githubusercontent.com/smallghosty/rule_script/main/quantumult-x/ad-reject.snippet, tag=广告拦截, enabled=true
https://raw.githubusercontent.com/smallghosty/rule_script/main/quantumult-x/emby.snippet, tag=Emby分流, enabled=true
https://raw.githubusercontent.com/smallghosty/rule_script/main/quantumult-x/direct.snippet, tag=国内直连, enabled=true
https://raw.githubusercontent.com/smallghosty/rule_script/main/quantumult-x/proxy.snippet, tag=国际代理, enabled=true
```

## 📝 自定义规则

### 添加自定义 Emby 服务器

如果你使用私有 Emby 服务器，可以在相应的规则文件中添加你的域名：

**Clash:**
```yaml
- DOMAIN-SUFFIX,your-emby-server.com,Emby
- DOMAIN,emby.example.com,Emby
```

**Surge:**
```ini
DOMAIN-SUFFIX,your-emby-server.com,Emby
DOMAIN,emby.example.com,Emby
```

**Quantumult X:**
```ini
HOST-SUFFIX,your-emby-server.com,Emby
HOST,emby.example.com,Emby
```

### 添加自定义广告域名

将需要拦截的广告域名添加到 `lists/ad-domains.txt`，然后在相应客户端的规则文件中添加拦截规则。

## 🔄 更新说明

规则会不定期更新，建议：

1. **Clash**: 使用 Rule Providers 功能，配置自动更新间隔
2. **Surge**: 使用 RULE-SET 引用在线规则，Surge 会自动更新
3. **Quantumult X**: 使用 filter_remote，定期手动更新或配置自动更新

## ⚠️ 注意事项

1. 使用前请先备份原有配置
2. 某些规则可能需要根据实际情况调整
3. Emby 规则仅包含官方域名和示例，请根据实际使用的服务器添加
4. 广告拦截规则可能影响某些网站的正常功能，如遇问题请适当调整
5. 建议定期更新规则以获得最佳效果

## 📊 规则统计

- **广告域名**: 60+ 条
- **Emby域名**: 10+ 条
- **直连域名**: 80+ 条
- **代理域名**: 70+ 条

## 🤝 贡献

欢迎提交 Issue 和 Pull Request 来完善规则！

## 📄 许可证

本项目采用 MIT 许可证

## 🔗 相关链接

- [Clash](https://github.com/Dreamacro/clash)
- [Surge](https://nssurge.com/)
- [Quantumult X](https://quantumult.app/)
- [Emby](https://emby.media/)

## 📮 反馈

如有问题或建议，请提交 Issue 或通过其他方式联系。

---

**最后更新时间**: 2026-02-17