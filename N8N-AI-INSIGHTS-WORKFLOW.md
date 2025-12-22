# N8N AI-Powered Insights Workflow

## Overview
This workflow receives the client's completed "Know Thyself" data and uses AI to generate profound, personalized insights that create "WOW" moments.

---

## Workflow Architecture

```
[Webhook Trigger] 
    ↓
[Extract & Structure Data]
    ↓
[AI Analysis - Dream & Purpose]
    ↓
[AI Analysis - Strengths Patterns]
    ↓
[AI Analysis - Values Alignment]
    ↓
[AI Analysis - Growth Opportunities]
    ↓
[AI Analysis - Cross-Section Integration]
    ↓
[Format Final Insights]
    ↓
[Send to Client] (Email/Display in Tool)
```

---

## N8N Workflow Setup

### Node 1: Webhook Trigger
- **Type:** Webhook
- **Method:** POST
- **Path:** `/know-thyself-insights`
- **Response:** Return immediately with "Analyzing your insights..."

### Node 2: Extract & Structure Data
- **Type:** Code (JavaScript)
- **Purpose:** Clean and structure the incoming data

```javascript
// Extract all form data
const data = {
  birthdayStory: $json.body.birthdayStory,
  whatLove: $json.body.whatLove,
  makeHappen: $json.body.makeHappen,
  biggestFear: $json.body.biggestFear,
  painPoints: $json.body.painPoints,
  idealLife: $json.body.idealLife,
  strengths: $json.body.strengths, // Array of 5
  activities: $json.body.activities, // Array of 5
  actionPlan: $json.body.actionPlan,
  values: $json.body.values, // Array of 5 objects with value, why, alignment
  goals: $json.body.goals, // Array of 3 goals with action plans
  email: $json.body.email,
  timestamp: new Date().toISOString()
};

return { json: data };
```

### Node 3: AI Analysis - Dream & Purpose
- **Type:** OpenAI (GPT-4 or GPT-3.5-turbo)
- **Purpose:** Analyze the deep purpose and vision

**Prompt:**
```
You are a world-class life coach and psychologist specializing in purpose discovery and self-actualization. Analyze the following information about a client and provide profound insights.

CLIENT'S 80TH BIRTHDAY STORY:
{{$json.birthdayStory}}

WHAT THEY LOVE DOING:
{{$json.whatLove}}

WHAT THEY WANT TO MAKE HAPPEN:
{{$json.makeHappen}}

BIGGEST FEAR:
{{$json.biggestFear}}

PAIN POINTS:
{{$json.painPoints}}

IDEAL LIFE:
{{$json.idealLife}}

Based on this, provide:

1. **THE DEEPER PURPOSE** (2-3 sentences): What is the underlying purpose or calling that connects all these elements? What is this person really trying to create in the world beyond surface goals?

2. **THE HIDDEN PATTERN** (2-3 sentences): What patterns do you see in what they love, fear, and desire? What does this reveal about their core identity?

3. **THE BREAKTHROUGH INSIGHT** (2-3 sentences): What is one profound insight they may not have realized about themselves? Something that will make them say "WOW, that's exactly it!"

4. **THE NORTH STAR** (1-2 sentences): If they stay true to this path described in their 80th birthday story, what is the ultimate impact they could have?

Keep insights personal, profound, and emotionally resonant. Avoid generic advice.
```

### Node 4: AI Analysis - Strengths Patterns
- **Type:** OpenAI
- **Purpose:** Identify strength synergies and unique combinations

**Prompt:**
```
You are an expert in positive psychology and strengths-based development. Analyze these strengths and activities:

TOP 5 STRENGTHS:
{{$json.strengths.join('\n')}}

TOP 5 ACTIVITIES WHERE THEY EXCEL:
{{$json.activities.join('\n')}}

THEIR STRENGTHS ACTION PLAN:
{{$json.actionPlan}}

Provide:

1. **THE UNIQUE STRENGTH SIGNATURE** (2-3 sentences): What is the unique combination of strengths that makes this person one-of-a-kind? How do these strengths work together to create their "superpower"?

2. **THE UNDERUTILIZED STRENGTH** (2-3 sentences): Which strength or activity pairing has the most untapped potential? How could they leverage this more?

3. **THE STRENGTH-BASED OPPORTUNITY** (2-3 sentences): Based on their action plan, what is one powerful way they could use their strengths that they haven't fully considered?

Be specific and insightful, not generic.
```

### Node 5: AI Analysis - Values Alignment
- **Type:** OpenAI
- **Purpose:** Analyze values conflicts and alignment opportunities

**Prompt:**
```
You are a values clarification expert and executive coach. Analyze these core values:

VALUES AND ALIGNMENT:
{{$json.values.map((v, i) => `
Value ${i+1}: ${v.value}
Why it matters: ${v.why}
Current alignment: ${v.alignment}%
`).join('\n')}}

Provide:

1. **THE VALUES CONFLICT** (2-3 sentences): Are there any values that might be in tension with each other? What internal conflict might this create, and how can they navigate it?

2. **THE ALIGNMENT GAP** (2-3 sentences): Which value has the biggest gap between importance and current alignment? What is this costing them, and what would change if they closed this gap?

3. **THE VALUES-DRIVEN DECISION FRAMEWORK** (2-3 sentences): Based on these values, what is the one filter they should use when making major life decisions?

Be psychologically insightful and practical.
```

### Node 6: AI Analysis - Growth Opportunities
- **Type:** OpenAI
- **Purpose:** Analyze goals and identify breakthrough opportunities

**Prompt:**
```
You are a strategic life planning expert. Analyze these personal growth goals:

GOALS:
{{$json.goals.map((g, i) => `
Goal ${i+1}: ${g.goal}
Why important: ${g.why}
Current challenges: ${g.challenges}
Action plan: ${g.actionPlan}
Target date: ${g.targetDate}
Success metrics: ${g.successMetrics}
`).join('\n')}}

Provide:

1. **THE KEYSTONE GOAL** (2-3 sentences): Which goal, if achieved, would make all the others easier or more meaningful? Why is this the most strategic starting point?

2. **THE HIDDEN OBSTACLE** (2-3 sentences): Based on the challenges they listed, what is the deeper psychological or systemic obstacle they need to address first?

3. **THE 80/20 LEVER** (2-3 sentences): What is the 20% of effort that would yield 80% of the results across all their goals? What should they focus on first?

Be strategic and actionable.
```

### Node 7: AI Analysis - Cross-Section Integration
- **Type:** OpenAI
- **Purpose:** Synthesize all sections into one coherent insight

**Prompt:**
```
You are a master synthesist and transformational coach. You have analyzed this client's dreams, strengths, values, and goals. Now create the ultimate integration.

DREAM & PURPOSE INSIGHTS:
{{$node["AI Analysis - Dream & Purpose"].json.choices[0].message.content}}

STRENGTHS INSIGHTS:
{{$node["AI Analysis - Strengths Patterns"].json.choices[0].message.content}}

VALUES INSIGHTS:
{{$node["AI Analysis - Values Alignment"].json.choices[0].message.content}}

GROWTH INSIGHTS:
{{$node["AI Analysis - Growth Opportunities"].json.choices[0].message.content}}

Provide:

1. **THE GOLDEN THREAD** (3-4 sentences): What is the one unifying theme that connects their dreams, strengths, values, and goals? What is the coherent story of who they are becoming?

2. **THE TRANSFORMATION MOMENT** (2-3 sentences): What is the most important realization or shift they need to make right now to align all these elements?

3. **THE 90-DAY CHALLENGE** (2-3 sentences): If they could only focus on ONE thing for the next 90 days that would create the biggest breakthrough across all areas, what would it be?

4. **THE LEGACY STATEMENT** (1-2 sentences): Based on everything, complete this sentence: "At your core, you are someone who..."

This should be deeply personal and create a "WOW" moment of self-recognition.
```

### Node 8: Format Final Insights
- **Type:** Code (JavaScript)
- **Purpose:** Structure all insights into a beautiful format

```javascript
const insights = {
  header: {
    name: $json.email.split('@')[0], // or actual name if collected
    generatedAt: new Date().toISOString(),
    title: "Your Personalized Know Thyself Insights"
  },
  
  dreamAndPurpose: {
    title: "Your Dream & Purpose",
    deeperPurpose: extractSection($node["AI Analysis - Dream & Purpose"].json.choices[0].message.content, "THE DEEPER PURPOSE"),
    hiddenPattern: extractSection($node["AI Analysis - Dream & Purpose"].json.choices[0].message.content, "THE HIDDEN PATTERN"),
    breakthroughInsight: extractSection($node["AI Analysis - Dream & Purpose"].json.choices[0].message.content, "THE BREAKTHROUGH INSIGHT"),
    northStar: extractSection($node["AI Analysis - Dream & Purpose"].json.choices[0].message.content, "THE NORTH STAR")
  },
  
  strengthsAnalysis: {
    title: "Your Unique Strengths",
    strengthSignature: extractSection($node["AI Analysis - Strengths Patterns"].json.choices[0].message.content, "THE UNIQUE STRENGTH SIGNATURE"),
    underutilizedStrength: extractSection($node["AI Analysis - Strengths Patterns"].json.choices[0].message.content, "THE UNDERUTILIZED STRENGTH"),
    strengthOpportunity: extractSection($node["AI Analysis - Strengths Patterns"].json.choices[0].message.content, "THE STRENGTH-BASED OPPORTUNITY")
  },
  
  valuesInsights: {
    title: "Your Core Values",
    valuesConflict: extractSection($node["AI Analysis - Values Alignment"].json.choices[0].message.content, "THE VALUES CONFLICT"),
    alignmentGap: extractSection($node["AI Analysis - Values Alignment"].json.choices[0].message.content, "THE ALIGNMENT GAP"),
    decisionFramework: extractSection($node["AI Analysis - Values Alignment"].json.choices[0].message.content, "THE VALUES-DRIVEN DECISION FRAMEWORK")
  },
  
  growthOpportunities: {
    title: "Your Growth Path",
    keystoneGoal: extractSection($node["AI Analysis - Growth Opportunities"].json.choices[0].message.content, "THE KEYSTONE GOAL"),
    hiddenObstacle: extractSection($node["AI Analysis - Growth Opportunities"].json.choices[0].message.content, "THE HIDDEN OBSTACLE"),
    eightyTwentyLever: extractSection($node["AI Analysis - Growth Opportunities"].json.choices[0].message.content, "THE 80/20 LEVER")
  },
  
  integration: {
    title: "Your Integration & Next Steps",
    goldenThread: extractSection($node["AI Analysis - Cross-Section Integration"].json.choices[0].message.content, "THE GOLDEN THREAD"),
    transformationMoment: extractSection($node["AI Analysis - Cross-Section Integration"].json.choices[0].message.content, "THE TRANSFORMATION MOMENT"),
    ninetyDayChallenge: extractSection($node["AI Analysis - Cross-Section Integration"].json.choices[0].message.content, "THE 90-DAY CHALLENGE"),
    legacyStatement: extractSection($node["AI Analysis - Cross-Section Integration"].json.choices[0].message.content, "THE LEGACY STATEMENT")
  }
};

function extractSection(text, sectionHeader) {
  const regex = new RegExp(`\\*\\*${sectionHeader}\\*\\*[:\\s]*(.+?)(?=\\n\\n|\\*\\*|$)`, 's');
  const match = text.match(regex);
  return match ? match[1].trim() : '';
}

return { json: insights };
```

### Node 9: Send to Client (Option A - Email)
- **Type:** Send Email (or Gmail node)
- **Purpose:** Send beautifully formatted insights

**Subject:** `Your Personalized Know Thyself Insights - A Deep Dive Into Who You Are`

**Body Template:**
```html
<!DOCTYPE html>
<html>
<head>
  <style>
    body { font-family: 'Inter', -apple-system, BlinkMacSystemFont, sans-serif; line-height: 1.6; color: #1a1a1a; max-width: 700px; margin: 0 auto; padding: 20px; }
    h1 { color: #000; font-size: 32px; font-weight: 700; margin-bottom: 10px; }
    h2 { color: #000; font-size: 24px; font-weight: 700; margin-top: 40px; margin-bottom: 20px; border-left: 4px solid #22c55e; padding-left: 16px; }
    h3 { color: #22c55e; font-size: 16px; font-weight: 600; margin-top: 24px; margin-bottom: 8px; text-transform: uppercase; letter-spacing: 0.5px; }
    p { margin-bottom: 16px; color: #333; }
    .header { background: #f9fafb; padding: 30px; border-radius: 8px; margin-bottom: 40px; }
    .section { background: white; padding: 30px; margin-bottom: 24px; border: 1px solid #e5e7eb; border-radius: 8px; }
    .legacy { background: #f0fdf4; padding: 24px; border-left: 4px solid #22c55e; margin-top: 40px; border-radius: 8px; }
    .footer { margin-top: 60px; padding-top: 30px; border-top: 2px solid #e5e7eb; text-align: center; color: #6b7280; }
  </style>
</head>
<body>
  <div class="header">
    <h1>Your Know Thyself Insights</h1>
    <p style="color: #6b7280; font-size: 14px;">Generated on {{$json.header.generatedAt}}</p>
  </div>

  <div class="section">
    <h2>Your Dream & Purpose</h2>
    
    <h3>The Deeper Purpose</h3>
    <p>{{$json.dreamAndPurpose.deeperPurpose}}</p>
    
    <h3>The Hidden Pattern</h3>
    <p>{{$json.dreamAndPurpose.hiddenPattern}}</p>
    
    <h3>The Breakthrough Insight</h3>
    <p>{{$json.dreamAndPurpose.breakthroughInsight}}</p>
    
    <h3>The North Star</h3>
    <p>{{$json.dreamAndPurpose.northStar}}</p>
  </div>

  <div class="section">
    <h2>Your Unique Strengths</h2>
    
    <h3>Your Unique Strength Signature</h3>
    <p>{{$json.strengthsAnalysis.strengthSignature}}</p>
    
    <h3>The Underutilized Strength</h3>
    <p>{{$json.strengthsAnalysis.underutilizedStrength}}</p>
    
    <h3>The Strength-Based Opportunity</h3>
    <p>{{$json.strengthsAnalysis.strengthOpportunity}}</p>
  </div>

  <div class="section">
    <h2>Your Core Values</h2>
    
    <h3>The Values Conflict</h3>
    <p>{{$json.valuesInsights.valuesConflict}}</p>
    
    <h3>The Alignment Gap</h3>
    <p>{{$json.valuesInsights.alignmentGap}}</p>
    
    <h3>Your Values-Driven Decision Framework</h3>
    <p>{{$json.valuesInsights.decisionFramework}}</p>
  </div>

  <div class="section">
    <h2>Your Growth Path</h2>
    
    <h3>The Keystone Goal</h3>
    <p>{{$json.growthOpportunities.keystoneGoal}}</p>
    
    <h3>The Hidden Obstacle</h3>
    <p>{{$json.growthOpportunities.hiddenObstacle}}</p>
    
    <h3>The 80/20 Lever</h3>
    <p>{{$json.growthOpportunities.eightyTwentyLever}}</p>
  </div>

  <div class="section">
    <h2>Your Integration & Next Steps</h2>
    
    <h3>The Golden Thread</h3>
    <p>{{$json.integration.goldenThread}}</p>
    
    <h3>The Transformation Moment</h3>
    <p>{{$json.integration.transformationMoment}}</p>
    
    <h3>Your 90-Day Challenge</h3>
    <p>{{$json.integration.ninetyDayChallenge}}</p>
  </div>

  <div class="legacy">
    <h3>Your Legacy Statement</h3>
    <p style="font-size: 18px; font-style: italic; color: #000;">{{$json.integration.legacyStatement}}</p>
  </div>

  <div class="footer">
    <p>Keep these insights close. Review them regularly. Let them guide your decisions.</p>
    <p style="font-size: 12px; margin-top: 20px;">© Fast Track - Know Thyself Tool</p>
  </div>
</body>
</html>
```

### Node 9: Send to Client (Option B - Return to Tool)
- **Type:** Webhook Response
- **Purpose:** Send JSON back to the tool to display insights

Return the `insights` object as JSON, and modify the tool to display it in a new "Your Insights" screen.

---

## Integration with Current Tool

### Update index.html

Add a new function to request insights after canvas is complete:

```javascript
const handleGenerateInsights = async () => {
  setIsGeneratingInsights(true);
  
  try {
    const response = await fetch('https://your-n8n-instance.com/webhook/know-thyself-insights', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify(formData)
    });
    
    const insights = await response.json();
    setAiInsights(insights);
    setShowInsightsModal(true);
  } catch (error) {
    console.error('Error generating insights:', error);
    alert('Unable to generate insights. Please try again.');
  } finally {
    setIsGeneratingInsights(false);
  }
};
```

Add a button in the Canvas view:

```javascript
<button
  onClick={handleGenerateInsights}
  className="w-full px-8 py-4 bg-gradient-to-r from-green-500 to-green-600 text-white rounded-lg hover:from-green-600 hover:to-green-700 transition-all duration-300 font-bold text-lg shadow-lg"
  disabled={isGeneratingInsights}
>
  {isGeneratingInsights ? 'Analyzing Your Journey...' : 'Generate AI-Powered Insights'}
</button>
```

---

## Estimated Costs

**Using OpenAI GPT-4:**
- ~5 API calls per analysis
- ~2,000-3,000 tokens per call
- Total: ~10,000-15,000 tokens per client
- Cost: ~$0.15-0.30 per analysis

**Using OpenAI GPT-3.5-turbo:**
- Cost: ~$0.02-0.03 per analysis

---

## Advanced Features to Consider

1. **Insights History**: Store all insights in a database and let clients see how they evolve over time
2. **PDF Generation**: Generate a beautiful PDF report of insights
3. **Insights Comparison**: Compare insights if they retake the tool in 6 months
4. **Coach Dashboard**: Coaches can review AI insights before sending to clients
5. **Custom Prompts**: Allow coaches to customize the AI prompts per client
6. **Multi-language Support**: Generate insights in the client's preferred language
7. **Voice Insights**: Use ElevenLabs to create an audio version of insights

---

## Implementation Timeline

- **Phase 1** (2-3 hours): Set up basic n8n workflow with OpenAI integration
- **Phase 2** (2-3 hours): Test and refine AI prompts for quality insights
- **Phase 3** (2-3 hours): Integrate with the HTML tool
- **Phase 4** (1-2 hours): Design beautiful email template
- **Phase 5** (Ongoing): Collect feedback and improve prompts

---

## Next Steps

1. Set up n8n instance (self-hosted or cloud)
2. Get OpenAI API key
3. Import this workflow into n8n
4. Test with sample data
5. Refine prompts based on output quality
6. Integrate with the tool
7. Launch and collect feedback!

This AI-powered insights feature will transform your "Know Thyself" tool from a reflection exercise into a profound self-discovery experience that creates real "WOW" moments.

