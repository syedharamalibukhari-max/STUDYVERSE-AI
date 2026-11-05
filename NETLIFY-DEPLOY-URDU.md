# StudyVerse AI — Netlify par deploy karne ka asaan tareeqa

## 1) ZIP extract karo
`studyverse-ai-final.zip` ko extract karo. Andar `studyverse-ai` folder hoga.

## 2) GitHub par upload karo
1. github.com par login karo.
2. **New repository** par click karo; naam `studyverse-ai` rakh do.
3. Repository create hone ke baad **Add file → Upload files** kholo.
4. Extract kiye gaye folder ke andar ki files/folders upload karo. `src`, `public`, `netlify`, `database`, `package.json`, `netlify.toml` sab upload hon.
5. `node_modules`, `dist`, `.env` ya koi secret/API key upload NAHI karni.
6. Neeche **Commit changes** click kar do.

## 3) Netlify par website publish karo
1. netlify.com par account banao/login karo.
2. **Add new site → Import an existing project** select karo.
3. GitHub connect karke `studyverse-ai` repository choose karo.
4. Build settings check karo:
   - Build command: `npm run build`
   - Publish directory: `dist`
   - Functions folder: `netlify/functions` (ye `netlify.toml` mein set hai)
5. **Deploy site** click karo.
6. Netlify dependencies install karke website build karega. Build successful ho to Netlify tumhein `something.netlify.app` link dega. Ye tumhari live website hogi.

## 4) HAM ko real AI banana (optional)
Website bina API key ke demo mode mein chal sakti hai. Real AI answers ke liye provider ki API key chahiye; provider ke charges ho sakte hain.

1. Netlify mein apni site kholo.
2. **Site configuration → Environment variables** par jao.
3. `OPENAI_API_KEY` naam ka variable add karo aur apni private API key uski value mein paste karo.
4. Optional: `OPENAI_MODEL` variable `gpt-4o-mini` value ke saath add kar sakte ho.
5. Site ko redeploy karo.

API key ko GitHub, frontend code, `VITE_` variable ya public chat mein kabhi mat dalna. Key sirf Netlify ke Environment Variables mein honi chahiye.

## 5) Search engine aur AdSense se pehle
- Pehle site ko khud mobile aur desktop par test karo.
- `public/robots.txt` aur `public/sitemap.xml` mein `YOUR-DOMAIN.example` ko apne actual Netlify URL ya custom domain se replace karo.
- Google Search Console mein apni website add karke sitemap submit karo.
- AdSense approval guaranteed nahi hoti. Original, complete educational content, clear About/Contact/Privacy pages aur policy compliance zaroori hain. Sirf sample chapters wali website ko complete learning library keh kar advertise na karo.

## Abhi kya live hai aur kya baqi hai?
Degrees/course catalogue, sample chapter, sample PDF, quiz, browser-based planner, code editor (run nahi karta), aur HAM chat interface included hain. HAM demo mode mein limited examples deta hai; live AI ke liye API key chahiye. Text/Markdown/CSV upload supported hai. PDF/DOCX extraction, full subject-wise notes, login/signup, synced accounts, admin CMS, PostgreSQL connection aur secure code execution abhi implement nahi hain. In features ko fake ya complete keh kar show nahi kiya gaya.
