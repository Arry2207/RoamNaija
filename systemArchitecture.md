# 🧱 RoamNaija System Architecture

This document outlines the technical blueprint behind **RoamNaija** — a platform designed to simplify interstate travel across Nigeria.  
It highlights the frontend, backend, and database architecture, how each component communicates, and why the approach is both scalable and feasible for real-world implementation.

---

## 🖥️ Frontend Architecture

**Tech Stack:**  
- **Framework:** React Native  
- **Language:** TypeScript  
- **UI Library:** Native Base + Tailwind CSS  
- **State Management:** Redux Toolkit  
- **Maps & Location:** Google Maps API + OpenStreetMap  

The frontend is built with **React Native** to ensure cross-platform compatibility (Android and iOS). The interface is lightweight, with modular components for trip search, booking, and user profiles.  

Each screen interacts with the backend through RESTful API calls. Local caching (via AsyncStorage) is used to store trip data and offline tickets, ensuring the app remains usable even when network coverage is poor — a key consideration for interstate travel in Nigeria.

---

## ⚙️ Backend Architecture

**Tech Stack:**  
- **Runtime:** Node.js  
- **Framework:** Express.js  
- **Authentication:** JWT + OAuth2  
- **APIs:** REST-based, with plans to extend to GraphQL for optimized queries  
- **External Integrations:**  
  - Google Places API for location data  
  - Transport company APIs for schedules and seat availability  
  - Cloudinary for image storage  

The backend acts as the central hub for user data, transport listings, and trip metadata.  
Each endpoint is designed around a microservice-friendly structure, separating core modules such as:

- **User Service:** Handles registration, authentication, and journey history  
- **Booking Service:** Manages seat reservations, fare details, and payment logs  
- **Travel Feed Service:** Stores user-generated posts and interactions  
- **Route Service:** Aggregates and processes route data from third-party APIs  

All services communicate through HTTP requests and internal event emitters to maintain modularity and scalability.

---

## 🗄️ Database Architecture

**Primary Database:** MongoDB (hosted on MongoDB Atlas)  
**Secondary (Cache):** Redis for session and temporary data  

**Database Collections:**
- `users` → user profiles, travel stats, saved routes  
- `bookings` → transport company, seat number, date, and payment reference  
- `routes` → source, destination, travel time, and distance  
- `operators` → verified transport company records  
- `posts` → travel feed content (images, captions, likes)  

MongoDB’s document model was chosen for its flexibility in handling diverse data types — from trip details to media posts — without rigid schema constraints. Redis ensures fast access to recurring data like trending routes or cached API responses.

---

## 🔗 Communication Flow

1. **User Request:**  
   The mobile app sends a request (e.g., `GET /routes?from=Lagos&to=Abuja`) to the backend.  

2. **Backend Processing:**  
   The Express server validates the request, fetches available routes from the database or a third-party API, and formats the response.  

3. **Response Delivery:**  
   Data is returned as a JSON payload to the mobile client, where it’s rendered in a friendly, minimal UI.  

4. **Real-Time Interactions:**  
   Socket.IO handles lightweight real-time features — like live route updates or community posts appearing on the Travel Feed.

---

## 🧩 Technical Feasibility

The proposed architecture is **technically feasible and locally adaptable** because:

- **Cross-platform scalability:** React Native and Node.js are lightweight, well-supported, and ideal for mobile-first markets.  
- **Offline-first design:** Local caching and Redis improve performance in areas with unstable internet.  
- **Data flexibility:** MongoDB’s schema-less model fits the evolving nature of transport data.  
- **Integration-ready:** APIs allow easy onboarding of new transport operators and future partnerships.  
- **Low infrastructure overhead:** The system can start small (single server on AWS or Render) and scale horizontally as adoption grows.  

In short, RoamNaija’s architecture is practical, scalable, and built to serve the realities of Nigeria’s travel ecosystem — reliable, connected, and simple to maintain.

---

**RoamNaija Architecture v1.0**  
*Designed for connection. Built for travelers.*
