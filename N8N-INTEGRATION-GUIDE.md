# N8N Webhook Integration Guide

## ✅ Integration Complete

The Know Thyself tool is now fully integrated with your n8n workflow for centralized data collection.

---

## 🔧 What Was Changed

### 1. **CONFIG Updated**
Added real webhook URL and tool metadata:
```javascript
const CONFIG = {
    SUBMIT_WEBHOOK: 'https://n8n-edge.fasttrack-diagnostic.com/webhook/608b17ea-9618-4877-ae3c-85eb2e89b700',
    TOOL_NAME: 'know_thyself',
    SPRINT_NUMBER: 1
}
```

### 2. **User Identification Added**
- Added `userName` and `userEmail` fields to formData
- Created identification form on intro screen (step 0.5)
- Users must enter their details before starting
- "LET'S START" button is disabled until both fields are filled

### 3. **Submit Function Rewritten**
The `handleSubmit()` function now sends proper n8n payload format:

```json
{
  "toolName": "know_thyself",
  "userId": "ivan@fasttrack.com",
  "sprintNumber": 1,
  "timestamp": "2024-12-16T14:30:00.000Z",
  "data": {
    "userName": "Ivan Petrovic",
    "userEmail": "ivan@fasttrack.com",
    "whatLove": "...",
    "whatGoodAt": "...",
    "dream": "...",
    "activities": [...],
    "strengths": [...],
    "values": [...],
    "goals": [...]
  }
}
```

### 4. **Error Handling Improved**
- Shows HTTP status codes on failure
- Preserves localStorage on error (no data loss)
- Clear success/failure messages
- Console logging for debugging

---

## 🧪 How to Test

### Test 1: Successful Submission
1. Open `know-thyself-tool.html`
2. Click "START" on cover page
3. **Enter your name and email** on intro screen
4. Complete all 4 sections with sample data
5. On final canvas, click **"Final Submit"**
6. Check browser console for payload (F12 → Console)
7. Verify success message appears
8. Check your n8n workflow for received data

### Test 2: Error Handling
1. Disconnect from internet (or use invalid webhook URL)
2. Try to submit
3. Verify error message shows
4. Verify data is still in localStorage
5. Reconnect and submit again

### Test 3: UserId Generation
- If user enters email: uses that email as userId
- If user enters name only: generates email like `ivanpetrovic@fasttrack.com`

---

## 📊 Payload Structure

### User Data
```json
{
  "userName": "string",
  "userEmail": "string (email format)"
}
```

### Section 1: Dream Launcher
```json
{
  "whatLove": "string",
  "whatGoodAt": "string",
  "giveToWorld": "string",
  "paidFor": "string",
  "inspired": "string",
  "feltBest": "string",
  "likeAboutSelf": "string",
  "hardships": "string",
  "dream": "string"
}
```

### Section 2: Strengths Amplifier
```json
{
  "activities": [
    { "activity": "string", "energy": "+" | "-" }
  ],
  "strengths": [
    { "strength": "string", "fitPercent": "number" }
  ],
  "doMore": "string",
  "doLess": "string",
  "startTo": "string"
}
```

### Section 3: Values Compass
```json
{
  "values": [
    { 
      "value": "string", 
      "howLive": "string", 
      "alignment": "number (0-100)" 
    }
  ]
}
```

### Section 4: Growth Blueprint
```json
{
  "goals": [
    { 
      "goal": "string", 
      "action": "string", 
      "byWhen": "date (YYYY-MM-DD)" 
    }
  ]
}
```

---

## 🔒 Data Safety

### localStorage Backup
- All data auto-saves to localStorage every 1 second
- Submit preserves localStorage (doesn't clear it)
- If webhook fails, data remains safe locally
- Users can retry submission without re-entering data

### What Happens on Error
1. Error is caught and logged
2. User sees clear error message
3. localStorage is NOT cleared
4. User can retry immediately
5. Support can access console logs for debugging

---

## 🎯 Next Steps for Other Tools

To integrate the remaining 4 tools (FIT/ABC, Segmentation, Value Proposition, Target Segment), follow this pattern:

### 1. Update CONFIG
```javascript
const CONFIG = {
    SUBMIT_WEBHOOK: 'https://n8n-edge.fasttrack-diagnostic.com/webhook/YOUR-WEBHOOK-ID',
    TOOL_NAME: 'fit_abc', // or 'segmentation', 'value_prop', 'target_segment'
    SPRINT_NUMBER: 2, // or 3, 4, 5
    STORAGE_KEY: 'fasttrack_toolname_data'
}
```

### 2. Add User Identification
- Add `userName` and `userEmail` to formData
- Add identification form on intro/first screen
- Require both fields before proceeding

### 3. Update Submit Function
```javascript
const payload = {
    toolName: CONFIG.TOOL_NAME,
    userId: formData.userEmail,
    sprintNumber: CONFIG.SPRINT_NUMBER,
    timestamp: new Date().toISOString(),
    data: { /* tool-specific fields */ }
};
```

### 4. Add Error Handling
- Try/catch around fetch
- Show HTTP status on error
- Preserve localStorage
- Console logging

---

## 🐛 Debugging

### Check Browser Console
1. Open DevTools (F12)
2. Go to Console tab
3. Look for "Submitting to n8n:" message
4. Check payload structure
5. Look for error messages

### Common Issues

**Error: Failed to fetch**
- Check internet connection
- Verify webhook URL is correct
- Check CORS settings on n8n

**Error: HTTP 400 Bad Request**
- Payload structure doesn't match n8n expectations
- Check field names and data types

**Error: HTTP 500 Internal Server Error**
- n8n workflow has an error
- Check n8n workflow logs

### Testing Without n8n
To test locally without hitting the webhook:
```javascript
// Temporarily comment out the fetch call
// const response = await fetch(CONFIG.SUBMIT_WEBHOOK, {...});
console.log('Would submit:', payload);
```

---

## ✅ Integration Checklist

- [x] n8n webhook URL configured
- [x] User identification fields added
- [x] Submit function sends proper payload format
- [x] Error handling implemented
- [x] localStorage backup preserved
- [x] Success/failure messages clear
- [x] Console logging for debugging
- [x] Email validation on form
- [x] Required fields enforced
- [x] Data structure documented

---

## 📞 Support

If submission fails:
1. Check browser console for errors
2. Verify user has internet connection
3. Test webhook URL with curl/Postman
4. Check n8n workflow is active
5. Data is safe in localStorage - can retry anytime

---

## 🎉 Ready to Use!

The tool is production-ready. Users can:
1. Complete the tool offline (localStorage)
2. Submit when online (n8n webhook)
3. Retry if submission fails (data preserved)
4. Data is backed up locally AND centrally

Your n8n workflow will receive all submissions with proper structure for MongoDB storage and company-wide analysis.





