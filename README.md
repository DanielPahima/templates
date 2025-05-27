# 🔁 Reusable CI/CD Pipeline Template

תבנית פייפליין מודולרית עבור GitHub Actions, לשימוש בפרויקטים שונים בארגון.  
מטרתה לייצר סטנדרט אחיד לכל שלבי CI/CD: Linting, Testing, Building, Deploying.

---

## 📁 מבנה רכיבי הפייפליין

| קטגוריה | מיקום |
|----------|--------|
| הגדרת משתנים לפי branch | `pipeline/vars/set-vars.yml` |
| בניית Docker / Python / Node | `pipeline/build/` |
| בדיקות אבטחה / יוניט | `pipeline/tests/` |
| Lint לכל שפה | `pipeline/lint/` |
| פריסה דרך ArgoCD | `pipeline/deploy/` |

---

## 🚀 שימוש לדוגמה בפרויקט אחר

```yaml
# .github/workflows/ci.yml
jobs:
  init-vars:
    uses: your-org/reusable-pipeline/pipeline/vars/set-vars.yml@main

  build:
    needs: init-vars
    uses: your-org/reusable-pipeline/pipeline/build/docker.yml@main
    with:
      docker-tag: ${{ needs.init-vars.outputs.image_tag }}
    secrets: inherit
