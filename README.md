# A buildin V2ray plugin for SSRPanel

Only one thing user should do is that setting up the database connection, without doing that user needn't do anything!

### Features

- Sync user from SSRPanel database to v2ray
- Log user traffic

### Benefits

- No other requirements
  - It's  able to run if you could launch v2ray core
- Less memory usage
  - It just takes about 5MB to 10MB memories more than v2ray core
  - Small RAM VPS would be joyful
- Simplicity configuration

### Install on Linux

you may want to see docs, all the things as same as the official docs except install command.

[V2ray installation](https://www.v2ray.com/en/welcome/install.html)

```
curl -L -s https://raw.githubusercontent.com/lovelyou/v2ray-ssrpanel-plugin/master/install-release.sh | sudo bash
```

#### Uninstall

```
curl -L -s https://raw.githubusercontent.com/ColetteContreras/v2ray-ssrpanel-plugin/master/uninstall.sh | sudo bash
```

### V2ray Configuration demo

```
{
  "log": {
    "loglevel": "debug"
  },
  "api": {
    "tag": "api",
    "services": [
      "HandlerService",
      "LoggerService",
      "StatsService"
    ]
  },
  "stats": {},
  "inbounds": [
    {
      "port": 10087,
      "protocol": "vmess",
      "streamSettings": {
        "network": "ws",
        "wsSettings": {
        "path": "/btfly"
        }
      },
      "tag": "proxy"
    },
    {
      "listen": "127.0.0.1",
      "port": 10550,
      "protocol": "dokodemo-door",
      "settings": {
        "address": "127.0.0.1"
      },
      "tag": "api"
    }
  ],
  "outbounds": [
    {
      "protocol": "freedom"
    }
  ],
  "routing": {
    "rules": [
      {
        "type": "field",
        "inboundTag": [
          "api"
        ],
        "outboundTag": "api"
      }
    ],
    "strategy": "rules"
  },
  "policy": {
    "levels": {
      "0": {
        "statsUserUplink": true,
        "statsUserDownlink": true
      }
    },
    "system": {
      "statsInboundUplink": true,
      "statsInboundDownlink": true
    }
  },
  "ssrpanel": {
    "nodeId": 33,
    "checkRate": 60,
    "user": {
      "inboundTag": "proxy",
      "level": 0,
      "alterId": 16,
      "security": "none"
    },
    "mysql": {
      "host": "",
      "port": ,
      "user": "",
      "password": "",
      "dbname": ""
    }
  }
}
```

### Contributing

Read [WiKi](https://github.com/ColetteContreras/v2ray-ssrpanel-plugin/wiki) carefully before submitting issues.

- Test and [report bugs](https://github.com/ColetteContreras/v2ray-ssrpanel-plugin/issues)
- Share your needs/experiences in [github issues](https://github.com/ColetteContreras/v2ray-ssrpanel-plugin/issues)
- Enhance documentation
- Contribute code by sending PR

### References

- [V2ray](https://github.com/v2ray/v2ray-core)
- [SSRPanel](https://github.com/ssrpanel/SSRPanel)
