---
{"dg-publish":true,"permalink":"/技术文档/公司/sino/SONIC/常见操作/单盘/sith命令/","dg-note-properties":{}}
---

# 常见实例
## 查看eeprom中的card-label
- `sith product show eeprom card-label`
## 查看card-label
- `sith product show card-label`
## 烧写card-label
- `sith product load_card_info_json <card-label_example.json>`
- ```json
  # card-label_example.json
  {
  "FormatVersion": "01",
  "EquipmentType": "1720",
  "EquipmentPartnumber": "20.050.1736",
  "HardwareVersion": "1.0",
  "SerialNumber": "123456",
  "BootFWSWCodeNumber": "N/A",
  "CLEI": "N/A",
  "ShelfID": "N/A",
  "NEName": "N/A",
  "APSLable": "N/A",
  "MACAddress1": "N/A",
  "MACAddress2": "N/A",
  "MACAddress3": "N/A",
  "MACAddress4": "N/A",
  "MACAddress5": "N/A",
  "MACAddress6": "N/A",
  "UserLabel": "N/A"
}
  ```