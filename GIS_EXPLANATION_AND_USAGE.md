# 📋 HALAL GOAT BIN PROJECT - DOCUMENTATION

## GIS (Geographic Information System) - Explanation & Usage

**Project:** Halal GOAT Bin: A Geographically-Oriented Application and Traceability System  
**Date:** February 1, 2026  
**Document:** GIS Overview & Project Implementation  

---

# GIS (Geographic Information System)

## 1. What is GIS?

**GIS = Geographic Information System**

> A system that **captures, stores, analyzes, and displays location-based data** on a **map**.

**Simple definition:** GIS = **Map + Data**

---

## 2. What GIS Can Do

| Function | Description | Example |
|----------|-------------|---------|
| **Display locations** | Show points on a map | Farm location pins |
| **Calculate distance** | Measure between two points | Distance from farm to haram facility |
| **Draw boundaries** | Create shapes/areas | Farm boundary, municipality border |
| **Visualize data** | Color-code based on data | Green = certified, Red = not certified |
| **Analyze patterns** | Find trends in location data | Which areas have most farms? |
| **Store coordinates** | Save latitude/longitude | Farm GPS coordinates |

---

## 3. Types of GIS Data

### 3.1 Point (📍)
Single location marker.

```
        📍
   (Farm location)
```

**Use:** Farm location, slaughterhouse location, haram facility location

### 3.2 Polygon (▢)
Custom shape with multiple points.

```
    ┌───────────┐
    │           │
    │   FARM    │
    │   AREA    │
    └───────────┘
```

**Use:** Farm boundary, municipality border

### 3.3 Circle (⭕)
Round area with radius.

```
      ╭─────────╮
    ╱     1km    ╲
   │    radius    │
   │      ⚫      │
    ╲            ╱
      ╰─────────╯
```

**Use:** Distance warning zone around haram facilities

### 3.4 Line (───)
Connected points forming a line.

```
   📍────────────📍
```

**Use:** Roads, routes, paths

---

## 4. GIS Providers & Options

### 4.1 Available Options

| Provider | Product | Cost | Ease of Use | Quality |
|----------|---------|------|-------------|---------|
| **Google** | Google Maps | Freemium | ⭐⭐⭐⭐⭐ Easy | ⭐⭐⭐⭐⭐ Excellent |
| **OpenStreetMap** | OSM + Leaflet | 100% Free | ⭐⭐⭐ Medium | ⭐⭐⭐⭐ Good |
| **Mapbox** | Mapbox | Freemium | ⭐⭐⭐⭐ Easy | ⭐⭐⭐⭐⭐ Excellent |
| **HERE** | HERE Maps | Freemium | ⭐⭐⭐⭐ Easy | ⭐⭐⭐⭐ Good |
| **ESRI** | ArcGIS | Paid | ⭐⭐ Complex | ⭐⭐⭐⭐⭐ Professional |

### 4.2 Cost Comparison

#### Google Maps
| Feature | Free Limit | After Limit |
|---------|------------|-------------|
| Map Display | 28,000 loads/month | $7 per 1,000 |
| Geocoding | 40,000/month | $5 per 1,000 |
| Distance Calculation | 40,000/month | $5 per 1,000 |

**Verdict:** Free for small-medium projects

#### OpenStreetMap + Leaflet
| Feature | Cost |
|---------|------|
| Map Display | ✅ 100% FREE |
| Geocoding | ✅ Free (Nominatim) |
| Distance Calculation | ✅ Free |
| No usage limits | ✅ Free |

**Verdict:** Best for budget / government projects

### 4.3 Recommendation for This Project

| Option | When to Use |
|--------|-------------|
| **Google Maps** | Easy implementation, familiar to users |
| **OpenStreetMap + Leaflet** | Government project, no budget for maps, no usage limits |

**Recommended:** OpenStreetMap + Leaflet (free, no limits, good for DOST/government project)

---

## 5. GIS Usage in This Project

### 5.1 Use Cases

| # | Use Case | Description | GIS Type |
|---|----------|-------------|----------|
| 1 | **Farm Location** | Farmer pins their farm on map | Point (📍) |
| 2 | **Slaughterhouse Location** | Mark slaughterhouse location | Point (📍) |
| 3 | **Haram Facility Location** | Mark pig farms, non-halal facilities | Point (📍) |
| 4 | **Haram Distance Calculation** | Calculate distance from farm to nearest haram | Distance calc |
| 5 | **View All Farms** | Show all farms on regional map | Multiple points |
| 6 | **Filter by Certification** | Color-code farms by status | Data visualization |
| 7 | **Filter by Municipality** | Show farms in specific area | Filtering |
| 8 | **Farm Boundary** | Draw exact farm area (optional) | Polygon (▢) |

### 5.2 Visual: GIS Features in System

```
┌─────────────────────────────────────────────────────────────────────────┐
│                                                                         │
│                         REGION 12 MAP                                   │
│                                                                         │
│         🟢 = Certified Farm                                             │
│         🔴 = Not Certified Farm                                         │
│         🟡 = Pending Certification                                      │
│         ⚫ = Haram Facility                                             │
│         🔵 = Slaughterhouse                                             │
│                                                                         │
│    ┌─────────────────────────────────────────────────────────────┐     │
│    │                                                             │     │
│    │              🟢        🟢                                   │     │
│    │                   🔴         🔵                             │     │
│    │         🟢                    🟢                            │     │
│    │                  ⚫                                         │     │
│    │              🔴       🟢        🟡                          │     │
│    │                                                             │     │
│    │    ─────────────────────────────────────────────────────   │     │
│    │    Maasim       │    Kiamba    │    Maitum                 │     │
│    │                                                             │     │
│    └─────────────────────────────────────────────────────────────┘     │
│                                                                         │
│    [Filter: All] [Certified Only] [By Municipality ▼]                  │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
```

### 5.3 Haram Distance Calculation

```
AUTOMATIC DISTANCE CALCULATION:

┌─────────────────────────────────────────────────────────────────────────┐
│                                                                         │
│                         ╭───────────╮                                   │
│                       ╱    1 km     ╲                                  │
│         🟢          │    DANGER     │         🟢                       │
│       (OK)          │     ZONE      │       (OK)                       │
│                     │      ⚫       │                                   │
│                     │  (Pig Farm)   │                                   │
│          🔴         ╲              ╱                                   │
│       (WARNING!)      ╰───────────╯                                    │
│                                                                         │
│    System automatically:                                                │
│    1. Finds all haram facilities                                        │
│    2. Calculates distance from each farm                                │
│    3. Flags farms within danger zone                                    │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
```

### 5.4 User Access to GIS Features

| User Role | Can View Map | Can Pin Location | Can View All Farms | Can See Haram Distance |
|-----------|--------------|------------------|--------------------|-----------------------|
| Farm Owner | ✅ | ✅ Own farm | ❌ | ✅ Own farm |
| Farm Worker | ✅ | ❌ | ❌ | ✅ Own farm |
| Certifier | ✅ | ❌ | ✅ All farms | ✅ All farms |
| LGU | ✅ | ❌ | ✅ Own municipality | ✅ Own municipality |
| DA | ✅ | ❌ | ✅ All Region 12 | ✅ All farms |
| Admin | ✅ | ✅ All | ✅ All farms | ✅ All farms |

---

## 6. Database Analysis for GIS

### 6.1 Current Database Structure (From Step 5)

#### farms Table
| Field | Type | GIS Related? |
|-------|------|--------------|
| id | BIGINT | ❌ |
| farm_code | VARCHAR | ❌ |
| name | VARCHAR | ❌ |
| owner_id | BIGINT | ❌ |
| address | TEXT | ❌ |
| barangay_id | BIGINT | ❌ |
| municipality_id | BIGINT | ✅ For filtering by area |
| province_id | BIGINT | ✅ For filtering by area |
| **latitude** | DECIMAL(10,8) | ✅ **GIS - Location** |
| **longitude** | DECIMAL(11,8) | ✅ **GIS - Location** |
| area_hectares | DECIMAL | ❌ (manual input) |
| **haram_distance_km** | DECIMAL | ✅ **GIS - Distance** |
| ... | ... | ... |

#### haram_facilities Table
| Field | Type | GIS Related? |
|-------|------|--------------|
| id | BIGINT | ❌ |
| name | VARCHAR | ❌ |
| type | VARCHAR | ❌ |
| address | TEXT | ❌ |
| municipality_id | BIGINT | ✅ For filtering |
| **latitude** | DECIMAL(10,8) | ✅ **GIS - Location** |
| **longitude** | DECIMAL(11,8) | ✅ **GIS - Location** |
| ... | ... | ... |

#### slaughterhouses Table
| Field | Type | GIS Related? |
|-------|------|--------------|
| id | BIGINT | ❌ |
| name | VARCHAR | ❌ |
| address | TEXT | ❌ |
| municipality_id | BIGINT | ✅ For filtering |
| **latitude** | DECIMAL(10,8) | ✅ **GIS - Location** |
| **longitude** | DECIMAL(11,8) | ✅ **GIS - Location** |
| ... | ... | ... |

### 6.2 GIS Fields Summary

| Table | GIS Fields | Status |
|-------|------------|--------|
| farms | latitude, longitude, haram_distance_km | ✅ **Already in design** |
| haram_facilities | latitude, longitude | ✅ **Already in design** |
| slaughterhouses | latitude, longitude | ✅ **Already in design** |

### 6.3 Conclusion: Database Ready for GIS?

**✅ YES! The database already has the needed fields for GIS:**

| Required for GIS | In Database? | Field |
|------------------|--------------|-------|
| Farm coordinates | ✅ Yes | farms.latitude, farms.longitude |
| Haram coordinates | ✅ Yes | haram_facilities.latitude, haram_facilities.longitude |
| Slaughterhouse coordinates | ✅ Yes | slaughterhouses.latitude, slaughterhouses.longitude |
| Distance storage | ✅ Yes | farms.haram_distance_km |
| Municipality filter | ✅ Yes | farms.municipality_id |
| Province filter | ✅ Yes | farms.province_id |

---

## 7. Optional: Farm Boundary (If Needed Later)

### 7.1 Current Approach: Point Only

```
farms table:
- latitude (single point)
- longitude (single point)
- area_hectares (manual input)
```

**Pros:** Simple, easy for farmers
**Cons:** No exact shape, area is estimated

### 7.2 Future Enhancement: Boundary Drawing

If we want exact farm boundary later, we need to add:

```
NEW: farm_boundaries table
- id
- farm_id (FK)
- coordinates (JSON or POLYGON type)
- area_calculated (auto-calculated)
- perimeter_calculated (auto-calculated)
- created_at
- updated_at
```

**Coordinates format (GeoJSON):**
```json
{
  "type": "Polygon",
  "coordinates": [
    [
      [125.5678, 6.1234],
      [125.5690, 6.1234],
      [125.5690, 6.1220],
      [125.5678, 6.1220],
      [125.5678, 6.1234]
    ]
  ]
}
```

### 7.3 Recommendation

| Phase | Approach |
|-------|----------|
| **Phase 1 (Now)** | Point only (latitude/longitude) — Already in database ✅ |
| **Phase 2 (Later)** | Add boundary drawing if needed |

---

## 8. Implementation Notes

### 8.1 How Distance Calculation Works

```
HAVERSINE FORMULA (Calculate distance between two points on Earth)

Given:
- Farm: lat1, lon1
- Haram: lat2, lon2

Distance = 2 × R × arcsin(√(sin²((lat2-lat1)/2) + cos(lat1) × cos(lat2) × sin²((lon2-lon1)/2)))

Where R = Earth's radius (6,371 km)
```

**In Laravel (PHP):**
```php
function calculateDistance($lat1, $lon1, $lat2, $lon2) {
    $earthRadius = 6371; // km
    
    $latDiff = deg2rad($lat2 - $lat1);
    $lonDiff = deg2rad($lon2 - $lon1);
    
    $a = sin($latDiff/2) * sin($latDiff/2) +
         cos(deg2rad($lat1)) * cos(deg2rad($lat2)) *
         sin($lonDiff/2) * sin($lonDiff/2);
    
    $c = 2 * atan2(sqrt($a), sqrt(1-$a));
    
    return $earthRadius * $c; // Distance in km
}
```

### 8.2 Auto-Calculate Haram Distance

```
WHEN FARM IS REGISTERED:

1. Farmer saves farm location (lat, long)
2. System queries all haram_facilities
3. System calculates distance to each haram facility
4. System finds the NEAREST haram facility
5. System saves distance to farms.haram_distance_km
6. If distance < threshold (e.g., 1km), flag warning
```

### 8.3 Map Library Options for Laravel + Vue

| Library | For | Installation |
|---------|-----|--------------|
| **Leaflet** | Vue.js | `npm install leaflet vue-leaflet` |
| **Google Maps** | Vue.js | `npm install @fawmi/vue-google-maps` |
| **Mapbox** | Vue.js | `npm install mapbox-gl` |

---

## 9. Summary

### 9.1 What is GIS?
- System to display and analyze location data on maps
- Can show points, draw boundaries, calculate distances

### 9.2 GIS in This Project
- Show farm locations on map
- Calculate distance from haram facilities
- Filter farms by municipality
- Visualize certification status

### 9.3 Database Ready?
**✅ YES** — All needed fields already exist:
- farms: latitude, longitude, haram_distance_km
- haram_facilities: latitude, longitude
- slaughterhouses: latitude, longitude

### 9.4 Recommendation
- Use **OpenStreetMap + Leaflet** (free, no limits)
- Use **Point only** for now (simple)
- Add **boundary drawing** later if needed

---

## 10. Questions for Meeting

| # | Question | Options |
|---|----------|---------|
| 1 | Which map provider to use? | Google Maps / OpenStreetMap / Mapbox |
| 2 | What is minimum distance from haram facility? | 500m / 1km / Other |
| 3 | Do we need farm boundary drawing? | Yes / No (point is enough) |

---

*Document Version: 1.0*  
*Last Updated: February 1, 2026*
