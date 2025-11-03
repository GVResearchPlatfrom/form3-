# GVresearchplatform QR Access Form

This GitHub Pages site collects Name, Organisation, Email, and Mobile number, stores them in Google Sheets via Apps Script, and redirects users to your PDF (https://qrco.de/bgQhI7).

## Setup Instructions

1. Create a new Google Sheet with headers:
   `Timestamp | Name | Organisation | Email | Mobile`

2. Open Apps Script (Extensions → Apps Script) and paste:

```javascript
function doPost(e) {
  var data = JSON.parse(e.postData.contents);
  var ss = SpreadsheetApp.getActiveSpreadsheet();
  var sheet = ss.getSheets()[0];
  sheet.appendRow([new Date(), data.name, data.org, data.email, data.mobile]);
  return ContentService.createTextOutput(JSON.stringify({result:'success'}))
    .setMimeType(ContentService.MimeType.JSON);
}
```

3. Deploy as Web App → Execute as Me → Anyone → Deploy → Allow → copy Web App URL.

4. In this repository:
   - Edit `index.html`
   - Replace the line:
     `let API_ENDPOINT = "";`
     with your Google Script URL:
     `let API_ENDPOINT = "https://script.google.com/macros/s/XXX/exec";`
   - Commit changes.

5. Enable GitHub Pages:
   - Settings → Pages → Branch: main → /(root) → Save

6. Open:
   https://GVresearchplatform.github.io/qr-access/
