# JSONBin Trip Planner - AI Agent Guide

## Overview

This guide explains how to read, interpret, and update the JSONBin trip planner file for the New York Holiday Escape trip. This file is the **single source of truth** for all trip data including flights, transports, hotels, events, and daily itineraries.

**JSONBin Bin ID:** `6b01b7cfac6210605a99fd23`
**Base URL:** `https://api.jsonbin.io/v3/b/6b01b7cfac6210605a99fd23`

---

## Quick Start: Accessing the JSONBin File

### Read the Data (GET Request)
```bash
curl https://api.jsonbin.io/v3/b/6b01b7cfac6210605a99fd23
```

**Returns:** A JSON object with structure shown below.

### Update the Data (PUT Request)
```bash
curl -X PUT https://api.jsonbin.io/v3/b/6b01b7cfac6210605a99fd23 \
  -H "Content-Type: application/json" \
  -H "X-Master-Key: $2a$10$UMksmOw979H1LIRIM9kXj.seYgLJ4s.WP9aB11Y7GwJjn5kOAtdRW" \
  -d @your-data.json
```

---

## Complete JSON Structure

### Top-Level Keys

```json
{
  "trip": { },              // Trip metadata
  "confirmed": { },         // Bookings (flights, hotels, transports)
  "events": { },            // Daily events keyed by day number
  "itinerary": { },         // Detailed daily itineraries
  "days": { },              // Day-specific planning (optional)
  "title": "...",           // Trip title
  "subtitle": "...",        // Trip subtitle
  "weather": "...",         // Weather info
  "heroImage": "...",       // Header image URL
  "packingItems": [ ]       // Packing checklist items
}
```

---

## 1. Trip Metadata (`trip`)

**Purpose:** Define the overall trip details.

**Structure:**
```json
{
  "trip": {
    "name": "New York Holiday Escape",
    "startDate": "2026-12-12",
    "endDate": "2026-12-23"
  }
}
```

**How to Read:**
- `name`: Display name of the trip
- `startDate`: First day (YYYY-MM-DD format)
- `endDate`: Last day (YYYY-MM-DD format)

**How to Update:**
- Change `name` to rename the trip
- Adjust `startDate` and `endDate` to modify trip duration
- Day calculations are automatic: trip runs from startDate to endDate

---

## 2. Confirmed Bookings (`confirmed`)

This section contains all bookings: flights, hotels, and transports. These are shown as blocked time in the itinerary.

### 2.1 Flights (`confirmed.flights`)

**Purpose:** Store all flights for the trip.

**Structure:**
```json
{
  "confirmed": {
    "flights": [
      {
        "flight": "BW520",
        "from": "POS",
        "to": "JFK",
        "departure": "2026-12-12T00:10",
        "arrival": "2026-12-12T04:30"
      },
      {
        "flight": "BW525",
        "from": "JFK",
        "to": "POS",
        "departure": "2026-12-23T15:20",
        "arrival": "2026-12-23T21:20"
      }
    ]
  }
}
```

**Field Explanation:**
- `flight`: Flight number/identifier (string)
- `from`: Origin airport code (string, e.g., "POS", "JFK")
- `to`: Destination airport code (string)
- `departure`: Departure datetime (ISO format: YYYY-MM-DDTHH:MM, e.g., "2026-12-12T00:10")
- `arrival`: Arrival datetime (ISO format)

**How to Add a Flight:**
```json
{
  "flight": "AA100",
  "from": "NYC",
  "to": "BOS",
  "departure": "2026-12-15T14:00",
  "arrival": "2026-12-15T16:00"
}
```

**Display Behavior:**
- Flights automatically appear in the Itinerary on their departure date
- Shown as blue-colored events with ✈️ icon
- Block time in the daily schedule (reduces available open time)
- Appear in Transportation section of sidebar

---

### 2.2 Hotels (`confirmed.hotels`)

**Purpose:** Store all hotel stays during the trip.

**Structure:**
```json
{
  "confirmed": {
    "hotels": [
      {
        "name": "The Gregorian Hotel",
        "from": "2026-12-12",
        "to": "2026-12-18"
      },
      {
        "name": "DoubleTree Times Square South",
        "from": "2026-12-18",
        "to": "2026-12-23"
      }
    ]
  }
}
```

**Field Explanation:**
- `name`: Hotel name (string)
- `from`: Check-in date (YYYY-MM-DD format)
- `to`: Check-out date (YYYY-MM-DD format)

**How to Add a Hotel:**
```json
{
  "name": "Park Hyatt New York",
  "from": "2026-12-21",
  "to": "2026-12-23"
}
```

**Display Behavior:**
- Shown in Accommodation section of sidebar
- Affects hotel-specific events (check-in, check-out)
- Not blocked as time events (hotels are daily)

---

### 2.3 Transports (`confirmed.transports`)

**Purpose:** Store all pre-booked transports (bus, train, taxi, metro, etc.).

**Structure:**
```json
{
  "confirmed": {
    "transports": [
      {
        "type": "bus",
        "from": "Times Square",
        "to": "Central Park",
        "departureTime": "2026-12-13T10:00",
        "arrivalTime": "2026-12-13T10:30",
        "bookingRef": "",
        "price": null,
        "provider": "NYC Bus",
        "notes": ""
      }
    ]
  }
}
```

**Field Explanation:**
- `type`: Transport type (string) - must be one of: `"flight"`, `"bus"`, `"train"`, `"metro"`, `"taxi"`, `"uber"`, `"car"`, `"rental"`, `"subway"`, or `"other"`
- `from`: Departure location (string)
- `to`: Destination location (string)
- `departureTime`: Departure datetime (ISO format: YYYY-MM-DDTHH:MM)
- `arrivalTime`: Arrival datetime (ISO format) - **optional**
- `bookingRef`: Booking reference number (string) - **optional**
- `price`: Cost in dollars (number or null) - **optional**
- `provider`: Transport company name (string) - **optional**
- `notes`: Additional details (string) - **optional**

**How to Add a Transport:**
```json
{
  "type": "train",
  "from": "Penn Station",
  "to": "Boston",
  "departureTime": "2026-12-15T14:00",
  "arrivalTime": "2026-12-15T17:30",
  "bookingRef": "AMTK12345",
  "price": 75,
  "provider": "Amtrak",
  "notes": "Northeast Regional, Seat 12A"
}
```

**Display Behavior:**
- Automatically appear in Itinerary on departure date
- Shown with colored events (purple-ish) with appropriate icon (🚌 bus, 🚆 train, etc.)
- Block time in daily schedule
- Appear in Transportation section of sidebar
- Appear in Transports management tab

---

## 3. Daily Events (`events`)

**Purpose:** Store specific events for each day of the trip.

**Structure:**
```json
{
  "events": {
    "1": [
      {
        "from": "00:00",
        "to": "04:30",
        "title": "Confirmed flight BW520: POS to JFK",
        "detail": "Caribbean Airlines",
        "location": "Piarco International Airport (POS)"
      },
      {
        "from": "15:00",
        "to": "16:00",
        "title": "Confirmed hotel check-in",
        "detail": "The Gregorian Hotel",
        "location": "The Gregorian Hotel, 42 W 35th St, New York, NY 10001"
      }
    ],
    "2": [
      {
        "from": "22:00",
        "to": "06:00",
        "title": "Sleep",
        "detail": "Overnight rest",
        "location": "The Gregorian Hotel, 42 W 35th St, New York, NY 10001"
      }
    ]
  }
}
```

**Field Explanation:**
- Key is day number (string: "1", "2", "3", etc.) where "1" = first day of trip
- Array contains event objects for that day
- `from`: Start time in 24-hour format (HH:MM, e.g., "10:00")
- `to`: End time in 24-hour format (HH:MM)
- `title`: Event title (string)
- `detail`: Event description/detail (string)
- `location`: Event location (string) - **optional**
- `coordinates`: [latitude, longitude] - **optional**

**How to Add an Event:**
```json
// Add to events["2"] array:
{
  "from": "10:00",
  "to": "12:30",
  "title": "Central Park Walk",
  "detail": "Scenic walking tour",
  "location": "Central Park, New York"
}
```

**Display Behavior:**
- Events appear as green-colored boxes in the daily itinerary
- Block time (reduce available open time)
- Support Edit and Navigate buttons
- Can include location for navigation features

**Day Number Mapping:**
- Day 1 = First day of trip (startDate)
- Day 2 = Second day
- Day 12 = Last day (if 12-day trip)
- Use `Math.ceil(dayNum)` to convert dates to day numbers

---

## 4. Detailed Itineraries (`itinerary`)

**Purpose:** Store the full day-by-day itinerary with detailed activities.

**Structure:**
```json
{
  "itinerary": {
    "1": {
      "day": 1,
      "date": "Saturday, Dec 12, 2026",
      "title": "Arrival via BW520 & Check-in at The Gregorian",
      "subtitle": "Arrive early morning from Piarco and settle into Midtown Manhattan.",
      "mapQuery": "Piarco International Airport to The Gregorian Hotel New York",
      "activities": [
        {
          "num": 1,
          "time": "12:10 AM",
          "title": "Flight Departure: BW520 (POS → JFK)",
          "category": "Transport",
          "categoryClass": "bg-blue-50 text-blue-700 border-blue-200",
          "icon": "fa-plane-departure",
          "location": "Piarco International Airport (POS)",
          "duration": "4h 20m flight",
          "notes": "Board Caribbean Airlines flight BW520...",
          "image": "https://...",
          "mapsUrl": "https://..."
        }
      ]
    }
  }
}
```

**Field Explanation (Day level):**
- `day`: Day number (integer)
- `date`: Full date string (e.g., "Saturday, Dec 12, 2026")
- `title`: Day's main title
- `subtitle`: Day's description
- `mapQuery`: Query for maps/navigation
- `activities`: Array of activities for the day

**Field Explanation (Activity level):**
- `num`: Activity number (integer, 1-based)
- `time`: Time display (string, e.g., "12:10 AM")
- `title`: Activity title
- `category`: Category (string: "Transport", "Hotel", "Sightseeing", "Food", etc.)
- `categoryClass`: Tailwind CSS classes for styling
- `icon`: FontAwesome icon class (e.g., "fa-plane-departure")
- `location`: Location name
- `duration`: Duration description
- `notes`: Detailed notes
- `image`: Image URL
- `mapsUrl`: Google Maps URL

**How to Add an Activity to Day 2:**
```json
{
  "num": 3,
  "time": "02:00 PM",
  "title": "Fifth Avenue Holiday Window Tour",
  "category": "Sightseeing",
  "categoryClass": "bg-amber-50 text-amber-700 border-amber-200",
  "icon": "fa-gift",
  "location": "Fifth Avenue (Saks, Bergdorf Goodman)",
  "duration": "2 hours",
  "notes": "Stroll down Fifth Ave to see legendary animated holiday window displays.",
  "image": "https://images.unsplash.com/photo-1512917774080-9991f1c4c750",
  "mapsUrl": "https://www.google.com/maps/search/?api=1&query=Saks+Fifth+Avenue+New+York"
}
```

**Display Behavior:**
- Shows in a card/detailed view (not in main itinerary grid)
- Used for reference and planning details
- Not directly tied to the daily schedule (separate from `events`)

---

## 5. Daily Planning State (`days`)

**Purpose:** Store custom planning notes/slots for each day (optional).

**Structure:**
```json
{
  "days": {
    "1": {
      "events": [
        {
          "id": "event-1795298780903",
          "from": "04:50",
          "to": "06:00",
          "title": "Immigration",
          "detail": "JFK Airport",
          "location": "John F. Kennedy..."
        }
      ]
    }
  }
}
```

**Purpose:**
- Stores manually entered plans for time slots
- Stores custom events users add via the UI
- Day-specific metadata

**How to Update:**
- Best handled via UI (Add Event button in Itinerary tab)
- Can be manually added to JSON if needed

---

## 6. Packing List (`packingItems`)

**Purpose:** Store the trip packing checklist.

**Structure:**
```json
{
  "packingItems": [
    {
      "id": 1,
      "text": "Passports & Flight Confirmations (BW520/BW525)",
      "packed": true
    },
    {
      "id": 2,
      "text": "Heavy Winter Coat / Parka",
      "packed": true
    },
    {
      "id": 3,
      "text": "Compact Travel Umbrella",
      "packed": false
    }
  ]
}
```

**Field Explanation:**
- `id`: Unique identifier (integer)
- `text`: Item description (string)
- `packed`: Whether packed (boolean: true/false)

**How to Add a Packing Item:**
```json
{
  "id": 18,
  "text": "Hand Warmers (HotHands)",
  "packed": false
}
```

**Display Behavior:**
- Shows in Packing Checklist widget on sidebar
- Shows progress bar (X of Y packed)
- Strikethrough when packed

---

## Common Operations

### Operation 1: Add a New Flight

**Steps:**
1. Read the JSONBin file
2. Navigate to `confirmed.flights` array
3. Add new flight object
4. Update JSONBin with PUT request

**Example:**
```json
// Current flights array
"flights": [
  { "flight": "BW520", ... },
  { "flight": "BW525", ... }
]

// Add this:
{
  "flight": "AA200",
  "from": "BOS",
  "to": "JFK",
  "departure": "2026-12-18T09:00",
  "arrival": "2026-12-18T11:00"
}

// Updated flights array:
"flights": [
  { "flight": "BW520", ... },
  { "flight": "BW525", ... },
  { "flight": "AA200", ... }  // ← NEW
]
```

**Result:** Flight appears in Itinerary and Transportation sidebar on departure date.

---

### Operation 2: Add a New Transport

**Steps:**
1. Read JSONBin
2. Navigate to `confirmed.transports` array
3. Add transport object
4. Update JSONBin

**Example:**
```json
{
  "type": "metro",
  "from": "Union Square",
  "to": "Times Square",
  "departureTime": "2026-12-14T17:00",
  "arrivalTime": "2026-12-14T17:15",
  "bookingRef": "N/A",
  "price": 2.75,
  "provider": "MTA",
  "notes": "Take Line N at Union Square"
}
```

**Result:** Transport appears in Itinerary as purple event at specified time, blocks schedule.

---

### Operation 3: Add an Event for a Specific Day

**Steps:**
1. Read JSONBin
2. Find or create day key in `events` object
3. Add event to that day's array
4. Update JSONBin

**Example (Add event to Day 3):**
```json
// Current Day 3 events
"3": [
  { "from": "10:00", "to": "12:00", "title": "...", ... },
  { "from": "15:00", "to": "17:00", "title": "...", ... }
]

// Add this event:
{
  "from": "12:00",
  "to": "13:00",
  "title": "Lunch at Rockefeller Center",
  "detail": "Holiday lunch spot",
  "location": "30 Rockefeller Plaza, New York"
}

// Updated Day 3:
"3": [
  { "from": "10:00", ... },
  { "from": "12:00", ... },  // ← NEW
  { "from": "15:00", ... }
]
```

**Result:** Event appears as green box on Day 3 itinerary, blocks time, can be edited.

---

### Operation 4: Change Hotel

**Steps:**
1. Read JSONBin
2. Navigate to `confirmed.hotels` array
3. Modify or add hotel object
4. Update JSONBin

**Example (Add second hotel):**
```json
// Current hotels
"hotels": [
  { "name": "The Gregorian Hotel", "from": "2026-12-12", "to": "2026-12-18" }
]

// Add this:
{
  "name": "The Plaza Hotel",
  "from": "2026-12-18",
  "to": "2026-12-23"
}

// Updated:
"hotels": [
  { "name": "The Gregorian Hotel", "from": "2026-12-12", "to": "2026-12-18" },
  { "name": "The Plaza Hotel", "from": "2026-12-18", "to": "2026-12-23" }  // ← NEW
]
```

**Result:** Hotel appears in Accommodation section. If dates overlap with events, those events get new hotel location.

---

### Operation 5: Update Trip Dates

**Steps:**
1. Read JSONBin
2. Navigate to `trip.startDate` and `trip.endDate`
3. Change dates
4. Update JSONBin

**Important:** Changing dates will not automatically adjust events. You must manually update event day numbers.

---

## Date and Time Format Reference

**ISO DateTime Format (for flights, transports):**
```
2026-12-13T10:00
└─ YYYY-MM-DDTHH:MM
```
- Always use 24-hour time
- Separates date and time with "T"
- Example: "2026-12-13T14:30" = 2:30 PM on Dec 13, 2026

**Time-Only Format (for events):**
```
10:00
└─ HH:MM (24-hour)
```
- Always use 24-hour format
- Example: "09:00" = 9 AM, "21:30" = 9:30 PM

**Date-Only Format (for hotels):**
```
2026-12-13
└─ YYYY-MM-DD
```
- Example: "2026-12-13" = December 13, 2026

---

## How the App Interprets the JSON

### On Page Load:
1. Fetches JSONBin file via GET request
2. Parses `trip` section to get trip dates
3. Builds day numbers (1 through total days)
4. Loads all flights, hotels, transports from `confirmed`
5. Loads all events from `events` section
6. Automatically adds flights/transports to events if they fall on a day
7. Renders itinerary with blocked time for flights/transports/events
8. Displays all items in appropriate UI sections

### Time Blocking Algorithm:
1. For each day, get all events, flights, and transports
2. Sort by start time
3. Calculate "open time" slots (gaps between events)
4. Display events as blocked time
5. Show open time slots as editable planning fields

### Auto-Generated Events from Bookings:
- Flights automatically create events in the `events` section at render time
- Transports automatically create events at render time
- Hotels automatically create check-in/check-out events
- These don't modify the JSON (calculated at runtime)

---

## Best Practices for AI Agent

### When Reading:
1. Always fetch fresh data (don't cache)
2. Parse all nested structures carefully
3. Validate date formats before processing
4. Check for missing optional fields (they can be null or undefined)
5. Handle day numbers correctly (1-indexed, not 0-indexed)

### When Updating:
1. Always fetch current data first (don't overwrite blindly)
2. Make incremental changes (add/modify specific items)
3. Preserve existing data (don't delete unless intentional)
4. Validate all dates are in correct format
5. Use PUT request with X-Master-Key header
6. Handle any existing coordinates in events (preserve them)

### When Adding Items:
1. **Flights:** Ensure departure < arrival time
2. **Transports:** Match type with valid values (bus, train, etc.)
3. **Events:** Ensure "from" time < "to" time
4. **Hotels:** Ensure check-in < check-out date
5. **Times:** Always use 24-hour format

### Conflict Resolution:
- If adding event overlaps with flight/transport: Both show up (overlapping events)
- If hotel dates overlap: Last one takes precedence for location
- If day exceeds trip end date: Clamp to available days

---

## Example: Complete Update Workflow

**Goal:** Add a train ride from NYC to Boston on Day 5

**Step 1: Read Current Data**
```bash
curl https://api.jsonbin.io/v3/b/6b01b7cfac6210605a99fd23
```

**Step 2: Identify Target Day**
- Day 5 = 2026-12-16 (from trip startDate 2026-12-12 + 4 days)

**Step 3: Add Transport to `confirmed.transports`**
```json
{
  "type": "train",
  "from": "Penn Station, NYC",
  "to": "South Station, Boston",
  "departureTime": "2026-12-16T14:00",
  "arrivalTime": "2026-12-16T17:30",
  "bookingRef": "AMTK-567890",
  "price": 85,
  "provider": "Amtrak",
  "notes": "Northeast Regional, Seat 12A, includes coffee"
}
```

**Step 4: (Optional) Add Event in `events["5"]`**
```json
{
  "from": "14:00",
  "to": "17:30",
  "title": "Amtrak Train to Boston",
  "detail": "Northeast Regional",
  "location": "Penn Station, NYC"
}
```

**Step 5: Update JSONBin**
```bash
curl -X PUT https://api.jsonbin.io/v3/b/6b01b7cfac6210605a99fd23 \
  -H "Content-Type: application/json" \
  -H "X-Master-Key: $2a$10$UMksmOw979H1LIRIM9kXj.seYgLJ4s.WP9aB11Y7GwJjn5kOAtdRW" \
  -d @updated-data.json
```

**Step 6: Reload App**
- Transport appears on Day 5 itinerary
- Shows as event with 🚆 icon
- Blocks 3.5 hours of open time
- Shows in Transportation sidebar

---

## Troubleshooting

### Transport/Flight Not Showing:
- Check date format is YYYY-MM-DDTHH:MM
- Verify day number matches trip date
- Ensure "from" time < "to" time
- Reload page to refresh data

### Events Appearing on Wrong Day:
- Verify day numbers (day 1 = startDate)
- Check "from" and "to" times are HH:MM format
- Confirm array is under correct day key

### Overlapping Times Not Showing:
- This is expected - both events display
- UI handles overlapping events correctly
- Both block time calculations

### JSON Parse Error:
- Validate JSON syntax (use JSONLint.com)
- Check for missing commas between array items
- Verify strings use double quotes (not single)
- Ensure no trailing commas

---

## API Reference

### GET Request (Read Data)
```
URL: https://api.jsonbin.io/v3/b/6b01b7cfac6210605a99fd23
Method: GET
Headers: None required
Response: { "record": { ... }, "metadata": { ... } }
```

The actual data is in `response.record` - extract that.

### PUT Request (Update Data)
```
URL: https://api.jsonbin.io/v3/b/6b01b7cfac6210605a99fd23
Method: PUT
Headers:
  Content-Type: application/json
  X-Master-Key: $2a$10$UMksmOw979H1LIRIM9kXj.seYgLJ4s.WP9aB11Y7GwJjn5kOAtdRW
Body: Complete JSON object (not wrapped in "record")
Response: { "subnodes": 1 }
```

**Important:** When you PUT, send the complete JSON object (the data only, not the metadata wrapper).

---

## Tips for AI Agents

1. **Always fetch before update** - Avoid overwriting concurrent changes
2. **Incremental updates** - Modify specific fields, not entire objects
3. **Preserve IDs** - Don't change object IDs (events have "id" fields)
4. **Validate thoroughly** - Check all fields before updating
5. **Test after update** - Reload app and verify changes appear
6. **Handle errors gracefully** - Network requests can fail
7. **Date math** - Convert dates to day numbers: `Math.ceil((dateMs - startDateMs) / (1000 * 60 * 60 * 24))`
8. **Array operations** - Use `.push()` to add, `.splice()` to remove, spread operator for modifications

---

## Summary

| Task | Location | Format | Action |
|------|----------|--------|--------|
| Read all data | JSONBin | GET request | Fetch and parse |
| Add flight | `confirmed.flights[]` | Object | Push to array, PUT |
| Add transport | `confirmed.transports[]` | Object | Push to array, PUT |
| Add event | `events[dayNum][]` | Object | Push to array, PUT |
| Add hotel | `confirmed.hotels[]` | Object | Push to array, PUT |
| Add packing item | `packingItems[]` | Object | Push to array, PUT |
| Change trip dates | `trip.startDate/endDate` | String (YYYY-MM-DD) | Update, PUT |
| Update existing item | Any location | Object | Modify fields, PUT |
| Remove item | Any array | - | Splice array, PUT |

---

**Last Updated:** 2026-11-22  
**Trip:** New York Holiday Escape (Dec 12-23, 2026)
