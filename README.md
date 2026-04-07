# Nitty Gritty — Manta Air Reservations Portal

A professional web-based tool for processing Radixx reservation exports, extracting connection flights, and managing flight schedules.

## 🚀 Deployment on GitHub Pages

### Step 1: Create a GitHub Repository
1. Go to [github.com](https://github.com) and sign in
2. Click **New repository**
3. Name it `nittygritty` (or any name)
4. Set visibility to **Public** (required for free GitHub Pages)
5. Click **Create repository**

### Step 2: Upload the Files
1. Click **Add file → Upload files**
2. Drag `index.html` into the upload area
3. Commit changes

### Step 3: Enable GitHub Pages
1. Go to **Settings → Pages**
2. Under **Source**, select **Deploy from a branch**
3. Select **main** branch, **/ (root)** folder
4. Click **Save**
5. Your site will be available at `https://yourusername.github.io/nittygritty/`

### Step 4: Connect Your Custom Domain
1. In **Settings → Pages → Custom domain**, enter `nittygritty.online`
2. Click **Save**
3. In your domain registrar (where you purchased nittygritty.online):
   - Add a **CNAME record**: `www` → `yourusername.github.io`
   - Add **A records** for the apex domain pointing to GitHub's IPs:
     - `185.199.108.153`
     - `185.199.109.153`
     - `185.199.110.153`
     - `185.199.111.153`
4. Enable **Enforce HTTPS** in GitHub Pages settings

---

## 🔑 Login Credentials
- **Username:** `mantares`
- **Password:** `Manta@123`

---

## 📋 How to Use

### Extracting Reservations

1. **Open Radixx** → Go to Search Reservations
2. **Set DEP DATE FROM** and **DEP DATE TO** to the date you want
3. **Click Search**
4. **Uncheck** Pending and Cancelled statuses → Search again
5. **Export to Excel** (click the Excel icon)
6. **In Nitty Gritty** → Extract Reservations → Upload the file
7. Click **Process & Download**

### Processing Rules Applied

| Rule | Logic |
|------|-------|
| **A/D Column** | If `Orig = MLE` → **A** (Arrival to resort); otherwise → **D** (Departure) |
| **CONN Source** | If `IATA = RSADGL01` → read from **Address1**; all others → read from **Comments** |
| **CONN Format** | `HHMM FLIGHTNO` (e.g., `0720 EK656`). Time = STA for arrivals, STD for departures |
| **Missing Time** | If flight not found in schedule, cell marked with ⚠️ |
| **PTC Column** | `ADT` → blank · `CHD` → `C` · `INF` → `I` |
| **Comments** | Non-flight text (TTG, REQ, CIP etc.) → moved to COMMENTS column |
| **Hotel Names** | If only hotel name detected in comments → CONN left blank |
| **Multiple Comments** | Last valid flight entry is used as the connection |

### Importing an Updated Flight Schedule
1. Download the new PDF from Maldives Airports Co.
2. Go to **Flight Schedule** → drag & drop the PDF
3. The system parses flight numbers and STA/STD times automatically

---

## ✈️ Pre-loaded Schedule

The Summer 2026 Maldives Airports International Flight Schedule is pre-loaded (valid 29 Mar – 24 Oct 2026). Key carriers include:
Emirates, Qatar, Etihad, Singapore Airlines, SriLankan, Turkish, Fly Dubai, Air Arabia, British Airways, Virgin Atlantic, and 40+ more.

---

## 📂 Output Excel Format

| Column | Description |
|--------|-------------|
| Flt No | Flight number |
| Last Name | Passenger surname |
| First Name | Passenger given name |
| PTC | Blank (ADT), C (CHD), I (INF) |
| Dep Date | Departure date |
| RBD | Booking class |
| Orig | Origin airport |
| Dest | Destination airport |
| A/D | A = Arrival to resort, D = Departure |
| Confirm | PNR / Record locator |
| CONN | Connection flight (e.g. 0720 EK656) — ⚠️ = time not in schedule |
| IATA | Agency/hotel IATA code |
| COMMENTS | Non-flight remarks (TTG, REQ, CIP etc.) |

---

*Built for Manta Air Reservations — Nitty Gritty v1.0*
