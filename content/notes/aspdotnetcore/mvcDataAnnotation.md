---
title: การใช้ Data Annotation เพื่อกำหนดคุณสมบัติของข้อมูลในการใช้งาน
date: 2024/10/24
tool: ASPDotNetCore
tag: Basic
img: ""
path: mvcDataAnnotation
---
| Key | Purpose |
| -------- | ------- |
|`[Key]` |  กำหนด Primary Key|
|`[Required]`|ใช้ในการกำหนดให้ฟิลด์ข้อมูลต้องมีค่า (ไม่สามารถเป็นค่าว่าง) เมื่อตรวจสอบความถูกต้อง|
|`[DisplayName]`|กำหนดชื่อที่อ่านง่ายสำหรับฟิลด์ข้อมูล|
|`[Range]`|กำหนดขอบเขตของค่าที่สามารถป้อนเข้าไปในฟิลด์|
|`[DisplayFormat]`|กำหนดรูปแบบการแสดงผลของค่าที่เก็บในฟิลด์ เช่น วันที่, จำนวนเงิน|
|`[MaxLength]`|กำหนดความยาวสูงสุดของค่าที่สามารถเก็บในฟิลด์ที่เป็นชนิดข้อมูลสตริง ช่วยป้องกันไม่ให้ข้อมูลเกินขนาดที่กำหนดในฐานข้อมูล|
| `[StringLength]` | กำหนดความยาวขั้นต่ำ/สูงสุดของข้อมูลชนิด string |
| `[RegularExpression]`| ตรวจสอบข้อมูลตามรูปแบบที่กำหนดโดยใช้ Regular Expression |
| `[EmailAddress]`| ตรวจสอบให้แน่ใจว่าข้อมูลที่ป้อนเป็นอีเมลที่ถูกต้องตามรูปแบบ |
| `[Phone]`| ตรวจสอบว่าข้อมูลที่ป้อนเป็นหมายเลขโทรศัพท์ที่ถูกต้องตามมาตรฐาน |
