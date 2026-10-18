# Confluence 3.0 Website — Initial MERN Draft

A responsive full-stack MERN application reproducing the visual identity, branding, layout, typography, navigation, and structure of the **Confluence 3.0** website (hosted by Rajagiri School of Engineering & Technology - RSET).

---

## 1. Project Structure

```text
colg_website/
├── package.json               # Root scripts (concurrently run dev)
├── full_confluence_dataset.json # Complete canonical event dataset
├── client/                    # React + Vite frontend
│   ├── public/
│   │   └── images/            # Official event banners & RSET logos
│   ├── src/
│   │   ├── components/        # Navbar, Footer, etc.
│   │   ├── pages/             # Home, Workshops, AdvisoryBoard, Speakers,
│   │   │                      # SponsorsPartners, Tickets, Contact, ScheduleDay, Venue
│   │   ├── data.json          # Formatted dataset for all pages & cards
│   │   ├── index.css          # Master stylesheet with theme tokens
│   │   ├── App.jsx            # Hash-based routing configuration
│   │   └── main.jsx
│   └── package.json
└── server/                    # Node.js + Express backend
    ├── models/
    │   ├── Registration.js    # Mongoose schema for Summit passes
    │   └── ContactMessage.js  # Mongoose schema for inquiries
    ├── server.js              # Express REST API, health check & validation
    ├── .env.example           # Environment template
    └── package.json
```

---

## 2. Implemented Features

1. **Homepage:**
   - Sticky navbar with RSET Silver Jubilee branding, navigation links, and responsive hamburger mobile menu.
   - Hero banner with artwork overlay, theme tagline (`India Impact Of AI`), ambient golden glow, and `Get Summit Pass` primary call-to-action.
   - Programme Overview section featuring Day 1 & Day 2 cards with dates, times, and direct schedule navigation.
   - Live Summit countdown timer counting down to August 31, 2026 at 4:00 PM IST with animated colon separators and date metadata.
   - Registration CTA card linking to pass options.
   - Consistent footer with copyright notice and developer attribution.

2. **Workshops (`#/workshops`):**
   - 37 verified workshops loaded directly from canonical event data.
   - Real-time search filter matching workshop title, resource person, or venue.
   - Numbered cards with date, time, resource person, affiliation, and venue.
   - "SOLD OUT" badge status indication.
   - Interactive modal popup with complete session details, schedule info, and external registration links.

3. **Advisory Board (`#/advisory-board`):**
   - Chief Patron spotlight card.
   - Patrons and Advisory Committee grid cards with names, designations, institutions, and profile avatars.
   - External LinkedIn links for board members.

4. **Distinguished Speakers (`#/speakers`):**
   - Full speaker roster with images and designations.
   - Circular portrait styling with royal navy border.
   - Professional titles and LinkedIn badges.

5. **Sponsors & Partners (`#/sponsors-partners` & `#/sponsors`):**
   - Categorized tiers: Title Sponsor (IBS Software), Platinum Sponsor, Gold Sponsors, Silver Sponsors, Partners, and Hydration Partners.
   - Clean partner logo cards.

6. **Tickets & Registration Interest (`#/tickets`):**
   - 3 leader tiers: Business Leader's Badge, Academic Leader's Badge, and Young Leader's Badge with feature checklists and color accents.
   - Pass selection state.
   - Connected MERN registration interest form submitting to `POST /api/registrations`.

7. **Contact (`#/contact`):**
   - Direct email, phone, and campus location cards.
   - Inquiry form with subject dropdown, name, email, and message inputs.
   - Client-side validation and connected backend API submission (`POST /api/contact`).

8. **Schedule Views (`#/day1` & `#/day2`) & Venue Finder (`#/venue`):**
   - Chronological Day 1 & Day 2 timeline cards with ceremony, keynote, speech, launch, and performance categories.
   - Campus venue locator with instant search by block or room.

9. **Backend REST API:**
   - `GET /api/health`: Server health check reporting uptime and database connection status.
   - `POST /api/registrations`: Summit pass interest submission with validation.
   - `POST /api/contact`: Contact message submission with validation.
   - Safe fallback when `MONGODB_URI` is not configured (returns clear 503 status code with instructions instead of pretending data was saved).

---

## 3. Installation & Running Instructions

### Prerequisites
- Node.js (v18+ or v20+)
- npm

### Quick Start (Client & Server Together)
From the project root:
```bash
# Run both client and server concurrently
npm run dev
```

### Running Separately

**Frontend (Client):**
```bash
cd client
npm install
npm run dev
```
Open [http://localhost:5173](http://localhost:5173) in your browser.

**Backend (Server):**
```bash
cd server
npm install
npm run dev
```
The server runs on [http://localhost:5000](http://localhost:5000).

---

## 4. Configuration & Database

Copy `.env.example` to `.env` in the `server` folder:
```bash
cd server
cp .env.example .env
```
Set your MongoDB connection string in `server/.env`:
```env
PORT=5000
MONGODB_URI=mongodb://localhost:27017/confluence3
```
*Note: If MongoDB is not configured or unavailable, the entire frontend and navigation remains fully operational, and the API gracefully returns informational messages.*

---

## 5. Verification & Testing Performed

- **Build & Bundle Verification:** Vite production build executed cleanly (`dist/` generated without compilation errors).
- **Frontend HTTP Serving:** Served at `http://localhost:5173` returning HTTP 200.
- **Backend API Serving:** Health check tested at `http://localhost:5000/api/health` returning JSON status.
- **Form Validation:** Validated client and server rejection of malformed inputs (HTTP 400 with actionable error messages).
- **Database Fallback:** Verified server returns honest 503 response stating database is unconfigured rather than showing false positive successes.
