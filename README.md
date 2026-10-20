# AVERON DEALS BOT — main.py

## Run
pip install -r requirements.txt
python main.py

## Payment Gateway — GlobalNexPay AUTOPAY (already configured)
- Panel: https://manage.globalnexpay.site
- API key (user_token) aur secret key code me pre-set hain, gateway **by default ON** hai.
- Admin panel -> ⚡ PAYMENT GATEWAY se status, min amount, test aur pending payments dekh sakte ho.
- Payment aane par wallet/order har 15 second me AUTO confirm hota hai (koi screenshot nahi).

## Payment options (dono hamesha available)
- ⚡ AUTO PAY — instant gateway link, auto verify.
- 📷 MANUAL PAY (QR SCANNER) — UPI QR + "I HAVE PAID", admin manually approve karta hai.
- 💚 WALLET / WALLET + PAY — partial wallet ke baad user AUTO ya MANUAL koi bhi 1 chun sakta hai.
- Wallet screen par bhi dono buttons: ⚡ AUTO PAY — ADD MONEY aur 📷 MANUAL PAY — QR SCANNER.

## Design
- Har button stylish bold font + random colour (primary/success/danger) + premium emoji icon.
- /start par bot-format header + random motivational quote (blockquote bold).
- Premium emoji pack updated (✅ id 6269141158111219856, plus naye 💳 🌐 💬 💲 🎧 📱 🛒 🎬 🚗 🔥 🏀 🎮 📺 ❤️ 📲).

## 📊 Payment History (Owner + Admin)
- Admin panel -> **📊 PAYMENT HISTORY**, ya command **/history**.
- Gateway panel me bhi: **⚡ AUTOPAY LOG DETAILS** aur **📊 AUTO vs MANUAL HISTORY**.
- Report me: AUTOPAY total/today/7-day, MANUAL total/today/7-day, %, grand total + latest 12 payment logs (user id, ref id, time, approving admin).
- Har confirm payment `payment_ledger` table me save hota hai (autopay gateway settle, manual QR deposit approve, manual order approve).

## 🔐 Secrets (.env) — ZARURI
Ab bot token / gateway keys / supplier keys code me nahi hain.
1. `.env.example` ko copy karke `.env` banao, sab NAYE (rotate kiye hue) keys daalo.
2. `pip install -r requirements.txt` phir `python main.py`.
3. Purani DB me gateway key pehle se save ho sakti hai — Admin -> ⚡ PAYMENT GATEWAY se nayi token set karo.

## 🔌 Supplier API + Profit (Admin -> 🔌 SUPPLIER API + PROFIT)
- CouponShops / Acczone / EliteToolz — har API alag **ON/OFF**, balance check, catalog view (product IDs).
- **PRODUCT MAPPING**: `service_key | duration | provider | product_id | cost | INR/USD`
- Har mapping par supplier cost, profit (₹ fixed ya %), **APPLY PRICE** = cost + profit, aur AUTO ON/OFF.
- **BULK PRICE + / -**: `+10%`, `-5%`, `+20`, `-15`, ya `netflix +10%`.
- **USD RATE**: USD cost ko ₹ me badalne ke liye.
- **AUTO DELIVERY** (global) OFF by default. ON + mapping AUTO ON + API ON ho tabhi payment confirm hone ke baad supplier se 1 order lagta hai aur user ko code/account auto bhej diya jata hai.
- Safety: order kabhi double nahi lagta, timeout par "uncertain" mark hota hai (dashboard check karo), price < cost ho to auto order nahi lagta (LOSS GUARD).
- **PROFIT REPORT**: today / 7 days / all-time sale − supplier cost (gateway fees alag).
- **SUPPLIER ORDERS**: latest orders + delivered order ka Resend (naya order nahi lagta).

## ✅ Tests
`python -m unittest discover -s tests -v`
