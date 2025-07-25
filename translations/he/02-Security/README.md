<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "382fddb4ee4d9c1bdc806e2ee99b70c8",
  "translation_date": "2025-07-17T07:30:01+00:00",
  "source_file": "02-Security/README.md",
  "language_code": "he"
}
-->
# שיטות עבודה מומלצות לאבטחה

אימוץ פרוטוקול Model Context (MCP) מביא עמו יכולות חדשות וחזקות ליישומים מונעי בינה מלאכותית, אך גם מציב אתגרים אבטחתיים ייחודיים שמעבר לסיכוני תוכנה מסורתיים. בנוסף לדאגות המוכרות כמו קידוד מאובטח, עיקרון ההרשאה המינימלית ואבטחת שרשרת האספקה, MCP ועומסי עבודה של AI מתמודדים עם איומים חדשים כגון הזרקת פרומפט, הרעלת כלים, שינוי דינמי של כלים, חטיפת סשנים, התקפות confused deputy ופגיעויות בהעברת טוקנים. סיכונים אלה עלולים להוביל לדליפת מידע, הפרות פרטיות והתנהגות מערכת בלתי צפויה אם לא ינוהלו כראוי.

השיעור הזה בוחן את הסיכונים האבטחתיים הרלוונטיים ביותר הקשורים ל-MCP — כולל אימות, הרשאה, הרשאות מופרזות, הזרקת פרומפט עקיפה, אבטחת סשנים, בעיות confused deputy, פגיעויות בהעברת טוקנים ופגיעויות בשרשרת האספקה — ומספק אמצעי בקרה ונהלים מומלצים שניתן ליישם כדי להפחית אותם. תלמד גם כיצד לנצל פתרונות של Microsoft כמו Prompt Shields, Azure Content Safety ו-GitHub Advanced Security כדי לחזק את יישום ה-MCP שלך. בהבנה ויישום של אמצעי הבקרה הללו, תוכל להפחית משמעותית את הסיכוי לפרצת אבטחה ולהבטיח שמערכות ה-AI שלך יישארו יציבות ואמינות.

# מטרות הלמידה

בסיום השיעור תוכל:

- לזהות ולהסביר את סיכוני האבטחה הייחודיים שמביא פרוטוקול Model Context (MCP), כולל הזרקת פרומפט, הרעלת כלים, הרשאות מופרזות, חטיפת סשנים, בעיות confused deputy, פגיעויות בהעברת טוקנים ופגיעויות בשרשרת האספקה.
- לתאר וליישם אמצעי בקרה יעילים להפחתת סיכוני אבטחה ב-MCP, כגון אימות חזק, עיקרון ההרשאה המינימלית, ניהול טוקנים מאובטח, בקרות אבטחת סשנים ואימות שרשרת האספקה.
- להבין ולנצל פתרונות של Microsoft כמו Prompt Shields, Azure Content Safety ו-GitHub Advanced Security להגנה על עומסי עבודה של MCP ו-AI.
- לזהות את החשיבות של אימות מטא-נתוני כלים, ניטור שינויים דינמיים, הגנה מפני התקפות הזרקת פרומפט עקיפה ומניעת חטיפת סשנים.
- לשלב שיטות עבודה מומלצות לאבטחה — כגון קידוד מאובטח, חיזוק שרתים וארכיטקטורת Zero Trust — ביישום ה-MCP שלך כדי להפחית את הסיכוי וההשפעה של פרצות אבטחה.

# אמצעי בקרה לאבטחת MCP

כל מערכת שיש לה גישה למשאבים חשובים מתמודדת עם אתגרים אבטחתיים מובנים. אתגרים אלה ניתנים בדרך כלל לטיפול באמצעות יישום נכון של אמצעי בקרה ועקרונות אבטחה בסיסיים. מאחר ש-MCP הוא פרוטוקול חדש יחסית, המפרט משתנה במהירות וככל שהפרוטוקול מתפתח, אמצעי הבקרה שבו יתבגרו ויאפשרו אינטגרציה טובה יותר עם ארכיטקטורות אבטחה ארגוניות ומקובלות.

מחקר שפורסם ב-[Microsoft Digital Defense Report](https://aka.ms/mddr) מציין כי 98% מהפרצות המדווחות היו נמנעות באמצעות היגיינת אבטחה חזקה, וההגנה הטובה ביותר מפני כל סוג של פרצה היא שמירה על היגיינת אבטחה בסיסית נכונה, שיטות קידוד מאובטחות ואבטחת שרשרת אספקה — אותן שיטות מוכחות שעדיין משפיעות משמעותית בהפחתת סיכוני אבטחה.

בואו נבחן כמה דרכים שבהן ניתן להתחיל לטפל בסיכוני אבטחה בעת אימוץ MCP.

> **[!NOTE]** המידע הבא נכון ליום **29 במאי 2025**. פרוטוקול MCP ממשיך להתפתח, ויישומים עתידיים עשויים להציג דפוסי אימות ואמצעי בקרה חדשים. לעדכונים והנחיות עדכניות, יש לעיין תמיד ב-[MCP Specification](https://spec.modelcontextprotocol.io/) ובמאגר הרשמי ב-[MCP GitHub repository](https://github.com/modelcontextprotocol) ובדף [security best practice page](https://modelcontextprotocol.io/specification/draft/basic/security_best_practices).

### הצגת הבעיה  
מפרט ה-MCP המקורי הניח שמפתחים יכתבו שרת אימות משלהם. זה דרש ידע ב-OAuth ובמגבלות אבטחה קשורות. שרתי MCP פעלו כשרתי OAuth 2.0 Authorization, וניהלו את אימות המשתמשים ישירות במקום להאציל זאת לשירות חיצוני כמו Microsoft Entra ID. החל מ-**26 באפריל 2025**, עדכון למפרט ה-MCP מאפשר לשרתי MCP להאציל את אימות המשתמשים לשירות חיצוני.

### סיכונים
- לוגיקת הרשאה שגויה בשרת MCP עלולה להוביל לחשיפת מידע רגיש ולבקרות גישה מוטעות.
- גניבת טוקן OAuth בשרת MCP המקומי. אם הטוקן נגנב, ניתן להשתמש בו כדי להעמיד פנים כשרת MCP ולגשת למשאבים ולמידע של השירות שאליו שייך הטוקן.

#### העברת טוקנים (Token Passthrough)  
העברת טוקנים אסורה במפורש במפרט ההרשאה מכיוון שהיא יוצרת מספר סיכוני אבטחה, ביניהם:

#### עקיפת אמצעי בקרה אבטחתיים  
שרת MCP או ממשקי API במורד הזרם עשויים ליישם אמצעי בקרה חשובים כמו הגבלת קצב, אימות בקשות או ניטור תעבורה, התלויים בקהל היעד של הטוקן או במגבלות קרדנציאליות אחרות. אם לקוחות יכולים לקבל ולהשתמש בטוקנים ישירות מול ממשקי API במורד הזרם מבלי ששרת MCP יאמת אותם כראוי או יוודא שהטוקנים הונפקו לשירות הנכון, הם עוקפים את אמצעי הבקרה הללו.

#### בעיות אחריות ומעקב  
שרת MCP לא יוכל לזהות או להבדיל בין לקוחות MCP כאשר הלקוחות קוראים עם טוקן גישה שהונפק במעלה הזרם, שעשוי להיות אטום לשרת MCP.  
יומני שרת המשאבים במורד הזרם עשויים להציג בקשות שנראות כאילו הגיעו ממקור שונה עם זהות שונה, במקום משרת MCP שמעביר בפועל את הטוקנים.  
שני גורמים אלה מקשים על חקירת תקריות, בקרה וביקורת.  
אם שרת MCP מעביר טוקנים מבלי לאמת את הטענות שלהם (כגון תפקידים, הרשאות או קהל יעד) או מטא-נתונים אחרים, שחקן זדוני המחזיק בטוקן גנוב יכול להשתמש בשרת כפרוקסי לדליפת מידע.

#### בעיות גבול אמון  
שרת המשאבים במורד הזרם מעניק אמון ליישויות ספציפיות. אמון זה עשוי לכלול הנחות לגבי מקור או דפוסי התנהגות של הלקוח. שבירת גבול האמון הזה עלולה לגרום לבעיות בלתי צפויות.  
אם הטוקן מתקבל על ידי מספר שירותים ללא אימות נכון, תוקף שיפרוץ שירות אחד יכול להשתמש בטוקן כדי לגשת לשירותים מחוברים אחרים.

#### סיכון תאימות עתידי  
גם אם שרת MCP מתחיל היום כ"פרוקסי טהור", ייתכן שיצטרך להוסיף אמצעי בקרה אבטחתיים בעתיד. התחלה עם הפרדה נכונה של קהל היעד של הטוקן מקלה על התפתחות מודל האבטחה.

### אמצעי בקרה להפחתה

**שרתי MCP אסור שיקבלו טוקנים שלא הונפקו במפורש עבור שרת ה-MCP**

- **סקירה וחיזוק לוגיקת ההרשאה:** בצע ביקורת קפדנית על יישום ההרשאה בשרת MCP שלך כדי לוודא שרק משתמשים ולקוחות מיועדים יכולים לגשת למשאבים רגישים. להנחיות מעשיות, ראה [Azure API Management Your Auth Gateway For MCP Servers | Microsoft Community Hub](https://techcommunity.microsoft.com/blog/integrationsonazureblog/azure-api-management-your-auth-gateway-for-mcp-servers/4402690) ו-[Using Microsoft Entra ID To Authenticate With MCP Servers Via Sessions - Den Delimarsky](https://den.dev/blog/mcp-server-auth-entra-id-session/).
- **אכיפת שיטות מאובטחות לניהול טוקנים:** פעל לפי [שיטות העבודה המומלצות של Microsoft לאימות טוקנים ולמשך חייהם](https://learn.microsoft.com/en-us/entra/identity-platform/access-tokens) כדי למנוע שימוש לרעה בטוקני גישה ולהפחית את הסיכון לשחזור או גניבת טוקנים.
- **הגנה על אחסון טוקנים:** אחסן טוקנים תמיד בצורה מאובטחת והשתמש בהצפנה כדי להגן עליהם במנוחה ובמעבר. לטיפים ליישום, ראה [Use secure token storage and encrypt tokens](https://youtu.be/uRdX37EcCwg?si=6fSChs1G4glwXRy2).

# הרשאות מופרזות לשרתי MCP

### הצגת הבעיה  
ייתכן ששרתי MCP קיבלו הרשאות מופרזות לשירות או למשאב שאליו הם ניגשים. לדוגמה, שרת MCP שהוא חלק מיישום מכירות מבוסס AI שמתחבר לאחסון נתונים ארגוני צריך לקבל גישה מוגבלת לנתוני המכירות בלבד, ולא להיות מורשה לגשת לכל הקבצים באחסון. בהתייחס לעיקרון ההרשאה המינימלית (אחד מעקרונות האבטחה הוותיקים ביותר), אין משאב שצריך לקבל הרשאות מעבר למה שנדרש לביצוע המשימות המיועדות לו. בינה מלאכותית מציבה אתגר מוגבר בתחום זה, כי כדי לאפשר לה גמישות, קשה להגדיר במדויק את ההרשאות הנדרשות.

### סיכונים  
- הענקת הרשאות מופרזות עלולה לאפשר דליפת מידע או שינוי נתונים שהשרת לא אמור היה לגשת אליהם. זה עלול להיות גם בעיית פרטיות אם הנתונים כוללים מידע אישי מזהה (PII).

### אמצעי בקרה להפחתה  
- **יישום עיקרון ההרשאה המינימלית:** הענק לשרת MCP רק את ההרשאות המינימליות הנדרשות לביצוע המשימות שלו. בדוק ועדכן הרשאות אלה באופן קבוע כדי לוודא שהן לא חורגות מהנדרש. להנחיות מפורטות, ראה [Secure least-privileged access](https://learn.microsoft.com/entra/identity-platform/secure-least-privileged-access).
- **שימוש בבקרת גישה מבוססת תפקידים (RBAC):** הקצה לשרת MCP תפקידים שמוגדרים בקפידה למשאבים ולפעולות ספציפיות, תוך הימנעות מהענקת הרשאות רחבות או מיותרות.
- **ניטור וביקורת הרשאות:** נטר באופן רציף את השימוש בהרשאות ובצע ביקורת על יומני הגישה כדי לזהות ולתקן במהירות הרשאות מופרזות או לא בשימוש.

# התקפות הזרקת פרומפט עקיפה

### הצגת הבעיה

שרתי MCP זדוניים או שנפרצו עלולים להוות סיכון משמעותי על ידי חשיפת נתוני לקוחות או הפעלת פעולות בלתי רצויות. סיכונים אלה רלוונטיים במיוחד בעומסי עבודה מבוססי AI ו-MCP, שבהם:

- **התקפות הזרקת פרומפט:** תוקפים משבצים הוראות זדוניות בפרומפטים או בתוכן חיצוני, שגורמות למערכת ה-AI לבצע פעולות בלתי רצויות או לדלוף מידע רגיש. למידע נוסף: [Prompt Injection](https://simonwillison.net/2025/Apr/9/mcp-prompt-injection/)
- **הרעלת כלים:** תוקפים משנים מטא-נתונים של כלים (כגון תיאורים או פרמטרים) כדי להשפיע על התנהגות ה-AI, לעקוף אמצעי בקרה או לדלוף מידע. פרטים: [Tool Poisoning](https://invariantlabs.ai/blog/mcp-security-notification-tool-poisoning-attacks)
- **הזרקת פרומפט חוצת תחומים:** הוראות זדוניות משובצות במסמכים, דפי אינטרנט או מיילים, שמעובדים על ידי ה-AI, מה שמוביל לדליפת מידע או מניפולציה.
- **שינוי דינמי של כלים (Rug Pulls):** הגדרות כלים יכולות להשתנות לאחר אישור המשתמש, מה שמכניס התנהגויות זדוניות חדשות ללא ידיעת המשתמש.

פגיעויות אלה מדגישות את הצורך באימות חזק, ניטור ואמצעי בקרה אבטחתיים בעת שילוב שרתי MCP וכלים בסביבת העבודה שלך. לעיון מעמיק יותר, ראה את הקישורים לעיל.

![prompt-injection-lg-2048x1034](../../../translated_images/prompt-injection.ed9fbfde297ca877c15bc6daa808681cd3c3dc7bf27bbbda342ef1ba5fc4f52d.he.png)

**הזרקת פרומפט עקיפה** (המכונה גם הזרקת פרומפט חוצת תחומים או XPIA) היא פגיעות קריטית במערכות AI גנרטיביות, כולל אלה המשתמשות בפרוטוקול Model Context (MCP). בהתקפה זו, הוראות זדוניות מוסתרות בתוך תוכן חיצוני — כגון מסמכים, דפי אינטרנט או מיילים. כאשר מערכת ה-AI מעבדת תוכן זה, היא עשויה לפרש את ההוראות המוטמעות כהוראות משתמש לגיטימיות, מה שמוביל לפעולות בלתי רצויות כמו דליפת מידע, יצירת תוכן מזיק או מניפולציה של אינטראקציות עם המשתמש. להסבר מפורט ודוגמאות מהעולם האמיתי, ראה [Prompt Injection](https://simonwillison.net/2025/Apr/9/mcp-prompt-injection/).

צורה מסוכנת במיוחד של התקפה זו היא **הרעלת כלים**. כאן, תוקפים מזריקים הוראות זדוניות למטא-נתונים של כלי MCP (כגון תיאורי כלים או פרמטרים). מאחר שמודלים לשוניים גדולים (LLMs) מסתמכים על מטא-נתונים אלה כדי להחליט אילו כלים להפעיל, תיאורים שנפרצו יכולים להטעות את המודל לבצע קריאות כלים לא מורשות או לעקוף אמצעי בקרה. מניפולציות אלה לרוב בלתי נראות למשתמשי הקצה אך יכולות להתפרש ולהיות מופעלות על ידי מערכת ה-AI. סיכון זה מוגבר בסביבות שרתי MCP מנוהלות, שבהן הגדרות הכלים יכולות להתעדכן לאחר אישור המשתמש — תרחיש המכונה לעיתים "[rug pull](https://www.wiz.io/blog/mcp-security-research-briefing#remote-servers-22)". במקרים כאלה, כלי שהיה קודם בטוח עלול להיות שונה מאוחר יותר לביצוע פעולות זדוניות, כגון דליפת מידע או שינוי התנהגות המערכת, ללא ידיעת המשתמש. למידע נוסף על וקטור התקפה זה, ראה [Tool Poisoning](https://invariantlabs.ai/blog/mcp-security-notification-tool-poisoning-attacks).

![tool-injection-lg-2048x1239 (1)](../../../translated_images/tool-injection.3b0b4a6b24de6befe7d3afdeae44138ef005881aebcfc84c6f61369ce31e3640.he.png)

## סיכונים  
פעולות AI בלתי מכוונות מציגות מגוון סיכוני אבטחה הכוללים דליפת מידע והפרות פרטיות.

### אמצעי בקרה להפחתה  
### שימוש ב-Prompt Shields להגנה מפני התקפות הזרקת פרומפט עקיפה  
-----------------------------------------------------------------------------

**AI Prompt Shields** הם פתרון שפותח על ידי Microsoft להגנה מפני התקפות הזרקת פרומפט ישירות ועקיפות. הם מסייעים באמצעות:

1.  **זיהוי וסינון:** Prompt Shields משתמשים באלגוריתמים מתקדמים של למידת מכונה ועיבוד שפה טבעית כדי לזהות ולסנן הוראות זדוניות המוטמעות בתוכן חיצוני, כגון מסמכים, דפי אינטרנט או מיילים.
    
2.  **הדגשה (Spotlighting):** טכניקה זו מסייעת למערכת ה-AI להבחין בין הוראות מערכת תקפות לבין קלטים חיצוניים שעלולים להיות לא אמינים. על ידי שינוי הטקסט הנכנס בצורה שהופכת אותו לרלוונטי יותר למודל, Spotlighting מבטיחה שה-AI יוכל לזהות טוב יותר ולהתעלם מהוראות זדוניות.
    
3.  **מפרידים וסימון נתונים (Delimiters and Datamarking):** הכנסת מפרידים בהודעת המערכת מגדירה במפורש את מיקום הטקסט הנכנס, ועוזרת למערכת ה-AI להבחין ולהפריד בין קלטי משתמש לתוכן חיצוני שעלול להיות מזיק. Datamarking מרחיב
בעיית ה-confused deputy היא פגיעות אבטחה שמתרחשת כאשר שרת MCP משמש כפרוקסי בין לקוחות MCP ל-APIs של צד שלישי. פגיעות זו יכולה להיות מנוצלת כאשר שרת ה-MCP משתמש ב-client ID סטטי לאימות מול שרת הרשאות צד שלישי שאינו תומך ברישום דינמי של לקוחות.

### סיכונים

- **עקיפת הסכמה מבוססת עוגיות**: אם משתמש כבר אותת דרך שרת הפרוקסי של MCP, שרת ההרשאות של צד שלישי עשוי להגדיר עוגיית הסכמה בדפדפן המשתמש. תוקף יכול לנצל זאת מאוחר יותר על ידי שליחת קישור זדוני עם בקשת הרשאה מעוצבת הכוללת URI הפניה זדוני.
- **גניבת קוד הרשאה**: כאשר המשתמש לוחץ על הקישור הזדוני, שרת ההרשאות עשוי לדלג על מסך ההסכמה בגלל העוגייה הקיימת, וקוד ההרשאה עלול להיות מנותב לשרת התוקף.
- **גישה לא מורשית ל-API**: התוקף יכול להחליף את קוד ההרשאה הגנוב בטוקנים ולתחם את עצמו כמשתמש כדי לגשת ל-API של צד שלישי ללא אישור מפורש.

### אמצעי הפחתה

- **דרישות הסכמה מפורשת**: שרתי פרוקסי MCP המשתמשים ב-client IDs סטטיים **חייבים** לקבל הסכמת משתמש עבור כל לקוח שנרשם דינמית לפני העברה לשרתי ההרשאות של צד שלישי.
- **יישום OAuth תקין**: יש לעקוב אחר שיטות האבטחה הטובות ביותר של OAuth 2.1, כולל שימוש ב-code challenges (PKCE) בבקשות הרשאה למניעת התקפות יירוט.
- **אימות לקוח**: יש ליישם אימות קפדני של URI הפניה ומזהי לקוח כדי למנוע ניצול על ידי גורמים זדוניים.


# פגיעויות Token Passthrough

### הצהרת הבעיה

"Token passthrough" הוא דפוס אנטי שבו שרת MCP מקבל טוקנים מלקוח MCP מבלי לאמת שהטוקנים הונפקו כראוי לשרת עצמו, ואז "מעביר אותם" ל-APIs במורד הזרם. פרקטיקה זו מפרה במפורש את מפרט ההרשאה של MCP ומציבה סיכוני אבטחה חמורים.

### סיכונים

- **עקיפת בקרות אבטחה**: לקוחות עלולים לעקוף בקרות אבטחה חשובות כמו הגבלת קצב, אימות בקשות או ניטור תעבורה אם הם משתמשים בטוקנים ישירות מול APIs במורד הזרם ללא אימות מתאים.
- **בעיות אחריות ומעקב**: שרת MCP לא יוכל לזהות או להבדיל בין לקוחות MCP כאשר משתמשים בטוקנים שהונפקו במעלה הזרם, מה שמקשה על חקירת תקריות וביקורת.
- **דליפת נתונים**: אם טוקנים מועברים ללא אימות תביעות מתאים, גורם זדוני עם טוקן גנוב יכול להשתמש בשרת כפרוקסי לדליפת נתונים.
- **הפרת גבולות אמון**: שרתי משאבים במורד הזרם עשויים להעניק אמון ליישויות מסוימות בהנחות לגבי מקור או דפוסי התנהגות. שבירת גבולות האמון עלולה לגרום לבעיות אבטחה בלתי צפויות.
- **שימוש לרעה בטוקנים מרובי שירותים**: אם טוקנים מתקבלים על ידי מספר שירותים ללא אימות מתאים, תוקף שיפרוץ שירות אחד יכול להשתמש בטוקן כדי לגשת לשירותים מחוברים אחרים.

### אמצעי הפחתה

- **אימות טוקנים**: שרתי MCP **אסור שיקבלו** טוקנים שלא הונפקו במפורש עבור שרת ה-MCP עצמו.
- **אימות קהל יעד**: יש תמיד לאמת שהטוקנים כוללים את תביעת הקהל הנכונה התואמת את זהות שרת ה-MCP.
- **ניהול מחזור חיים תקין של טוקנים**: יש ליישם טוקני גישה קצרים ופרקטיקות סיבוב טוקנים מתאימות כדי להפחית את הסיכון לגניבה ושימוש לרעה בטוקנים.


# חטיפת סשן

### הצהרת הבעיה

חטיפת סשן היא וקטור התקפה שבו לקוח מקבל מזהה סשן מהשרת, וצד לא מורשה משיג ומשתמש באותו מזהה סשן כדי להתחפש ללקוח המקורי ולבצע פעולות לא מורשות בשמו. הדבר מדאיג במיוחד בשרתי HTTP מדינתיים המטפלים בבקשות MCP.

### סיכונים

- **הזרקת פקודות חטיפת סשן**: תוקף שהשיג מזהה סשן יכול לשלוח אירועים זדוניים לשרת שמשתף מצב סשן עם השרת שאליו הלקוח מחובר, מה שעלול לגרום לפעולות מזיקות או לגישה לנתונים רגישים.
- **התחזות בחטיפת סשן**: תוקף עם מזהה סשן גנוב יכול לבצע קריאות ישירות לשרת MCP, לעקוף אימות ולהיחשב כמשתמש לגיטימי.
- **פגיעה בזרמי המשך**: כאשר שרת תומך בהעברה מחדש/זרמים ניתנים להמשך, תוקף יכול לקטוע בקשה מוקדם מדי, מה שיגרום להמשך מאוחר יותר על ידי הלקוח המקורי עם תוכן שעלול להיות זדוני.

### אמצעי הפחתה

- **אימות הרשאות**: שרתי MCP שמיישמים הרשאה **חייבים** לאמת את כל הבקשות הנכנסות ו**אסור** להשתמש בסשנים לאימות.
- **מזהי סשן מאובטחים**: שרתי MCP **חייבים** להשתמש במזהי סשן מאובטחים, לא דטרמיניסטיים, שנוצרים באמצעות מחוללי מספרים אקראיים מאובטחים. יש להימנע ממזהים צפויים או סדרתיים.
- **קישור סשן למשתמש ספציפי**: שרתי MCP **מומלץ** לקשר מזהי סשן למידע ייחודי למשתמש המורשה (כגון מזהה משתמש פנימי) באמצעות פורמט כמו `<user_id>:<session_id>`.
- **פג תוקף סשן**: יש ליישם פג תוקף וסיבוב סשנים תקינים כדי להגביל את חלון הפגיעות במקרה של פגיעה במזהה סשן.
- **אבטחת תעבורה**: יש להשתמש תמיד ב-HTTPS לכל התקשורת כדי למנוע יירוט מזהי סשן.


# אבטחת שרשרת אספקה

אבטחת שרשרת האספקה נשארת בסיסית בעידן ה-AI, אך היקף מה שנחשב לשרשרת האספקה שלך התרחב. בנוסף לחבילות קוד מסורתיות, עליך כעת לאמת ולנטר בקפידה את כל הרכיבים הקשורים ל-AI, כולל מודלים בסיסיים, שירותי embeddings, ספקי הקשר ו-APIs של צד שלישי. כל אחד מהם עלול להכניס פגיעויות או סיכונים אם לא מנוהל כראוי.

**שיטות מפתח לאבטחת שרשרת אספקה ל-AI ו-MCP:**
- **אמת את כל הרכיבים לפני האינטגרציה:** זה כולל לא רק ספריות קוד פתוח, אלא גם מודלים, מקורות נתונים ו-APIs חיצוניים. בדוק תמיד מקור, רישוי ופגיעויות ידועות.
- **שמור על צינורות פריסה מאובטחים:** השתמש בצינורות CI/CD אוטומטיים עם סריקות אבטחה משולבות כדי לזהות בעיות מוקדם. ודא שרק ארטיפקטים מהימנים מופצים לסביבת הייצור.
- **נטר ובצע ביקורת מתמשכת:** יישם ניטור שוטף לכל התלויות, כולל מודלים ושירותי נתונים, כדי לזהות פגיעויות חדשות או התקפות על שרשרת האספקה.
- **החל עקרון הרשאות מינימליות ובקרות גישה:** הגבל גישה למודלים, נתונים ושירותים רק למה שנדרש לשרת ה-MCP לפעול.
- **הגיב במהירות לאיומים:** הקם תהליך לתיקון או החלפת רכיבים שנפגעו, ולסיבוב סודות או אישורים במקרה של פריצה.

[GitHub Advanced Security](https://github.com/security/advanced-security) מספקת תכונות כמו סריקת סודות, סריקת תלות וניתוח CodeQL. כלים אלה משתלבים עם [Azure DevOps](https://azure.microsoft.com/en-us/products/devops) ו-[Azure Repos](https://azure.microsoft.com/en-us/products/devops/repos/) כדי לסייע לצוותים לזהות ולהפחית פגיעויות בקוד וברכיבי שרשרת האספקה של AI.

מיקרוסופט גם מיישמת שיטות אבטחת שרשרת אספקה נרחבות פנימית עבור כל המוצרים. למידע נוסף ראו ב-[The Journey to Secure the Software Supply Chain at Microsoft](https://devblogs.microsoft.com/engineering-at-microsoft/the-journey-to-secure-the-software-supply-chain-at-microsoft/).


# שיטות אבטחה מבוססות שיחזקו את עמידות האבטחה של יישום ה-MCP שלך

כל יישום MCP יורש את עמידות האבטחה הקיימת של סביבת הארגון שעליה הוא בנוי, ולכן כששוקלים את אבטחת MCP כמרכיב במערכות ה-AI הכוללות שלך מומלץ לשפר את עמידות האבטחה הכוללת הקיימת. בקרות האבטחה המובנות הבאות רלוונטיות במיוחד:

-   שיטות קידוד מאובטח ביישום ה-AI שלך - הגנה מפני [OWASP Top 10](https://owasp.org/www-project-top-ten/), [OWASP Top 10 ל-LLMs](https://genai.owasp.org/download/43299/?tmstv=1731900559), שימוש בכספות מאובטחות לסודות וטוקנים, יישום תקשורת מאובטחת מקצה לקצה בין כל רכיבי היישום וכו'.
-   חיזוק השרת -- שימוש ב-MFA כשאפשר, שמירת עדכוני תיקונים, אינטגרציה עם ספק זהות צד שלישי לגישה וכו'.
-   שמירת מכשירים, תשתיות ויישומים מעודכנים עם תיקונים
-   ניטור אבטחה -- יישום רישום וניטור של יישום AI (כולל לקוחות/שרתים של MCP) ושליחת הלוגים ל-SIEM מרכזי לזיהוי פעילויות חריגות
-   ארכיטקטורת Zero Trust -- בידוד רכיבים באמצעות בקרות רשת וזהות באופן לוגי כדי למזער תנועה רוחבית במקרה של פגיעה ביישום AI.

# נקודות מפתח

- יסודות האבטחה נשארים קריטיים: קידוד מאובטח, הרשאות מינימליות, אימות שרשרת אספקה וניטור מתמשך הם חיוניים ל-MCP ולעומסי עבודה של AI.
- MCP מציג סיכונים חדשים — כגון הזרקת פקודות, הרעלת כלים, חטיפת סשן, בעיות confused deputy, פגיעויות token passthrough והרשאות מופרזות — שדורשים בקרות מסורתיות וייעודיות ל-AI.
- השתמש באימות, הרשאה וניהול טוקנים חזקים, תוך ניצול ספקי זהות חיצוניים כמו Microsoft Entra ID כשאפשר.
- הגן מפני הזרקת פקודות עקיפה והרעלת כלים על ידי אימות מטא-נתוני כלים, ניטור שינויים דינמיים ושימוש בפתרונות כמו Microsoft Prompt Shields.
- יישם ניהול סשנים מאובטח באמצעות מזהי סשן לא דטרמיניסטיים, קישור סשנים לזהויות משתמשים, ולעולם אל תשתמש בסשנים לאימות.
- מנע התקפות confused deputy על ידי דרישת הסכמה מפורשת של המשתמש עבור כל לקוח שנרשם דינמית ויישום שיטות אבטחה תקינות של OAuth.
- הימנע מפגיעויות token passthrough על ידי הבטחת שרתי MCP יקבלו רק טוקנים שהונפקו במפורש עבורם ואימות תביעות הטוקן כראוי.
- התייחס לכל הרכיבים בשרשרת האספקה של ה-AI שלך — כולל מודלים, embeddings וספקי הקשר — באותה קפדנות כמו תלות בקוד.
- הישאר מעודכן עם מפרטי MCP המתפתחים ותרום לקהילה כדי לסייע לעצב תקנים מאובטחים.

# משאבים נוספים

## משאבים חיצוניים
- [Microsoft Digital Defense Report](https://aka.ms/mddr)
- [MCP Specification](https://spec.modelcontextprotocol.io/)
- [MCP Security Best Practices](https://modelcontextprotocol.io/specification/draft/basic/security_best_practices)
- [MCP Authorization Specification](https://modelcontextprotocol.io/specification/draft/basic/authorization)
- [OAuth 2.0 Security Best Practices (RFC 9700)](https://datatracker.ietf.org/doc/html/rfc9700)
- [Prompt Injection in MCP (Simon Willison)](https://simonwillison.net/2025/Apr/9/mcp-prompt-injection/)
- [Tool Poisoning Attacks (Invariant Labs)](https://invariantlabs.ai/blog/mcp-security-notification-tool-poisoning-attacks)
- [Rug Pulls in MCP (Wiz Security)](https://www.wiz.io/blog/mcp-security-research-briefing#remote-servers-22)
- [Prompt Shields Documentation (Microsoft)](https://learn.microsoft.com/azure/ai-services/content-safety/concepts/jailbreak-detection)
- [OWASP Top 10](https://owasp.org/www-project-top-ten/)
- [OWASP Top 10 for LLMs](https://genai.owasp.org/download/43299/?tmstv=1731900559)
- [GitHub Advanced Security](https://github.com/security/advanced-security)
- [Azure DevOps](https://azure.microsoft.com/products/devops)
- [Azure Repos](https://azure.microsoft.com/products/devops/repos/)
- [The Journey to Secure the Software Supply Chain at Microsoft](https://devblogs.microsoft.com/engineering-at-microsoft/the-journey-to-secure-the-software-supply-chain-at-microsoft/)
- [Secure Least-Privileged Access (Microsoft)](https://learn.microsoft.com/entra/identity-platform/secure-least-privileged-access)
- [Best Practices for Token Validation and Lifetime](https://learn.microsoft.com/entra/identity-platform/access-tokens)
- [Use Secure Token Storage and Encrypt Tokens (YouTube)](https://youtu.be/uRdX37EcCwg?si=6fSChs1G4glwXRy2)
- [Azure API Management as Auth Gateway for MCP](https://techcommunity.microsoft.com/blog/integrationsonazureblog/azure-api-management-your-auth-gateway-for-mcp-servers/4402690)
- [Using Microsoft Entra ID to Authenticate with MCP Servers](https://den.dev/blog/mcp-server-auth-entra-id-session/)

## מסמכי אבטחה נוספים

להנחיות אבטחה מפורטות יותר, עיין במסמכים הבאים:

- [MCP Security Best Practices 2025](./mcp-security-best-practices-2025.md) - רשימה מקיפה של שיטות אבטחה מומלצות ליישומי MCP
- [Azure Content Safety Implementation](./azure-content-safety-implementation.md) - דוגמאות ליישום אינטגרציה של Azure Content Safety עם שרתי MCP
- [MCP Security Controls 2025](./mcp-security-controls-2025.md) - בקרות וטכניקות אבטחה עדכניות לפריסות MCP
- [MCP Best Practices](./mcp-best-practices.md) - מדריך מהיר לשיטות אבטחה ב-MCP

### הבא

הבא: [פרק 3: התחלה](../03-GettingStarted/README.md)

**כתב ויתור**:  
מסמך זה תורגם באמצעות שירות תרגום מבוסס בינה מלאכותית [Co-op Translator](https://github.com/Azure/co-op-translator). למרות שאנו שואפים לדיוק, יש לקחת בחשבון כי תרגומים אוטומטיים עלולים להכיל שגיאות או אי-דיוקים. המסמך המקורי בשפת המקור שלו נחשב למקור הסמכותי. למידע קריטי מומלץ להשתמש בתרגום מקצועי על ידי מתרגם אנושי. אנו לא נושאים באחריות לכל אי-הבנה או פרשנות שגויה הנובעת משימוש בתרגום זה.