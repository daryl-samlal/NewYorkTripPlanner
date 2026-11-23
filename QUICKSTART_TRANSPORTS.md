# Quick Start: Add Transports to Your Trip

## 30-Second Setup

### Step 1: Get Your Data
1. Go to https://jsonbin.io/
2. Find your trip plan data (you already have flights)

### Step 2: Add Transports Array
Add this to your `confirmed` object:

```json
"transports": [
  {
    "type": "bus",
    "from": "JFK Airport",
    "to": "Times Square",
    "departureTime": "17:00",
    "arrivalTime": "18:30",
    "bookingRef": "BUS-NYC-001",
    "price": "15"
  }
]
```

### Step 3: Save & Reload
- Click Save in JSONBin
- Reload your trip planner app
- ✅ You'll see your bus in the Transportation card!

---

## Common Transports to Add

### Airport to Hotel (Bus)
```json
{
  "type": "bus",
  "from": "JFK Airport Terminal 4",
  "to": "Times Square Hotel",
  "departureTime": "17:00",
  "arrivalTime": "18:30",
  "bookingRef": "MEGABUS-456",
  "price": "15"
}
```

### Day Trip by Train
```json
{
  "type": "train",
  "from": "Penn Station, NYC",
  "to": "Boston South Station",
  "departureTime": "2026-12-16 10:00",
  "arrivalTime": "2026-12-16 13:45",
  "bookingRef": "AMTRAK-98765",
  "price": "85"
}
```

### Metro Ride in NYC
```json
{
  "type": "metro",
  "from": "5th Ave (53rd St)",
  "to": "Times Square (42nd St)",
  "departureTime": "14:30",
  "arrivalTime": "14:40",
  "price": "2.90"
}
```

### Uber to Theater
```json
{
  "type": "uber",
  "from": "Hotel",
  "to": "Broadway Theater",
  "departureTime": "19:00",
  "arrivalTime": "19:20",
  "price": "12.50"
}
```

---

## Transport Types Reference

| Type | Icon | Good For |
|------|------|----------|
| `bus` | 🚌 | Long distance buses, airport shuttles |
| `train` | 🚆 | Amtrak, regional trains, day trips |
| `metro` | 🚆 | Subway/metro in cities |
| `subway` | 🚆 | Underground train systems |
| `car` | 🚗 | Rental cars, personal vehicles |
| `rental` | 🚗 | Car rental services |
| `taxi` | 🚕 | Taxi services |
| `uber` | 🚗 | Uber, Lyft, ride-sharing |

---

## Full JSON Example

Here's what your complete data might look like:

```json
{
  "trip": {
    "name": "NYC Holiday Trip",
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
        "from": "JFK",
        "to": "Hotel",
        "departureTime": "17:00",
        "arrivalTime": "18:30",
        "bookingRef": "BUS-001",
        "price": "15"
      },
      {
        "type": "train",
        "from": "Penn Station",
        "to": "Boston",
        "departureTime": "2026-12-16 10:00",
        "arrivalTime": "2026-12-16 13:45",
        "bookingRef": "AMTRAK-001",
        "price": "85"
      }
    ],
    "hotels": [
      {
        "name": "Hotel Name",
        "address": "123 Main St",
        "from": "2026-12-12",
        "to": "2026-12-23"
      }
    ]
  }
}
```

---

## Tips & Tricks

✅ **Mix & Match** - Use flights AND other transports together
✅ **Flexible Times** - Use "17:00" or "2026-12-16 17:00" format
✅ **Optional Fields** - Don't include `price` if you don't want to show it
✅ **No Booking Ref?** - Leave `bookingRef` empty or omit it
✅ **Multiple Transports** - Add as many as you need in the array
✅ **Any Order** - Transports display in the order you list them

---

## Troubleshooting

| Problem | Solution |
|---------|----------|
| Transport not showing | Make sure `type` field is lowercase (bus, train, etc.) |
| Icon looks wrong | Check the transport type spelling |
| JSON error | Use JSONBin's validator - look for syntax errors |
| Old data showing | Hard refresh your browser (Ctrl+Shift+R or Cmd+Shift+R) |
| Can't find transports array | Make sure it's inside the `confirmed` object |

---

## Need More Help?

- Full documentation: See `TRANSPORT_FEATURE.md`
- Example data: See `example-transport-data.json`
- Implementation details: See `CHANGES_SUMMARY.md`

---

## Ready?

1. ✏️ Open your JSONBin data
2. ➕ Add a `transports` array
3. 💾 Save your changes
4. 🔄 Reload the app
5. 🎉 See your transports displayed!

That's it! 🚀
