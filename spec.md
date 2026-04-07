# UI Specification: Credit Card Limit Control App
**Design System:** iOS Human Interface Guidelines (HIG) + Google Material Icons
**Typography:** SF Pro Display / SF Pro Text
**Theme:** Light Mode (with iOS standard semantic colors)

## 1. Global Layout & Navigation
* **Navigation Bar:** Large Title แบบ iOS พิมพ์ข้อความ "วงเงินและการใช้จ่าย" 
* **Background:** สี `systemGroupedBackground` (#F2F2F7) 
* **List Style:** `Inset Grouped List` (ขอบมน Corner Radius 12pt, มีช่องว่างซ้ายขวา)
* **Currency Format:** ใช้ `THB` เป็นมาตรฐานเดียวกันทั้งแอป (แสดงผลด้านล่างของตัวเลข หรือต่อท้ายตัวเลขตามความเหมาะสมของพื้นที่)

## 2. Interaction & Behavior (การตอบสนองของระบบ)
* **Dynamic Subtitle Display:** หากเปิดใช้งาน ให้แสดงรายละเอียดที่ตั้งค่าไว้แบบกระชับ (ซ่อนค่าที่ตั้งเป็นสูงสุด)
* **Status Color:** คำว่า "เปิด" ใน Subtitle ให้ใช้สีเขียว (`systemGreen`) เพื่อให้สังเกตสถานะได้ชัดเจนขึ้น ส่วนคำว่า "ปิดใช้งาน" ให้ใช้สีแดง (`systemRed`)
* **Detail View Return:** กด "ตกลง" ในหน้าย่อย จะกลับมาหน้าหลักพร้อมอัปเดตค่า 
* **Global Save & Biometrics Flow:** หน้าหลักมีปุ่ม "บันทึก" (สถานะ Disable) เมื่อมีการเปลี่ยนค่าปุ่มจะเปลี่ยนเป็น Enable -> กดบันทึก -> สแกน Face ID -> แสดง Toast Message "บันทึกการตั้งค่าสำเร็จ" -> ปุ่มกลับเป็น Disable

---

## 3. Screen 1: Main Dashboard (หน้าหลัก)

### 3.1 Selected Card Info (ข้อมูลบัตรที่กำลังตั้งค่า)
* **UI Element:** การ์ดสีขาวขอบมน (Corner Radius 12pt) พร้อมเงาบางๆ (Drop Shadow)
* **Content:**
    * **Image:** รูปภาพกราฟิกบัตรเครดิตจำลองขนาดเล็ก
    * **Title:** ชื่อบัตร (เช่น "KTC Visa Platinum") - ตัวหนา
    * **Subtitle:** หมายเลขบัตรแบบ Masked Format: `xxxx 1234` - สี `systemGray`
    * **Detail:** "วงเงินสูงสุด: 100,000 THB" (Credit Limit) 

### 3.2 Section: 🇹🇭 ใช้จ่ายภายในประเทศ (Domestic)
* **UI Element:** Inset Grouped List
* **Row 1: ช้อปปิ้งออนไลน์**
    * Icon: `shopping_cart` (Google Material Icon) พื้นหลังกลมสีฟ้า
    * Title: ช้อปปิ้งออนไลน์
    * Subtitle: "<span style="color: green;">เปิด</span> • รวม 10,000 THB/ด."
    * Accessory: Chevron (`>`) กดเพื่อไปหน้าตั้งค่า
* **Row 2: รูดซื้อสินค้าหน้าร้าน**
    * Icon: `storefront` (Google Material Icon) พื้นหลังกลมสีฟ้า
    * Title: รูดซื้อสินค้าหน้าร้าน
    * Subtitle: "<span style="color: green;">เปิด</span> • ไม่จำกัด"
    * Accessory: Chevron (`>`)
* **Row 3: แตะจ่าย (Contactless)**
    * Icon: `contactless` (Google Material Icon) พื้นหลังกลมสีฟ้า
    * Title: แตะจ่าย (Contactless)
    * Subtitle: "<span style="color: red;">ปิดใช้งาน</span>" 
    * Accessory: Chevron (`>`)

### 3.3 Section: ✈️ ใช้จ่ายต่างประเทศ (International)
* **UI Element:** Inset Grouped List
* **Row 1: ช้อปปิ้งออนไลน์**
    * Icon: `public` (Google Material Icon) พื้นหลังกลมสีส้ม
    * Title: ช้อปปิ้งออนไลน์
    * Subtitle: "<span style="color: green;">เปิด</span> • รวม 5,000 THB/ด. • 3 ครั้ง/ด."
    * Accessory: Chevron (`>`)
* **Row 2: รูดซื้อสินค้าหน้าร้าน**
    * Icon: `luggage` หรือ `flight_takeoff` (Google Material Icon) พื้นหลังกลมสีส้ม
    * Title: รูดซื้อสินค้าหน้าร้าน
    * Subtitle: "<span style="color: green;">เปิด</span> • รวม 30,000 THB/ด. • สูงสุด 5,000 THB/ครั้ง" 
    * Accessory: Chevron (`>`)
* **Row 3: แตะจ่าย (Contactless)**
    * Icon: `contactless` (Google Material Icon) พื้นหลังกลมสีส้ม
    * Title: แตะจ่าย (Contactless)
    * Subtitle: "<span style="color: green;">เปิด</span> • ไม่จำกัด"
    * Accessory: Chevron (`>`)

### 3.4 Section: ⚙️ ใช้จ่ายบัตรทำธุรกรรมอื่น (Other Transactions)
* **UI Element:** Inset Grouped List
* **Row 1: ถอนเงินสด**
    * Icon: `atm` (Google Material Icon) พื้นหลังกลมสีเขียว
    * Title: ถอนเงินสด
    * Control: `UISwitch` (Toggle) สถานะ = เปิด (On)
* **Row 2: ผูกบัตรและบริการรายเดือน**
    * Icon: `subscriptions` (Google Material Icon) พื้นหลังกลมสีม่วง
    * Title: ผูกบัตรและบริการรายเดือน
    * Control: `UISwitch` (Toggle) สถานะ = เปิด (On)

### 3.5 Sticky Action Button (ส่วนบันทึกการตั้งค่า)
* **UI Element:** ปุ่มขนาดใหญ่ (Primary Button) วางตรึงไว้ด้านล่างสุดของหน้าจอ (Safe Area)
* **Text:** "บันทึก" (Save)

---

## 4. Screen 2: Detail Setting View (หน้าย่อยตั้งค่า - ตัวอย่าง: ช้อปปิ้งออนไลน์)
* **Navigation Bar:** Title "ช้อปปิ้งออนไลน์" และปุ่ม "ตกลง" (OK) ที่มุมขวาบน
* **Section 1: สถานะการใช้งาน**
    * Row: "อนุญาตการใช้งาน" 
    * Control: `UISwitch` (เปิด/ปิด หลัก)

* **Section 2: การจำกัดวงเงินและความถี่ (Limit & Frequency Controls)**
    * *กฎทั่วไป:* เมื่อผู้ใช้กดที่ตัวเลขเพื่อแก้ไข ระบบต้องแสดง **Numeric Keyboard (Number Pad)** ขึ้นมาให้กรอกตัวเลขโดยตรง

    * **Row 1: วงเงินรวมต่อเดือน (Monthly Limit)**
        * Text Field: แสดงตัวเลขยอดเงิน (มีคำว่า THB วางไว้ด้านล่างหรือต่อท้าย)
        * Control: `UISlider` แบบมีปุ่มไอคอนลบ `-` ที่ปลายด้านซ้าย และปุ่มไอคอนบวก `+` ที่ปลายด้านขวา (สำหรับแตะเพิ่ม/ลดค่าทีละ Step)
        * Labels กำกับ Slider: 
            * ฝั่งซ้าย: "1 (ต่ำสุด)"
            * ฝั่งขวา: "[วงเงินสูงสุดของบัตร] (สูงสุด)"
            
    * **Row 2: ยอดสูงสุดต่อรายการ (Max per Transaction)**
        * Text Field: แสดงตัวเลขยอดเงิน (มีคำว่า THB)
        * Control: `UISlider` แบบมีปุ่ม `-` และ `+`
        * Labels กำกับ Slider:
            * ฝั่งซ้าย: "1 (ต่ำสุด)"
            * ฝั่งขวา: "[วงเงินสูงสุดของบัตร] (สูงสุด)"
            
    * **Row 3: จำนวนรายการต่อเดือน (Transactions per month)**
        * Text Field: แสดงตัวเลข (มีคำว่า "ครั้ง" วางไว้ด้านล่างหรือต่อท้าย)
        * Control: `UISlider` แบบมีปุ่ม `-` และ `+` (เปลี่ยนจาก Stepper เดิมมาใช้ Slider ให้สอดคล้องกัน)
        * Labels กำกับ Slider:
            * ฝั่งซ้าย: "1 (ต่ำสุด)"
            * ฝั่งขวา: "999 (สูงสุด / ไม่จำกัด)" *(หมายเหตุ: หากผู้ใช้เลื่อนไปที่ 999 ระบบจะตีความว่า "ไม่จำกัด")*

* **Section 3: Footer Note**
    * ข้อความอธิบายเงื่อนไขการใช้งาน (ฟอนต์ขนาดเล็ก สี `systemGray`)