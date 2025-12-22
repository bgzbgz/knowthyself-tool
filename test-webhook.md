# Test N8N Webhook

## Quick Test with curl

### Windows PowerShell
```powershell
$body = Get-Content test-payload-example.json -Raw
Invoke-RestMethod -Uri "https://n8n-edge.fasttrack-diagnostic.com/webhook/608b17ea-9618-4877-ae3c-85eb2e89b700" -Method POST -Body $body -ContentType "application/json"
```

### macOS/Linux
```bash
curl -X POST \
  https://n8n-edge.fasttrack-diagnostic.com/webhook/608b17ea-9618-4877-ae3c-85eb2e89b700 \
  -H "Content-Type: application/json" \
  -d @test-payload-example.json
```

### Using Postman
1. Create new request
2. Set method to **POST**
3. URL: `https://n8n-edge.fasttrack-diagnostic.com/webhook/608b17ea-9618-4877-ae3c-85eb2e89b700`
4. Headers:
   - `Content-Type: application/json`
5. Body (raw JSON):
   - Paste contents from `test-payload-example.json`
6. Click **Send**

### Expected Response
```json
{
  "success": true,
  "message": "Data received",
  "id": "some-mongodb-id"
}
```

## Browser Console Test

You can also test directly from the browser console (F12):

```javascript
fetch('https://n8n-edge.fasttrack-diagnostic.com/webhook/608b17ea-9618-4877-ae3c-85eb2e89b700', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({
    toolName: 'know_thyself',
    userId: 'test@fasttrack.com',
    sprintNumber: 1,
    timestamp: new Date().toISOString(),
    data: {
      userName: 'Test User',
      userEmail: 'test@fasttrack.com',
      dream: 'Test submission'
    }
  })
})
.then(r => r.json())
.then(data => console.log('Success:', data))
.catch(err => console.error('Error:', err));
```

## Verify in n8n

After sending test payload:
1. Go to your n8n workflow
2. Check execution history
3. Verify webhook triggered
4. Check MongoDB for new entry
5. Verify all fields mapped correctly

## Common Responses

### ✅ Success (200 OK)
```json
{ "success": true }
```

### ❌ Bad Request (400)
```json
{ "error": "Missing required field: toolName" }
```

### ❌ Server Error (500)
```json
{ "error": "Internal server error" }
```

### ❌ CORS Error
```
Access to fetch has been blocked by CORS policy
```
**Fix:** Add CORS headers to n8n webhook response

## Troubleshooting

| Error | Cause | Solution |
|-------|-------|----------|
| Failed to fetch | Network/CORS | Check internet, verify n8n CORS settings |
| 400 Bad Request | Wrong payload structure | Check field names match n8n expectations |
| 500 Server Error | n8n workflow error | Check n8n workflow logs |
| Timeout | n8n slow/down | Check n8n server status |

## MongoDB Query

After successful submission, query MongoDB:

```javascript
db.know_thyself.find({ userId: "ivan@fasttrack.com" })
```

Expected document:
```json
{
  "_id": ObjectId("..."),
  "toolName": "know_thyself",
  "userId": "ivan@fasttrack.com",
  "sprintNumber": 1,
  "timestamp": ISODate("2024-12-16T14:30:00.000Z"),
  "data": { ... },
  "createdAt": ISODate("2024-12-16T14:30:01.123Z")
}
```





