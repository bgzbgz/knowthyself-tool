# AI Insights - Quick Start Guide

## 🚀 Get AI-Powered Insights Running in 30 Minutes

This guide will help you set up the AI-powered insights feature that generates profound, personalized analysis of your clients' "Know Thyself" responses.

---

## Prerequisites

1. **n8n account** (Cloud or Self-hosted)
   - Cloud: https://n8n.io (Easiest, $20/month)
   - Self-hosted: https://docs.n8n.io/hosting/ (Free, requires server)

2. **OpenAI API Key**
   - Sign up: https://platform.openai.com
   - Get API key: https://platform.openai.com/api-keys
   - Add $10-20 credit (each analysis costs ~$0.15-0.30)

---

## Step 1: Set Up n8n (5 minutes)

### Option A: n8n Cloud (Recommended)
1. Go to https://n8n.io
2. Click "Start for free"
3. Create account
4. You'll get a URL like: `https://your-name.app.n8n.cloud`

### Option B: Self-Hosted
```bash
# Using Docker
docker run -it --rm \
  --name n8n \
  -p 5678:5678 \
  -v ~/.n8n:/home/node/.n8n \
  n8nio/n8n

# Access at: http://localhost:5678
```

---

## Step 2: Add OpenAI Credentials (2 minutes)

1. In n8n, go to **Settings** → **Credentials**
2. Click **Add Credential**
3. Search for "OpenAI"
4. Enter your OpenAI API key
5. Click **Save**
6. Note the credential ID for later

---

## Step 3: Import the Workflow (3 minutes)

1. Download `n8n-insights-workflow.json` from your project
2. In n8n, click **Workflows** → **Import from File**
3. Select `n8n-insights-workflow.json`
4. The workflow will be imported with all nodes

---

## Step 4: Configure the Workflow (5 minutes)

### Update OpenAI Credentials
1. Click on each OpenAI node (there are 5):
   - AI - Dream Analysis
   - AI - Strengths Analysis
   - AI - Values Analysis
   - AI - Growth Analysis
   - AI - Integration

2. For each node:
   - Click on the node
   - Under "Credentials", select your OpenAI credential
   - Click "Save"

### Get Your Webhook URL
1. Click on the **Webhook** node (first node)
2. Click **Execute Node** (or activate the workflow)
3. Copy the "Test URL" or "Production URL"
4. It will look like:
   ```
   https://your-name.app.n8n.cloud/webhook/know-thyself-insights
   ```

---

## Step 5: Test the Workflow (5 minutes)

### Test with Sample Data

Use a tool like Postman, or run this in PowerShell:

```powershell
$body = @{
    birthdayStory = "On my 80th birthday, I'm surrounded by entrepreneurs I've mentored who changed the world..."
    whatLove = "Teaching, mentoring, and seeing people grow"
    makeHappen = "Help 1000 entrepreneurs build successful, meaningful businesses"
    biggestFear = "Not making enough impact"
    painPoints = "Spreading myself too thin"
    idealLife = "Teaching, traveling, and inspiring change"
    strengths = @("Leadership", "Communication", "Empathy", "Strategic Thinking", "Creativity")
    activities = @("Public speaking", "One-on-one coaching", "Writing", "Problem solving", "Networking")
    actionPlan = "Focus on my top 3 strengths in my daily work"
    values = @(
        @{ value = "Growth"; why = "Constant evolution"; alignment = 80 }
        @{ value = "Impact"; why = "Making a difference"; alignment = 70 }
        @{ value = "Freedom"; why = "Autonomy matters"; alignment = 60 }
        @{ value = "Connection"; why = "Relationships are key"; alignment = 75 }
        @{ value = "Excellence"; why = "Quality over quantity"; alignment = 85 }
    )
    goals = @(
        @{ 
            goal = "Launch online mentorship program"
            why = "Scale my impact"
            challenges = "Time and technical skills"
            actionPlan = "Hire a tech partner, dedicate 10 hours/week"
            targetDate = "2024-06-01"
            successMetrics = "100 members enrolled"
        }
    )
    email = "test@example.com"
} | ConvertTo-Json -Depth 10

Invoke-RestMethod -Uri "YOUR_WEBHOOK_URL_HERE" -Method Post -Body $body -ContentType "application/json"
```

**Expected Result:** You should receive a JSON response with profound insights in ~15-30 seconds.

---

## Step 6: Integrate with Your Tool (10 minutes)

### Update index.html

1. Open `index.html`
2. Find the `CanvasView` component (around line 2189)
3. Add state for insights:

```javascript
const [isGeneratingInsights, setIsGeneratingInsights] = useState(false);
const [aiInsights, setAiInsights] = useState(null);
const [showInsightsModal, setShowInsightsModal] = useState(false);
```

4. Add the function to call n8n:

```javascript
const handleGenerateInsights = async () => {
  setIsGeneratingInsights(true);
  
  try {
    const response = await fetch('YOUR_N8N_WEBHOOK_URL', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify(formData)
    });
    
    if (!response.ok) throw new Error('Failed to generate insights');
    
    const insights = await response.json();
    setAiInsights(insights);
    setShowInsightsModal(true);
  } catch (error) {
    console.error('Error generating insights:', error);
    alert('Unable to generate insights. Please try again later.');
  } finally {
    setIsGeneratingInsights(false);
  }
};
```

5. Add a button in the Summary Dashboard (after Export/Share/Submit buttons):

```javascript
<button
  onClick={handleGenerateInsights}
  disabled={isGeneratingInsights}
  className="px-6 py-3 bg-green-500 text-white rounded-lg hover:bg-green-600 transition-colors font-medium disabled:opacity-50 disabled:cursor-not-allowed"
>
  {isGeneratingInsights ? (
    <>
      <span className="inline-block animate-spin mr-2">⏳</span>
      Generating Your Insights...
    </>
  ) : (
    'Generate AI Insights'
  )}
</button>
```

6. Add the Insights Modal component:

```javascript
const InsightsModal = ({ insights, onClose }) => {
  if (!insights) return null;
  
  return (
    <div className="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center p-4 z-50 overflow-y-auto">
      <div className="bg-white rounded-lg max-w-4xl w-full max-h-[90vh] overflow-y-auto">
        <div className="sticky top-0 bg-white border-b px-6 py-4 flex justify-between items-center">
          <h2 className="text-2xl font-bold">Your Personalized Insights</h2>
          <button onClick={onClose} className="text-gray-500 hover:text-gray-700 text-2xl">×</button>
        </div>
        
        <div className="p-6 space-y-8">
          {/* Dream & Purpose */}
          <section>
            <h3 className="text-xl font-bold mb-4 border-l-4 border-green-500 pl-4">Your Dream & Purpose</h3>
            <div className="space-y-4">
              <div>
                <h4 className="text-green-600 font-semibold text-sm uppercase mb-2">The Deeper Purpose</h4>
                <p className="text-gray-700">{insights.dreamAndPurpose.deeperPurpose}</p>
              </div>
              <div>
                <h4 className="text-green-600 font-semibold text-sm uppercase mb-2">The Hidden Pattern</h4>
                <p className="text-gray-700">{insights.dreamAndPurpose.hiddenPattern}</p>
              </div>
              <div>
                <h4 className="text-green-600 font-semibold text-sm uppercase mb-2">The Breakthrough Insight</h4>
                <p className="text-gray-700">{insights.dreamAndPurpose.breakthroughInsight}</p>
              </div>
              <div>
                <h4 className="text-green-600 font-semibold text-sm uppercase mb-2">The North Star</h4>
                <p className="text-gray-700">{insights.dreamAndPurpose.northStar}</p>
              </div>
            </div>
          </section>
          
          {/* Strengths */}
          <section>
            <h3 className="text-xl font-bold mb-4 border-l-4 border-green-500 pl-4">Your Unique Strengths</h3>
            <div className="space-y-4">
              <div>
                <h4 className="text-green-600 font-semibold text-sm uppercase mb-2">Your Unique Strength Signature</h4>
                <p className="text-gray-700">{insights.strengths.strengthSignature}</p>
              </div>
              <div>
                <h4 className="text-green-600 font-semibold text-sm uppercase mb-2">The Underutilized Strength</h4>
                <p className="text-gray-700">{insights.strengths.underutilizedStrength}</p>
              </div>
              <div>
                <h4 className="text-green-600 font-semibold text-sm uppercase mb-2">The Strength-Based Opportunity</h4>
                <p className="text-gray-700">{insights.strengths.strengthOpportunity}</p>
              </div>
            </div>
          </section>
          
          {/* Values */}
          <section>
            <h3 className="text-xl font-bold mb-4 border-l-4 border-green-500 pl-4">Your Core Values</h3>
            <div className="space-y-4">
              <div>
                <h4 className="text-green-600 font-semibold text-sm uppercase mb-2">The Values Conflict</h4>
                <p className="text-gray-700">{insights.values.valuesConflict}</p>
              </div>
              <div>
                <h4 className="text-green-600 font-semibold text-sm uppercase mb-2">The Alignment Gap</h4>
                <p className="text-gray-700">{insights.values.alignmentGap}</p>
              </div>
              <div>
                <h4 className="text-green-600 font-semibold text-sm uppercase mb-2">Your Values-Driven Decision Framework</h4>
                <p className="text-gray-700">{insights.values.decisionFramework}</p>
              </div>
            </div>
          </section>
          
          {/* Growth */}
          <section>
            <h3 className="text-xl font-bold mb-4 border-l-4 border-green-500 pl-4">Your Growth Path</h3>
            <div className="space-y-4">
              <div>
                <h4 className="text-green-600 font-semibold text-sm uppercase mb-2">The Keystone Goal</h4>
                <p className="text-gray-700">{insights.growth.keystoneGoal}</p>
              </div>
              <div>
                <h4 className="text-green-600 font-semibold text-sm uppercase mb-2">The Hidden Obstacle</h4>
                <p className="text-gray-700">{insights.growth.hiddenObstacle}</p>
              </div>
              <div>
                <h4 className="text-green-600 font-semibold text-sm uppercase mb-2">The 80/20 Lever</h4>
                <p className="text-gray-700">{insights.growth.eightyTwentyLever}</p>
              </div>
            </div>
          </section>
          
          {/* Integration */}
          <section>
            <h3 className="text-xl font-bold mb-4 border-l-4 border-green-500 pl-4">Your Integration & Next Steps</h3>
            <div className="space-y-4">
              <div>
                <h4 className="text-green-600 font-semibold text-sm uppercase mb-2">The Golden Thread</h4>
                <p className="text-gray-700">{insights.integration.goldenThread}</p>
              </div>
              <div>
                <h4 className="text-green-600 font-semibold text-sm uppercase mb-2">The Transformation Moment</h4>
                <p className="text-gray-700">{insights.integration.transformationMoment}</p>
              </div>
              <div>
                <h4 className="text-green-600 font-semibold text-sm uppercase mb-2">Your 90-Day Challenge</h4>
                <p className="text-gray-700">{insights.integration.ninetyDayChallenge}</p>
              </div>
            </div>
          </section>
          
          {/* Legacy Statement */}
          <section className="bg-green-50 p-6 rounded-lg border-l-4 border-green-500">
            <h4 className="text-green-600 font-semibold text-sm uppercase mb-2">Your Legacy Statement</h4>
            <p className="text-lg italic text-gray-900">{insights.integration.legacyStatement}</p>
          </section>
        </div>
        
        <div className="sticky bottom-0 bg-white border-t px-6 py-4">
          <button
            onClick={onClose}
            className="w-full px-6 py-3 bg-black text-white rounded-lg hover:bg-gray-800 transition-colors font-medium"
          >
            Close
          </button>
        </div>
      </div>
    </div>
  );
};
```

7. Render the modal:

```javascript
{showInsightsModal && (
  <InsightsModal 
    insights={aiInsights} 
    onClose={() => setShowInsightsModal(false)} 
  />
)}
```

---

## Cost Estimation

**Per Client Analysis:**
- Using GPT-4: ~$0.15-0.30
- Using GPT-3.5-turbo: ~$0.02-0.03

**Monthly Costs (100 clients):**
- GPT-4: $15-30
- GPT-3.5-turbo: $2-3

**Recommendation:** Start with GPT-3.5-turbo to test, upgrade to GPT-4 for better insights.

---

## Tips for Best Results

1. **Test with Real Data:** Use actual client responses to refine prompts
2. **Iterate on Prompts:** Adjust the AI prompts based on feedback
3. **Add Examples:** Include 2-3 example responses in prompts for consistency
4. **Set Temperature:** 0.7-0.9 for creative, insightful responses
5. **Monitor Costs:** Set up billing alerts in OpenAI dashboard
6. **Cache Insights:** Store in database to avoid re-generating
7. **Add Fallbacks:** Handle API failures gracefully

---

## Troubleshooting

### Webhook Returns 404
- Ensure workflow is activated (toggle at top right)
- Check webhook URL is correct
- Verify CORS settings if calling from browser

### AI Returns Generic Insights
- Lower temperature (0.6-0.7)
- Add more specific examples in prompts
- Increase max tokens for longer responses

### Slow Response Time
- Expect 15-30 seconds for all 5 AI calls
- Consider using GPT-3.5-turbo (faster, cheaper)
- Add loading spinner and progress indicators

### High Costs
- Switch from GPT-4 to GPT-3.5-turbo
- Reduce max tokens in each node
- Cache insights for returning users

---

## Next Steps

1. ✅ Set up n8n
2. ✅ Import workflow
3. ✅ Test with sample data
4. ✅ Integrate with tool
5. ⏭️ Test with 5-10 real clients
6. ⏭️ Collect feedback
7. ⏭️ Refine prompts
8. ⏭️ Launch to all clients!

---

## Support

- **n8n Docs:** https://docs.n8n.io
- **OpenAI Docs:** https://platform.openai.com/docs
- **Community:** n8n forum, Discord

Need help? Create an issue or reach out to your development team!

