## 👨‍👩‍👧 Core Accounts

1. **Parent**
    
2. **Kid**
    

---

## 📚 Learning Content (static / seeded)

3. **Subject**
    
4. **Topic**
    
5. **Question**
    

---

## ⚙️ Parent Control & Configuration

6. **ParentTopicSettings**
    
7. **ParentKidSettings** _(optional global rules)_
    
8. **ParentDashboardConfig**
    

---

## ⏱️ Runtime / Learning Activity

9. **LearningSession**
    
10. **Attempt**
    
11. **TimeTracking** _(optional fine-grained timing)_
    

---

## 📈 Progress & State (derived but stored)

12. **TopicProgress**
    
13. **SubjectProgress** _(optional)_
    

---

## 📊 Analytics & Display (for parent UI)

14. **AnalyticsSnapshot**
    
15. **TopicAnalyticsSnapshot**
    

---

## 💡 Suggestions & Transparency

16. **Recommendation**
    
17. **RecommendationReason**
    

---

## 🔄 History & Auditing (explain “why”)

18. **DifficultyHistory**
    
19. **TopicUnlockHistory**
    

---

## ✅ Minimal MVP (if you want to cut down)

**Absolutely required only:**

- Parent
    
- Kid
    
- Subject
    
- Topic
    
- Question
    
- ParentTopicSettings
    
- LearningSession
    
- Attempt
    
- TopicProgress
    

Everything else = **analytics quality & UX improvement**

---

If you want, next I can:

- Tag tables as **Phase 1 / Phase 2 / Phase 3**
    
- Collapse tables for a **leaner version**
    
- Start generating **one table at a time** (SQL + JPA)
    
- Map **each dashboard chart → table(s)**
    

Just tell me 👍

how can we display analytics for parents, suggest not much exp

Great question — and you’re right to ask for **“not much exp”** 👍  
For parents, analytics must be **simple, visual, and reassuring**, not technical.

Below is a **minimal, parent-friendly analytics approach**, based on the tables you already have.

---

## 🎯 Parent Analytics Goal (keep this rule)

> A parent should understand their child’s learning status in **under 10 seconds**.

So we focus on **4 simple sections only**.

---

# 1️⃣ “Today / This Week” Summary (TOP CARD)

**What parents see**

- ⏱️ Time spent learning
    
- ✅ Correct answers
    
- 📈 Overall accuracy
    

**How to display**

- 3 big numbers (cards)
    
- No charts needed
    

**Tables used**

- `AnalyticsSnapshot`
    

**Example**

`This Week ⏱️ 45 minutes ✅ 38 correct answers 📈 76% accuracy`

➡️ Parents instantly know: _“Are we doing OK?”_

---

# 2️⃣ Subject Progress (Simple Progress Bars)

**What parents see**

- Math progress bar
    
- Science progress bar
    

**How to display**

- Horizontal progress bars
    
- Green / yellow / red only
    

**Tables used**

- `SubjectProgress`  
    (or aggregated from `TopicProgress`)
    

**Example**

`Math     ████████░░ 80% Science  █████░░░░░ 52%`

➡️ No charts, no graphs — **just clarity**

---

# 3️⃣ Topics That Need Attention (MOST IMPORTANT)

**What parents see**

- 2–3 topics max
    
- Simple message
    

**How to display**

- List with icons
    
- Red / yellow indicator
    

**Tables used**

- `TopicAnalyticsSnapshot`
    
- `Recommendation`
    

**Example**

`⚠️ Needs Practice • Addition (Accuracy 48%) • Plants (Long response time)`

➡️ Parents know **where to help**, not just numbers.

---

# 4️⃣ Recommendations (Actionable, Not Technical)

**What parents see**

- Plain English suggestions
    

**How to display**

- Cards or checklist
    
- One sentence per item
    

**Tables used**

- `Recommendation`
    
- `RecommendationReason` (hidden behind “Why?”)
    

**Example**

`💡 Suggested for You • Practice Addition at difficulty 2 • Keep Science difficulty locked for now`

Click “Why?” →

`Accuracy below 60% in last 7 days`

➡️ Trust + transparency

---

# ❌ What NOT to show (very important)

Do NOT show parents:

- Raw attempts
    
- Question IDs
    
- Percent per question
    
- Complex charts
    
- Trend lines with axes
    

➡️ That’s **teacher-level**, not parent-level

---

# 🧠 Simple Color Logic (keep it universal)

|Metric|Green|Yellow|Red|
|---|---|---|---|
|Accuracy|≥ 75%|50–74%|< 50%|
|Time spent|On target|Low|Very low|
|Difficulty|Appropriate|—|Too high|

Parents understand colors **instantly**.

---

# 🧩 How this maps cleanly to your tables

|UI Section|Tables|
|---|---|
|Weekly summary|AnalyticsSnapshot|
|Subject bars|SubjectProgress|
|Weak topics|TopicAnalyticsSnapshot|
|Suggestions|Recommendation|
|Explanation|RecommendationReason|

➡️ No heavy joins  
➡️ Fast even on H2 in-memory

---

# 🚀 Minimal Analytics MVP (recommended)

If you want **just enough**:

✅ AnalyticsSnapshot  
✅ TopicProgress  
✅ Recommendation

That’s it.  
Everything else can come later.