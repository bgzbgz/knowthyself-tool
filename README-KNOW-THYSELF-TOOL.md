# Know Thyself Tool - Fast Track (v2.0)

## 🎯 Overview
Comprehensive interactive tool for the "Power of Knowing Yourself" sprint in Fast Track's Individual and Company Identity module. **Now with full Fast Track style matching Market Size and WOOP tools!**

## ✨ What's NEW in v2.0

### 🎨 Dramatic Opening
- ✅ **Cover page** with `manki-kim-BtHjHxh-D7I-unsplash.jpg` image
- ✅ **Large title** (text-9xl) "KNOW THYSELF"
- ✅ Overlay gradient for professional look
- ✅ START button that transforms on hover
- ✅ **Fast Track philosophy quote** on intro screen

### 🖤 Black Intro Screen
- ✅ **PURPOSE** section - brutal, direct copy
- ✅ **MISTAKES TO AVOID** in yellow highlight
- ✅ **THE JOURNEY** grid showing all 4 sections (01-04)
- ✅ Large fonts (text-9xl, text-6xl) matching other tools

### 🏆 Celebration Screens (NOT Childish)
- ✅ **Bold milestone statements** (DREAM DEFINED, VALUES ALIGNED, etc.)
- ✅ **Progress metrics** (25%, 50%, 75%, 100%)
- ✅ **Black background** with white text - sophisticated
- ✅ **Auto-advance** (2 seconds) - quick, confident
- ✅ **No emojis, no confetti** - Fast Track DNA maintained
- ✅ Clean progress bars and Monument font percentage display

### ❓ Help System
- ✅ **Help button (?)** - Fixed top-right, yellow hover
- ✅ **HelpModal** - Shows WHY/WHAT/HOW for each section
- ✅ Context-specific help content
- ✅ "GOT IT" button to close

### 📊 Canvas View (Final Summary)
- ✅ **Aristotle quote** at top: "To know yourself is the beginning of all wisdom"
- ✅ Comprehensive summary of all 4 sections
- ✅ Visual cards for each section
- ✅ **Share With Team** button (LOCKED IN confirmation)
- ✅ **Export PDF** button
- ✅ **Final Submit** button (powerful alerts, no emojis)
- ✅ Edit button to go back

### 🎯 Better UX
- ✅ Horizontal progress indicator with dots
- ✅ Smooth animations (slideIn, fadeIn)
- ✅ Professional color coding (green, yellow, blue, red borders)
- ✅ Real-time validation with green checkmarks
- ✅ Character counters on all text fields

## 🚀 Features Implemented

### Four Integrated Sections:
1. **Dream Launcher** - Define personal dream aligned with values
2. **Values Compass** - Align values with professional actions  
3. **Strengths Amplifier** - Identify and leverage natural strengths
4. **Personal Growth Blueprint** - Create actionable growth roadmap

### ✅ 8-Point Tool Criteria (ALL MET):
1. ✅ **Forces final clear decision** - Canvas view shows complete summary
2. ✅ **Zero questions needed** - Help button always available, inline guidance
3. ✅ **Easy first steps** - Simple text inputs build to deeper reflection
4. ✅ **Instant feedback** - Real-time validation with red/green states & character counts
5. ✅ **Gamification** - Progress dots, animations, section unlocking, completion badges
6. ✅ **Crystal clear results** - Canvas view shows all insights in organized format
7. ✅ **Public commitment** - Share with team functionality + Final Submit
8. ✅ **Smells like Fast Track** - Matches Market Size & WOOP tool style perfectly

### Design System Compliance:
- ✅ **Plaak** font for headings (text-9xl for cover, text-6xl for sections)
- ✅ **Riforma** font for body text
- ✅ **Monument Grotesk Mono** for labels
- ✅ Black/White/Grey color palette
- ✅ Yellow (#fff469) highlights for emphasis
- ✅ 4px black left border on context boxes
- ✅ Numbered sections with black backgrounds

### User Experience:
- ✅ **Cover page** - Dramatic opening with image
- ✅ **Intro screen** - Black background with PURPOSE, MISTAKES, JOURNEY
- ✅ **Progressive disclosure** - Sections unlock sequentially
- ✅ **Auto-save** - Data persists in localStorage
- ✅ **Real-time validation** - Immediate feedback on all inputs
- ✅ **Smooth animations** - Professional transitions (0.3s slideIn, 0.5s fadeIn)
- ✅ **Help button** - Always accessible, yellow hover effect
- ✅ **Canvas view** - Final summary page with all insights
- ✅ **Print-friendly** - PDF export capability

### Technical:
- ✅ **Single HTML file** - No build process needed
- ✅ **React 18** - Embedded via CDN
- ✅ **TailwindCSS** - For styling
- ✅ **localStorage** - Data persistence
- ✅ **n8n webhooks** - Ready for integration
- ✅ **PDF libraries** - jsPDF + html2canvas for export
- ✅ **Offline-capable** - After first load

## 📋 How to Use

### 1. Setup
- Place font files in same directory:
  - `Plaak3Trial-43-Bold.otf`
  - `RiformaLL-Regular.otf`
  - `MonumentGrotesk-Mono.otf`
- Place cover image: `manki-kim-BtHjHxh-D7I-unsplash.jpg`

### 2. Configuration
- Update webhook URLs in the code (line 222-226):
```javascript
const CONFIG = {
    AUTOSAVE_WEBHOOK: 'YOUR_N8N_AUTOSAVE_WEBHOOK_URL',
    SHARE_WEBHOOK: 'YOUR_N8N_SHARE_WEBHOOK_URL',
    SUBMIT_WEBHOOK: 'YOUR_N8N_SUBMIT_WEBHOOK_URL',
    STORAGE_KEY: 'fasttrack_know_thyself_data'
};
```

### 3. User Journey

```
COVER PAGE (Step 0)
    ↓ Click START
BLACK INTRO SCREEN (Step 0.5)
    ↓ Click LET'S START
SECTION 1: Dream Launcher
    ↓ Complete & click Next
SECTION 2: Values Compass
    ↓ Complete & click Next
SECTION 3: Strengths Amplifier
    ↓ Complete & click Next
SECTION 4: Growth Blueprint
    ↓ Complete & click View Canvas
CANVAS VIEW (Step 999)
    ↓ Share / Export / Submit
```

### 4. Individual Uses Tool
- Opens with dramatic cover page
- Reads intro with PURPOSE and MISTAKES
- Completes all 4 sections (progressive unlock)
- Takes ~45-90 minutes
- Auto-saves progress throughout
- Views final canvas summary
- Shares with team or exports PDF

### 5. Guru-Led Meeting
- Individuals bring completed canvas
- Share discoveries in team meeting
- Build team cohesion through shared insights

## 🎨 Design Comparisons

### vs Market Size Tool:
- ✅ Same cover page style
- ✅ Same black intro screen
- ✅ Same help button (?)
- ✅ Same large fonts (text-9xl)
- ✅ Same progress indicator style

### vs WOOP Tool:
- ✅ Same canvas view at end
- ✅ Same multi-button export (Share/Export/Submit)
- ✅ Same celebration elements
- ✅ Same validation messaging
- ✅ Same autosave functionality

## 🔧 Validation Rules

### Section 1 - Dream Launcher:
- Dream: minimum 20 characters
- Alignment: minimum 20 characters
- Real-time character counters
- Green checkmarks on valid input

### Section 2 - Values Compass:
- Three core values: minimum 2 characters each
- Three value alignments with current/ideal ratings (1-10)
- Gap detection warns if gap > 2 points
- Red warning for significant gaps

### Section 3 - Strengths Amplifier:
- Three strengths: minimum 3 characters each
- Application strategy: minimum 20 characters
- Green success feedback on valid entries

### Section 4 - Personal Growth Blueprint:
- Two goals required
- Goal: minimum 10 characters
- Action steps: minimum 15 characters
- Deadline: date picker (future dates only)
- 90-day commitment: minimum 30 characters
- Green success messages on completion

## 🎯 Target Audience Fit

Built for **Elite YPO CEOs** who:
- ✅ Have zero tolerance for instructions (help button on demand)
- ✅ Possess high pattern recognition (familiar UI patterns from other tools)
- ✅ Expect iPhone-standard quality (smooth, premium animations)
- ✅ Are time-constrained (progressive, efficient, autosave)
- ✅ Value brutal honesty (direct validation messages)

## 📤 Data Flow

```
Cover page → Intro screen
    ↓
Individual completes 4 sections
    ↓
Auto-saves to localStorage (every 1 second)
    ↓
Sends to n8n webhook (autosave)
    ↓
Completes all sections
    ↓
Views Canvas summary
    ↓
Shares with team (webhook)
    ↓
Exports to PDF
    ↓
Final Submit (webhook)
    ↓
Brings to Guru-led meeting
```

## 🚦 Status

**READY FOR TESTING** ✅

### What's NEW:
1. ✅ Dramatic cover page with image
2. ✅ Black intro screen with PURPOSE/MISTAKES/JOURNEY
3. ✅ Help button (?) with modal
4. ✅ Canvas view with comprehensive summary
5. ✅ Much larger fonts matching other tools
6. ✅ Better validation with green checkmarks
7. ✅ Character counters on all inputs
8. ✅ Professional animations throughout
9. ✅ Color-coded sections for visual hierarchy
10. ✅ Multiple export options (Share/Export/Submit)

### Next Steps:
1. Add your n8n webhook URLs
2. Test with real users
3. Gather feedback
4. Iterate based on CEO feedback

## 📝 Files Included

- `know-thyself-tool.html` - Complete tool (all-in-one)
- `README-KNOW-THYSELF-TOOL.md` - This file
- `TESTING-CHECKLIST.md` - QA checklist
- `manki-kim-BtHjHxh-D7I-unsplash.jpg` - Cover image (required)
- Font files (required):
  - `Plaak3Trial-43-Bold.otf`
  - `RiformaLL-Regular.otf`
  - `MonumentGrotesk-Mono.otf`

## 🎓 Guru Integration

This tool is designed to be completed **BEFORE** the team meeting. The Guru:
- Does NOT fill out this tool
- Facilitates team meeting where participants share their insights
- Uses shared results to build team cohesion
- Guides discussion based on discoveries from the canvas

---

## 🎉 Improvements from v1.0

| Feature | v1.0 | v2.0 |
|---------|------|------|
| Cover page | ❌ | ✅ With image |
| Intro screen | ❌ | ✅ Black with PURPOSE/MISTAKES |
| Help button | ❌ | ✅ Fixed top-right with yellow hover |
| Help modal | ❌ | ✅ WHY/WHAT/HOW for each section |
| Font sizes | Small | ✅ Large (text-9xl, text-6xl) |
| Canvas view | ❌ | ✅ Comprehensive summary |
| Validation feedback | Basic | ✅ Character counters + green checkmarks |
| Export options | Basic | ✅ Share + Export + Submit |
| Animations | Simple | ✅ Professional (slideIn, fadeIn) |
| Progress indicator | Dots only | ✅ Dots + connecting lines |

**Built with ❤️ for Fast Track's elite CEO program - Now matching Market Size & WOOP tool style!**
