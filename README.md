# Titans Clinic

A full-stack healthcare platform connecting clinics and pharmacies, built with the MERN stack. Patients, doctors, pharmacists, and admins each have dedicated portals with role-based access. The system handles appointment booking, prescriptions, medication ordering, real-time chat, Stripe payments, and health package subscriptions.

## Features

### Patient
- Register/login with JWT authentication and OTP-based password reset via email
- Browse doctors by specialty and book appointments from available slots
- View and manage medical history
- Subscribe to health packages (with family member discounts)
- Real-time chat with doctors via Socket.io
- Pay for appointments and medications via Stripe
- Purchase prescriptions directly from the pharmacy module
- Download prescriptions as PDF

### Doctor
- Manage available appointment slots
- Reschedule, cancel, or assign follow-up appointments
- Issue prescriptions linked to patient records
- Real-time chat with patients
- View wallet balance and transaction history
- Accept or reject employment contracts

### Admin
- Approve/reject doctor registration requests
- Add/remove users and administrators
- Manage health care packages (add, edit, delete)
- View all registered users

### Pharmacy (linked system)
- Shared patient database with clinic — no separate registration needed
- Real-time notifications for new prescriptions

## Tech Stack

**Backend:** Node.js, Express.js, MongoDB, Mongoose, JWT, bcryptjs, Socket.io, Nodemailer, Stripe, PDFKit, Multer  
**Frontend:** React, Material UI, React Bootstrap, Axios  
**Database:** MongoDB Atlas  
**Real-time:** Socket.io, WebSocket (ws)

## Architecture

```
/src
  /Routes         → doctorRoute, patientRoute, adminRoute, pharmacistRoute, securityRoute
  /Models         → userModel, appointmentModel, notificationModel, messageModel
  /middleware     → authMiddleware (JWT protection)
  /config         → db.js (MongoDB connection)
  app.js          → Express server + Socket.io setup
```

## Getting Started

```bash
# Install dependencies
npm install

# Set environment variables
cp .env.example .env
# Add: MONGO_URI, JWT_SECRET, STRIPE_SECRET_KEY, EMAIL credentials

# Run development server
npm run dev
```

## Key API Endpoints

| Method | Route | Description |
|--------|-------|-------------|
| POST | `/security/register` | Register new user |
| POST | `/security/login` | Login + receive JWT |
| POST | `/security/sendOTP` | Send OTP to email |
| POST | `/admin/createAdmin` | Add new admin |
| POST | `/admin/DoctorAcceptance/:username` | Approve doctor |
| POST | `/doctor/addAvailableSlots` | Add appointment slots |
| GET | `/doctor/getUpcomingAppointment` | View upcoming appointments |
| GET | `/patient/getDoctorNames` | Browse doctors |
| POST | `/patient/buyPrescription/:id` | Purchase prescription |

## Key Concepts Demonstrated

- RESTful API design with role-based access control
- Real-time communication with Socket.io
- Payment integration with Stripe
- JWT authentication with OTP email verification
- Multi-module system with shared database across clinic and pharmacy
- PDF generation for prescriptions
