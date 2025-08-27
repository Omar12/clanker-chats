Awesome — here are plug-and-play Dataview snippets for Obsidian. I’ll give you two setups:
- Option A (Recommended): one note per 1:1 with frontmatter → easiest to query.

---

# Option A — One note per 1:1 (frontmatter-driven)

## Folder & file pattern

```
/1on1s/
  /TeamMemberName/
    2025-08-26 1on1.md
    2025-09-09 1on1.md
```

## Templater/Note template

```
---
type: 1on1
person: TeamMemberName
date: {{date:YYYY-MM-DD}}
mood: 3
topics: []
summary: >
  Discussed migration project progress...
---

# 📝 1:1 – {{date:YYYY-MM-DD}} – [[TeamMemberName]]

**Key Topics:**  
-  

**Highlights / Wins:**  
-  

**Challenges / Blockers:**  
-  

**Growth & Development:**  
-  

**Feedback (2-way):**  
- From them:  
- From you:  

**Next Steps / Actions:**  
- [ ]  
```

## Person dashboard queries (put these in dashboard-summary.md)

### Table of all 1:1s

```
TABLE date, mood, topics, file.link AS Note
FROM "1on1s/TeamMemberName"
WHERE type = "1on1" AND person = "TeamMemberName"
SORT date DESC
```

### Average mood + latest

```
TABLE round(avg(mood), 2) AS "Avg Mood", min(date) AS "First", max(date) AS "Latest"
FROM "1on1s/TeamMemberName"
WHERE type = "1on1" AND person = "TeamMemberName"
```

### Open action items

```
TASK FROM "1on1s/TeamMemberName"
WHERE !completed
```

## Team roll-up (place anywhere)

```
TABLE person, round(avg(mood),2) AS "Avg Mood", length(rows) AS "Count", max(date) AS "Last 1:1"
FROM "1on1s"
WHERE type = "1on1"
GROUP BY person
SORT "Last 1:1" DESC
```

---

## Query Summaries

```
TABLE date, summary
FROM "1on1s/TeamMemberName"
WHERE type = "1on1" AND person = "TeamMemberName"
SORT date ASC
```

## Use ChatGPT to create a Yearly Narrative Summary

At year-end:
1.	 Copy the “Summaries” table from Obsidian (for one person or your whole team).
2.	 Paste it into ChatGPT with a prompt like:

```
“Here are summaries from my 1:1s with [Name] in 2025. Please create a year-end narrative highlighting key wins, recurring challenges, growth areas, morale trends, and any risks/opportunities I should be aware of as their manager.”
```

---

Quick tips
- Install the Dataview plugin (Community Plugins) and enable JavaScript queries if you use the dataviewjs blocks.
- Consistency beats perfection: keep mood: numeric, date: ISO (YYYY-MM-DD), and stick to the same headings so queries stay clean.
- If you expect heavy querying/reporting, prefer Option A (one 1:1 per note with frontmatter).

Want me to tailor the template and queries to your exact folder names and tags?