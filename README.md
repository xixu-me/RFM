# RFM - Rulesets for META

A comprehensive collection of optimized rulesets, maintained with a focus on reliability, frequent updates, and efficient performance. These rulesets are specifically designed to work seamlessly with [META](https://github.com/xixu-me/META).

## Why Choose These Rulesets?

### 🔄 Dual Format Support

- **MRS Format**: Optimized binary format, providing efficient performance and low memory usage
- **YAML Format**: Human-readable files for easy inspection, debugging, and modification

### 🚀 Superior Update Mechanism

- **Frequent Updates**: Rulesets are rebuilt and published **multiple times daily** (every 4 hours)
- **Automatic CDN Cache Purging**: Ensures you always get the freshest rulesets via jsDelivr

### 📊 Comprehensive Data Sources

- Aggregates data from **multiple reliable upstream sources**:
  - [Loyalsoldier/domain-list-custom](https://github.com/Loyalsoldier/domain-list-custom)
  - [v2fly/domain-list-community](https://github.com/v2fly/domain-list-community)
  - [blackmatrix7/ios_rule_script](https://github.com/blackmatrix7/ios_rule_script)
  - [felixonmars/dnsmasq-china-list](https://github.com/felixonmars/dnsmasq-china-list)
  - [crazy-max/WindowsSpyBlocker](https://github.com/crazy-max/WindowsSpyBlocker)
  - And many more...

### ✂️ Optimized Processing

- **Redundancy Removal**: Intelligent processing to eliminate redundant domain entries
- **Exclusion Lists**: Carefully maintained exclusion lists to prevent false positives
- **Efficient Domain Handling**: Special handling for different domain types (full, domain, regexp, keyword)

### 🔧 Two Ruleset Collections

- **Basic**: Essential rulesets for common usage scenarios
- **Universal**: Expanded ruleset collection with more comprehensive coverage

## Quick Start with META

The easiest way to use these rulesets is with META, which automates the entire configuration process. For usage instructions, refer to the [META Usage Guide](https://github.com/xixu-me/META?tab=readme-ov-file#usage-guide).

## Available Rulesets

### Basic Branch ([`@basic`](https://github.com/xixu-me/RFM/tree/basic))

| Ruleset | Description |
|---------|-------------|
| `fake-ip-filter.mrs` | Domains that should not be assigned fake IP mappings for connection |
| `applications.yaml` | Applications recommended for direct connection |
| `private.mrs` | Domains serving private/local networks and fulfill specific technical roles |
| `direct.mrs` | Domains recommended for direct connection |
| `proxy.mrs` | Domains recommended for proxy connection |
| `reject.mrs` | Advertisement and tracking domains for blocking |
| `gfw.mrs` | Domains in the Great Firewall blocklist |
| `tld-!cn.mrs` | Top-level domains not used in mainland China |
| `cncidr.mrs` | China IP CIDR blocks |
| `lancidr.mrs` | LAN IP CIDR blocks |
| And more... | Various provider-specific CIDR blocks |

### Universal Branch ([`@universal`](https://github.com/xixu-me/RFM/tree/universal))

Contains rulesets for specific applications/services/regions to provide more granular control.

## How It Works

This repository employs an advanced GitHub Actions workflow to:

1. **Data Collection**: Fetch domain lists from multiple authoritative sources
2. **Processing**:
   - Remove redundant and invalid domains
   - Apply exclusion lists
   - Handle different domain types appropriately
3. **Format Conversion**: Convert to both MRS (binary) and YAML formats
4. **Publishing**:
   - Push to separate branches for organization
   - Create GitHub releases
   - Purge CDN caches for immediate availability

## Use through Manual Configuration

If you prefer manual configuration, apply the rulesets to your configuration like this:

```yaml
rule-providers:
  applications:
    type: http
    interval: 14400
    format: yaml
    behavior: classical
    url: https://cdn.jsdelivr.net/gh/xixu-me/RFM@basic/applications.yaml
    path: ./rulesets/applications.yaml
  lancidr:
    type: http
    interval: 14400
    format: mrs
    behavior: ipcidr
    url: https://cdn.jsdelivr.net/gh/xixu-me/RFM@basic/lancidr.mrs
    path: ./rulesets/lancidr.mrs
  cncidr:
    type: http
    interval: 14400
    format: mrs
    behavior: ipcidr
    url: https://cdn.jsdelivr.net/gh/xixu-me/RFM@basic/cncidr.mrs
    path: ./rulesets/cncidr.mrs
  cloudflarecidr:
    type: http
    interval: 14400
    format: mrs
    behavior: ipcidr
    url: https://cdn.jsdelivr.net/gh/xixu-me/RFM@basic/cloudflarecidr.mrs
    path: ./rulesets/cloudflarecidr.mrs
  googlecidr:
    type: http
    interval: 14400
    format: mrs
    behavior: ipcidr
    url: https://cdn.jsdelivr.net/gh/xixu-me/RFM@basic/googlecidr.mrs
    path: ./rulesets/googlecidr.mrs
  telegramcidr:
    type: http
    interval: 14400
    format: mrs
    behavior: ipcidr
    url: https://cdn.jsdelivr.net/gh/xixu-me/RFM@basic/telegramcidr.mrs
    path: ./rulesets/telegramcidr.mrs
  xcidr:
    type: http
    interval: 14400
    format: mrs
    behavior: ipcidr
    url: https://cdn.jsdelivr.net/gh/xixu-me/RFM@basic/xcidr.mrs
    path: ./rulesets/xcidr.mrs
  private:
    type: http
    interval: 14400
    format: mrs
    behavior: domain
    url: https://cdn.jsdelivr.net/gh/xixu-me/RFM@basic/private.mrs
    path: ./rulesets/private.mrs
  direct:
    type: http
    interval: 14400
    format: mrs
    behavior: domain
    url: https://cdn.jsdelivr.net/gh/xixu-me/RFM@basic/direct.mrs
    path: ./rulesets/direct.mrs
  proxy:
    type: http
    interval: 14400
    format: mrs
    behavior: domain
    url: https://cdn.jsdelivr.net/gh/xixu-me/RFM@basic/proxy.mrs
    path: ./rulesets/proxy.mrs
  geolocation-cn:
    type: http
    interval: 14400
    format: mrs
    behavior: domain
    url: https://cdn.jsdelivr.net/gh/xixu-me/RFM@universal/geolocation-cn.mrs
    path: ./rulesets/geolocation-cn.mrs
  reject:
    type: http
    interval: 14400
    format: mrs
    behavior: domain
    url: https://cdn.jsdelivr.net/gh/xixu-me/RFM@basic/reject.mrs
    path: ./rulesets/reject.mrs
  win-spy:
    type: http
    interval: 14400
    format: mrs
    behavior: domain
    url: https://cdn.jsdelivr.net/gh/xixu-me/RFM@universal/win-spy.mrs
    path: ./rulesets/win-spy.mrs
  xai:
    type: http
    interval: 14400
    format: mrs
    behavior: domain
    url: https://cdn.jsdelivr.net/gh/xixu-me/RFM@universal/xai.mrs
    path: ./rulesets/xai.mrs
  openai:
    type: http
    interval: 14400
    format: mrs
    behavior: domain
    url: https://cdn.jsdelivr.net/gh/xixu-me/RFM@universal/openai.mrs
    path: ./rulesets/openai.mrs
  gemini:
    type: http
    interval: 14400
    format: mrs
    behavior: domain
    url: https://cdn.jsdelivr.net/gh/xixu-me/RFM@universal/google-gemini.mrs
    path: ./rulesets/gemini.mrs
  notebooklm:
    type: http
    interval: 14400
    format: mrs
    behavior: domain
    url: https://cdn.jsdelivr.net/gh/xixu-me/RFM@universal/google-notebooklm.mrs
    path: ./rulesets/notebooklm.mrs
  anthropic:
    type: http
    interval: 14400
    format: mrs
    behavior: domain
    url: https://cdn.jsdelivr.net/gh/xixu-me/RFM@universal/anthropic.mrs
    path: ./rulesets/anthropic.mrs
  perplexity:
    type: http
    interval: 14400
    format: mrs
    behavior: domain
    url: https://cdn.jsdelivr.net/gh/xixu-me/RFM@universal/perplexity.mrs
    path: ./rulesets/perplexity.mrs
  bilibili:
    type: http
    interval: 14400
    format: mrs
    behavior: domain
    url: https://cdn.jsdelivr.net/gh/xixu-me/RFM@universal/bilibili.mrs
    path: ./rulesets/bilibili.mrs
  youtube:
    type: http
    interval: 14400
    format: mrs
    behavior: domain
    url: https://cdn.jsdelivr.net/gh/xixu-me/RFM@universal/youtube.mrs
    path: ./rulesets/youtube.mrs
  telegram:
    type: http
    interval: 14400
    format: mrs
    behavior: domain
    url: https://cdn.jsdelivr.net/gh/xixu-me/RFM@universal/telegram.mrs
    path: ./rulesets/telegram.mrs
  x:
    type: http
    interval: 14400
    format: mrs
    behavior: domain
    url: https://cdn.jsdelivr.net/gh/xixu-me/RFM@universal/x.mrs
    path: ./rulesets/x.mrs
  binance:
    type: http
    interval: 14400
    format: mrs
    behavior: domain
    url: https://cdn.jsdelivr.net/gh/xixu-me/RFM@universal/binance.mrs
    path: ./rulesets/binance.mrs
  google:
    type: http
    interval: 14400
    format: mrs
    behavior: domain
    url: https://cdn.jsdelivr.net/gh/xixu-me/RFM@universal/google.mrs
    path: ./rulesets/google.mrs
  microsoft:
    type: http
    interval: 14400
    format: mrs
    behavior: domain
    url: https://cdn.jsdelivr.net/gh/xixu-me/RFM@universal/microsoft.mrs
    path: ./rulesets/microsoft.mrs
  xget:
    type: http
    interval: 14400
    format: mrs
    behavior: domain
    url: https://cdn.jsdelivr.net/gh/xixu-me/RFM@universal/xget.mrs
    path: ./rulesets/xget.mrs
  cloudflare:
    type: http
    interval: 14400
    format: mrs
    behavior: domain
    url: https://cdn.jsdelivr.net/gh/xixu-me/RFM@universal/cloudflare.mrs
    path: ./rulesets/cloudflare.mrs
  speedtest:
    type: http
    interval: 14400
    format: mrs
    behavior: domain
    url: https://cdn.jsdelivr.net/gh/xixu-me/RFM@universal/speedtest.mrs
    path: ./rulesets/speedtest.mrs

rules:
  - RULE-SET,applications,DIRECT
  - RULE-SET,lancidr,DIRECT,no-resolve
  - RULE-SET,private,DIRECT
  - RULE-SET,reject,Advertising
  - RULE-SET,win-spy,Advertising
  - RULE-SET,xai,xAI
  - RULE-SET,openai,OpenAI
  - RULE-SET,gemini,Gemini
  - RULE-SET,notebooklm,NotebookLM
  - RULE-SET,anthropic,Anthropic
  - RULE-SET,perplexity,Perplexity
  - RULE-SET,bilibili,bilibili
  - RULE-SET,youtube,YouTube
  - RULE-SET,telegram,Telegram
  - RULE-SET,x,X
  - RULE-SET,binance,Binance
  - RULE-SET,google,Google
  - RULE-SET,microsoft,Microsoft
  - RULE-SET,xget,Xget
  - RULE-SET,cloudflare,Cloudflare
  - RULE-SET,speedtest,Speedtest
  - RULE-SET,direct,Mainland China 🇨🇳
  - RULE-SET,proxy,PROXY
  - RULE-SET,telegramcidr,Telegram
  - RULE-SET,xcidr,X
  - RULE-SET,googlecidr,Google
  - RULE-SET,cloudflarecidr,Cloudflare
  - RULE-SET,cncidr,Mainland China 🇨🇳
  - MATCH,Others
```

## Updates and Maintenance

The rulesets are automatically updated multiple times daily, ensuring you always have the most current data. The GitHub Actions workflow runs at scheduled intervals and also triggers on pushes to the main branch.

## Disclaimer

1. This repository is strictly for educational and research purposes.
2. Use at your own risk. The repository assumes no responsibility for potential issues.
3. No guarantee of accuracy, completeness, or reliability.
4. Not liable for data loss or damages.
5. Ensure compliance with relevant licenses and legal regulations.
6. No endorsement of third-party hardware/software.
7. User modifications are their own responsibility.
8. Terms may change at any time. By using this repository, you agree to these terms.

## License

Copyright &copy; [Xi Xu](https://xi-xu.me). All rights reserved.

Licensed under the [GPL-3.0](LICENSE) license.  
