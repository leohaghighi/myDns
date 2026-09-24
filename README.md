# Xbox Smart DNS + Telegram Bot

یک Smart DNS شخصی (dnsmasq + sniproxy) روی VPS، با ربات تلگرام برای مدیریت IPهای مجاز.
نصب با **یک خط** انجام می‌شود و با Amnezia VPN تداخلی ندارد (اگر پورت‌های ۵۳/۸۰/۴۴۳ آزاد نباشند، بدون تغییر هیچ چیز متوقف می‌شود).

> Personal Smart DNS for a VPS (dnsmasq + SNI proxy), locked to whitelisted home IPs that you manage from a Telegram bot. Ubuntu/Debian only.

## نصب

روی سرور، به‌عنوان root (`sudo -i`) این خط را paste کن (به‌جای `YOUR_USER/YOUR_REPO` نام مخزن خودت):

```bash
bash <(curl -fsSL https://raw.githubusercontent.com/leohaghighi/myDns/blob/main/Install.sh](https://raw.githubusercontent.com/leohaghighi/myDns/refs/heads/main/Install.sh)
```

قبلش در تلگرام به `@BotFather` برو، `/newbot` بزن و توکن را بردار. نصب‌کننده توکن را می‌پرسد
(یا: `BOT_TOKEN=123:abc bash <(curl ...)`).

در پایان یک لینک `t.me/...?start=...` چاپ می‌شود؛ آن را روی گوشی باز کن تا **مالک ربات** شوی.

## ربات

| نقش | چه کاری می‌تواند |
|---|---|
| مالک (owner) | همه‌چیز؛ ادمین دعوت/ارتقا/تنزل می‌کند |
| ادمین (admin) | کاربر دعوت و حذف می‌کند، IP هر کسی را ثبت/حذف می‌کند، دامنه اضافه می‌کند |
| کاربر (user) | فقط IP خودش را ثبت می‌کند |

- **دعوت دوستت:** در ربات `/invite admin` (برای ادمین) یا `/invite` (برای کاربر) را بزن و لینک یک‌بار مصرفِ ۲۴ ساعته را برایش بفرست.
- **ثبت IP (راه ۱ – یک لمس):** «🔗 لینک ثبت IP» را بزن و لینک شخصی را با گوشی/کامپیوتری که به اینترنت خانه‌ی ایکس‌باکس وصل است (VPN خاموش) باز کن. سرور خودش IP را می‌بیند و ثبت می‌کند.
- **ثبت IP (راه ۲):** خود IP را برای ربات بفرست (مثلاً `5.120.10.20`).
- هر نفر آخرین ۳ IP خودش را نگه می‌دارد.
- دستورهای مدیر: `/users` `/remove ID` `/setip ID IP` `/delip IP` `/status` `/domains` `/adddomain d` `/removedomain d` `/logs`

در ایکس‌باکس: DNS را دستی بگذار و IP سرور را (که نصب‌کننده چاپ می‌کند) وارد کن.

## نکته‌ها

- لینک ثبت IP روی HTTP ساده است. توکنش شخصی و ۱۲۸ بیتی است ولی اگر لو رفت `/newlink` بزن.
- پورت لینک (پیش‌فرض 8787/tcp) باید در فایروال هاستینگ باز باشد. همین‌طور ۵۳ (UDP/TCP)، ۸۰ و ۴۴۳.
- توکن ربات فقط روی سرور در `/etc/smartdns/bot.json` (دسترسی root) ذخیره می‌شود، نه در مخزن.
- اجرای دوباره‌ی همان خط، اسکریپت‌ها را به‌روز می‌کند و کاربرها پاک نمی‌شوند.

## دستورهای سرور

```
smartdns status | list | logs
sudo smartdns ip <IP ...>      # لیست IPهای مجاز را جایگزین می‌کند (none = خالی)
sudo smartdns add <domain>     # sudo smartdns remove <domain>
sudo smartdns uninstall        # حذف کامل (ربات هم پاک می‌شود)
```
