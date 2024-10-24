---
title: บันทึกการใช้งาน Nuxt Content ในการทำเว็บบล็อค ในรูปแบบ Git-base CMS
date: '2024/09/12'
description:
tag: Note
tags: ['Nuxt' , 'Nuxt Module' , 'Vue' , 'CMS']
img: /img/nuxtContent/cover2.png
path: basicNuxtContent
draft: false
---

---
## เบื้องต้น

Nuxt Content คือ Module ที่ใน Framework Nuxt.js ที่ช่วยให้พัฒนาแอปพลิเคชันที่มีเนื้อหาแบบ dynamic โดยใช้ไฟล์ Markdown,JSON,YAML หรือ CSV เป็นแหล่งเก็บข้อมูล ซึ่งข้อมูลเหล่านี้ไม่จำเป็นต้องพึ่งพาฐานข้อมูลแบบดัง ทำให้การพัฒนาเว็บไซต์ที่เน้นเนื้อหามีความสะดวกและยืดหยุ่น

### โครงสร้างไฟล์สำคัญ

อย่างแรกที่เราจะต้องทำความรู้จักเลยนั่นก็คือ Directory Structure หรือโครงสร้างโฟลเดอร์และไฟล์ต่างๆในการจัดระบบไฟล์ ดังนี้

1. **📁 โฟลเดอร์ content** : เป็น directory ที่ระบุเอาไว้ใน Nuxt.js document เพื่อใช้ในการสรางระบบจัดการเนื้อหา(File-base CMS) โดยที่ Nuxt Content จะอ่านโฟลเดอร์ **content/** ในโปรเจ็คเราและทำารแยกไฟล์ .md , .yml , .csv และ .json เพื่อใช้ในการสร้าง File-base CMS
2. **📁 โฟลเดอร์ pages** : เป็น directory ที่ใช้ในการสร้างหน้าต่างๆสำหรับการกำหนด rounting ต่างๆของ Nuxt.js อยู่แล้ว โดยที่ใช่โฟลเดอร์ **pages/** เราจะสร้างไฟล์ `[...path].vue` ซึ่งเป็นหน้าที่ใช้แสดงเนื้อหาต่างๆของเรา โดยจะรับ parameter เข้ามาภายในวงเล็บสี่เหลี่ยม เพื่อใช้ในการทำ Dynamic Routes ที่จะมีการเปลี่ยนแปลงตลอดตามไฟล์เอกสารที่เราจะเลือกดูเนื้อหา โดยที่
   -  `[...]` กำหนดว่าเส้นทางที่เราจะไปสามารถเข้าถึงไฟล์ที่มีหลายระดับชั้นหรือหลายโฟลเดอร์ซ้อนอยู่ได้ทั้งหมด เช่น
   -  `path` จะเป็นค่า parameter ที่จะมีการเปลี่ยนแปลงตลอดเช่น phanuphun.com/article/pathName

### เครื่องมือที่ใช้งาน

1. **Nuxt Content** : ใช้ในการจัดการเนื้อหาในรูปแบบ File-base CMS
2. **Tailwind CSS** : ใช้ในการจัดเนื้อหาและตกแต่งควาสวยงาม
   -  **Tailwind Typography** : เป็น Plugin เสริมของทาง Tailwind ที่จะช่วยให้เราไม่ต้องเขียนแท็ก HTML สำหรับการแสดงผล Markdown เอง

<ref-box>
เนื่องจากการแสดงผล Markdown จำเป็นต้องผ่านการแปลงมาเป็นแท็ก HTML ก่อน และเราจำเป็นต้องเขียน CSS ในการให้กับแท็กเหล่านั้นเอง ซึ่งเป็นเรื่องยุ่งยากมากๆ เราจึงต้องลง Plugin เสริมของ tailwind อย่าง `@tailwindcss/typography` ที่มีการกำหนด Style มาให้กับเราอย่างครบครัน
</ref-box>

---
## Markdown

เป็นไฟล์เอกสารเนื้อหาที่เราจำนำมาแสดงบนเว็บไซต์โดยมีนามสกุลเป็น .md โดยที่ในการเขียน Markdown Language จะมีสิ่งที่เรียกว่า **Front matter** ที่เป็นบล็อคข้อมูลในการกำหนด **MetaData** ของบทความนั้นๆของเราไม่ว่าจะเป็น ชื่อเรื่อง ผู้เขียน วันที่สร้าง คำสำคัญ รูปภาพ หรือแม้กระทั่งในการทำ SEO เราก็สามารถกำหนด Page Title หรือ Meta Description ได้อย่างง่ายด่ายผ่านตรงนี้ ทั้งนี้รูปแบบของ Front Matter ก็ไม่ได้เฉพาะเจาะจง เราสามารถปรับแต่งได้เองเช่นกัน

**ตัวอย่างการกำหนด Fron Matter ในไฟล์ Markdown**

```ts
---
title: ทำเว็บบล็อคด้วย Nuxt Content
description: ....
date: '2024/09/12'
tags: ['nuxt' , 'nuxt content' ,'vue' ]
img:
path: "nuxt-content"
---
```

<ref-box>
 <b>Native parameter</b> เป็นค่าที่ Nuxt Content รองรับและสามารถนำไปใช้ใน SEO หรือแสดงผลในส่วนต่างๆ ของหน้าเว็บ<a class="text-blue-400 hover:text-blue-600" href="https://content.nuxt.com/usage/markdown#front-matter"> เอกสาร 📄 </a>
</ref-box>

### การเพิ่ม Markdown Style

อย่างที่กล่าวไปก่อนหน้านี้ว่าเราจะใช้ `@tailwindcss/typography` เพื่อเพิ่ม style ต่างๆให้กับแท็ก HTML ที่ผ่านการ Render มาจากแท็กของไฟล์ Markdown

1. ติดตั้งปลั๊กอิน **@tailwindcss/typography**

```shell
npm install @tailwindcss/typography
```

2. เพิ่มปลั๊กอินลงในไฟล์ **tailwind.config.js**

```ts
export default {
   content: [],
   theme: {
      extend: {},
   },
   plugins: [require("@tailwindcss/typography")],
};
```

3. จากนั้นเรียกใช้ class `prose` ในส่วนที่เราต้องการแสดงผล markdown

```vue
<template>
   <ContentRenderer :value="doc" class="prose max-w-full"></ContentRenderer>
</template>
```

### การตกแต่งเนื้อหาด้วย Compoenent

เราสามารถตกแต่งเนื้อหาของบทความของเราให้แตกต่างออกไปจากรูปแบบเดิมๆที่ Markdown Language สามารถทำได้ โดยเราสามารถ Import Component ที่เราสร้างขึ้นมาเองเพื่อใช้ในตกแต่งบทความของเราได้ตามใจชอบ

**สิ่งสำคัญ** ในการจะเรียกใช้ Component เลยนั่นก็คือ Nuxt Content จะสามารถเรียกใช้ Component ที่อยู่ในโฟลเดอร์ `/components/content/` ได้เท่านั้น นั่นหมายความว่า หาก Component ที่เราจะใช้อยู่นอกเหนือจากนี้ Component ที่เรียกใช้ในไฟล์ .md จะไม่แสดงผลหรือไม่ทำงาน แสดงว่าเราจำเป็นต้องสร้างโฟลเดอร์ **content** ขึ้นมาในโฟลเดอร์ **components** เพื่อให้ Nuxt สามารถสร้าง route ได้ถูกต้อง

-  การใช้งานเบื้องต้นกรณีที่ไม่ได้กำหนดอะไรมากมายมีเพียง slot ธรรมดาๆที่เป็น default เราสามารส่งเนื้อหาเข้าไปได้เลย
```md
::CompontentName
เนื้อหาที่เพิ่มลงไปภายใน component
::
```

-  ในกรณีที่มีการกำหนด slot แยกออกมาต่างหากหรือมีมากกว่าหนึ่ง slot โดยมีการกำหนด name ให้กับ slot เช่นในตัวอย่างมีการกำหนด slot อยู่ 2 ตัวก็คือ note-header กับ note-text โดยเมื่อเราต้องการจะใช้ slot ตรงส่วนไหนของ Component ที่เรากำหนด ก็เพียงใช prefix **#** แล้วตามด้วยชื่อของ slot นั้นๆ ตามตัวอย่างด้านล่าง เพื่อเป็นการกำหนด slot ที่เราต้องการจะใช้งาน

```md
::ComponentName
#note-header
หัวข้อที่จะใช้ slot note-header
#note-text
เนื้อหาคำอธิบายที่จะใช้ใน slot note-text
::
```

- ทั้งนี้ทั้งนั้นเราสามารถเปิดแท็ก component ที่เราเรียกใช้ใน template ได้เหมือนปกติเช่นกันในกรณีที่ component ของเรามีการรับค่า props เข้าไปเพื่อปรับแต่ง ก็สามารถเปิดแท็กได้ตามปกติเลยโดยไม่ต้องใช้เหมือนข้างต้น **เพียงแต่ว่าอาจเกิดปัญหาในเรื่องที่ props ที่เราตั้งชื่อเองบางชื่ออาจไม่ทำงาน**

### การปรับแต่ง Markdown Style

ในเมื่อเราสามารถแสดงผล Markdown style ได้จาก `@tailwindcss/typography` แล้ว แน่นอนว่าย่อมมีบางแท็กที่เรายังไม่ชอบ เราจึงต้องมีการปรับแต่งเองเพิ่มเติมบ้าง ให้เราไปที่ **tailwind.config.js** จะเห็นว่าเราสามารถปรับแต่ง plugin ได้โดยการไปที่ **theme** → **extend** → **pluginName** → **typography(theme) => ({})**

-  จะเห็นได้ว่าตรง `typography` เราใช้เป็น callback function ซึ่งจริงๆเราไม่จำเป็นต้องทำแบบนี้ก็ได้โดยเราใช้เป็น Object ปกติได้เลย **การที่เราใช้เป็น callback funtion ก็เพื่อเราจะ function** **theme** **เข้ามาเพื่อใช้ค่าสีที่มาจาก class ต่างๆที่เราใช้ในการกำหนด propsValue ให้กับ props นั้นๆนั่นเอง** ต่างกันเพียงเล็กน้อยเท่านั้นจากที่เราใช้ `-` ก็เปลี่ยนมาใช้ `.` แทน
-  ส่วนการกำหนด props ที่เป็นคุณสมบัตินั้นจะเห็นได้ว่าการกำหนดค่าที่นี่ใช้แบบ Camel Case แทน
-  `DEFAULT` ตรงนี้จะเป็นการกำหนด css theme mode เริ่มต้นนั่นเอง
-  `invert` เป็น theme mode ที่ **@tailwindcss/typography** ใช้แทน dark mode นั่นก็หมายความว่าหากมีการเปลี่ยนโหมดก็สามารถมาที่ตรงนี้ได้

```js
/** @type {import('tailwindcss').Config} */
export default {
   content: ["./src/**/*.{html,js,ts,vue}"],
   theme: {
      extend: {
         typography: (theme) => ({
            DEFAULT: {
               css: {
                  code: {
                     backgroundColor: theme("colors.gray.200"),
                     color: theme("colors.black"),
                     padding: "0.2em 0.4em",
                     borderRadius: "0.25rem",
                     fontWeight: "600",
                  },
               },
            },
            invert: {
               css: {
                  code: {
                     backgroundColor: `#1E242A`,
                     color: theme("colors.white"),
                  },
               },
            },
         }),
      },
   },
   plugins: [require("@tailwindcss/typography")],
};
```

---

## Composables

### การดึงเนื้อหาเอกสารด้วย queryContent

`queryContent()` เป็น composable ที่ช่วยในการดึงข้อมูลของไฟล์หนึ่งไฟล์ออกมา จากตัวอย่างการใช้งานนี้ผมจะระบุ path เพื่อดึงเนื้อหาไฟล์เอกสารที่ชื่อว่า **nuxt.md** ซึ่งอยู่ในโฟลเดอร์ **/articles** จากตัวอย่างจะเห็นได้ว่าเราทำเพียงแค่ระบุโฟลเดอร์ **/articles** ได้เลย เนื่องจากตัว Nuxt Content จะมองหาไฟล์เอกสารของเราที่ **/content** อยู่แล้ว และไม่จำเป็นที่เราต้องระบุนามสกุล .md ไปด้วย สามารถใช้ชื่อของไฟล์ตรงๆได้เลย ไม่อย่างนั้นจะหาไฟล์ไม่เจอแม้จะมีอยู่จริงก็ตาม เมื่อเราได้ข้อมูลของไฟล์เอกสารมาแล้วเราก็สามารถใช้ component `ContentRenderer` ในการแสดงผลข้อมูลในไฟล์ออกมาแสดงที่หน้าเว็บได้เเล้ว

```vue
<script setup lang="ts">
const { data } = await useAsyncData("article", () =>
   queryContent("/articles/nuxt").findOne()
);
</script>
```

### การเพิ่มเงื่อนไขใน Query

-  `where` : การจะ Query ข้อมูลแบบมีเงื่อนไขเราสามารถใช้ where ในการหาไฟล์ที่เฉพาะเจาะจงได้ โดยการใช้ where นั้นจะใช้รูปแบบไวยากรณ์ของ Mongo
-  `sort` : เป็นการจัดเรียงข้อมูลโดยจะมีค่า  **1**  ที่หมายถึงเรียงจากน้อยไปมาก และ  **-1**  เรียงจากมากไปน้อย
-  `limit` : การจำกัดเนื้อหาข้อมูล โดยส่งค่าเป็นตัวเลขได้เลย
-  `skip` : เป็นการข้ามข้อมูล โดยส่งค่าเป็นตัวเลขได้เลยเหมือนกับ limit

<ref-box>
เอกสารรูปแบบไวยากรณ์ของ  <a class="text-blue-400 hover:text-blue-600" href="https://www.mongodb.com/docs/manual/reference/operator/query/">  MongoDB 📄</a>
</ref-box>


---

## Component

### การดึงเนื้อหาในเอกสารด้วย ContentDoc

`<ContentDoc>` เป็น component ที่ใช้ในการดึงข้อมูลเนื้อหาไฟล์ใน directory จะเห็นได้ว่ามีความคล้ายกับ **queryContent()** แต่มีความต่างกันตรงที่ **ContentDoc** จะใช้ใน template ไม่ใช่ script

-  **path** : กำหนด path directory ในการดึงไฟล์
-  **v-slot** : ใช้เพื่อดึงข้อมูลเนื้อหารายการออกมา โดย `doc` เป็น slot prop ที่ใช้ในการแสดงเนื้อหาใน template

```vue
<template>
   <ContentDoc :path="`/articles/${fileName}`" v-slot="{ doc }">
      <pre> {{ doc }} </pre>
   </ContentDoc>
</template>
```

### การดึงรายการเนื้อหาด้วย ContentList

`<ContentList>` เป็น component ที่ใช้ในการดึงและแสดงไฟล์เอกสารออกมา สามารถระบุ attribute ที่เฉพาะเจาะจงได้ในการดึงรายการไฟล์ใน directory

-  **path** : กำหนด path directory ในการดึงไฟล์ในโฟลเดอร์นั้นๆ
-  **field** : กำหนด field ที่เรากำหนด front matter ในไฟล์ **.md** มา เช่น title , description หรือ tags(ที่เรากำหนดเอง)
-  **query** : ใช้เงื่อนไขในการกำหนด
-  **v-slot** : ใช้เพื่อดึงข้อมูลเนื้อหารายการออกมา โดย `list` เป็น slot prop ที่ใช้ในการแสดงเนื้อหาใน template

```vue
<script setup lang="ts">
const queryParams = {
   sort: [{ date: -1 }],
};
</script>

<template>
   <ContentList
      :path="`/articles`"
      fields="title,path"
      :query="queryParams"
      v-slot="{ list }"
   >
      <pre> {{ list }} </pre>
   </ContentList>
</template>
```

### การแสดงผลเนื้อหาด้วย ContentRenderer

`<ContentRenderer>` เป็น component ที่ใช้ในการแสดงผลไฟล์ **.md** โดยเราสามารถใช้งานร่วมกับ **ContentDoc** หรือ **queryContent** ก็ได้

1. การใช้งานร่วมกับ conposable `queryContent()`

```vue
<script setup lang="ts">
const { data } = await useAsyncData("home", () => queryContent("/").findOne());
</script>

<template>
   <ContentRenderer :value="data">
      <h1>{{ data.title }}</h1>
   </ContentRenderer>
</template>
```

2. การใช้งานร่วมกับ component `ContentDoc`

```vue
<template>
   <ContentDoc :path="`/articles/${path}`" v-slot="{ doc }">
      <ContentRenderer>
         <h1>{{ doc.title }}</h1>
      </ContentRenderer>
   </ContentDoc>
</template>
```

---

## เพิ่มเติม

### การทำ Search

โดยการทำค้นหาจะใช้การ query ด้วย `where` ในการกำหนดเงื่อนไข จากโค้ดด้านล่างนี้ผมจะใช้ตัวแปร **search** ไปผูกกับ input จากนั้นสร้างตัวแปร **searchParams** ขึ้นมาจากนั้นใช้ **computed** ในการคำนวณการค้นหาที่เปลี่ยนแปลงตลอดเวลาที่เราพิมพ์ในช่องค้นหา จากนั้นจะคืนค่ากลับมาที่ตัวแปร searchParams เพื่อให้เรานำไปใช้ต่อ ซึ่งเราสามารถนำไปใช้กัย component **ContentDoc** หรือ composable **queryContent()** ได้ทั้งคู่เลยเพื่อใช้ในการแสดงผลข้อมูล

**เพิ่มเติมการใช้ where**

-  `$or` เป็นตัวเปรียบเทียบทางตรรกศาสตร์ของ Mongo ซึ่งก็คือ **หรือ** ในเชิงตรรกศาสตร์นั่นแหละ ในที่นี้จะใช้การเปรียบเทียบฟีลด์อยู่ 2 ฟีลด์ก็คือ title กับ description ไม่ว่าการค้นหาที่เราพิมพ์ไปจะตรงกับส่วนไหนในเอกสารใดๆก็ตามให้คืนค่ากลับมาทั้งหมดที่มีส่วนเหมือนกับที่เราพิมพ์
-  `$regex` เป็นคำสั่งของ Regular Expression เพื่อทำการค้นหาข้อความที่ครงกับรูปแบบที่เรากำหนด ในกรณีนี้ก็คือ หาข้อความจากฟีลด์ title และ description ว่ามีข้อความไหนตรงกับตัวแปร search ของเราหรือไม่ โดยเราจะเพิ่ม option เข้าไปนั่นก็คือ **i (case-insensitive)** ซึ่งจะไม่สนว่าเป็นตัวอักษรพิมพ์ใหญ่พิมพ์เล็ก

```js
<script setup lang="ts">
   const search = ref<string>('')
   const searchParams = computed(() => ({
      where: [
         {
            $or: [
               { title: { $regex: new RegExp(search.value, 'i') } },
               { description: { $regex: new RegExp(search.value, 'i') } }
            ]
         }
      ]
   }))
</script>
```

### การทำ Table of contents

Table of content(TOC) เป็นการทำสารบัญจากแท็ก **h2** และ **h3** เพื่อง่ายต่อการเลือกดูเนื้อหาโดยแยกตามหัวข้อที่แปลงมาเป็นแท็ก html

1. ดึงเนื้อหาไฟล์เอกสารออกมาด้วย **queryContent()** หรือ **ContentDoc** ในที่นี้จะเลือกใช้ `queryContent()`

```ts
<script setup lang="ts">
   const { data } = await useAsyncData('home', () => queryContent(`/articles/${path}`).findOne())
   const tocData = data.value?.body?.toc?.links
</script>
```

2.การนำไปใช้งาน โดยเราจะนำ `link.id` ซึ่งก็คือ id ของหัวข้อนั้นๆ ที่เราจะนำไปใช้ ในแท็ก **a** เพื่อใช้เลื่อนไปตามหัวข้อของบทความของเรา โดยจะใช้ฟังก์ชัน `encodeURIComponent` ซึ่งเป็น Javascript Built-in Fucntion เพื่อถอดรหัสข้อมูลที่เกิดจากความผิดพลาดจากช่องว่างของ space bar ที่จะถูกแทนที่ด้วยอักขระพิเศษ เช่น # % หรือ ? จึงทำให้ path ของเนื้อหาบทความของเราผิดเพี้ยนไป

---

## อ้างอิง

<ref-box>
https://content.nuxt.com/get-started/installation
https://github.com/nuxt/content/discussions/1343
https://github.com/tailwindlabs/tailwindcss-typography#customizing-the-css
https://nuxt.com/docs/getting-started/introduction
https://tailwindcss.com/docs/configuration
https://www.mongodb.com/docs/manual/reference/operator/query/
</ref-box>
