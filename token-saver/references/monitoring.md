# ניטור צריכה

התחל מהמובנה (חינם), הוסף כלי חיצוני רק אם צריך מעקב רציף.

## מובנה ב-Claude Code (בלי התקנה)
- `/context`: רשת חיה של מה ממלא את החלון (system prompt, כלי MCP, זיכרון, היסטוריה, מקום פנוי). `/context all`: פירוט לפי פריט ורמזי אופטימיזציה.
- `/usage`: ניצול ותקרות התוכנית (כינויים `/cost`, `/stats`; `d`/`w` ל-24 שעות מול 7 ימים).
- statusline: אפשר להציג שימוש בשורת הסטטוס.
- claude.ai: Settings > Usage.

## ccusage
מנתח צריכת טוקנים ועלות מוערכת מלוגים מקומיים. בלי העלאה לענן.
```
npx ccusage@latest
```
- תת-פקודות: `daily`, `weekly`, `monthly`, `session`, `blocks` (חלונות 5 שעות), `statusline`.
- ספציפי ל-Claude: `ccusage claude daily`.

## claude-monitor
ניטור בזמן אמת: קצב שריפה, חיזוי מתי תיגמר המכסה, ואזהרות מול תקרות התוכנית.
```
uv tool install claude-monitor
```
- חלופה: `pip install claude-monitor`. כינויים: `claude-monitor`, `cmonitor`, `ccm`.
- פלט JSON: `claude-monitor --once --output json`. אפשר לחבר ל-statusline.

## תוספי statusline
מציגים מכסה, קונטקסט וטוקנים בשורת הסטטוס בזמן אמת.
- aiedwardyi/claude-usage-monitor:
```
curl -fsSL https://raw.githubusercontent.com/aiedwardyi/claude-usage-monitor/v0.2.0/install.sh | bash
```
- daniel3303/ClaudeCodeStatusLine: משכפלים ומפנים את statusline ב-settings.json לסקריפט (ר' README ברפו).

## מד על שולחן העבודה (אופציונלי)
- usage4claude (סרגל תפריט ב-macOS), token-monitor (widget חוצה-כלים): אותה מכסה, פשוט משטח תצוגה אחר.
