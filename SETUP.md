# Spreadsheet Extension — Setup Guide

## THE HTTPS PROBLEM (read this first)

Tableau refuses any URL that starts with `http://` — even `http://localhost`.
The manifest validation literally regex-checks for `https://`.

You need a real HTTPS URL. The fastest way is ngrok (free, 2 minutes).

---

## OPTION A — ngrok (recommended, works in 2 minutes)

### Step 1 — Start your local server
Open a terminal in the folder containing spreadsheet.html and run:
```
python -m http.server 8765
```
Leave this running.

### Step 2 — Install ngrok (one time only)
Go to https://ngrok.com/download and download for Windows.
Extract ngrok.exe anywhere convenient (e.g. same folder).

### Step 3 — Create a free ngrok account and get your authtoken
Sign up free at https://dashboard.ngrok.com
Copy your authtoken from the dashboard, then run once:
```
ngrok config add-authtoken YOUR_TOKEN_HERE
```

### Step 4 — Start ngrok tunnel
Open a second terminal and run:
```
ngrok http 8765
```
You will see something like:
```
Forwarding   https://a1b2c3d4.ngrok-free.app -> http://localhost:8765
```
Copy that https URL (e.g. https://a1b2c3d4.ngrok-free.app)

### Step 5 — Paste URL into spreadsheet.trex
Open spreadsheet.trex in Notepad.
Find this line:
```
<url>https://PASTE-YOUR-NGROK-URL-HERE/spreadsheet.html</url>
```
Replace it with your actual ngrok URL, for example:
```
<url>https://a1b2c3d4.ngrok-free.app/spreadsheet.html</url>
```
Save the file.

### Step 6 — Load in Tableau Desktop
1. Open a dashboard in Tableau Desktop
2. Drag Extension object onto canvas
3. Click "Access Local Extensions"
4. Select spreadsheet.trex
5. Click Allow

Done. The spreadsheet runs inside your dashboard.

---

## OPTION B — GitHub Pages (free HTTPS, permanent URL)

Best if you want it to work on Tableau Server/Online too.

1. Create a free GitHub account at github.com
2. Create a new repository (e.g. "spreadsheet-extension"), set to Public
3. Upload spreadsheet.html to the repository
4. Go to repo Settings → Pages → Source: Deploy from main branch → Save
5. After 1-2 minutes your URL is:
   https://YOURUSERNAME.github.io/spreadsheet-extension/spreadsheet.html
6. Open spreadsheet.trex in Notepad, paste that URL into the <url> tag
7. Load the .trex in Tableau Desktop as above

GitHub Pages URL never expires and works everywhere.

---

## OPTION C — Any web hosting

If you have web hosting (cPanel, AWS, Azure, etc.) that serves HTTPS:
1. Upload spreadsheet.html to your server
2. Get the HTTPS URL (e.g. https://your-domain.com/spreadsheet.html)
3. Paste into the <url> tag in spreadsheet.trex

---

## After loading — Import Tableau data

1. Click "⬇ From Tableau" in the toolbar
2. Pick a worksheet from the dropdown
3. Click Import
4. Your data appears in the spreadsheet — now run formulas on it

---

## Supported formulas (70+)

Math: SUM AVERAGE MAX MIN COUNT PRODUCT ROUND ABS SQRT POWER MOD INT SIGN
      FLOOR CEILING RAND RANDBETWEEN EXP LN LOG SIN COS TAN and more

Logic: IF IFS AND OR NOT XOR SWITCH IFERROR IFNA

Text: LEN UPPER LOWER PROPER TRIM LEFT RIGHT MID FIND SUBSTITUTE
      REPLACE CONCATENATE TEXTJOIN and more

Date: TODAY NOW YEAR MONTH DAY HOUR MINUTE WEEKDAY

---

## Keyboard shortcuts

Arrow keys     Navigate cells
Enter          Confirm + move down
Tab            Confirm + move right
Shift+Arrow    Extend selection
F2             Edit cell
Escape         Cancel edit
Delete         Clear selected cells
Ctrl+B         Bold
Ctrl+I         Italic
Ctrl+U         Underline
Double-click   Edit cell in place
