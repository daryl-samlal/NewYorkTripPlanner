# Quick Start: Using the Transports Tab

## 🚀 Getting Started (5 minutes)

### Step 1: Access Transports Tab
1. Open your NYC Trip Planner app
2. Click the **"Transports"** button in the top navigation
3. You'll see the Transportation Management page

### Step 2: Add Your First Transport
1. Click **"+ Add Transport"** button
2. Fill in the required fields:
   - **Transport Type**: Choose from Bus, Train, Metro, Taxi, Uber, Car Rental, Flight, or Other
   - **From Location**: Starting point (e.g., "Penn Station")
   - **To Location**: Destination (e.g., "LaGuardia Airport")
   - **Departure Time**: When you're leaving (e.g., "2026-12-14 14:00")

3. Optionally fill in:
   - **Arrival Time**: When you arrive
   - **Booking Reference**: Your booking number (e.g., "BUS123456")
   - **Price**: How much it costs
   - **Provider**: Company name (e.g., "AirTrain")
   - **Notes**: Any special details

4. Click **"Add Transport"** to save

### Step 3: View Your Transports
- All your bookings appear in the list
- Each card shows:
  - 🚌 Transport type with icon
  - Route (From → To)
  - Times (departure & arrival)
  - Booking reference & price
  - Any notes you added

### Step 4: Manage Your Transports
- **Delete**: Click the trash icon on any transport to remove it
- **View Details**: All information is visible on the card
- **Copy Booking Reference**: Easy to highlight and copy

---

## 📋 Common Transport Examples

### Airport Shuttle
```
Type: Bus
From: Hotel (The Gregorian Hotel)
To: JFK Airport Terminal 2
Departure: 2026-12-23 11:30 AM
Booking Ref: BUS789456
Price: $25.00
Provider: AirTrain
Notes: Meet at hotel lobby, 15 min early
```

### NYC Subway
```
Type: Metro
From: Times Square Station
To: Central Park Station
Departure: 2026-12-15 10:00 AM
Price: $2.75
Notes: Use MetroCard
```

### Train to Another City
```
Type: Train
From: Penn Station
To: Boston South Station
Departure: 2026-12-16 15:30
Arrival: 2026-12-16 18:45
Price: $65.00
Booking Ref: AMTK987654
Provider: Amtrak
Notes: Assigned seat 12B
```

### Rideshare
```
Type: Uber
From: Times Square
To: Central Park
Departure: 2026-12-15 19:00
Booking Ref: UBER-XYZ123
Price: $22.50
Notes: Scheduled ride, driver will text
```

---

## 🎯 Pro Tips

### ✅ Date/Time Format
- Format: `YYYY-MM-DD HH:MM` (e.g., `2026-12-14 14:00`)
- Or use the date/time picker on your device
- Times are flexible - you can use 24-hour or 12-hour format

### ✅ Booking Reference
- Keep this handy! Save your booking confirmation
- Format examples: `BUS123456`, `AMTK-98765`, `UBER-ABC123`
- Useful for checking in or tracking

### ✅ Price Tracking
- Enter the amount you paid
- Helps track your total transport budget
- Useful for expense reports

### ✅ Notes Field
- Save driver instructions ("Call when you arrive")
- Record special requirements ("Wheelchair accessible")
- Note pickup details ("Hotel lobby by 7am")
- Remember any tips ("Express lane costs extra")

### ✅ Transport Type Selection
- Use the same type for consistency (e.g., all subways as "Metro")
- For uncommon types, use "Other"
- Icons help quickly identify transport type

---

## 🔄 Seeing Your Transports Everywhere

### In Itinerary Tab
Your transports also appear in the **Transportation card** on the right sidebar of your Itinerary view:
- Shows all bookings with type icons
- Quick reference while planning daily activities
- Professional display for sharing

### Status Display
The hero section shows: **"X transports confirmed"**
- Keeps you aware of all bookings
- Quick verification before your trip

---

## 🔄 Syncing & Saving

**Your data automatically syncs to:**
- ✅ Browser local storage (instant, works offline)
- ✅ Cloud (JSONBin) - when you have internet
- ✅ All your devices if you share the URL

**Saves happen when:**
- You add a transport
- You delete a transport
- Page reloads automatically fetch latest data

---

## ❓ Troubleshooting

### Transport not showing up?
1. ✓ Check if you clicked "Add Transport"
2. ✓ Verify all required fields (Type, From, To, Departure) are filled
3. ✓ Check the "No transports added yet" message is gone
4. ✓ Reload the page

### Can't delete a transport?
1. ✓ Confirm the deletion dialog
2. ✓ Check the trash icon appears on hover
3. ✓ Verify you clicked the right transport

### Date/time not saving correctly?
1. ✓ Use format: `YYYY-MM-DD HH:MM`
2. ✓ Or use the date picker widget
3. ✓ Check browser console (F12) for errors

### Price not displaying?
1. ✓ Price must be a valid number (e.g., `18.50`)
2. ✓ No special characters allowed
3. ✓ Decimal separator is a period (.)

---

## 🎓 Video Walkthrough

1. **Accessing Transports** - Click the "Transports" tab
2. **Adding Transport** - Fill the form and click "Add Transport"
3. **Managing List** - View, delete, or export your bookings
4. **Viewing in Itinerary** - See transports on sidebar

---

## 📞 Need Help?

**Check these resources:**
- Full documentation: `TRANSPORTS_TAB_IMPLEMENTATION.md`
- Architecture guide: `ARCHITECTURE.md`
- Data format reference: `example-transport-data.json`

**Report issues:**
- GitHub Issues on NewYorkTripPlanner
- Include: screenshot, browser, and steps to reproduce

---

**Happy Traveling! 🗽✈️**
