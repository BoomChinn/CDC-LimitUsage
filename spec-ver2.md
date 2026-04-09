# UI Specification: Credit Card Management & Limit Control App
**Design System:** iOS Human Interface Guidelines (HIG) + Google Material Icons
**Typography:** SF Pro Display / SF Pro Text
**Theme:** Light Mode (with iOS standard semantic colors)

## 1. Global Layout & Navigation Structure
* **App Hierarchy:** 1. `หน้าตั้งค่าบัตรเครดิต` (Root: Card Settings) -> 
    2. `หน้าจัดการวงเงินและค่าใช้จ่าย` (Limit Dashboard) -> 
    3. `หน้าตั้งค่าย่อยรายหมวด` (Detail Limit Setting)
* **Background:** สี `systemGroupedBackground` (#F2F2F7)
* **List Style:** `Inset Grouped List` (ขอบมน Corner Radius 12pt)
* **Currency Format:** ใช้ `THB` เป็นมาตรฐาน (แสดงผลด้านล่างของตัวเลข หรือต่อท้ายตัวเลข)
* **Card Format:** `xxxx 1234`

---

## 2. Interaction & Behavior (การตอบสนองของระบบ)
* **Card Lock Dependency (ฟีเจอร์ล็อคบัตร):** * เมื่อผู้ใช้กด "ล็อคบัตรเครดิต" ที่หน้าแรก (Screen 1) สถานะของบัตรจะถูกระงับ
    * หากกดเข้ามาที่ "จัดการวงเงินและค่าใช้จ่าย" (Screen 2) ระบบจะแสดง **Information Banner** แถบสีเหลือง/เทา ด้านบนสุด เพื่อแจ้งเตือน และ **Disable** (ทำเป็นสีเทา กดไม่ได้) เมนูและ Switch ทั้งหมดในหน้านั้น เพื่อให้รู้ว่าไม่มีผลใดๆ จนกว่าจะปลดล็อค
* **Dynamic Subtitle Display:** หากฟีเจอร์เปิดใช้งาน ให้ใช้ Text สีเขียว (`systemGreen`) และแสดงรายละเอียดที่ถูกจำกัด หากปิดใช้งานให้ใช้สีแดง (`systemRed`) และแสดงคำว่า "ปิดใช้งาน"
* **Global Save & Biometrics Flow (อัปเดตใหม่):** * เมื่อผู้ใช้อยู่ที่หน้า "จัดการวงเงินและค่าใช้จ่าย" (Screen 2) และมีการเปลี่ยนค่า ปุ่ม "บันทึก" จะ Enable
    * เมื่อกด "บันทึก" -> ระบบแสดง **Face ID / Biometric Scan**
    * เมื่อสแกนผ่าน -> **เด้งกลับไปที่หน้าแรก "ตั้งค่าบัตรเครดิต" (Screen 1) ทันที**
    * แสดง **Toast Message** (iOS HUD Style) ตรงกลางหน้าจอ Screen 1 ว่า "บันทึกการตั้งค่าสำเร็จ" เป็นเวลา 3 วินาที

---

## 3. Screen 1: ตั้งค่าบัตรเครดิต (Credit Card Settings - หน้าแรกสุด)
*อ้างอิงจาก Global Banking App Standard (เน้นเข้าถึงง่าย จัดการความปลอดภัยรวดเร็ว)*

* **Navigation Bar:** Large Title "ตั้งค่าบัตรเครดิต"

### 3.1 Selected Card Info (ข้อมูลบัตร)
* **UI Element:** การ์ดสีขาวขอบมน (Corner Radius 12pt) มี Drop Shadow
* **Content:**
    * **Image:** รูปภาพกราฟิกบัตรเครดิตจำลองขนาดเล็ก
    * **Title:** ชื่อบัตร (เช่น "KTC Visa Platinum") - ตัวหนา
    * **Subtitle:** `xxxx 1234` - สี `systemGray`
    * **Detail:** "วงเงินสูงสุด: 100,000 THB" 

### 3.2 Section: 🛡️ การจัดการและความปลอดภัย (Card Management)
* **UI Element:** Inset Grouped List
* **Row 1: ล็อคบัตรเครดิต (Freeze / Lock Card)**
    * Icon: `lock` (Google Material Icon) พื้นหลังกลมสีแดง
    * Title: ล็อคบัตรเครดิต
    * Subtitle: "ระงับการใช้งานชั่วคราว"
    * Control: `UISwitch` (Toggle) 
* **Row 2: จัดการวงเงินและค่าใช้จ่าย (Limit & Controls)**
    * Icon: `tune` หรือ `speed` (Google Material Icon) พื้นหลังกลมสีฟ้า
    * Title: จัดการวงเงินและค่าใช้จ่าย
    * Accessory: Chevron (`>`) *กดเพื่อไป Screen 2*
* **Row 3: ดูรหัส PIN (View PIN)** *(อิงจาก Global App)*
    * Icon: `dialpad` (Google Material Icon) พื้นหลังกลมสีเทา
    * Title: ดูรหัส PIN ของบัตร
    * Accessory: Chevron (`>`)
* **Row 4: อายัด/ออกบัตรใหม่ (Report Lost or Stolen)** *(อิงจาก Global App)*
    * Icon: `credit_card_off` (Google Material Icon) พื้นหลังกลมสีส้ม
    * Title: อายัดและขอออกบัตรใหม่
    * Accessory: Chevron (`>`)

---

## 4. Screen 2: วงเงินและการใช้จ่าย (Limit Dashboard)
*เข้าผ่านเมนู "จัดการวงเงินและค่าใช้จ่าย" จากหน้าแรก*

* **Navigation Bar:** Title "วงเงินและการใช้จ่าย" พร้อมปุ่ม `< ตั้งค่าบัตร`

### 4.1 Information Banner (แสดงเฉพาะเมื่อบัตรถูกล็อค)
* **UI Element:** แถบยาวขอบมน พื้นหลังสี `systemYellow` (อ่อนๆ) หรือ `systemGray4` 
* **Icon:** `info` (Google Material Icon) สีเทาเข้ม
* **Text:** "บัตรถูกล็อคอยู่ คุณไม่สามารถตั้งค่าหรือปรับเปลี่ยนวงเงินได้ในขณะนี้"
* *Behavior:* หากแสดง Banner นี้ ลิสต์รายการด้านล่างทั้งหมด (4.2 - 4.4) จะถูกลด Opacity เหลือ 50% (Disabled State) และกดไม่ได้

*(ลิสต์ด้านล่างนี้จะแสดงผลและใช้งานได้ปกติ เมื่อบัตรไม่ได้ถูกล็อค)*

### 4.2 Section: 🇹🇭 ใช้จ่ายภายในประเทศ (Domestic)
* **UI Element:** Inset Grouped List
* **Row 1: ช้อปปิ้งออนไลน์**
    * Icon: `shopping_cart` (พื้นหลังกลมสีฟ้า)
    * Title: ช้อปปิ้งออนไลน์
    * Subtitle: "<span style="color: green;">เปิด</span> • รวม 10,000 THB/ด."
    * Accessory: Chevron (`>`)
* **Row 2: รูดซื้อสินค้าหน้าร้าน**
    * Icon: `storefront` (พื้นหลังกลมสีฟ้า)
    * Title: รูดซื้อสินค้าหน้าร้าน
    * Subtitle: "<span style="color: green;">เปิด</span> • ไม่จำกัด"
    * Accessory: Chevron (`>`)
* **Row 3: แตะจ่าย (Contactless)**
    * Icon: `contactless` (พื้นหลังกลมสีฟ้า)
    * Title: แตะจ่าย (Contactless)
    * Subtitle: "<span style="color: red;">ปิดใช้งาน</span>" 
    * Accessory: Chevron (`>`)

### 4.3 Section: ✈️ ใช้จ่ายต่างประเทศ (International)
* **UI Element:** Inset Grouped List
* *(โครงสร้างเดียวกับ 4.2 แต่เปลี่ยนไอคอนเป็นรูปลูกโลก/เครื่องบิน พื้นหลังสีส้ม)*

### 4.4 Section: ⚙️ ใช้จ่ายบัตรทำธุรกรรมอื่น (Other Transactions)
* **UI Element:** Inset Grouped List
* **Row 1: ถอนเงินสด** (Icon: `atm` สีเขียว | Control: `UISwitch`)
* **Row 2: ผูกบัตรและบริการรายเดือน** (Icon: `subscriptions` สีม่วง | Control: `UISwitch`)

### 4.5 Sticky Action Button (ส่วนบันทึกการตั้งค่า)
* **UI Element:** ปุ่มขนาดใหญ่ (Primary Button) ตรึงไว้ด้านล่างสุด (Safe Area)
* **Text:** "บันทึก" (Save)
* **State:** Disabled (สีเทา) เป็นค่าเริ่มต้น จะเปลี่ยนเป็น Enable (สีกดได้) เมื่อมีการปรับเปลี่ยนค่า

---

## 5. Screen 3: Detail Setting View (หน้าย่อยตั้งค่า - ตัวอย่าง: ช้อปปิ้งออนไลน์)
* **Navigation Bar:** Title "ช้อปปิ้งออนไลน์" และปุ่ม "ตกลง" (OK) ที่มุมขวาบน

* **Section 1: สถานะการใช้งาน**
    * Row: "อนุญาตการใช้งาน" 
    * Control: `UISwitch` (เปิด/ปิด หลัก)

* **Section 2: การจำกัดวงเงินและความถี่ (Limit & Frequency Controls)**
    * *กฎทั่วไป:* แตะที่ตัวเลข -> แสดง **Numeric Keyboard (Number Pad)** ทันที
    * **Row 1: วงเงินรวมต่อเดือน (Monthly Limit)**
        * Text Field: แสดงตัวเลขยอดเงิน (พร้อม THB)
        * Control: `UISlider` มีปุ่ม `-` (ซ้าย) และ `+` (ขวา)
        * Labels: ฝั่งซ้าย "1 (ต่ำสุด)", ฝั่งขวา "[วงเงินสูงสุด] (สูงสุด)"
    * **Row 2: ยอดสูงสุดต่อรายการ (Max per Transaction)**
        * Text Field: แสดงตัวเลขยอดเงิน (พร้อม THB)
        * Control: `UISlider` มีปุ่ม `-` (ซ้าย) และ `+` (ขวา)
        * Labels: ฝั่งซ้าย "1 (ต่ำสุด)", ฝั่งขวา "[วงเงินสูงสุด] (สูงสุด)"
    * **Row 3: จำนวนรายการต่อเดือน (Transactions per month)**
        * Text Field: แสดงตัวเลข (พร้อมคำว่า "ครั้ง")
        * Control: `UISlider` มีปุ่ม `-` (ซ้าย) และ `+` (ขวา)
        * Labels: ฝั่งซ้าย "1 (ต่ำสุด)", ฝั่งขวา "999 (สูงสุด / ไม่จำกัด)" 

* **Section 3: Footer Note**
    * ข้อความอธิบายเงื่อนไขการใช้งาน (สี `systemGray`)