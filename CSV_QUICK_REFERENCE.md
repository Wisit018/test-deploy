# 📊 CSV Export - Quick Reference

## สรุปสั้น

✅ **ส่งออกครบ:** 216 ฟิลด์ทั้งหมด  
✅ **พร้อม Import:** นำไป import เข้า Database ต้นทางได้ทันที  
✅ **รูปแบบถูกต้อง:** ตรงตามโครงสร้าง EgDeliver9.DBF  
✅ **ภาษาไทย:** UTF-8 with BOM รองรับภาษาไทย  

---

## 🎯 ปุ่มส่งออก 2 ปุ่ม

| ปุ่ม | คำอธิบาย | ชื่อไฟล์ | เหมาะสำหรับ |
|------|---------|----------|------------|
| **📥 ส่งออกรายการที่เลือก** | ส่งออกรายการที่มี delivernum เดียวกัน | `delivery_[NUM]_[TIME].csv` | ส่งออก 1 ใบสั่งซื้อ |
| **📅 ส่งออกรายการตามวันที่** | ส่งออกทุกรายการในวันที่เลือก | `deliveries_[DATE]_[TIME].csv` | ส่งออกหลายใบสั่งซื้อ |

---

## 📋 ข้อมูลที่ส่งออก (216 ฟิลด์)

### กลุ่มหลัก (10 กลุ่ม)

| กลุ่ม | จำนวนฟิลด์ | ตัวอย่างฟิลด์สำคัญ |
|------|-----------|------------------|
| 1. ข้อมูลการทำงาน | 8 | WORKDATE, WORKTIME, OPERATOR, DELIVERNUM |
| 2. ประเภทและสื่อ | 9 | MEDIADESC, CHANNELDES, DATADESC |
| 3. การชำระเงิน | 24 | PAYDESC, PAYMENT, PAYDAY, CUSBANKAC |
| 4. การจัดส่ง & บุคลากร | 15 | SHIPDESC, SALEREPID, ROUTEDESC |
| 5. Messenger & วันที่ | 7 | DATE, DAY, MSNID |
| 6. สินค้า | 13 | CODE, TITLE, PRICE, QTY, TOTAL |
| 7. ลูกค้า | 60 | CUSTOMERID, FIRSTNAME, LASTNAME, ADDR1 |
| 8. การนัดหมาย | 19 | APPTDATE, APPTTIME, APPTTEL, APPTADDR |
| 9. สถานะต่างๆ | 65 | DELIVER, RECEIVE, PAYMENT, FINISH |
| 10. ระบบและเพิ่มเติม | 14 | UNIQUEID, EMAILADDR, FOLLOWUP |

**รวม:** 216 ฟิลด์

---

## 🔢 รูปแบบข้อมูล

| ประเภท | รูปแบบ | ตัวอย่าง | จำนวนฟิลด์ |
|--------|--------|---------|-----------|
| วันที่ (Date) | DD/MM/YYYY | 15/10/2025 | 33 ฟิลด์ |
| ตัวเลข (Number) | 1234.50 | 1250.00 | 38 ฟิลด์ |
| ใช่/ไม่ใช่ (Logical) | T / F | T | 33 ฟิลด์ |
| ข้อความ (Text) | Text | ชื่อสินค้า | 112 ฟิลด์ |

---

## 🚀 ขั้นตอนใช้งาน

### ส่งออก (Export)
1. เปิดหน้า Dashboard
2. เลือกรายการหรือเลือกวันที่
3. คลิกปุ่มส่งออก
4. ไฟล์จะถูกดาวน์โหลด

### นำเข้า (Import)
1. เปิดโปรแกรม DBF Manager
2. File → Import → From CSV
3. เลือกไฟล์ CSV
4. ตั้งค่า: Delimiter = Comma, Encoding = UTF-8
5. เริ่ม Import

---

## ⚡ ข้อมูลสำคัญที่ต้องรู้

### ✅ ข้อมูลที่ส่งออก (มีทั้งหมด)
- ข้อมูลลูกค้า (CUSTOMERID, ชื่อ-นามสกุล, ที่อยู่ 2 ชุด)
- ข้อมูลสินค้า (CODE, TITLE, PRICE, QTY, TOTAL)
- ข้อมูลการชำระเงิน (PAYDESC, PAYMENT, บัตรเครดิต, ธนาคาร)
- ข้อมูลการจัดส่ง (SHIPDESC, DELIVER, RECEIVE)
- ข้อมูลการนัดหมาย (APPTDATE, APPTTIME, APPTADDR)
- สถานะต่างๆ (PAYMENT, DELIVER, RECEIVE, FINISH)
- Media & Channel (MEDIADESC, CHANNELDES)

### ❌ ข้อมูลที่ไม่ส่งออก (ไม่มีใน EgDeliver9.DBF)
- FOLLOWUPDAYS (ฟิลด์เพิ่มเติมในระบบใหม่)
- SYMPTOM (ฟิลด์เพิ่มเติมในระบบใหม่)
- URGENCY (ฟิลด์เพิ่มเติมในระบบใหม่)

---

## 🎨 การ Map ฟิลด์พิเศษ

### ฟิลด์ที่มีการใช้งานพิเศษ:

| ฟิลด์ในระบบ | ฟิลด์ใน DBF | คำอธิบาย |
|------------|------------|---------|
| Keyword | MOOBAN2 | ใช้ฟิลด์ MOOBAN2 เก็บ Keyword |
| Follow Up Days | FOLLOWUP | จำนวนวัน (ไม่ใช่ FOLLOWUPDAYS) |
| อาการ | - | ไม่ส่งออก (ไม่มีใน DBF) |
| ระดับความปวด | - | ไม่ส่งออก (ไม่มีใน DBF) |

---

## 💡 เคล็ดลับ

### การเปิดไฟล์ใน Excel:
1. ใช้ Excel Import Wizard (ไม่ใช่เปิดโดยตรง)
2. Data → Get Data → From Text/CSV
3. File Origin: UTF-8
4. Delimiter: Comma

### การตรวจสอบข้อมูลก่อน Import:
- ตรวจจำนวนแถว
- ตรวจ DELIVERNUM ซ้ำ
- ตรวจวันที่ถูกรูปแบบ
- ตรวจ TOTAL ไม่เป็น 0

---

## 📂 ไฟล์ที่เกี่ยวข้อง

| ไฟล์ | คำอธิบาย |
|------|---------|
| `CSV_EXPORT_MAPPING_SUMMARY.md` | สรุปละเอียดทุกฟิลด์ 216 ฟิลด์ |
| `CSV_EXPORT_GUIDE_TH.md` | คู่มือใช้งานแบบละเอียด |
| `CSV_QUICK_REFERENCE.md` | เอกสารฉบับนี้ (สรุปสั้น) |

---

## 🔗 Quick Links

- **Dashboard:** `/dashboard`
- **Documentation:** `CSV_EXPORT_GUIDE_TH.md`
- **Full Mapping:** `CSV_EXPORT_MAPPING_SUMMARY.md`

---

**เวอร์ชัน:** 2.0 (Complete Export)  
**อัปเดตล่าสุด:** 24 ตุลาคม 2025  

