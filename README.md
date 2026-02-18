<img width="681" height="293" alt="image" src="https://github.com/user-attachments/assets/94ef8c7c-45fc-46c9-a3be-9cfc6688fff7" />






בעולם אבטחת המידע, Shells הם כלי מרכזי בשרשרת התקיפה. הם מאפשרים לתוקף להריץ פקודות על מערכת יעד מרחוק. הבנת המנגנונים הללו חיונית לא רק עבור בודקי חדירות (Penetration Testers), אלא גם עבור אנשי הגנה (Blue Team) כדי לזהות ולבלום פעילות עוינת ברשת הארגונית.

🎯 יעדי הלמידה
בסיום מדריך זה, תדעו:

להבין את תפקיד ה-Shell באבטחה התקפית.

להגדיר ולהשתמש ב-Reverse Shell וב-Bind Shell.

להטמיע ולהשתמש ב-Web Shells.

🛠 דרישות קדם
כדי להפיק את המרב מהמדריך, מומלץ להחזיק בידע בסיסי בנושאים הבאים:

הבנה בסיסית ברשתות (Networking).

היכרות עם אבטחת אפליקציות אינטרנט.

מיומנות בעבודה עם שורת הפקודה (CLI).

היכרות בסיסית עם שפות סקריפט (Bash, Python, או PHP).

⚠️ דגשים חשובים (Caveats)
ללא Frameworks: במדריך זה לא נשתמש ב-Metasploit או בכלים אוטומטיים אחרים. המטרה היא להבין איך Shells עובדים "מתחת למכונה" ללא סיוע של כלים גנרטיביים.

מערכת הפעלה: כל הדוגמאות במדריך מבוססות על מערכות Linux.

🚀 תחילת העבודה
הפעלת המעבדה
כדי להתחיל בתרגול, יש להפעיל את המכונה הווירטואלית (VM):

לחצו על כפתור Start Machine. (טעינת המערכת אורכת כ-2 דקות).

המכונה תופיע בצד ימין של המסך (Split View).

ניתן להשתמש ב-AttackBox של המערכת או להתחבר דרך ה-VPN האישי שלכם כדי לדמות את עמדת התוקף

סקירה כללית: מהו Shell?
Shell (מעטפת) היא תוכנה המאפשרת למשתמש לתקשר עם מערכת ההפעלה (OS). בעוד שקיימים ממשקים גרפיים (GUI), בעולם הסייבר הכוונה היא בדרך כלל לממשק שורת פקודה (CLI).

<img width="966" height="361" alt="image" src="https://github.com/user-attachments/assets/f8db4406-a095-4a59-99b1-85d9c706a00b" />


בתחום ה-Offensive Security, המושג מתייחס לסשן (Session) שבו תוקף משיג גישה למערכת שנפרצה, מה שמאפשר לו להריץ פקודות ותוכנות מרחוק על שרת היעד.

🚩 פעילויות תוקף לאחר השגת Shell
ברגע שתוקף משיג גישת Shell, הוא יכול לבצע מגוון פעולות קריטיות:

שליטה מרחוק (Remote Control): הרצת פקודות ישירות על שרת היעד כאילו הוא יושב מולו.

העלאת הרשאות (Privilege Escalation): אם הגישה הראשונית מוגבלת (משתמש רגיל), התוקף יחפש פרצות כדי להפוך למנהל מערכת (Root/Admin).

הוצאת נתונים (Data Exfiltration): חיפוש, קריאה והעתקה של מידע רגיש (כמו מסדי נתונים או קבצי סיסמאות) אל מחוץ לארגון.

עקיבות ושימור גישה (Persistence): יצירת משתמשים חדשים או התקנת Backdoors כדי להבטיח גישה למערכת גם לאחר ריסוט או ניסיון ניקוי.

פעולות פוסט-אקספלויטציה (Post-Exploitation): פריסת נוזקות, מחיקת לוגים לטשטוש עקבות, או השבתת שירותי אבטחה.

דילוג ברשת (Pivoting): שימוש במערכת שנפרצה כ"קרש קפיצה" (Pivot) כדי לתקוף מערכות אחרות בתוך הרשת הפנימית שאליהן אין גישה ישירה מהאינטרנט.


השאלה,התשובה
מהו ממשק שורת הפקודה המאפשר למשתמשים לתקשר עם מערכת ההפעלה?,Shell
איזה תהליך כולל שימוש במערכת פרוצה כנקודת זינוק לתקיפת מכונות אחרות ברשת?,Pivoting
מהי פעילות נפוצה שתוקפים מבצעים לאחר השגת Shell כדי להשיג הרשאות ניהול?,Privilege Escalation
<img width="942" height="609" alt="image" src="https://github.com/user-attachments/assets/4666e230-ea9e-45fd-94c8-b4fee543618f" />
.

