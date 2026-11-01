# Pickup scheduling for a small courier agent (Bengaluru)

Rebuilt from my strategy internship (Apr-Jun 2024) at a small courier agent in Bengaluru. In the internship I planned the pickup areas and routes on Google Maps and My Maps. My Excel from then was lost, so this file rebuilds the scheduling numbers with the same method.

**Skills used:** Excel (lookups, SUMIFS, charts), zone planning, scenario and sensitivity checks.

## The problem

The agent works from one small shop in central Bengaluru with 3-4 staff, one matador and one scooter. Customers book a pickup (mostly international courier, Express or Economy), the crew goes to them, packs the item on site and brings it back, and parcels are later dropped at the courier companies' collection centres.

For every booking, someone went out straight away. That meant many short, separate trips across the city - more fuel, and staff away from the shop.

## What I suggested

Group pickups by area into planned runs:

- the city is split into 5 zones (Central, South, West, North, East)
- each zone gets one scooter run (small items) and one matador run (large items) a day
- bookings after 1 pm go on the next day's run
- **Option 2:** same as above, but Express pickups are still done straight away (customers pay for speed)

## Results (one month of made-up pickups)

| | Before (go for every booking) | Option 1: all on runs | Option 2: runs + Express straight away |
|---|---|---|---|
| Fuel in the month | Rs 10,240 | Rs 8,020 (22% less) | Rs 9,420 (8% less) |
| Km in the month | 2,973 | 2,325 (22% less) | 2,702 (9% less) |
| Picked up the same day | 100% | 38% | 64% |

Option 1 saves the most fuel, but most afternoon bookings wait till the next day. Option 2 saves less but keeps Express same-day, so that is the one I would recommend.

**The trade-off in money.** Option 2 uses about Rs 1,400 more fuel a month than Option 1, and in return 57 more of the 224 pickups are done the same day. That is roughly Rs 24 for each extra same-day pickup - the marginal cost of keeping the faster service. For Express customers who pay for speed, I think that is worth it.

How sure are these numbers? The saving depends on my rule of thumb for extra stops: if a run needs 4 km for every extra stop instead of 2, the fuel saving drops to about 16% (Option 1) and 6% (Option 2). "Before" assumes every booking was picked up the same day. The numbers will also move a little once all distances are checked on Google Maps.

## How I worked through it (DMAIC)

1. **Define** - one trip for every booking: too much fuel, and staff away from the shop.
2. **Measure** - one month of pickups (224), with km and fuel for each trip.
3. **Analyse** - grouped 31 localities into 5 zones and looked at when in the day bookings come in.
4. **Improve** - zone runs with a 1 pm cut-off, and Express kept on call.
5. **Control** - a fixed cut-off and a daily run sheet per zone. This part is my proposal and was not tested.

## What's in the Excel

- **Notes** - disclaimers, assumptions (yellow cells) and sources
- **Summary** - before vs the two options, with a chart
- **Areas** - 31 localities, zone, km and minutes from the hub
- **Pickup log** - 4 weeks of made-up pickups (Mon-Sat)
- **Runs** - one row per day, zone and vehicle: pickups, km and fuel

## Disclaimers

1. My original Excel from the internship was lost. This is a rebuilt version (Oct 2026) that follows the same method.
2. The pickup log is made up for illustration. The real pickup records belonged to the company and are not used. The company name and exact location are left out.
3. Distances and times are estimates from public pincode data (straight line x 1.3, at Bengaluru's average speed). I am checking them on Google Maps.
4. Fuel prices are public Bengaluru prices for 23 May 2024. Mileage figures are claimed figures; real mileage in traffic may be lower.
5. Run km is a rule of thumb (2 x farthest stop + 2 km for every extra stop), not an actual route.
6. Only pickup trips are counted. Drop-offs at the courier companies' centres are the same either way.
7. These are not company figures. The ~10% on my earlier CV was my rough estimate at the time; the numbers here come from this rebuilt file.
8. I used an AI assistant (Claude) to help rebuild the formulas and make the sample pickup log. The method and inputs are mine.

## Next steps

- [ ] Check all distances on Google Maps
- [ ] Power BI dashboard on the same data
- [ ] Try a better stop order within each run (Python) and the KPIs in SQL

## Sources

- Pincode locations: [IndiaPIN dataset](https://github.com/harshvardhaniimi/IndiaPIN) (India Post data)
- Road factor ~1.3: [Boeing (2017)](https://arxiv.org/abs/1708.00836)
- Bengaluru speed (~30 min per 10 km in 2024): [TomTom Traffic Index via The News Minute](https://www.thenewsminute.com/karnataka/bengaluru-ranked-worlds-third-slowest-city-in-2024-traffic-index)
- Fuel prices, 23 May 2024: [IIFL](https://www.indiainfoline.com/news/economy/petrol-and-diesel-prices-today-may-23rd-2024)
- Mileage: [Tata Ace Gold (TrucksBuses)](https://www.trucksbuses.com/scv/pickups-and-mini-trucks/tata-ace-gold/mileage), [Honda Activa (91wheels)](https://www.91wheels.com/bikes/honda/activa-6g/mileage)
