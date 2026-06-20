# Trip Planner Skill

Use this skill when the user asks to create or update a trip planning HTML page. The output is a **single self-contained HTML file** (no external CSS/JS, no API keys) that works on desktop and mobile.

## Output File
- Single `.html` file, e.g. `trip-plan.html`
- All CSS inline in `<style>`, all JS inline in `<script>` at end of `<body>`

## HTML Structure

```
<style>...</style>
</head>
<body>
  <!-- FAB toggle for settings -->
  <div class="fab" id="fabBtn">&#8942;</div>
  <div class="fab-dropdown" id="settingsPanel">...</div>

  <!-- HERO / SLIDESHOW -->
  <div class="hero" id="hero">
    <div class="hero-slideshow">...</div>
    <div class="hero-content">
      <p class="hero-subtitle">Route summary</p>
      <h1>Trip Title</h1>
      <p class="hero-tagline">Tagline</p>
      <div class="hero-cta">...</div>
      <!-- toggle for ditched plans if multiple plans -->
    </div>
  </div>

  <!-- CAROUSEL -->
  <div class="carousel">
    <div class="carousel-card" data-index="0">Plan 1 card</div>
    <div class="carousel-card" data-index="1">Plan 2 card</div>
    ...
  </div>

  <!-- TABS -->
  <div class="tabs">
    <div class="tab active" onclick="showPlan(0)">Plan 1</div>
    <div class="tab" onclick="showPlan(1)">Plan 2</div>
    ...
  </div>

  <!-- PLAN SECTIONS -->
  <div class="container">
    <div class="plan active">
      <p class="plan-title">Plan Title</p>
      <p class="plan-sub">Route description</p>
      <!-- MAP SECTION -->
      <div class="map-section">
        <div class="map-h">📍 Route header</div>
        <iframe loading="lazy" src="..."></iframe>
        <a class="map-link" href="..." target="_blank">Open in Google Maps</a>
      </div>
      <!-- ITINERARY STOPS -->
      <div class="day day1">
        <div class="day-header"><span>🗺</span> Day N — Title</div>
        <div class="stop">
          <div class="stop-time">HH:MM</div>
          <div class="stop-icon">EMOJI</div>
          <div class="stop-detail">
            <div class="stop-name">Place Name</div>
            <div class="stop-desc">Description</div>
            <div class="stop-drive">Drive time from previous stop</div>
            <div class="stop-imgs">...</div>
            <div class="stop-acts">...</div>
          </div>
        </div>
        ...
      </div>
      <!-- INFO BOXES -->
      <div class="info-box"><h3>Food & Drink</h3><ul>...</ul></div>
      <div class="info-box"><h3>Accommodation</h3><ul>...</ul></div>
      <div class="info-box"><h3>Tips</h3><ul>...</ul></div>
    </div>
    ...
  </div>

  <script>...</script>
</body>
```

## Key Conventions

### Google Maps Embeds
- **Embed URL** (shows route line on page): `https://maps.google.com/maps?saddr=START&daddr=WAYPOINT1+to:WAYPOINT2+to:END&dirflg=d&output=embed`
- **Link URL** (opens in Google Maps): `https://www.google.com/maps/dir/START/WAYPOINT1/WAYPOINT2/END`
- Use `+` for spaces in URL params, `+` also in link URL paths for multi-word waypoints
- Add `&dirflg=d` for driving mode
- Use `Co+Sligo`, `Co+Mayo` etc. to disambiguate place names
- All major sightseeing stops AND rest stops should be in the map URL

### Images
- **Pexels CDN**: `https://images.pexels.com/photos/{ID}/pexels-photo-{ID}.jpeg?auto=compress&cs=tinysrgb&w=800`
- **Heritage Ireland CDN**: `https://heritageireland.ie/assets/uploads/2020/03/{filename}.jpg`
- **Flickr**: `https://live.staticflickr.com/{server}/{id}_{secret}_b.jpg`
- Always add `loading="lazy"` to images
- Use `alt` text matching the place name

### Routes
- **Google My Maps embeds**: Use `<iframe src="https://www.google.com/maps/d/embed?mid={ID}&ehbc=2E312F" allowfullscreen></iframe>` for custom drawn routes (e.g. scenic loops)
- Wrap My Maps iframes in `overflow:hidden` containers with negative margin to clip Google UI chrome

### Stop Types & Icons
| Icon | Meaning |
|------|---------|
| 🚗 | Depart / Drive |
| ☕ | Coffee / Rest break |
| 🌊 | Beach |
| 🏞 | Viewpoint / Nature |
| 🏰 | Castle / Historic |
| 🏛 | Museum / Cultural |
| 🍽 | Lunch / Food |
| 🚶 | Walk / Stroll |
| 🏠 | Check-in / Accommodation |
| 📷 | Photo stop |
| 🏕 | Outdoor activity |

### Stop Structure
- Each stop gets: `.stop-time` (HH:MM), `.stop-icon` (emoji), `.stop-name`, `.stop-desc`, `.stop-drive`
- Must-see attractions get: `<span class="must-see">★ Must-See</span>` in `.stop-name`
- Cafe/baby-friendly tags: `<span class="cafe-tag">Cafe</span>` or `act-badge act-baby` in activities
- `.stop-imgs` contains 2-3 place-specific images in horizontal scroll
- `.stop-acts` contains activity badges with optional "Book" buttons (`.act-book`)

### Activities Section
```html
<div class="stop-acts">
  <div class="acts-heading">🎯 Activities</div>
  <div class="act-row">
    <span class="act-badge act-baby">👶 Activity description</span>
    <a class="act-book" href="BOOKING_URL" target="_blank">Book</a>
  </div>
</div>
```
- Free/walk-in activities: just `.act-badge`, no Book button
- Bookable activities: add `.act-row` with `.act-book` link
- Baby-friendly: add `act-baby` class for green badge
- Couple-only: add `act-couple` class

### Accommodation
- Must sleep 5 (or as specified), under budget
- Use real, bookable direct links from Airbnb or selfcater.com
- Airbnb format: `https://www.airbnb.ie/rooms/{ROOM_ID}`
- Selfcater format: `https://selfcater.com/rentals/ireland/{county}/{property-slug}`

### Rest Stops (for baby)
- When any drive exceeds ~1.5hr, add a rest stop
- Format: Quick coffee/nappy break at a service station or town centre
- 15 min duration
- Add to Google Maps URL as a waypoint

## CSS Architecture

### Layout
- `.stop{display:flex;flex-flow:row wrap;padding:.85rem 1.2rem;position:relative}`
- `.stop-time{flex:1 1 100%;...}` → row 1, full width
- `.stop-icon{position:absolute;left:1.2rem;top:2.2rem}` → icon floats in padding
- `.stop-detail{flex:1;min-width:0;padding:0 1.6rem}` → row 2, symmetric padding
- Mobile: `.stop-icon{display:none}`, reduce `.stop` padding

### Key Classes
| Class | Purpose |
|-------|---------|
| `.stop` | Flex row for each itinerary entry |
| `.stop-time` | Time column (full-width row on desktop) |
| `.stop-icon` | Emoji icon (absolute positioned on desktop, hidden on mobile) |
| `.stop-detail` | Name + desc + drive + images + activities |
| `.stop-imgs` | Horizontal scroll of place images |
| `.stop-acts` | Green card with activity badges + book buttons |
| `.must-see` | Red ★ Must-See badge |
| `.cafe-tag` | Green cafe tag badge |
| `.plan.active` | Visible plan (others hidden) |
| `.plan.ditched` | Hidden by default, shown via toggle |

### Responsive Breakpoint
- `@media(max-width:600px)` for mobile

## JavaScript

### Plan Switching
```javascript
function showPlan(i) {
  var m = [3,0,1,2][i]; // map plan index to DOM index (if reordering)
  document.querySelectorAll('.plan').forEach((p, idx) => p.classList.toggle('active', idx === m));
  document.querySelectorAll('.tab').forEach((t, idx) => t.classList.toggle('active', idx === i));
  document.querySelector('.container').scrollIntoView({behavior: 'smooth'});
}
```

### Lightbox
- Click image → overlay fullscreen with prev/next, swipe, keyboard nav
- `touch-action:none` on lightbox overlay
- Gallery dedupes identical image URLs

### FAB / Settings
- Floating action button at `bottom:2rem;left:1.5rem`
- Toggle panel auto-hides after 3.5s
- Use for toggling ditched plans visibility

### Toggle Ditched Plans
```javascript
function toggleDitched(on) {
  document.querySelectorAll('.ditched').forEach(el => el.classList.toggle('show', on));
  if (!on) showPlan(0); // reset to first plan
}
```

## Road Trip Planning Rules
- Max 1.5hr between stops (excludes departure from home city)
- All stops in Republic of Ireland only (no Northern Ireland)
- Use `saddr`/`daddr` route format for maps (NOT `maps?q=`)
- Accommodation: sleep 5+, under €250/night
- Photos from Pexels CDN or Heritage Ireland CDN
- No external API keys, no local files — single sharable HTML

## Image Sourcing Priority
1. Pexels CDN (`images.pexels.com/photos/{id}/...`)
2. Heritage Ireland CDN (`heritageireland.ie/assets/uploads/2020/03/`)
3. Flickr static CDN (`live.staticflickr.com/{server}/{id}_{secret}_b.jpg`)
4. User-provided URLs

## Session Logging
After each session, update AGENTS.md in the project root with compaction format:
```
### date — Session N
- **Goal:** ...
- **Progress:** ...
- **Key Decisions:** ...
- **Next Steps:** ...
```
