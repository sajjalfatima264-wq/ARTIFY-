
🎨 Artify Hub: Curated Excellence for Every Level of Art

Artify Hub is a premium digital platform meticulously designed to elevate the art world. By providing a sophisticated and seamless online experience, the platform promotes artists ranging from emerging talents to established professionals.

---

 📖 Project Overview

The mission of Artify Hub is to provide a **"Curated Excellence"** experience. It utilizes a high-end interface to connect artists with discerning art lovers, emphasizing both artistic brilliance and accessibility.

### Visual Identity & UI

*   **Typography:** Built with **Playfair Display** and **Montserrat** for a professional aesthetic.
*   **Theme:** A luxurious **gold (#d4af37) and dark-gray** color palette.
*   **Design Style:** Features an elegant **glass-morphism UI** to provide an immersive browsing environment for users.

---

## 👥 User Roles

Artify Hub features a centralized portal catering to three distinct roles to ensure a tailored experience for everyone:

### 1. Artist Portal
Empowering creators with a secure and private dashboard to manage their digital presence:
*   **New Submissions:** Easily upload and showcase artworks to a global gallery. (`artist_upload.php`)
*   **Order Management:** A real-time "Incoming Requests" system to approve or reject customer orders. (`artist_requests.php`)
*   **Portfolio Tracking:** Tools to monitor curated collections and sales history. (`view_my_art.php`)
*   **Direct Support:** Integrated systems for immediate assistance with queries. (`file_complaint.php`)

### 2. Customer Experience
Designed for seamless discovery and engagement with high-fidelity viewing:
*   **Art Discovery:** Explore a main gallery to find pieces that match personal aesthetic goals. (`main_gallery.php`)
*   **Purchase History:** Transparent tracking of all past acquisitions. (`purchase_history.php`)
*   **Secure Authentication:** Personal accounts for secure profile management and long-term gallery relationships.

### 3. Administrative Control
The "central nervous system" of the platform, providing full **CRUD** (Create, Read, Update, Delete) capabilities:
*   **Data Control:** Management of records for artists, artworks, customers, and exhibitions.
*   **Gallery Governance:** Tools to add, search, and delete content to maintain curation standards.
*   **Analytics & Reporting:** Access to system statistics and growth reports for strategic decision-making. (`admin_report.php`)
*   **Support & Relations:** Oversight of complaints and community relationship management.

---

## 🖼️ Exhibition Management
Artify Hub bridges the gap between artists and collectors through curated shows and dynamic events:
*   **Scheduled Events:** Dedicated exhibitions highlighting specific themes or time-bound collections. (`einsert.php`)
*   **Artist Integration:** Creators can assign specific works to curated shows to increase visibility. (`assign_art.php`)
*   **Dynamic Access:** A "Hero" section with quick-access buttons to drive traffic to new exhibitions. (`FrontEnd.php`)

---

## 🛠️ Tech Stack
*   **Backend:** PHP 7+
*   **Database:** MySQL
*   **Frontend:** HTML5, CSS3 (Custom Glassmorphism Design), JavaScript
*   **Styling:** Montserrat & Playfair Display Fonts

---

## 🚀 Installation & Setup

### 1. Database Setup

**Step A: Import the Main Database**
Run the initial SQL dump provided in the repository (`art_gallery.sql`). This creates all tables (`artist`, `customer`, `exhibition`, `gallery`, `artwork`) and seeds default data.

**Step B: Run Critical Updates (For New Features)**
Since we added **"Sold/Available Status"**, **"Exhibition Titles"**, and **"User Authentication"** during development, you **must** run these commands in your PHPMyAdmin/Database terminal for the site to work correctly:

```sql
-- 1. Add Exhibition Title Column (Required for Exhibitions List)
ALTER TABLE exhibition ADD ename VARCHAR(100) AFTER gid;

-- 2. Add Status Column (Required for "Sold" badge logic and overselling prevention)
ALTER TABLE artwork ADD COLUMN status VARCHAR(20) DEFAULT 'Available';

-- 3. Add Photo Column (If missing from old dump)
ALTER TABLE artwork ADD COLUMN photo VARCHAR(255);

-- 4. Add Username/Password to Customer (For Login System)
ALTER TABLE customer ADD COLUMN username VARCHAR(50) UNIQUE, ADD COLUMN password VARCHAR(255);
```

### 2. Configuration
Open `connection.php` and update your database credentials:

```php
$conn = new mysqli("localhost", "root", "", "art_gallery");
```

### 3. Directory Permissions
Ensure you have a folder named **`Images/`** in your root directory.
*   **Location:** `ARTIFY/Images/`
*   **Permissions:** This folder must be writable (chmod 777 or 755) so Artists can upload photos.

---

## 🔑 Login Credentials

### 1. Admin Login
> **Username:** `admin`  
> **Password:** `admin123`

### 2. Artist Login (Sample Data)
> **Username:** `ART1` (or check `artist` table)  
> **Password:** `password` (Default seeded in SQL)

### 3. Customer Login
You can register a new customer via the "Customer Login" page or use seeded data from the SQL dump.

---

## 📂 Project Structure
```
/ARTIFY
├── /Images                  # Stores uploaded artwork images
├── admin_dashboard.php     # Admin Control Panel
├── FrontEnd.php            # Main Landing Page & Dashboard Router
├── main_gallery.php        # Public Gallery with Smart Filters
├── exhibitions_list.php    # Public Exhibition List
├── buy_artwork.php         # Purchase Request Page
├── process_purchase.php    # Backend Logic for Sales (Anti-Overselling)
├── assign_art.php          # Artist assigns art to exhibition
├── connection.php          # DB Config
└── /css & /fonts           # Assets
```

---

## 🌟 Key Features Implemented
1.  **Smart Gallery:** Dynamic sidebar filters (Type, Price, Search) that adapt to database content.
2.  **Exhibition Logic:** Admins create shows; Artists assign art; Customers view curated collections.
3.  **Sales Logic:** "Sold" / "Available" status management using MySQL Transactions to prevent overselling.
4.  **Glassmorphism UI:** Consistent high-end design across all user dashboards.

---

## 🐛 Common Troubleshooting

**1. Images not displaying?**
- Check if `Images/` folder exists in the same directory as your PHP files.
- Ensure `move_uploaded_file` is pointing to the correct folder path.

**2. "Undefined index: id" error?**
- Ensure you are logged in as the correct user type (e.g., trying to access Artist tools while logged in as Admin).

**3. Filter Bar looks misaligned?**
- Ensure you are using the updated CSS with `flex-basis: 0` and `* { box-sizing: border-box; }`.

**4. "Exhibition not found" or Dropdown empty?**
- Did you run the `ALTER TABLE` commands in Step 1B?
- Ensure you have logged in as an Artist to assign art *before* looking for it in the Exhibition View.

---

## 📄 License
This project is created for educational purposes.

© 2022 Artify Hub. All rights reserved.
