---
name: token-saver
description: >-
  עוזר לצרוך פחות טוקנים ומכסה ב-Claude Code וב-claude.ai. שני מצבים: ביקורת
  (בודק גודל CLAUDE.md, מספר שרתי MCP והרגלי עבודה, ומחזיר תוכנית חיסכון מדורגת
  לפי אימפקט) וליווי (כללי עבודה חסכוניים לסשן הנוכחי). הפעל כשמבקשים לחסוך
  טוקנים, לבדוק צריכה, או כשנגמרה המכסה. Helps reduce token and quota usage on
  Claude Code and claude.ai. Two modes: audit (checks CLAUDE.md size, MCP
  server count, work habits, returns a ranked savings plan) and coach (lean
  working rules for the current session). Trigger on "חסוך טוקנים", "אכלתי את
  המכסה", "בדוק לי את הצריכה", "token audit", "save tokens", "hit my limit",
  "reduce token usage".
---

# חוסך הטוקנים (token-saver)

בכל תור נשלחת כל ההיסטוריה מחדש. הקונטקסט הוא לא זיכרון חינם, הוא החשבון. הסקיל הזה מקצץ אותו.

## איזה מצב
- המשתמש רוצה לדעת מה מבזבז ולתקן: **מצב ביקורת**.
- המשתמש רק רוצה לעבוד חסכוני מעכשיו: **מצב ליווי**.
- בספק: הצע ביקורת קצרה קודם.

## מצב ביקורת (audit)
בצע לפי הסדר. הפקודות המדויקות, הספים וקטלוג ההמלצות ב-references/audit-checklist.md.

1. **סביבה.** יש גישה ל-bash וקבצים (Claude Code)? המשך לצעד 2. אין (claude.ai)? דלג לצעד 4, שאלות בלבד.
2. **CLAUDE.md.** מדוד: `wc -l ~/.claude/CLAUDE.md CLAUDE.md 2>/dev/null`. מעל 200 שורות = מנופח, נטען בכל סשן ואף פעם לא מפונה.
3. **שרתי MCP.** ספור ערכים תחת "mcpServers" ב-`~/.claude.json` וב-`.mcp.json` (או `claude mcp list`). כל שרת דוחף סכמות לחלון גם בלי שימוש.
4. **שלוש שאלות הרגלים:**
   - כמה ארוכות השיחות? מפרידים נושאים ב-/clear (claude.ai: צ'אט חדש) או צ'אט אחד ארוך?
   - מה מודל ברירת המחדל? Fable/Opus יקרים; Sonnet לשוטף.
   - איזה effort? ברירת מחדל high; medium מספיק לרוב העבודה.
   - ב-claude.ai הוסף: משתמשים ב-Projects לידע חוזר? web search/connectors דלוקים בלי שימוש?
5. **טבלה מדורגת.** החזר: ממצא | המלצה | פקודה | אימפקט, ממוין מהאימפקט הגבוה לנמוך.

לרקע של כל המלצה: references/principles.md. לכלי ניטור: references/monitoring.md.

## מצב ליווי (coach)
אמץ את הכללים האלה לסשן הנוכחי. הרקע המלא (מה, למה, איך) ב-references/principles.md.

- Sonnet כברירת מחדל; Fable/Opus רק ל-20% הקשים (ארכיטקטורה, באג קשה, כתיבה קריטית).
- effort low/medium לשוטף, high רק כשזה קריטי.
- /clear בין נושאים לא קשורים (claude.ai: צ'אט חדש).
- הצע /compact ממוקד בהפסקה טבעית, לא באמצע משימה.
- הצבע על קובץ ושורות; אל תבקש להדביק קבצים, לוגים או מסכים שלמים.
- העבר עבודה מרובת פלט (טסטים, קריאת לוגים) לתת-סוכן, שהפלט יישאר מחוץ לשיחה הראשית.
- משימה גדולה: הצע מבנה מנהל-עובדים. המודל החזק (פייבל 5) מנצח בלבד, תתי-סוכני Opus מבצעים, ובעיה חוזרת למנהל להכרעה. הפרומפט המוכן ב-references/principles.md עיקרון 11.
- אל תחליף מודל או effort באמצע סשן; זה מבטל את המטמון.
- בקשה ספציפית (שם קובץ, פלט צפוי) חוסכת סבב תיקונים.

## קבצים
- `references/principles.md`: 12 העקרונות (מה, למה, איך) ושלושה מיתוסים.
- `references/audit-checklist.md`: צעדי הביקורת המדויקים וקטלוג המלצות.
- `references/monitoring.md`: כלי ניטור והתקנתם.
