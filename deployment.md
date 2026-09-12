# Ghid de Deployment & SEO (Render + Google Search Console)

Acest ghid descrie procesul prin care site-ul CTI FMI Unibuc poate fi pus online, pe platforma **Render**, și cum îl putem înscrie în **Google Search Console** pentru indexare SEO corespunzătoare.

---

## 1. Publicarea Site-ului (Deployment) folosind Render

Deoarece site-ul este unul **Static (doar HTML/CSS/JS)**, publicarea pe Render.com este complet gratuită, foarte rapidă și asigură SSL automat.

### Pași necesari:

1. **Găzduiește codul sursă** 
   - Încarcă tot codul (inclusiv `index.html` și folderul `assets`) într-un repository public sau privat pe **GitHub** sau **GitLab**.

2. **Creează un cont pe Render**
   - Mergi la [Render.com](https://render.com/) și autentifică-te folosind contul de GitHub.

3. **Creează un serviciu Static Site**
   - În dashboard-ul Render, apasă butonul **New +** și alege **Static Site**.
   - Conectează repository-ul de GitHub unde ai urcat codul.

4. **Setări de configurare Render**
   - **Name**: Numele dorit pentru site (ex: `cti-unibuc-site`).
   - **Branch**: `main` sau `master` (depinde unde ai încărcat codul).
   - **Build Command**: *Lasă gol* (Fiind site pur static, nu necesită un build proces, cum ar fi webpack sau npm run build).
   - **Publish Directory**: `.` (rădăcina proiectului, deoarece `index.html` este chiar acolo). Sau lasă-l implicit dacă acesta detectează automat root-ul.

5. **Deploy**
   - Apasă pe **Create Static Site**.
   - În câteva momente (sub 1-2 minute), Render îți va genera un URL de tipul `https://nume-ales.onrender.com`. 
   - Odată pus pe Render, poți adăuga și un **Custom Domain** din setările site-ului pe Render (de exemplu, un domeniu oferit de facultate).

---

## 2. Înregistrarea în Google Search Console

Pentru ca studenții să găsească site-ul ușor atunci când caută „CTI Unibuc”, este esențial să forțăm Google să ne indexeze paginile.

### Pași necesari:

1. **Accesează GSC**
   - Deschide [Google Search Console](https://search.google.com/search-console).
   - Autentifică-te cu un cont Google (de preferat o adresă de email instituțională sau adresa tehnică DevCore).

2. **Adaugă Proprietatea**
   - Dă click pe **Adaugă o proprietate (Add property)**.
   - Vei avea două opțiuni: **Domeniu** (Domain) sau **Prefix URL** (URL Prefix).
   - **Dacă folosești URL-ul Render (`https://...onrender.com`)**: Alege „Prefix URL” și lipește link-ul exact.
   - **Dacă folosești domeniul tău propriu (ex: `cti.unibuc.ro`)**: Este recomandat să alegi „Domeniu”, pentru a acoperi automat http/https și www/non-www.

3. **Verificarea Proprietății**
   - Dacă ai ales **Prefix URL**, Google îți va oferi un fișier `.html` pe care să-l descarci. Acel fișier trebuie să îl urci în folderul principal (lângă `index.html`), apoi să îi dai Push pe GitHub. Render va prelua automat fișierul. Apoi dai „Verify” în GSC.
   - O altă opțiune simplă pentru Prefix URL este **Eticheta HTML (HTML Tag)**:
     - GSC îți va genera un cod meta (ex: `<meta name="google-site-verification" content="XYZ123..." />`).
     - Adaugă acest cod în secțiunea `<head>` a fișierului `index.html`.
     - Fă push la modificări, așteaptă ca Render să redeploieze și apasă **Verificați (Verify)** în GSC.
   - Dacă ai ales **Domeniu**, verificarea se face adăugând o înregistrare de tip **TXT în panoul de control DNS** al furnizorului tău de domenii.

4. **Trimiterea Sitemap-ului (Opțional, dar recomandat)**
   - Deși nu este un site masiv, un sitemap ajută. Poți genera rapid un fișier `sitemap.xml` (folosind unelte gratuite online precum *XML Sitemaps*) care conține linkurile spre toate paginile tale: `index.html`, `despre.html`, `studenti.html` etc.
   - Pune `sitemap.xml` în directorul root.
   - În GSC, mergi în stânga la secțiunea **Sitemaps**, introdu URL-ul (ex: `sitemap.xml`) și apasă Submit.

5. **Verificarea Indexării**
   - Mergi în secțiunea **Inspectare adrese URL (URL Inspection)**.
   - Lipește link-ul paginii tale principale (`https://...`).
   - Apasă pe **Solicită indexarea (Request Indexing)** pentru a alerta roboții Google.

### Ce beneficii aduc Meta Tag-urile SEO adăugate?
Am integrat deja tag-urile SEO OpenGraph (OG) și Descrieri în toate fișierele HTML. Prin urmare:
- Google va afișa sub link o descriere corectă, relevantă despre programul CTI FMI.
- La partajarea site-ului pe WhatsApp, Facebook, LinkedIn, va apărea frumos Titlul paginii, Tipul și Descrierea sa.
