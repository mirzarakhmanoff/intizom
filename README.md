# Intizom — landing

Statik sayt: build kerak emas, papkani shundayligicha joylaysiz.

## Tuzilishi

| Yo'l | Nima |
|---|---|
| `/` | Landing (uz / ru / en) |
| `/privacy/` | Maxfiylik siyosati |
| `/terms/` | Foydalanish shartlari |
| `/delete-account/` | Hisobni o'chirish (Google Play Data safety uchun) |
| `/assets/` | Rasmlar, nishonlar, favicon |

To'rttala sahifa bitta `index.html` ning nusxasi: qaysi hujjatni ko'rsatishni manzilning o'zi hal qiladi.
**`index.html` ni o'zgartirsangiz, uni uchala papkaga qayta nusxalang:**

```bash
for d in privacy terms delete-account; do cp index.html $d/index.html; done
```

Tilni majburlash: `?lang=uz`, `?lang=ru`, `?lang=en` (masalan do'kon sahifasi uchun `/privacy/?lang=en`).

## Mahalliy ko'rish

```bash
python3 -m http.server 8080      # keyin http://localhost:8080
```

Faylni brauzerda to'g'ridan-to'g'ri ochmang: rasmlar `/assets/...` manzilidan olinadi, shuning uchun server kerak.

## Joylash

Sayt domenning ildizida turishi kerak (`https://DOMEN/`), ichki papkada emas.

- **Cloudflare Pages / Netlify / Vercel:** papkani yuklang yoki repozitoriyni ulang. Build buyrug'i yo'q, chiqish papkasi shu papkaning o'zi.
- **O'z serveringiz (nginx):**
  ```nginx
  server {
    server_name DOMEN;
    root /var/www/intizom-landing;
    index index.html;
    location / { try_files $uri $uri/ =404; }
    location /assets/ { expires 30d; add_header Cache-Control "public"; }
  }
  ```
  HTTPS uchun: `certbot --nginx -d DOMEN`.

## Chiqarishdan oldin

- [ ] Hujjatlardagi qavslarni to'ldiring: `[KOMPANIYA NOMI]`, `[MANZIL]`, `[SANA]`, `[HOSTING]`, `[SERVER MAMLAKATI]`, `[N]`, qonun va sud. `index.html` da `[` deb qidiring (uch tilda).
- [ ] Do'kon havolalari: `href="#yuklab"` turgan to'rtta `sbadge` havolasiga App Store va Google Play manzillarini qo'ying.
- [ ] Nishonlar: `assets/badge-*.svg` ni Apple va Google saytidan olingan rasmiy fayllar bilan almashtiring.
- [ ] `<head>` dagi TODO: `canonical` va `og:image`.
- [ ] Aloqa emaili hozir shaxsiy Gmail. Domen pochtasi tayyor bo'lsa almashtiring.
- [ ] Hujjatlarni yurist ko'rib chiqsin. Ular qoralama.
- [ ] Mashq ma'lumotlari uchun "RepDB (repdb.co)" yozuvi pastda qolishi shart (litsenziya talabi).
