# Smart-AI-Cricket-Paddle-Booking-Receptionist
# 🏏 Cricket/Paddle Booking Bot (n8n Workflow)

## 📌 Overview
This is a **full-featured booking system** built with [n8n](https://n8n.io).  
It manages **availability checking, booking requests, user detail collection, and admin notifications** through **Telegram**.

The workflow uses:
- **Telegram Bot** – user interaction
- **Google Sheets** – booking storage & availability management
- **Gemini API** – AI-powered intent recognition and detail extraction
- **Automated Admin Notifications** – for confirmed bookings

---

## ✨ Features
- 📲 **Telegram Bot Interface** – `/start`, `/availability`, `/rates`, `/help` commands  
- 📅 **Availability Checking** – dynamically checks Google Sheets for booked slots  
- 🧠 **AI Intent Analysis** – understands natural language booking requests  
- ✅ **Conflict Validation** – prevents double bookings  
- 👤 **User Detail Collection** – gathers name, phone, and player count  
- 🎉 **Booking Confirmation** – sends final confirmation with booking ID  
- 📢 **Admin Notifications** – alerts admin of new confirmed bookings  

---

## 🗂️ Workflow Structure
1. **Telegram Trigger** – listens for incoming messages  
2. **Quick Commands** – handles `/availability`, `/rates`, `/help`  
3. **AI Intent Analyzer (Gemini API)** – classifies user request  
4. **Validate Booking Request** – checks availability in Google Sheets  
5. **Pending Booking** – saves temporary booking until details are provided  
6. **User Details Extraction (Gemini API)** – parses user’s info  
7. **Booking Confirmation** – generates booking ID, cost, and confirmation message  
8. **Save Booking** – writes to `Bookings` sheet  
9. **Admin Notification** – sends booking summary to admin Telegram chat  

---

## 🛠️ Setup Instructions

### 1. Prerequisites
- An [n8n](https://n8n.io) instance (self-hosted or cloud)  
- A Telegram bot (via [@BotFather](https://t.me/botfather))  
- Google Sheets API credentials  
- Gemini API key (for AI processing)  

### 2. Import Workflow
- Open n8n → **Workflows → Import from File**  
- Select the provided JSON file  

### 3. Configure Environment Variables
Update the following fields in your workflow:
- `YOUR_GOOGLE_SHEET_ID` → ID of your Google Sheet  
- `YOUR_GEMINI_API_KEY` → Gemini API key  
- `ADMIN_TELEGRAM_CHAT_ID` → Telegram chat ID of admin  

### 4. Google Sheets Setup
Create two sheets:
- **Bookings** – confirmed bookings  
  - Columns: `Booking ID, Date, Start Time, Duration, Customer Name, Phone, Players, Cost, Status, User ID, Booked At`  
- **PendingBookings** – temporary reservations  
  - Columns: `Timestamp, User ID, Username, Date, Time, Duration, Cost, Status, Chat ID`  

### 5. Activate Workflow
- Turn **Active** to `true` in n8n  
- Start chatting with your Telegram bot to test  

---

## 📖 Example Interaction
```
User: /start
Bot: Welcome! Here are our rates and availability.

User: Book for tomorrow 6 PM
Bot: ✅ Great! Slot available.
      Please provide: Full Name, Phone, Players

User: John Doe, +123456789, 6
Bot: 🎉 Booking Confirmed!
      Booking ID: BCB12345678
      Date: 2025-08-25, Time: 6 PM
      Total Cost: $45

(Admin receives booking notification)
```

---

## 🚀 Future Enhancements
- Payment integration (Stripe/PayPal)  
- Multi-location support  
- Automatic reminders (24h before booking)  
- Cancellation & rescheduling options  

---

## 📄 License
This workflow is provided as-is under the **MIT License**.  
Feel free to modify and extend for your use case.  
