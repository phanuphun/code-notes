---
title: ตั้งค่าไฟล์ .editorconfig
date: '2024/09/12'
tool: EditorConfig
img: ''
path: npmPublishPackage
draft: false
---

```shell
root = true

[*]
indent_style = space
indent_size = 3
end_of_line = lf
charset = utf-8
trim_trailing_whitespace = true
insert_final_newline = true
```

- `[]` : กำหนดประเภทไฟล์ที่จะนไปใช้
- `indent_style` : กำหนดรูปแบบการเยื้อง
- `indent_size` : ระยะการเยื้อง
- `end_of_line` : ?!
- `charset` : กำหนดรูปแบบตัวอักษร
- `trim_trailing_whitespace` : ลบช่องว่างที่ไม่จำเป็น
- `insert_final_newline` : เพิ่มบรรทัดใหม่ที่ท้ายไฟล์ทุกครั้งที่ Save