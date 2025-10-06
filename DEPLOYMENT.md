# Railway Deployment Guide

## การ Deploy บน Railway

### 1. เตรียมโปรเจค

โปรเจคนี้ได้ถูกเตรียมให้พร้อมสำหรับ deploy บน Railway แล้ว โดยมีไฟล์ที่จำเป็นดังนี้:

- `railway.json` - Railway configuration
- `Procfile` - Process definition สำหรับ Railway
- `env.example` - ตัวอย่าง environment variables
- `.gitignore` - ไฟล์ที่ควร ignore

### 2. ตั้งค่า Environment Variables

ใน Railway dashboard ให้ตั้งค่า environment variables ดังนี้:

```
DB_HOST=your_mysql_host
DB_PORT=3306
DB_USER=your_username
DB_PASSWORD=your_password
DB_NAME=your_database_name
SESSION_SECRET=your_very_secure_session_secret_here
NODE_ENV=production
```

### 3. การ Deploy

#### วิธีที่ 1: ผ่าน Railway CLI

1. ติดตั้ง Railway CLI:
```bash
npm install -g @railway/cli
```

2. Login เข้า Railway:
```bash
railway login
```

3. สร้างโปรเจคใหม่:
```bash
railway init
```

4. Deploy:
```bash
railway up
```

#### วิธีที่ 2: ผ่าน GitHub Integration

1. Push โค้ดไปยัง GitHub repository
2. ไปที่ [Railway Dashboard](https://railway.app)
3. คลิก "New Project" > "Deploy from GitHub repo"
4. เลือก repository ของคุณ
5. ตั้งค่า environment variables
6. Railway จะ deploy อัตโนมัติ

### 4. ตั้งค่า Database

#### ใช้ Railway MySQL Service

1. ใน Railway dashboard คลิก "New Service" > "Database" > "MySQL"
2. Railway จะสร้าง MySQL database ให้อัตโนมัติ
3. คัดลอก connection string ไปตั้งค่า environment variables

#### ใช้ External MySQL

หากต้องการใช้ MySQL ภายนอก ให้ตั้งค่า environment variables ดังนี้:

```
DB_HOST=your_external_mysql_host
DB_PORT=3306
DB_USER=your_username
DB_PASSWORD=your_password
DB_NAME=your_database_name
```

### 5. การตรวจสอบ Deployment

1. ตรวจสอบ logs ใน Railway dashboard
2. ตรวจสอบ health check endpoint: `https://your-app.railway.app/health`
3. เข้าถึงแอปพลิเคชันผ่าน URL ที่ Railway ให้

### 6. การอัปเดต

เมื่อมีการเปลี่ยนแปลงโค้ด:

1. Push ไปยัง GitHub repository
2. Railway จะ deploy อัตโนมัติ (หากใช้ GitHub integration)
3. หรือใช้ `railway up` (หากใช้ CLI)

### 7. การ Debug

หากมีปัญหา:

1. ตรวจสอบ logs ใน Railway dashboard
2. ตรวจสอบ environment variables
3. ตรวจสอบ database connection
4. ตรวจสอบ health check endpoint

#### แก้ไขปัญหา Health Check ล้มเหลว

หากเจอปัญหา "Healthcheck failed!" ให้ตรวจสอบ:

1. **Environment Variables**: ตรวจสอบว่าตั้งค่าถูกต้องแล้ว
   ```bash
   DB_HOST=your_mysql_host
   DB_PORT=3306
   DB_USER=your_username
   DB_PASSWORD=your_password
   DB_NAME=your_database_name
   SESSION_SECRET=your_secure_secret
   NODE_ENV=production
   ```

2. **Database Connection**: ตรวจสอบว่า database service ทำงานอยู่
3. **Port Configuration**: ตรวจสอบว่า PORT environment variable ถูกต้อง
4. **Logs**: ดู logs ใน Railway dashboard เพื่อหาสาเหตุ

#### การแก้ไขปัญหาเฉพาะ

**ปัญหา**: Health check ล้มเหลว
**วิธีแก้**: 
- ใช้ Dockerfile แทน Nixpacks
- เพิ่ม healthcheckTimeout เป็น 300 วินาที
- ตรวจสอบว่า `/health` endpoint ทำงานได้

**ปัญหา**: Database connection ล้มเหลว
**วิธีแก้**:
- ตรวจสอบ environment variables
- ใช้ Railway MySQL service
- หรือใช้ external MySQL service

### 8. Production Considerations

- เปลี่ยน `SESSION_SECRET` เป็นค่าที่ปลอดภัย
- ใช้ production-grade session store (เช่น Redis)
- ตั้งค่า proper CORS policies
- ใช้ HTTPS (Railway ให้อัตโนมัติ)
- ตั้งค่า proper error handling และ logging

### 9. ไฟล์ที่สำคัญ

- `server.js` - Main application file
- `db.js` - Database configuration
- `package.json` - Dependencies และ scripts
- `railway.json` - Railway configuration
- `Procfile` - Process definition
- `env.example` - Environment variables template

### 10. Support

หากมีปัญหาในการ deploy สามารถตรวจสอบ:

- [Railway Documentation](https://docs.railway.app)
- [Railway Community](https://discord.gg/railway)
- Application logs ใน Railway dashboard
