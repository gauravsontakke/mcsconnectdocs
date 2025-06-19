
# 🌐 Website Layout Structure for MCS Flutter App

This section outlines how the Flutter app's mobile UI translates into a structured, responsive website layout.

---

## 🏠 Home Page (`/`)

### Components:
- 🔍 **Search Bar** – Search for Offers, Business, Jobs
- 🖼 **Highlights Carousel** – E.g. "Hotel Offers"
- 🔘 **Navigation Grid**:
  - NRI Jobs, Items for Sale, MCS Offers, Business Services
  - Travel Assistance, All Events, MCS  News, MCS Help Line
- 🏢 **Featured Mandals** – Horizontal scroll or grid
- 🗞 **Marathi News Papers** – Grid layout
- 📋 **Job Listings**, **Marketplace Items**, **B2B Offers**

---

## 👥 Mandal Listing Page (`/mandals`)

- **Search Bar**: by Name, City, Country
- **Cards**: Image, Title, Location, CTA (e.g., View)

---

## 📄 Mandal Details Page (`/mandals/:id`)

### Sections:
- 🏷 **Header**: Mandal Name (e.g., Maharashtra Mandal Qatar)
- 🧾 **About Us**
- 📍 **Address**
- 📞 **Contact Info**: Phone, Email, Fax
- 🎥 **Intro Video Link**
- 🔗 **Social Media Icons**

---

## 🧾 Business Directory Page (`/business`)

### Features:
- 🔘 Filter Tabs: All, Web Development, Import, Export…
- 🔍 Search
- 🏪 Business Cards:
  - Logo/Image, Title, Location
  - Category (Web Development, Grocery, etc.)
  - Offer (e.g., Get 10% upto 15%)
  - CTA Button (GET or View)

---

## 📅 Events Page (`/events`)

### List of Events:
- 📅 Title
- 🗺 Location with map pin
- 🕒 Date & Time
- ✅ Interested Button
- 🎟 Logo/Image (optional)

---

## 💬 MCS Help/Chat Page (`/help`)

- Chat interface with messages aligned left/right
- Avatar (optional)
- Input text field at the bottom

---

## 📱 Mobile Bottom Navigation

- महाराष्ट्र मंडळ
- Events
- Home
- Marketplace
- Business

Convert this into a top navbar or side menu on desktop screens.

---

## ✅ Suggestions for Web Version

- Use `go_router` or `auto_route` (for Flutter Web)
- For responsive layout: `LayoutBuilder`, `MediaQuery`, or `flutter_screenutil`
- Separate `mobile/`, `tablet/`, and `desktop/` widgets for layout flexibility
