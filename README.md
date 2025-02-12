# Event Reservation System

## Overview  
The Event Reservation System allows users to browse events and make reservations for specific events.

---

## Features & Functionalities  

### **Event Management**  

#### 📌 **Listing Events**  
- Retrieve all events with optional search by `name` or `location`.  
- Query parameter: `search` (matches `name` or `location`).  
- Display fields: `name`, `slug`, `location`, `event_date`, `capacity`.  
- Pagination implemented.  

#### ➕ **Creating an Event**  
- Create a new event.  
- All fields (`name`, `description`, `location`, `event_date`, `capacity`) are required and validated.  

#### ✏️ **Updating an Event**  
- Modify details of an existing event.  
- All fields are required and must pass validation.  

#### 🗑️ **Deleting an Event**  
- Events can be deleted only if there are no confirmed reservations.  
- If confirmed reservations exist, deletion is prohibited (`400 Bad Request`).  

#### 🔍 **Viewing a Single Event**  
- Retrieve full event details including reservations.  
- Display fields: `name`, `slug`, `location`, `event_date`, `capacity`, `reservations`.  

#### ✅ **Validation Rules for Events**  
- `event_date` must be a future date.  
- `capacity` must be a positive integer.  

---

### **Reservation Management**  

#### 🎟 **Creating a Reservation**  
- Users can reserve tickets for an event.  
- `ticket_quantity` must not exceed the available `capacity`.  
- Default status: `pending`.  

#### ✔️ **Confirming a Reservation**  
- A reservation can be confirmed only if its current status is `pending`.  
- If not `pending`, confirmation is prohibited (`400 Bad Request`).  
- Upon confirmation, the event’s available `capacity` decreases by `ticket_quantity`.  

#### ❌ **Cancelling a Reservation**  
- A reservation can be cancelled only if its current status is `confirmed`.  
- If not `confirmed`, cancellation is prohibited (`400 Bad Request`).  
- Upon cancellation, the event’s available `capacity` increases by `ticket_quantity`.  

#### ✅ **Validation Rules for Reservations**  
- `event_id` must refer to an existing event.  
- `ticket_quantity` must be a positive integer and must not exceed available `capacity`.  
- `user_name` is required.  

---

## API Endpoints  

### **Event Endpoints**  
- `GET /events` - List all events (supports search & pagination).  
- `POST /events` - Create a new event.  
- `GET /events/{event}` - Get details of a specific event.  
- `PUT /events/{event}` - Update an existing event.  
- `DELETE /events/{event}` - Delete an event (if no confirmed reservations exist).  

### **Reservation Endpoints**  
- `POST /reservations` - Create a reservation.  
- `PUT /reservations/{reservation}/confirm` - Confirm a reservation.  
- `PUT /reservations/{reservation}/cancel` - Cancel a reservation.  


