# qingping-tlv

Qingping（青萍）设备 TLV 协议的编码/解码实现，供 Home Assistant 的 qingping 集成引用。

纯 Python，无第三方依赖。

## 安装

```bash
pip install git+https://github.com/<你的用户名>/qingping-tlv.git@v0.1.0
```

## 用法

### 解码（设备上报数据）

```python
from qingping_tlv import tlv_decode, tlv_unpack

# 整包（以 0x4347 "CG" 开头）
data = tlv_unpack(bytes.fromhex("4347..."))
# 单个 TLV 数据块
sensors = tlv_decode(b"\x01\x04\x00\xa2\x0c")
# {"temperature": 20.5, ...}
```

### 编码（下发命令）

```python
from qingping_tlv import (
    build_config_command,
    build_led_switch_command,
    build_request_settings_command,
)

cmd = build_config_command(...)  # 采集间隔等配置
led = build_led_switch_command(True)
req = build_request_settings_command()
# 通过 BLE write 发给设备
```
