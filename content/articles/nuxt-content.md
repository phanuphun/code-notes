---
title: บันทึก Nuxt Content
date: '2024/09/12'
description: Nuxt Content เป็นโมดูลของ Nuxt.js ที่ช่วยให้คุณสามารถจัดการและแสดงเนื้อหาต่างๆ ในเว็บไซต์หรือแอปพลิเคชัน โดยใช้ไฟล์ Markdown (.md), JSON, YAML, หรือ CSV ได้อย่างง่ายดาย โดยไม่จำเป็นต้องมีฐานข้อมูลหลังบ้าน (backend database) ซึ่งเหมาะสำหรับการทำเว็บบล็อก, เอกสาร, หรือเว็บไซต์ที่เน้นเนื้อหา
tags: ['Nuxt' , 'Nuxt Content']
thumbnail: 'https://miro.medium.com/v2/resize:fit:864/1*H-hII9inrBamchRCz8EWaw.png' 
path: "nuxt-content"
draft: true 
---

### โครงสร้างไฟล์
- content โฟลเดอร์สำหรับจัดเก็บไฟล์ .md .json .yaml ในการเขียน content
- page โฟลเดอร์ที่ใช้ในการจัดการ Rounting ต่างๆใน Nuxt 
    - ในโฟลเดอร์นี้จะต้องมีไฟล์ `[...slug.vue]`เพื่อใช้ในการดึงเนื้อหาต่างๆในโฟลเดอร์ Content มาแสดง

### ContentList
### ContentDoc 

### Markdown style ไม่แสดง
1. ติดตั้งปลั๊กอิน typography ของ Tailwind `npm install @tailwindcss/typography`
2. เพิ่มปลั๊กอินลงในไฟล์ `tailwind.config.js`
```js
export default {
  content: [],
  theme: {
    extend: {},
  },
  plugins: [
    require('@tailwindcss/typography'),
  ],
}
```
3. เรียกใช้ Class `prose` ที่ส่วนแสดงผลไฟล์ markdown
```js
    <ContentRenderer :value="doc" class="prose max-w-full"></ContentRenderer>
```
::Card
#note-text
ปัญหานี้เกิดจากตัว Tailwind ไม่ได้ให้ style พื้นฐานสำหรับแท็ก Html มาพอนำ Markdown มา Render เป็น Html จึงทำให้ไม่มีสไตล์แล้วกลายเป็น Plain text ธรรมดาๆ
::