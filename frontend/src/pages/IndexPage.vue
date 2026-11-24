<template>
  <q-page padding>
    <div class="text-h4 q-mb-md"> Version Control + Docker Demo (Quasar) </div>

    <q-card class="q-mb-md">
      <q-card-section>
        <div class="text-h6">Git Workflow (ตัวอย่างขั้นตอนทำงาน)</div>
        <q-list bordered separator class="q-mt-sm">
          <q-item v-for="(step, index) in gitSteps" :key="index">
            <q-item-section avatar>
              <q-badge>{{ index + 1 }}</q-badge>
            </q-item-section>
            <q-item-section>
              <q-item-label>{{ step.title }}</q-item-label>
              <q-item-label caption>{{ step.detail }}</q-item-label>
            </q-item-section>
          </q-item>
        </q-list>
      </q-card-section>
    </q-card>

    <q-card class="q-mb-md">
      <q-card-section>
        <div class="text-h6">Docker Concepts (สรุปสั้น ๆ)</div>
        <q-list bordered separator class="q-mt-sm">
          <q-item v-for="(item, index) in dockerItems" :key="index">
            <q-item-section>
              <q-item-label>{{ item.title }}</q-item-label>
              <q-item-label caption>{{ item.detail }}</q-item-label>
            </q-item-section>
          </q-item>
        </q-list>
      </q-card-section>
    </q-card>

    <!-- Docker Quick Reference (การบ้าน Lab 1.1) -->
    <q-card>
      <q-card-section>
        <div class="text-h6">Docker Quick Reference (สรุปคำสั่งใช้งานบ่อย)</div>
        <div class="text-caption text-grey-7 q-mb-sm">
          คำสั่ง Docker และ Docker Compose พร้อมคำอธิบายการใช้งานภาษาไทย
        </div>
        <q-list bordered separator class="q-mt-sm">
          <q-item v-for="(cmd, index) in dockerQuickRef" :key="index">
            <q-item-section avatar>
              <q-badge color="secondary" text-color="white">{{
                index + 1
              }}</q-badge>
            </q-item-section>
            <q-item-section>
              <q-item-label
                class="text-weight-bold text-primary"
                style="font-family: monospace"
              >
                {{ cmd.command }}
              </q-item-label>
              <q-item-label caption class="q-mt-xs">
                <strong>ใช้เมื่อ:</strong> {{ cmd.usage }}
              </q-item-label>
            </q-item-section>
          </q-item>
        </q-list>
      </q-card-section>
    </q-card>
  </q-page>
</template>

<script setup>
const gitSteps = [
  {
    title: 'แก้โค้ด Quasar ใน src/',
    detail: 'เพิ่มหน้า / component ใหม่ เช่น IndexPage.vue, Layout ต่าง ๆ'
  },
  {
    title: 'ตรวจสอบสถานะไฟล์',
    detail: 'ใช้คำสั่ง `git status` ดูว่าไฟล์ไหนเปลี่ยนแปลงบ้าง'
  },
  {
    title: 'เพิ่มไฟล์เข้า staging',
    detail: 'จากรากโปรเจกต์ ใช้ git add frontend/src/pages/IndexPage.vue'
  },
  {
    title: 'สร้าง commit พร้อมข้อความแบบ Conventional Commits',
    detail: 'เช่น `feat: add Git workflow demo page`'
  },
  {
    title: 'push ขึ้น GitHub',
    detail: 'ใช้ git push -u origin feature/quasar-demo แล้วเปิด Pull Request'
  }
]

const dockerItems = [
  {
    title: 'Image',
    detail:
      'แพ็กเกจที่มีไฟล์และการตั้งค่าที่ใช้สร้าง container เช่น image ที่รวม Quasar SPA กับ Nginx'
  },
  {
    title: 'Container',
    detail: 'อินสแตนซ์ที่สร้างจาก image เช่น container ที่รัน Nginx เพื่อเสิร์ฟไฟล์ Quasar'
  },
  {
    title: 'Volume',
    detail: 'เก็บข้อมูลให้คงอยู่แยกจากวงจรชีวิตของ container เช่น ไฟล์อัปโหลดของ backend'
  },
  {
    title: 'Network',
    detail: 'ให้บริการใน Docker ติดต่อกันได้ เช่น Nginx ส่งต่อคำขอไปยัง Express'
  }
]

// การบ้าน Lab 1.1: เพิ่มการ์ด Docker Quick Reference อย่างน้อย 4 คำสั่ง พร้อมคำอธิบายภาษาไทย
const dockerQuickRef = [
  {
    command: 'docker build -t <image-name> -f <Dockerfile> <context>',
    usage:
      'ใช้เมื่อต้องการสร้าง Docker Image จาก Dockerfile เพื่อเตรียมนำไปรันเป็น container เช่น การสร้าง Quasar SPA image'
  },
  {
    command:
      'docker run -d -p <host-port>:<container-port> --name <name> <image>',
    usage:
      'ใช้เมื่อต้องการสร้างและรัน container ในเบื้องหลัง (Background/Detached mode) พร้อม map port ระหว่างเครื่องโฮสต์กับ container'
  },
  {
    command: 'docker stop <container> && docker rm <container>',
    usage:
      'ใช้เมื่อต้องการหยุดการทำงานของ container และลบออกจากระบบเพื่อคืนพอร์ตและทรัพยากร ก่อนสร้างหรือรันใหม่'
  },
  {
    command: 'docker compose up -d --build',
    usage:
      'ใช้เมื่อต้องการสั่ง build images ใหม่และเริ่มต้นรันทุก services ที่ระบุใน docker-compose.yml พร้อมกันในโหมดเบื้องหลัง'
  },
  {
    command: 'docker compose ps',
    usage:
      'ใช้เมื่อต้องการตรวจสอบสถานะการทำงาน พอร์ต และความพร้อมของ services ทั้งหมดที่จัดการผ่าน Docker Compose'
  },
  {
    command: 'docker compose down',
    usage:
      'ใช้เมื่อต้องการหยุดและลบ containers, networks และทรัพยากรทั้งหมดที่สร้างขึ้นโดย Compose เมื่อเสร็จสิ้นการทำงาน'
  }
]
</script>
