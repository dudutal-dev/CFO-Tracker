# 📘 הוראות דפלוי ל-GitHub Pages

## 🚀 העלאה לראשונה (5 דקות)

### שלב 1: יצירת ריפו חדש ב-GitHub

1. כנס ל-[github.com](https://github.com) ולחץ ➕ → "New repository"
2. מלא:
   - **Repository name:** `cfo-tracker` (או כל שם שתבחר)
   - **Visibility:** Public (חובה ל-GitHub Pages חינם) או Private (דורש GitHub Pro)
   - ⚠️ **אל תסמן** "Initialize with README" — הקבצים כבר אצלך
3. לחץ "Create repository"

### שלב 2: העלאת הקבצים

**אפשרות א' — דרך ממשק הווב של GitHub (קל):**
1. בריפו החדש, לחץ "uploading an existing file"
2. גרור את **כל הקבצים מתוך התיקייה `cfo-tracker-github/`**:
   - `index.html`
   - `README.md`
   - `.gitignore`
   - `.nojekyll`
   - `DEPLOY.md` (אופציונלי)
3. Commit message: "Initial commit"
4. לחץ "Commit changes"

**אפשרות ב' — דרך Git CLI (לגיקים):**
```bash
cd /path/to/cfo-tracker-github
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/cfo-tracker.git
git push -u origin main
```

### שלב 3: הפעלת GitHub Pages

1. בריפו → **Settings** (למעלה מימין)
2. בתפריט הצדדי → **Pages**
3. תחת "Build and deployment":
   - **Source:** Deploy from a branch
   - **Branch:** `main`
   - **Folder:** `/ (root)`
4. לחץ **Save**
5. חכה 1-2 דקות

### שלב 4: גישה לאפליקציה

בעוד 1-2 דקות, האפליקציה תהיה זמינה ב:

```
https://YOUR_USERNAME.github.io/cfo-tracker/
```

לדוגמה: `https://dudutal-dev.github.io/cfo-tracker/`

---

## 🔄 עדכון גרסאות

**כשאני שולח לך עדכון לקובץ `index.html`:**

### דרך ממשק הווב (קל):
1. היכנס לריפו ב-GitHub
2. לחץ על `index.html`
3. לחץ על ✏️ "Edit"
4. מחק את הכל (Ctrl+A → Delete)
5. הדבק את הקובץ החדש
6. Commit changes
7. תוך 1-2 דקות — האפליקציה מעודכנת

### דרך Git CLI:
```bash
# החלף את index.html במקומי
git add index.html
git commit -m "Update app"
git push
```

---

## 🔐 שמירה על פרטיות

**⚠️ האפליקציה שלך עושה את הפעולות הבאות במכשיר בלבד — שום דבר לא נשלח לשרת:**
- כל הנתונים ב-localStorage של הדפדפן
- אין שליחה של מידע לשרתים חיצוניים
- שליחת מייל = פתיחת Gmail בדפדפן (Google רק)

**אבל שים לב:** כיוון שהאפליקציה ציבורית ב-GitHub Pages, **אל תעלה קורות חיים או נתונים רגישים לריפו**. CVs שאתה מעלה נשמרים רק ב-localStorage של הדפדפן שלך.

---

## 🆘 פתרון בעיות

### "Page not found" אחרי דפלוי
- חכה 2-5 דקות (GitHub לוקח זמן)
- בדוק ששם הקובץ הוא בדיוק `index.html` (אותיות קטנות!)
- בדוק שה-branch הוא `main` (לא `master`)

### פונטים לא נטענים
- הבעיה: חסימת Google Fonts ברשת מסוימת
- פתרון: פותחים מדפדפן רגיל ולא דרך VPN מוגבל

### האפליקציה לא שומרת נתונים
- בדוק שלא פתחת ב-Incognito
- ב-Safari: ודא שהגלישה הפרטית כבויה
- במובייל: הוסף למסך הבית → נפתח כ-PWA ונשמר בנפרד

### PWA לא מותקן במובייל
- ודא שגלישה דרך HTTPS (GitHub Pages → כן)
- ב-iOS: חובה Safari, לא Chrome
- ב-Android: Chrome או Edge

---

## 📂 מבנה הקבצים

```
cfo-tracker/
├── index.html           ← האפליקציה המלאה (136KB)
├── README.md            ← תיעוד ראשי
├── DEPLOY.md            ← המדריך הזה
├── .gitignore           ← קבצים להתעלם
└── .nojekyll            ← דילוג על Jekyll
```

האפליקציה היא **קובץ HTML יחיד** — כל ה-CSS, JS, ונתוני ברירת המחדל בפנים. אין תהליך build.

---

## 🔗 קישורים שימושיים

- [GitHub Pages Docs](https://docs.github.com/en/pages)
- [PWA Docs (MDN)](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps)
- [File System API (Chrome)](https://developer.chrome.com/articles/file-system-access/)
