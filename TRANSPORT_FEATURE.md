# Multi-Transport Support Feature

## Overview
The NYC Trip Planner now supports multiple types of transportation beyond flights, including buses, trains, car rentals, taxis, and metro systems.

## Data Structure

### Transport Object
Each transport record should have the following structure:

```json
{
  "type": "bus|train|car|rental|taxi|uber|metro|subway",
  "from": "Boston",
  "to": "New York",
  "departureTime": "14:30",
  "arrivalTime": "16:45",
  "bookingRef": "BUS123456",
  "price": "45.00",
  "provider": "Greyhound",
  "notes": "Optional notes"
}
```

## JSON Data Format

The confirmed transports are stored under `confirmed.transports` in your JSONBin data:

```json
{
  "trip": {
    "name": "New York City Holiday Magic",
    "startDate": "2026-12-12",
    "endDate": "2026-12-23"
  },
  "confirmed": {
    "flights": [
      {
        "flight": "BW520",
        "from": "POS",
        "to": "JFK",
        "departure": "2026-12-12T12:10:00",
        "arrival": "2026-12-12T16:30:00"
      }
    ],
    "transports": [
      {
        "type": "bus",
        "from": "JFK Airport",
        "to": "Times Square",
        "departureTime": "17:00",
        "arrivalTime": "18:30",
        "bookingRef": "BUS-NYC-001",
        "price": "15.00",
        "provider": "MegaBus"
      },
      {
        "type": "train",
        "from": "New York",
        "to": "Boston",
        "departureTime": "2026-12-18 10:00",
        "arrivalTime": "2026-12-18 13:45",
        "bookingRef": "AMTRAK-45678",
        "price": "85.00",
        "provider": "Amtrak"
      },
      {
        "type": "metro",
        "from": "Port Authority",
        "to": "Central Park",
        "departureTime": "09:00",
        "arrivalTime": "09:15",
        "price": "2.90"
      }
    ],
    "hotels": []
  }
}
```

## Supported Transport Types

| Type | Icon | Use Case |
|------|------|----------|
| `flight` | ✈️ | Commercial flights |
| `bus` | 🚌 | Bus services (Greyhound, Megabus, etc.) |
| `train` | 🚆 | Train/rail services (Amtrak, etc.) |
| `car` | 🚗 | Personal/rental cars |
| `rental` | 🚗 | Car rental services |
| `taxi` | 🚕 | Taxi services |
| `uber` | 🚗 | Ride-sharing services |
| `metro` | 🚆 | Metro/subway systems |
| `subway` | 🚆 | Subway systems |

## UI Display

### Transportation Summary Card
- Located in the right sidebar below Accommodation
- Displays all booked transports (flights + other transports)
- Shows transport type with appropriate icon
- Displays departure/arrival locations and times
- Shows booking reference if available
- Displays price if available

### Status Badge
The status badge at the top now shows total confirmed transports:
- "2 transports confirmed" (instead of just flight count)
- Includes both flights and other transport types

## How to Add Transports to Your Trip

1. **Edit your JSONBin data** at: https://jsonbin.io/

2. **Add transports array** to the `confirmed` object:

```json
"confirmed": {
  "flights": [...],
  "transports": [
    {
      "type": "bus",
      "from": "JFK Airport",
      "to": "Hotel Location",
      "departureTime": "17:00",
      "arrivalTime": "18:30",
      "bookingRef": "BUS-123",
      "price": "15"
    }
  ]
}
```

3. **Save and reload** the app to see your transports displayed

## Field Reference

| Field | Type | Required | Notes |
|-------|------|----------|-------|
| `type` | string | Yes | Transport type (bus, train, etc.) |
| `from` | string | Yes | Departure location |
| `to` | string | Yes | Arrival location |
| `departureTime` | string | No | Time or datetime (flexible format) |
| `arrivalTime` | string | No | Time or datetime (flexible format) |
| `bookingRef` | string | No | Booking reference number |
| `price` | string/number | No | Cost of transport |
| `provider` | string | No | Service provider name |
| `notes` | string | No | Additional notes |

## Examples

### Bus from Airport to Hotel
```json
{
  "type": "bus",
  "from": "JFK Airport",
  "to": "Times Square Hotel",
  "departureTime": "17:00",
  "arrivalTime": "18:30",
  "bookingRef": "MEGABUS-456",
  "price": "15.00"
}
```

### Amtrak Train to Boston
```json
{
  "type": "train",
  "from": "Penn Station, NYC",
  "to": "South Station, Boston",
  "departureTime": "2026-12-18 14:00",
  "arrivalTime": "2026-12-18 17:30",
  "bookingRef": "AMTRAK-98765",
  "price": "85.00",
  "provider": "Amtrak"
}
```

### Metro/Subway (Local)
```json
{
  "type": "metro",
  "from": "Penn Station",
  "to": "Central Park South",
  "departureTime": "10:30",
  "arrivalTime": "10:45",
  "price": "2.90"
}
```

### Uber/Taxi
```json
{
  "type": "uber",
  "from": "Hotel",
  "to": "Times Square",
  "departureTime": "19:00",
  "arrivalTime": "19:20",
  "price": "12.50"
}
```

## Future Enhancements

Potential features for the next version:
- Add/edit transports directly in the app UI
- Track transport costs in a summary
- Add transport options to daily planning
- Integration with booking services
- Real-time tracking of transports
- Route optimization between locations
- Transport notes and special requirements

## Questions?

The Transportation section displays all your booked transports in one convenient location alongside your flights and accommodations for easy trip planning!
