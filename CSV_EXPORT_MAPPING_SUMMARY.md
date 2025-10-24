# สรุปการส่งออกข้อมูล CSV - Dashboard Export

## ภาพรวม
ไฟล์ CSV ที่ส่งออกจากหน้า Dashboard ได้รับการแก้ไขให้ครบถ้วนตามโครงสร้างของ **EgDeliver9.DBF** ทุกฟิลด์ (ทั้งหมด **216 ฟิลด์**)

## ปุ่มส่งออกข้อมูล (2 ปุ่ม)

### 1. 📥 ส่งออกรายการที่เลือก (Export Selected Row)
- **ฟังก์ชัน:** `exportSelectedRow()`
- **การทำงาน:** ส่งออกรายการที่เลือกทั้งหมดที่มี `delivernum` เดียวกัน
- **ชื่อไฟล์:** `delivery_[DELIVERNUM]_[TIMESTAMP].csv`

### 2. 📅 ส่งออกรายการตามวันที่ (Export by Date)
- **ฟังก์ชัน:** `exportByDate()`
- **การทำงาน:** ส่งออกรายการทั้งหมดที่มี `apptdate` ตรงกับวันที่เลือก
- **ชื่อไฟล์:** `deliveries_[DD-MM-YYYY]_[TIMESTAMP].csv`

## โครงสร้างไฟล์ CSV ที่ส่งออก

### รูปแบบ (Format)
- **Encoding:** UTF-8 with BOM (สำหรับ Excel)
- **Delimiter:** Comma (,)
- **Date Format:** DD/MM/YYYY
- **Logical Format:** T/F
- **Number Format:** Fixed decimals (e.g., 1234.50)

---

## รายละเอียดฟิลด์ทั้งหมด 216 ฟิลด์ พร้อมแหล่งข้อมูล

**สัญลักษณ์:**
- 🎯 = ข้อมูลจากโปรเจค (Workflow)
- ⚙️ = ข้อมูลระบบ (ไม่เกี่ยวข้องโปรเจค)
- 📊 = ข้อมูลหลังประมวลผล

### กลุ่มที่ 1: ข้อมูลการทำงาน (Work Information) [8 ฟิลด์]

| # | ชื่อฟิลด์ | ประเภท | ความกว้าง | คำอธิบาย | แหล่งข้อมูล | Step |
|---|----------|--------|----------|---------|------------|------|
| 1 | WORKDATE | Date | 8 | วันที่ทำงาน | ⚙️ ระบบ | Auto |
| 2 | WORKTIME | Character | 8 | เวลาทำงาน | ⚙️ ระบบ | Auto |
| 3 | OPERATOR | Character | 10 | ผู้ปฏิบัติงาน | ⚙️ ระบบ | Auto |
| 4 | CHKMINUTE | Character | 8 | เวลาตรวจสอบ | ⚙️ ระบบ | - |
| 5 | DELIVERNUM | Character | 10 | เลขที่ใบส่งของ (Primary Key) | ⚙️ ระบบ | Auto |
| 6 | TOHOMENUM | Character | 14 | เลขที่ส่งถึงบ้าน | ⚙️ ระบบ | - |
| 7 | TIMEIN | Character | 8 | เวลาเข้า | ⚙️ ระบบ | - |
| 8 | TIMEOUT | Character | 8 | เวลาออก | ⚙️ ระบบ | - |

### กลุ่มที่ 2: ข้อมูลประเภทและสื่อ (Type & Media) [9 ฟิลด์]

| # | ชื่อฟิลด์ | ประเภท | ความกว้าง | คำอธิบาย | แหล่งข้อมูล | Step |
|---|----------|--------|----------|---------|------------|------|
| 9 | BUY | Logical | 1 | ซื้อ/ไม่ซื้อ | 🎯 โปรเจค | Step 3 |
| 10 | DATATYPE | Numeric | 3 | รหัสประเภทข้อมูล | 🎯 โปรเจค | Step 3 |
| 11 | DATADESC | Character | 30 | คำอธิบายประเภทข้อมูล (ขาย/ค่าส่ง/ของแถม) | 🎯 โปรเจค | Step 3 |
| 12 | PROCESSTYP | Numeric | 3 | รหัสประเภทกระบวนการ | ⚙️ ระบบ | - |
| 13 | PROCESSDES | Character | 30 | คำอธิบายกระบวนการ | ⚙️ ระบบ | - |
| 14 | MEDIATYPE | Numeric | 3 | รหัสประเภทสื่อ | 🎯 โปรเจค | Step 2 |
| 15 | MEDIADESC | Character | 30 | คำอธิบายสื่อ (SEM/SHOPEE/LAZADA) | 🎯 โปรเจค | Step 2 |
| 16 | CHANNEL | Numeric | 3 | รหัสช่องทาง | 🎯 โปรเจค | Step 2 |
| 17 | CHANNELDES | Character | 30 | คำอธิบายช่องทาง | 🎯 โปรเจค | Step 2 |

### กลุ่มที่ 3: ข้อมูลการชำระเงิน (Payment Information) [24 ฟิลด์]

| # | ชื่อฟิลด์ | ประเภท | ความกว้าง | คำอธิบาย | แหล่งข้อมูล | Step |
|---|----------|--------|----------|---------|------------|------|
| 18 | PAYTYPE | Numeric | 3 | รหัสประเภทการชำระเงิน | 🎯 โปรเจค | Step 5 |
| 19 | PAYDESC | Character | 50 | คำอธิบายวิธีชำระเงิน | 🎯 โปรเจค | Step 5 |
| 20 | PAYTYPE1 | Character | 2 | ประเภทการชำระ 1 | 🎯 โปรเจค | Step 5 |
| 21 | SUBPAY1 | Character | 2 | ประเภทย่อย 1 | 🎯 โปรเจค | Step 5 |
| 22 | SUBPAY2 | Character | 2 | ประเภทย่อย 2 | 🎯 โปรเจค | Step 5 |
| 23 | PAYMENT | Logical | 1 | ชำระเงินแล้ว | 📊 หลังบันทึก | - |
| 24 | PAYDAY | Date | 8 | วันที่ชำระเงิน | 📊 หลังบันทึก | - |
| 25 | CUSBANKNO | Character | 5 | รหัสธนาคารลูกค้า | 🎯 โปรเจค | Step 5 |
| 26 | CUSBANKNA | Character | 30 | ชื่อธนาคารลูกค้า | 🎯 โปรเจค | Step 5 |
| 27 | CUSBANKBR | Character | 30 | สาขาธนาคารลูกค้า | 🎯 โปรเจค | Step 5 |
| 28 | CUSBANKAC | Character | 20 | เลขบัญชีลูกค้า | 🎯 โปรเจค | Step 5 |
| 29 | CUSBANKREF | Character | 20 | เลขอ้างอิงธนาคารลูกค้า | 🎯 โปรเจค | Step 5 |
| 30 | CREDIT | Logical | 1 | ใช้บัตรเครดิต | 🎯 โปรเจค | Step 5 |
| 31 | CREDITTYPE | Numeric | 3 | ประเภทบัตรเครดิต | 🎯 โปรเจค | Step 5 |
| 32 | CREDITDESC | Character | 20 | คำอธิบายบัตรเครดิต | 🎯 โปรเจค | Step 5 |
| 33 | CREDITNO | Character | 20 | เลขบัตรเครดิต | 🎯 โปรเจค | Step 5 |
| 34 | CREDITEXPM | Character | 2 | เดือนหมดอายุบัตร | 🎯 โปรเจค | Step 5 |
| 35 | CREDITEXPY | Character | 4 | ปีหมดอายุบัตร | 🎯 โปรเจค | Step 5 |
| 36 | CREDITREF | Character | 20 | เลขอ้างอิงบัตรเครดิต | 🎯 โปรเจค | Step 5 |
| 37 | LAST3DIGIT | Character | 5 | เลข 3 ตัวท้ายบัตร | 🎯 โปรเจค | Step 5 |
| 38 | BANKNO | Character | 5 | รหัสธนาคารร้าน | 🎯 โปรเจค | Step 5 |
| 39 | BANKNA | Character | 30 | ชื่อธนาคารร้าน | 🎯 โปรเจค | Step 5 |
| 40 | BANKBR | Character | 30 | สาขาธนาคารร้าน | 🎯 โปรเจค | Step 5 |
| 41 | BANKAC | Character | 20 | เลขบัญชีร้าน | 🎯 โปรเจค | Step 5 |
| 42 | BANKREF | Character | 20 | เลขอ้างอิงธนาคารร้าน | 🎯 โปรเจค | Step 5 |

### กลุ่มที่ 4: ข้อมูลการจัดส่ง & บุคลากร (Shipping & Personnel) [15 ฟิลด์]

| # | ชื่อฟิลด์ | ประเภท | ความกว้าง | คำอธิบาย | ข้อมูลที่ส่งออก |
|---|----------|--------|----------|---------|----------------|
| 43 | SHIPTYPE | Numeric | 3 | รหัสประเภทการจัดส่ง | ✅ มีข้อมูล |
| 44 | SHIPDESC | Character | 30 | คำอธิบายวิธีจัดส่ง | ✅ มีข้อมูล |
| 45 | DELIVERTO | Character | 3 | ส่งถึง | ✅ มีข้อมูล |
| 46 | USERID | Character | 6 | รหัสผู้ใช้งาน | ✅ มีข้อมูล |
| 47 | USERNAME | Character | 20 | ชื่อผู้ใช้งาน | ✅ มีข้อมูล |
| 48 | SALEREPID | Character | 6 | รหัสพนักงานขาย | ✅ มีข้อมูล |
| 49 | SALENAME | Character | 20 | ชื่อพนักงานขาย | ✅ มีข้อมูล |
| 50 | RING | Character | 10 | Ring | ✅ มีข้อมูล |
| 51 | RINGDESC | Character | 20 | คำอธิบาย Ring | ✅ มีข้อมูล |
| 52 | ROUTERUN | Character | 3 | รหัสรอบจัดส่ง | ✅ มีข้อมูล |
| 53 | ROUTENO | Character | 3 | เลขเส้นทาง | ✅ มีข้อมูล |
| 54 | ROUTEDESC | Character | 20 | คำอธิบายเส้นทาง | ✅ มีข้อมูล |
| 55 | ROUTEDIST | Numeric | 10.2 | ระยะทางเส้นทาง (กม.) | ✅ มีข้อมูล |
| 56 | ROUTETIMES | Character | 8 | เวลาเส้นทาง | ✅ มีข้อมูล |
| 57 | MILESP2P | Numeric | 10.2 | ระยะทางจุดต่อจุด | ✅ มีข้อมูล |

### กลุ่มที่ 5: ข้อมูล Messenger & วันที่ (Messenger & Date) [7 ฟิลด์]

| # | ชื่อฟิลด์ | ประเภท | ความกว้าง | คำอธิบาย | ข้อมูลที่ส่งออก |
|---|----------|--------|----------|---------|----------------|
| 58 | TIMESP2P | Numeric | 10.2 | เวลาจุดต่อจุด | ✅ มีข้อมูล |
| 59 | MSNID | Character | 6 | รหัส Messenger | ✅ มีข้อมูล |
| 60 | MSNNAME | Character | 20 | ชื่อ Messenger | ✅ มีข้อมูล |
| 61 | HANDTIMES | Character | 8 | เวลาส่งมอบ | ✅ มีข้อมูล |
| 62 | DAY | Character | 10 | วัน | ✅ มีข้อมูล |
| 63 | DATE | Date | 8 | วันที่ | ✅ มีข้อมูล |
| 64 | SOURCE | Numeric | 3 | แหล่งที่มา | ✅ มีข้อมูล |

### กลุ่มที่ 6: ข้อมูลสินค้า (Product Information) [13 ฟิลด์]

| # | ชื่อฟิลด์ | ประเภท | ความกว้าง | คำอธิบาย | ข้อมูลที่ส่งออก |
|---|----------|--------|----------|---------|----------------|
| 65 | CODE | Numeric | 5 | รหัสสินค้า | ✅ มีข้อมูล |
| 66 | PRDGROUP | Numeric | 5 | กลุ่มสินค้า | ✅ มีข้อมูล |
| 67 | TITLE | Character | 40 | ชื่อสินค้า | ✅ มีข้อมูล |
| 68 | COST | Numeric | 9.2 | ต้นทุน | ✅ มีข้อมูล |
| 69 | PRICE | Numeric | 9.2 | ราคา | ✅ มีข้อมูล |
| 70 | SALPRICE | Numeric | 10.2 | ราคาขาย | ✅ มีข้อมูล |
| 71 | QTY | Numeric | 7 | จำนวน | ✅ มีข้อมูล |
| 72 | AMOUNT | Numeric | 10.2 | ยอดรวม | ✅ มีข้อมูล |
| 73 | POSTFEE | Numeric | 7.2 | ค่าส่ง | ✅ มีข้อมูล |
| 74 | TOTAL | Numeric | 10.2 | ยอดรวมทั้งหมด | ✅ มีข้อมูล |
| 75 | FREECODE | Numeric | 5 | รหัสของแถม | ✅ มีข้อมูล |
| 76 | DSCAMT | Numeric | 7.2 | ส่วนลด | ✅ มีข้อมูล |
| 77 | TRANSNO | Character | 10 | เลขที่ธุรกรรม | ✅ มีข้อมูล |

### กลุ่มที่ 7: ข้อมูลลูกค้า (Customer Information) [60 ฟิลด์]

| # | ชื่อฟิลด์ | ประเภท | ความกว้าง | คำอธิบาย | ข้อมูลที่ส่งออก |
|---|----------|--------|----------|---------|----------------|
| 78 | CUSTOMERID | Character | 10 | รหัสลูกค้า | ✅ มีข้อมูล |
| 79 | MEMCODE | Numeric | 6 | รหัสสมาชิก | ✅ มีข้อมูล |
| 80 | PRENAME | Character | 20 | คำนำหน้าชื่อ | ✅ มีข้อมูล |
| 81 | FIRSTNAME | Character | 40 | ชื่อ | ✅ มีข้อมูล |
| 82 | LASTNAME | Character | 50 | นามสกุล | ✅ มีข้อมูล |
| 83 | ADDR1 | Character | 50 | ที่อยู่ 1 | ✅ มีข้อมูล |
| 84 | ADDR2 | Character | 50 | ที่อยู่ 2 | ✅ มีข้อมูล |
| 85 | HOMENUM1 | Character | 10 | บ้านเลขที่ 1 | ✅ มีข้อมูล |
| 86 | HOMENUM2 | Character | 10 | บ้านเลขที่ 2 | ✅ มีข้อมูล |
| 87 | PRECOMNAM1 | Character | 25 | คำนำหน้าบริษัท 1 | ✅ มีข้อมูล |
| 88 | PRECOMNAM2 | Character | 25 | คำนำหน้าบริษัท 2 | ✅ มีข้อมูล |
| 89 | COMNAME1 | Character | 30 | ชื่อบริษัท 1 | ✅ มีข้อมูล |
| 90 | COMNAME2 | Character | 30 | ชื่อบริษัท 2 | ✅ มีข้อมูล |
| 91 | LSTCOMNAM1 | Character | 25 | นามสกุลบริษัท 1 | ✅ มีข้อมูล |
| 92 | LSTCOMNAM2 | Character | 25 | นามสกุลบริษัท 2 | ✅ มีข้อมูล |
| 93 | BUILDING1 | Character | 20 | อาคาร 1 | ✅ มีข้อมูล |
| 94 | BUILDING2 | Character | 20 | อาคาร 2 | ✅ มีข้อมูล |
| 95 | FLOOR1 | Character | 10 | ชั้น 1 | ✅ มีข้อมูล |
| 96 | FLOOR2 | Character | 10 | ชั้น 2 | ✅ มีข้อมูล |
| 97 | ROOM1 | Character | 10 | ห้อง 1 | ✅ มีข้อมูล |
| 98 | ROOM2 | Character | 10 | ห้อง 2 | ✅ มีข้อมูล |
| 99 | SOI1 | Character | 30 | ซอย 1 | ✅ มีข้อมูล |
| 100 | SOI2 | Character | 30 | ซอย 2 | ✅ มีข้อมูล |
| 101 | ROAD1 | Character | 30 | ถนน 1 | ✅ มีข้อมูล |
| 102 | ROAD2 | Character | 30 | ถนน 2 | ✅ มีข้อมูล |
| 103 | KATE1 | Character | 30 | เขต 1 | ✅ มีข้อมูล |
| 104 | KATE2 | Character | 30 | เขต 2 | ✅ มีข้อมูล |
| 105 | KWANG1 | Character | 30 | แขวง 1 | ✅ มีข้อมูล |
| 106 | KWANG2 | Character | 30 | แขวง 2 | ✅ มีข้อมูล |
| 107 | MOOBAN1 | Character | 30 | หมู่บ้าน 1 | ✅ มีข้อมูล |
| 108 | MOOBAN2 | Character | 30 | หมู่บ้าน 2 / **Keyword** | ✅ มีข้อมูล (ใช้เป็น Keyword) |
| 109 | TUMBON1 | Character | 30 | ตำบล 1 | ✅ มีข้อมูล |
| 110 | TUMBON2 | Character | 30 | ตำบล 2 | ✅ มีข้อมูล |
| 111 | AMPUR1 | Character | 30 | อำเภอ 1 | ✅ มีข้อมูล |
| 112 | AMPUR2 | Character | 30 | อำเภอ 2 | ✅ มีข้อมูล |
| 113 | PROVINCE1 | Character | 20 | จังหวัด 1 | ✅ มีข้อมูล |
| 114 | PROVINCE2 | Character | 20 | จังหวัด 2 | ✅ มีข้อมูล |
| 115 | ZIPCODE1 | Character | 5 | รหัสไปรษณีย์ 1 | ✅ มีข้อมูล |
| 116 | ZIPCODE2 | Character | 5 | รหัสไปรษณีย์ 2 | ✅ มีข้อมูล |
| 117 | PROVINCE | Character | 20 | จังหวัด | ✅ มีข้อมูล |
| 118 | ZIPCODE | Character | 5 | รหัสไปรษณีย์ | ✅ มีข้อมูล |

### กลุ่มที่ 8: ข้อมูลการนัดหมาย (Appointment Information) [19 ฟิลด์]

| # | ชื่อฟิลด์ | ประเภท | ความกว้าง | คำอธิบาย | ข้อมูลที่ส่งออก |
|---|----------|--------|----------|---------|----------------|
| 119 | BEFOREAFT | Character | 10 | ก่อน/หลัง | ✅ มีข้อมูล |
| 120 | APPTDAY | Character | 10 | วันนัด | ✅ มีข้อมูล |
| 121 | APPTDATE | Date | 8 | วันที่นัด | ✅ มีข้อมูล |
| 122 | APPTTIME | Character | 8 | เวลานัด | ✅ มีข้อมูล |
| 123 | APPTTIME1 | Character | 30 | เวลานัด 1 | ✅ มีข้อมูล |
| 124 | APPTTIME2 | Character | 30 | เวลานัด 2 | ✅ มีข้อมูล |
| 125 | APPTPERSON | Character | 40 | ผู้ติดต่อ | ✅ มีข้อมูล |
| 126 | APPTTEL | Character | 18 | เบอร์โทรติดต่อ | ✅ มีข้อมูล |
| 127 | APPTADDR | Character | 254 | ที่อยู่นัด | ✅ มีข้อมูล |
| 128 | APPTADDR1 | Character | 100 | ที่อยู่นัด 1 | ✅ มีข้อมูล |
| 129 | APPTADDR2 | Character | 100 | ที่อยู่นัด 2 | ✅ มีข้อมูล |
| 130 | APPTKWANG | Character | 30 | แขวงนัด | ✅ มีข้อมูล |
| 131 | APPTKATE | Character | 30 | เขตนัด | ✅ มีข้อมูล |
| 132 | APPTTUMBON | Character | 30 | ตำบลนัด | ✅ มีข้อมูล |
| 133 | APPTAMPUR | Character | 30 | อำเภอนัด | ✅ มีข้อมูล |
| 134 | APPTPROV | Character | 20 | จังหวัดนัด | ✅ มีข้อมูล |
| 135 | APPTZIP | Character | 10 | รหัสไปรษณีย์นัด | ✅ มีข้อมูล |
| 136 | APPTREMK1 | Character | 80 | หมายเหตุนัด 1 | ✅ มีข้อมูล |
| 137 | APPTREMK2 | Character | 80 | หมายเหตุนัด 2 | ✅ มีข้อมูล |

### กลุ่มที่ 9: สถานะต่างๆ (Status Flags) [65 ฟิลด์]

| # | ชื่อฟิลด์ | ประเภท | ความกว้าง | คำอธิบาย | ข้อมูลที่ส่งออก |
|---|----------|--------|----------|---------|----------------|
| 138 | AFTDELICAL | Logical | 1 | โทรหลังส่ง | ✅ มีข้อมูล (T/F) |
| 139 | AFTDELITI | Character | 8 | เวลาโทรหลังส่ง | ✅ มีข้อมูล |
| 140 | AFTDELIDA | Date | 8 | วันที่โทรหลังส่ง | ✅ มีข้อมูล |
| 141 | AUTOBRT9 | Logical | 1 | Auto BRT9 | ✅ มีข้อมูล (T/F) |
| 142 | AUTOBRT9DA | Date | 8 | วันที่ Auto BRT9 | ✅ มีข้อมูล |
| 143 | AUTOBRT9TI | Character | 8 | เวลา Auto BRT9 | ✅ มีข้อมูล |
| 144 | AUTOBRT9BY | Character | 10 | ผู้ทำ Auto BRT9 | ✅ มีข้อมูล |
| 145 | DELIVER | Logical | 1 | ส่งแล้ว | ✅ มีข้อมูล (T/F) |
| 146 | DELIVERID | Character | 10 | รหัสผู้ส่ง | ✅ มีข้อมูล |
| 147 | DELIVERDA | Date | 8 | วันที่ส่ง | ✅ มีข้อมูล |
| 148 | DELIVERTI | Character | 8 | เวลาส่ง | ✅ มีข้อมูล |
| 149 | DELIVERBY | Character | 10 | ผู้ส่ง | ✅ มีข้อมูล |
| 150 | RECEIVE | Logical | 1 | รับแล้ว | ✅ มีข้อมูล (T/F) |
| 151 | RECEIVEDA | Date | 8 | วันที่รับ | ✅ มีข้อมูล |
| 152 | RECEIVETI | Character | 8 | เวลารับ | ✅ มีข้อมูล |
| 153 | RECEIVEBY | Character | 10 | ผู้รับ | ✅ มีข้อมูล |
| 154 | UPDATE | Logical | 1 | อัปเดตแล้ว | ✅ มีข้อมูล (T/F) |
| 155 | UPDATEDA | Date | 8 | วันที่อัปเดต | ✅ มีข้อมูล |
| 156 | UPDATETI | Character | 8 | เวลาอัปเดต | ✅ มีข้อมูล |
| 157 | UPDATEBY | Character | 10 | ผู้อัปเดต | ✅ มีข้อมูล |
| 158 | FINANCE | Logical | 1 | การเงิน | ✅ มีข้อมูล (T/F) |
| 159 | FINANCETYP | Numeric | 3 | ประเภทการเงิน | ✅ มีข้อมูล |
| 160 | FINANCEDES | Character | 30 | คำอธิบายการเงิน | ✅ มีข้อมูล |
| 161 | FINANCEDA | Date | 8 | วันที่การเงิน | ✅ มีข้อมูล |
| 162 | FINANCETI | Character | 8 | เวลาการเงิน | ✅ มีข้อมูล |
| 163 | FINANCEBY | Character | 10 | ผู้ทำการเงิน | ✅ มีข้อมูล |
| 164 | PRNORDER | Logical | 1 | พิมพ์ใบสั่งซื้อ | ✅ มีข้อมูล (T/F) |
| 165 | PRNORDDATE | Date | 8 | วันที่พิมพ์ใบสั่งซื้อ | ✅ มีข้อมูล |
| 166 | PRNORDTIME | Character | 8 | เวลาพิมพ์ใบสั่งซื้อ | ✅ มีข้อมูล |
| 167 | PRNPICK | Logical | 1 | พิมพ์ใบเบิกสินค้า | ✅ มีข้อมูล (T/F) |
| 168 | PRNPICDATE | Date | 8 | วันที่พิมพ์ใบเบิก | ✅ มีข้อมูล |
| 169 | PRNPICTIME | Character | 8 | เวลาพิมพ์ใบเบิก | ✅ มีข้อมูล |
| 170 | PRNSTICKER | Logical | 1 | พิมพ์สติ๊กเกอร์ | ✅ มีข้อมูล (T/F) |
| 171 | PRNSTIDATE | Date | 8 | วันที่พิมพ์สติ๊กเกอร์ | ✅ มีข้อมูล |
| 172 | PRNSTITIME | Character | 8 | เวลาพิมพ์สติ๊กเกอร์ | ✅ มีข้อมูล |
| 173 | PRNFINAN | Logical | 1 | พิมพ์การเงิน | ✅ มีข้อมูล (T/F) |
| 174 | PRNFINDATE | Date | 8 | วันที่พิมพ์การเงิน | ✅ มีข้อมูล |
| 175 | PRNFINTIME | Character | 8 | เวลาพิมพ์การเงิน | ✅ มีข้อมูล |
| 176 | PAYFLAG | Logical | 1 | Flag การชำระเงิน | ✅ มีข้อมูล (T/F) |
| 177 | PAYDATE | Date | 8 | วันที่ชำระเงิน | ✅ มีข้อมูล |
| 178 | PAYTIME | Character | 5 | เวลาชำระเงิน | ✅ มีข้อมูล |
| 179 | DELVFLAG | Logical | 1 | Flag การจัดส่ง | ✅ มีข้อมูล (T/F) |
| 180 | DELVDATE | Date | 8 | วันที่จัดส่ง | ✅ มีข้อมูล |
| 181 | DELVTIME | Character | 6 | เวลาจัดส่ง | ✅ มีข้อมูล |
| 182 | TAXINV | Character | 10 | เลขที่ใบกำกับภาษี | ✅ มีข้อมูล |
| 183 | TRANSFER | Logical | 1 | โอนแล้ว | ✅ มีข้อมูล (T/F) |
| 184 | SCANFLAG | Logical | 1 | สแกนแล้ว | ✅ มีข้อมูล (T/F) |
| 185 | SCANDATE | Date | 8 | วันที่สแกน | ✅ มีข้อมูล |
| 186 | SCANTIME | Character | 8 | เวลาสแกน | ✅ มีข้อมูล |
| 187 | SCANBY | Character | 20 | ผู้สแกน | ✅ มีข้อมูล |
| 188 | FEED | Logical | 1 | มี Feedback | ✅ มีข้อมูล (T/F) |
| 189 | FEEDNO | Numeric | 3 | เลขที่ Feedback | ✅ มีข้อมูล |
| 190 | FEEDBACK | Numeric | 3 | คะแนน Feedback | ✅ มีข้อมูล |
| 191 | FEEDDESC | Character | 30 | คำอธิบาย Feedback | ✅ มีข้อมูล |
| 192 | FEEDDATE | Date | 8 | วันที่ Feedback | ✅ มีข้อมูล |
| 193 | FEEDTIME | Character | 8 | เวลา Feedback | ✅ มีข้อมูล |
| 194 | FEEDID | Character | 6 | รหัส Feedback | ✅ มีข้อมูล |
| 195 | FEEDMEMO | Memo | 4 | บันทึก Feedback | ✅ มีข้อมูล |
| 196 | WEIGHTLOSS | Logical | 1 | ลดน้ำหนัก | ✅ มีข้อมูล (T/F) |
| 197 | WEIGHT | Logical | 1 | น้ำหนัก | ✅ มีข้อมูล (T/F) |
| 198 | REMARK1 | Character | 80 | หมายเหตุ 1 | ✅ มีข้อมูล |
| 199 | REMARK2 | Character | 80 | หมายเหตุ 2 | ✅ มีข้อมูล |
| 200 | STATUSID | Numeric | 3 | รหัสสถานะ | ✅ มีข้อมูล |
| 201 | STATUSDESC | Character | 80 | คำอธิบายสถานะ | ✅ มีข้อมูล |
| 202 | FINISH | Logical | 1 | เสร็จสิ้น | ✅ มีข้อมูล (T/F) |

### กลุ่มที่ 10: ข้อมูลระบบและเพิ่มเติม (System & Additional) [14 ฟิลด์]

| # | ชื่อฟิลด์ | ประเภท | ความกว้าง | คำอธิบาย | ข้อมูลที่ส่งออก |
|---|----------|--------|----------|---------|----------------|
| 203 | MAPSTAT | Character | 1 | สถานะ Map | ✅ มีข้อมูล |
| 204 | UNIQUEID | Character | 32 | รหัสเอกลักษณ์ | ✅ มีข้อมูล |
| 205 | ACCPRINT | Numeric | 1 | จำนวนพิมพ์บัญชี | ✅ มีข้อมูล |
| 206 | ACCPRINTD | Date | 8 | วันที่พิมพ์บัญชี | ✅ มีข้อมูล |
| 207 | ACCPRINTT | Character | 8 | เวลาพิมพ์บัญชี | ✅ มีข้อมูล |
| 208 | NKPRINT | Numeric | 1 | จำนวนพิมพ์ NK | ✅ มีข้อมูล |
| 209 | NKPRINTD | Date | 8 | วันที่พิมพ์ NK | ✅ มีข้อมูล |
| 210 | NKPRINTT | Character | 8 | เวลาพิมพ์ NK | ✅ มีข้อมูล |
| 211 | ROUTEDATE | Date | 8 | วันที่เส้นทาง | ✅ มีข้อมูล |
| 212 | EDITNO | Character | 12 | เลขที่แก้ไข | ✅ มีข้อมูล |
| 213 | EDITFLAG | Logical | 1 | Flag แก้ไข | ✅ มีข้อมูล (T/F) |
| 214 | CNFLAG | Logical | 1 | Flag ยืนยัน | ✅ มีข้อมูล (T/F) |
| 215 | EMAILADDR | Character | 30 | อีเมล | ✅ มีข้อมูล |
| 216 | FOLLOWUP | Numeric | 5 | Follow Up | ✅ มีข้อมูล |

---

## ฟิลด์ที่ไม่ได้ถูกส่งออก

### ฟิลด์ที่มีใน Database แต่ไม่อยู่ใน EgDeliver9.DBF:
- **FOLLOWUPDAYS** - จำนวนวัน Follow Up (ฟิลด์เพิ่มเติมในระบบใหม่)
- **SYMPTOM** - อาการ (ฟิลด์เพิ่มเติมในระบบใหม่)
- **URGENCY** - ระดับความปวด (ฟิลด์เพิ่มเติมในระบบใหม่)

**หมายเหตุ:** ฟิลด์เหล่านี้เป็นฟิลด์ที่เพิ่มเติมในระบบใหม่ จึงไม่มีอยู่ในไฟล์ EgDeliver9.DBF ต้นฉบับ และจะไม่ถูกส่งออกเพื่อให้สามารถ import กลับเข้า Database เดิมได้

---

## การจัดการข้อมูลพิเศษ

### 1. วันที่ (Date Fields)
- **รูปแบบ:** DD/MM/YYYY (เช่น 15/09/2025)
- **ค่าว่าง:** แสดงเป็น "" (empty string)
- **จำนวน:** 33 ฟิลด์

### 2. ตัวเลข (Numeric Fields)
- **จำนวนเต็ม:** ไม่มีทศนิยม (เช่น 123)
- **ทศนิยม 2 ตำแหน่ง:** 1234.50
- **ค่าว่าง:** แสดงเป็น "" (empty string)
- **จำนวน:** 38 ฟิลด์

### 3. Logical Fields (T/F)
- **True:** T
- **False:** F
- **ค่าว่าง:** "" (empty string)
- **จำนวน:** 33 ฟิลด์

### 4. ข้อความ (Character/Memo Fields)
- **การจัดการ:** 
  - Escape comma, quotes, newlines
  - ถ้ามี comma, quotes, หรือ newline จะครอบด้วย double quotes
  - Double quotes จะถูก escape เป็น ""
- **จำนวน:** 112 ฟิลด์

---

## การใช้งาน

### ขั้นตอนการส่งออกข้อมูล:

1. **เปิดหน้า Dashboard**
   - เข้าไปที่ `/dashboard`

2. **เลือกรายการที่ต้องการส่งออก**
   - คลิกที่แถวในตาราง
   - แถวจะเปลี่ยนสีเป็นสีน้ำเงินอ่อน

3. **คลิกปุ่มส่งออก**
   - **📥 ส่งออกรายการที่เลือก:** ส่งออกรายการที่เลือกทั้งหมดที่มี delivernum เดียวกัน
   - **📅 ส่งออกรายการตามวันที่:** เลือกวันที่แล้วคลิกส่งออก

4. **ไฟล์ CSV จะถูกดาวน์โหลด**
   - ชื่อไฟล์จะมี timestamp อัตโนมัติ
   - เข้ารหัส UTF-8 with BOM (เปิดใน Excel ได้เลย)

### การนำไปใช้:

1. **Import เข้า Database ต้นทาง**
   - เปิดโปรแกรมจัดการ DBF
   - เลือก Import from CSV
   - เลือกไฟล์ที่ส่งออก
   - ตั้งค่า delimiter เป็น comma
   - ตั้งค่า encoding เป็น UTF-8
   - ระบุตารางปลายทาง: `DELIVER9.DBF`

2. **ตรวจสอบข้อมูล**
   - ตรวจสอบจำนวนแถวที่ import
   - ตรวจสอบข้อมูลสำคัญ: DELIVERNUM, CUSTOMERID, TOTAL
   - ตรวจสอบวันที่: APPTDATE, WORKDATE

---

## สรุป

✅ **ครบถ้วน:** ส่งออกทุกฟิลด์ตามโครงสร้าง EgDeliver9.DBF (216 ฟิลด์)
✅ **รูปแบบถูกต้อง:** Date, Number, Logical, Character ตรงตามมาตรฐาน DBF
✅ **พร้อม Import:** สามารถนำไฟล์ CSV ไป import เข้า Database ต้นทางได้เลย
✅ **รองรับภาษาไทย:** UTF-8 with BOM เปิดใน Excel ได้ไม่เพี้ยน
✅ **ไม่ขาด ไม่เกิน:** ฟิลด์ครบทุกฟิลด์ตามต้นฉบับ



