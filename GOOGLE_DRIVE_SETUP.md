# ☁️ מדריך הגדרת סנכרון Google Drive

האפליקציה תומכת בגיבוי ושחזור ישיר ל-Google Drive האישי שלך. זה דורש **הקמה חד-פעמית של Client ID** בגוגל קלאוד — **חינמי לחלוטין, לוקח 10-15 דקות**.

---

## 🎯 למה זה טוב לך

- ✅ הקובץ נשמר ב-**Drive האישי שלך** (לא בשרת חיצוני)
- ✅ גוגל לא רואה את התוכן (JSON אצלך)
- ✅ סנכרון בין מחשב וטלפון בלחיצה אחת
- ✅ אפשר לראות/להוריד את הקבצים ידנית בכל זמן
- ✅ אפשר למחוק הרשאה בכל רגע ב-[myaccount.google.com/permissions](https://myaccount.google.com/permissions)

---

## 📋 מה צריך לעשות — 4 שלבים

### שלב 1: צור Google Cloud Project

1. היכנס ל: **https://console.cloud.google.com**
2. התחבר עם חשבון הגוגל שלך
3. למעלה שמאל, לחץ על התפריט "Select a project"
4. לחץ "**NEW PROJECT**"
5. מלא:
   - **Project name**: `CFO Tracker` (או כל שם שתבחר)
   - **Location**: No organization
6. לחץ "**CREATE**"
7. חכה ~30 שניות עד שהפרויקט נוצר

### שלב 2: הפעל את Google Drive API

1. בצד השמאל של הקונסול: **APIs & Services** → **Library**
2. בחיפוש, הקלד: `Google Drive API`
3. לחץ על "**Google Drive API**"
4. לחץ "**ENABLE**"
5. חכה שיתאפשר (~20 שניות)

### שלב 3: הגדר OAuth Consent Screen

> זה המסך שיראו המשתמשים (רק אתה) כשמבקשים הרשאות.

1. **APIs & Services** → **OAuth consent screen**
2. **User Type**: בחר "**External**" → Create
3. מלא רק את השדות החובה:
   - **App name**: `CFO Tracker`
   - **User support email**: המייל שלך
   - **Developer contact**: המייל שלך
4. לחץ "**Save and Continue**"
5. בשלב **Scopes**: לא צריך להוסיף — לחץ "**Save and Continue**"
6. בשלב **Test users**: לחץ "**+ ADD USERS**" → הוסף את המייל שלך → Save
7. לחץ "**Save and Continue**" → **Back to Dashboard**

### שלב 4: צור את ה-OAuth Client ID

1. **APIs & Services** → **Credentials**
2. לחץ "**+ CREATE CREDENTIALS**" → "**OAuth client ID**"
3. **Application type**: "**Web application**"
4. **Name**: `CFO Tracker Web`
5. תחת **Authorized JavaScript origins**, לחץ "**+ ADD URI**" והוסף את **כל** הכתובות שבהן תשתמש באפליקציה:
   - `https://YOUR_USERNAME.github.io` (החלף ב-username שלך)
   - `http://localhost:8000` (לבדיקות מקומיות, אופציונלי)
   - `https://YOUR_USERNAME.github.io/cfo-tracker` (אופציונלי, אם האפליקציה בתת-נתיב)
   
   ⚠️ חשוב: חייב להיות **בדיוק** הדומיין שבו האפליקציה רצה — ללא `/` בסוף
6. לחץ "**CREATE**"
7. יופיע פופאפ עם **Client ID** ו-**Client Secret**
8. **העתק את ה-Client ID** (הארוך, עם `.apps.googleusercontent.com` בסוף)

דוגמה ל-Client ID:
```
123456789012-abcdefghijklmnopqrstuvwxyz1234.apps.googleusercontent.com
```

---

## 🔌 חבר לאפליקציה

1. פתח את האפליקציה (האפליקציה שלך ב-GitHub Pages)
2. עבור ל: **"עוד"** → **"☁️ סנכרון Google Drive"**
3. לחץ על **"הגדרת חיבור Google Drive"**
4. הדבק את ה-**Client ID** שהעתקת
5. לחץ OK

**עכשיו:**
- **גבה** — לחץ "גבה ל-Google Drive" — בפעם הראשונה תבקש הרשאות
- **שחזר** — לחץ "שחזר מ-Google Drive" — תראה את רשימת הגיבויים

---

## 🔄 תהליך הסנכרון המומלץ

### במחשב בסוף היום:
1. עשית שינויים במשרות / רדאר
2. "עוד" → ☁️ **גבה ל-Google Drive**
3. תראה תאריך הגיבוי האחרון

### בטלפון למחרת בבוקר:
1. פתח האפליקציה
2. "עוד" → ☁️ **שחזר מ-Google Drive**
3. בחר מהרשימה את הגיבוי האחרון
4. אשר את השחזור
5. הכל מסונכרן

> 💡 **טיפ**: בפעם הראשונה בכל מכשיר תצטרך לאשר את ההרשאות של גוגל.

---

## 🔐 אבטחה ופרטיות

### מה הרשאות האפליקציה מבקשת?

האפליקציה מבקשת `drive.file` scope — זה אומר שיש לה גישה **רק לקבצים שהיא יצרה** (לא לכל ה-Drive שלך).

### איפה הקבצים נשמרים?

בתיקייה בשם `CFO Tracker Backups` ב-Google Drive שלך. תוכל לראות/להוריד/למחוק אותם ידנית מ: **https://drive.google.com**

### איך אני מוחק הרשאות?

1. **https://myaccount.google.com/permissions**
2. מצא "CFO Tracker"
3. לחץ "**Remove Access**"

עד הסרת ההרשאה, האפליקציה לא תוכל לגשת ל-Drive שלך.

### מה עם בטיחות ה-Client ID?

Client ID **אינו סוד** — זה מזהה ציבורי. מה שכן סוד זה ה-**Client Secret** (שלא משתמשים בו כלל באפליקציה client-side). 

⚠️ עם זאת, שים לב לכך: אם מישהו יעתיק את ה-Client ID שלך ויצור אפליקציה זהה עם אותו `Authorized JavaScript origin` — הוא יוכל לבקש הרשאות בשם האפליקציה שלך. הסיכוי נמוך, אבל כדאי להיות מודעים.

---

## 🆘 פתרון בעיות

### "Error 400: redirect_uri_mismatch"
חסרה הכתובת ב-**Authorized JavaScript origins**. חזור ל-Credentials והוסף את ה-URL המדויק.

### "Access blocked: This app's request is invalid"
ה-OAuth Consent Screen לא הוגדר נכון. חזור אליו ובדוק שהוא לא ב-Draft.

### "The given origin is not allowed"
ההסכמה למתן הרשאות לא מכירה את הדומיין. וודא שהוא נוסף ב-Authorized JavaScript origins.

### "App is blocked"
אם האפליקציה עדיין ב-"Testing" mode, רק `Test users` יכולים להתחבר. הוסף את המייל שלך ב-OAuth Consent Screen → Test users.

### "Quota exceeded"
הגבלה יומית של Google Drive API. חכה 24 שעות, או בקש הגדלת מכסה (לרוב לא צריך — המכסה היא 1 מיליארד שאילתות ליום).

---

## 📊 עלויות

**אפס.** Google Drive API חינמי עד הגבולות הבאים:

- 1,000,000,000 שאילתות ליום (אתה לא תגיע לזה)
- 15 GB שטח ב-Drive הרגיל (מעל זה צריך לשלם — אבל הגיבויים שלנו הם ~100KB כל אחד, אז אלפי גיבויים = 100MB בלבד)

---

## 🎯 סיכום

אחרי ההגדרה החד-פעמית (10-15 דקות), הסנכרון הוא **לחיצה אחת**:

| פעולה | מיקום | משך |
|-------|-------|-----|
| גיבוי | "עוד" → ☁️ גבה ל-Drive | 2 שניות |
| שחזור | "עוד" → ☁️ שחזר מ-Drive → בחר | 5 שניות |

מוכן להתחיל? **פתח את https://console.cloud.google.com ובוא נצא לדרך!**
