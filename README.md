# Hermes Donat Mini App

Telegram ichida Feed Up donat tarkibini tanlash oynasi. Bu repoda faqat HTML/CSS/JavaScript bor. Python agent va Smartup ulanishi mavjud VPS’da qoladi.

## Ko‘rish

- `demo.html` — namuna; hech qanday serverga yoki Smartupga so‘rov yubormaydi.
- `index.html` — Telegram botidagi tugmadan ochiladigan haqiqiy oyna. Oddiy brauzerda zakaz ma’lumotini ko‘rsatmaydi: Telegram imzosi tekshiriladi.

Namuna ta’mlari misol uchun berilgan. Haqiqiy tovarlar agentdagi donat assortimentidan olinadi. Narx Smartupdan olinadi. Jonli qoldiq ulanmagan; mavjud ta’mlarni operator belgilaydi.

## GitHub Pages

1. Shu beshta faylni loyiha repozitoriysiga joylang (`index.html`, `demo.html`, `.nojekyll`, `.gitignore`, `README.md`).
2. Repository Settings → Pages → Deploy from a branch → main → /(root).
3. GitHub ko‘rsatgan `https://AKKAUNT.github.io/REPO/` manzilini oling.

Alohida domen sotib olish talab qilinmaydi. GitHub Pages Python agentni ishlatmaydi; agent VPS’da 24/7 ishlaydi.

## VPS API

Oyna `https://89.39.94.60/mini-app/api` manziliga ulanadi. Bu manzilda ishonchli HTTPS sertifikati va faqat `/mini-app/` uchun agentning `127.0.0.1:8080` portiga proxy sozlanishi kerak. Agentning asosiy paneli localhostda qoladi.

IP uchun Let’s Encrypt sertifikatini olish mumkin: Certbot 5.4 yoki yangiroq versiyada `--ip-address 89.39.94.60 --preferred-profile shortlived` ishlatiladi. IP sertifikati qisqa muddatli bo‘lgani uchun avtomatik yangilash va nginx’ni yangilangan sertifikat bilan qayta yuklash ham sozlanadi. Buni mavjud xizmatlarni tekshirib, VPS’da alohida o‘rnatish lozim.

Agent yangilagichidagi kerakli shakl (GitHub ko‘rsatgan haqiqiy URL bilan):

```text
.venv/bin/python telegram_buttons_yoqish.py --apply --public-url https://AKKAUNT.github.io/REPO/ --api-url https://89.39.94.60/mini-app/api
```

Bu buyruq VPS’da root sifatida `/opt/hermes-agent` ichida bajariladi. Yangilagich avval agent versiyasi, mavjud fayllar va tasdiqlash ruxsatlarini tekshiradi; ishchi bazani almashtirmaydi. Oyna va API HTTPS orqali ochilishi tasdiqlanmaguncha yangi havolani botga yoqmaydi.

Backend CORS’da faqat shu GitHub Pages originiga ruxsat beradi. Har bir zakaz so‘rovida Telegram imzosi, operator IDsi va yangi zakaz nusxasi qayta tekshiriladi. Faqat yakuniy yuborish tugmasi Smartup importini chaqiradi.

## Donat qoidalari

- Izohsiz: Strawberry + Nutty teng.
- Faqat shokolad: Nutty.
- Qulupnay yoki rozoviy: Strawberry.
- Aniq miqdorli izoh: ta’mlar yig‘indisi zakaz miqdoriga teng bo‘lsa, odatdagi avtomatik yo‘l.
- Mix / assorti / har xil: ombordagi turli donatlardan operator tanlaydi.

## Manbalar

- https://docs.github.com/en/pages/getting-started-with-github-pages/what-is-github-pages
- https://letsencrypt.org/2026/03/11/shorter-certs-certbot
