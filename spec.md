# UI Specification: Credit Card Limit Control App
**Design System:** iOS Human Interface Guidelines (HIG) + Google Material Icons
**Typography:** SF Pro Display / SF Pro Text
**Theme:** Light Mode (with iOS standard semantic colors)

## 1. Global Layout & Navigation
* **Navigation Bar:** Large Title แบบ iOS พิมพ์ข้อความ "วงเงินและการใช้จ่าย" 
* **Background:** สี `systemGroupedBackground` (#F2F2F7) 
* **List Style:** `Inset Grouped List` (ขอบมน Corner Radius 12pt, มีช่องว่างซ้ายขวา)

## 2. Interaction & Behavior (การตอบสนองของระบบ)
* **Dynamic Subtitle Display:** สำหรับหมวดช้อปปิ้งออนไลน์, ร้านค้า และ Cashless หากเปิดใช้งาน ให้แสดงรายละเอียดการตั้งค่าเฉพาะส่วนที่ "ถูกจำกัด" (ตั้งค่าต่ำกว่าค่าสูงสุด) ด้วยรูปแบบที่สั้นและกระชับ หากค่าใดตั้งไว้สูงสุดให้ซ่อนค่านั้นไป (ถือว่าไม่จำกัด)
    * *ตัวอย่าง 1 (ถูกจำกัดแค่รายเดือน):* "เปิด • รวม 10,000 THB/ด."
    * *ตัวอย่าง 2 (ถูกจำกัดรายเดือนและต่อครั้ง):* "เปิด • รวม 20,000 THB/ด. • สูงสุด 5,000 THB/ครั้ง"
    * *ตัวอย่าง 3 (ถูกจำกัดทั้งหมด):* "เปิด • รวม 10,000 THB/ด. • สูงสุด 2,000 THB/ครั้ง • 5 ครั้ง/ด."
    * *ตัวอย่าง 4 (ไม่ได้จำกัดอะไรเลย):* "เปิด • ไม่จำกัด"
* **Detail View Return:** เมื่อผู้ใช้ปรับค่าใน "หน้าย่อย (Screen 2)" และกดปุ่ม "ตกลง" ระบบจะพากลับมาที่ "หน้าหลัก (Screen 1)" ทันที โดยค่าที่เลือกจะอัปเดตแสดงผลในหน้าหลัก (เป็นสถานะ Draft)
* **Global Save & Biometrics Flow:** * หน้าหลักจะมีปุ่ม "บันทึก" อยู่ด้านล่างสุด สถานะเริ่มต้นคือ **Disable** (กดไม่ได้)
    * เมื่อผู้ใช้มีการเปลี่ยนค่าใดๆ ก็ตาม (เปิด/ปิด Switch หรือกลับมาจากหน้าตั้งค่า) ปุ่ม "บันทึก" จะเปลี่ยนสถานะเป็น **Enable**
    * เมื่อกด "บันทึก" ระบบจะแสดงหน้าจอจำลอง **Face ID / Biometric Scan** * เมื่อสแกนผ่าน จะแสดง **Toast Message** (iOS HUD Style) ตรงกลางจอเป็นเวลา 3 วินาทีว่า "บันทึกการตั้งค่าสำเร็จ"
    * หลังจากนั้น ปุ่ม "บันทึก" จะกลับไปเป็นสถานะ **Disable** อีกครั้ง

---

## 3. Screen 1: Main Dashboard (หน้าหลัก)

### 3.1 Selected Card Info (ข้อมูลบัตรที่กำลังตั้งค่า)
* **UI Element:** การ์ดสีขาวขอบมน (Corner Radius 12pt) พร้อมเงาบางๆ (Drop Shadow)
* **Content:**
    * **Image:** รูปภาพกราฟิกบัตรเครดิตจำลองขนาดเล็ก (Mini Card) วางฝั่งซ้าย
    * **Title:** ชื่อบัตร (เช่น "KTC Visa Platinum") - ตัวหนา
    * **Subtitle:** หมายเลขบัตรแบบ Masked (เช่น `**** **** **** 1234`) - สี `systemGray`
    * **Detail:** "วงเงินสูงสุด: 100,000 THB" (Credit Limit) - วางตำแหน่งมุมขวาหรือบรรทัดล่างสุดให้เห็นชัดเจน

### 3.2 Section: 🇹🇭 ใช้จ่ายภายในประเทศ (Domestic)
* **UI Element:** Inset Grouped List
* **Row 1: ช้อปปิ้งออนไลน์**
    * Icon: `shopping_cart` (Google Material Icon) พื้นหลังกลมสีฟ้า
    * Title: ช้อปปิ้งออนไลน์
    * Subtitle: "เปิด • รวม 10,000 THB/ด." *(ซ่อนการแสดงยอดต่อครั้ง/จำนวนครั้ง เพราะตั้งค่าไว้สูงสุด)*
    * Accessory: Chevron (`>`) กดเพื่อไปหน้าตั้งค่า
* **Row 2: ช้อปปิ้งผ่านร้านค้า**
    * Icon: `storefront` (Google Material Icon) พื้นหลังกลมสีฟ้า
    * Title: รูดซื้อสินค้าหน้าร้าน
    * Subtitle: "เปิด • ไม่จำกัด" *(ตั้งค่าไว้สูงสุดทั้งหมด)*
    * Accessory: Chevron (`>`)
* **Row 3: Cashless / Contactless**
    * Icon: `contactless` (Google Material Icon) พื้นหลังกลมสีฟ้า
    * Title: แตะจ่าย (Contactless)
    * Subtitle: "ปิดใช้งาน" (Text สี `systemRed`)
    * Accessory: Chevron (`>`)

### 3.3 Section: ✈️ ใช้จ่ายต่างประเทศ (International)
* **UI Element:** Inset Grouped List
* **Row 1: ช้อปปิ้งออนไลน์**
    * Icon: `public` (Google Material Icon) พื้นหลังกลมสีส้ม
    * Title: ช้อปปิ้งออนไลน์ (ต่างประเทศ)
    * Subtitle: "เปิด • รวม 5,000 THB/ด. • 3 ครั้ง/ด." *(ซ่อนยอดต่อครั้ง)*
    * Accessory: Chevron (`>`)
* **Row 2: ช้อปปิ้งผ่านร้านค้า**
    * Icon: `luggage` หรือ `flight_takeoff` (Google Material Icon) พื้นหลังกลมสีส้ม
    * Title: รูดซื้อสินค้าหน้าร้าน (ต่างประเทศ)
    * Subtitle: "เปิด • รวม 30,000 THB/ด. • สูงสุด 5,000 THB/ครั้ง" 
    * Accessory: Chevron (`>`)
* **Row 3: Cashless / Contactless**
    * Icon: `contactless` (Google Material Icon) พื้นหลังกลมสีส้ม
    * Title: แตะจ่าย (Contactless)
    * Subtitle: "เปิด • ไม่จำกัด"
    * Accessory: Chevron (`>`)

### 3.4 Section: ⚙️ ใช้จ่ายบัตรทำธุรกรรมอื่น (Other Transactions)
* **UI Element:** Inset Grouped List
* **Row 1: บัตรถอนเงินสด (Cash Advance)**
    * Icon: `atm` (Google Material Icon) พื้นหลังกลมสีเขียว
    * Title: ถอนเงินสด
    * Control: `UISwitch` (Toggle) สถานะ = เปิด (On)
* **Row 2: ผูกบัตรกับร้านค้า/อุปกรณ์ (Device & Subscriptions)**
    * Icon: `subscriptions` (Google Material Icon) พื้นหลังกลมสีม่วง
    * Title: ผูกบัตรและบริการรายเดือน
    * Control: `UISwitch` (Toggle) สถานะ = เปิด (On)

### 3.5 Sticky Action Button (ส่วนบันทึกการตั้งค่า)
* **UI Element:** ปุ่มขนาดใหญ่เต็มความกว้าง (Primary Button) วางตรึงไว้ด้านล่างสุดของหน้าจอ (Safe Area)
* **Text:** "บันทึก" (Save)
* **State:** Disabled (สีเทา) เป็นค่าเริ่มต้น

---

## 4. Screen 2: Detail Setting View (หน้าย่อยตั้งค่า - ตัวอย่าง: ช้อปปิ้งออนไลน์)
* **Navigation Bar:** Title "ช้อปปิ้งออนไลน์" และปุ่ม "ตกลง" (OK) ที่มุมขวาบน
* **Section 1: สถานะการใช้งาน**
    * Row: "อนุญาตการใช้งาน" (Enable Online Shopping)
    * Control: `UISwitch` (เปิด/ปิด หลัก)
* **Section 2: การจำกัดวงเงิน (Limit Controls)**
    * **Row 1: วงเงินรวมต่อเดือน (Monthly Limit)**
        * Text Field ให้กรอกตัวเลข พร้อมหน่วย "THB"
        * Control: `UISlider` สำหรับปรับจำนวนเงิน มีข้อความกำกับ "0" ฝั่งซ้าย และ "สูงสุด" ฝั่งขวา
    * **Row 2: ยอดสูงสุดต่อรายการ (Max per Transaction)**
        * Text Field ให้กรอกตัวเลข พร้อมหน่วย "THB"
        * Control: `UISlider` สำหรับปรับจำนวนเงินแบบเดียวกับด้านบน มีข้อความกำกับ "0" ฝั่งซ้าย และ "สูงสุด" ฝั่งขวา
* **Section 3: การจำกัดความถี่ (Frequency Controls)**
    * **Row 1: จำนวนรายการต่อเดือน (Transactions per month)**
        * Control: `UIStepper` (- / +) แสดงตัวเลขตรงกลาง พร้อมหน่วย "ครั้ง" (หากบวกไปจนสุดให้แสดงคำว่า "ไม่จำกัด")
* **Section 4: Footer Note**
    * ข้อความอธิบายเงื่อนไขการใช้งาน (ฟอนต์ขนาดเล็ก สี `systemGray`) วางไว้ใต้ List