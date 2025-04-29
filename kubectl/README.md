به‌طور کلی نسخه‌ی kubectl (کلاینت) و نسخه‌ی API server (سرور خوشه) باید حداکثر یک نسخه‌ی جزئی (minor) با هم اختلاف داشته باشند تا از مشکلات ناسازگاری جلوگیری شود. یعنی اگر سرور شما ۱٫۲۷ است، بهتر است کلاینت ۱٫۲۶، ۱٫۲۷ یا ۱٫۲۸ باشد.

با توجه به مثال قبلی
ما در مثال از k3s ورژن v1.27.4 استفاده کردیم.

شما اما کلاینت kubectl را روی 1.33.0 تنظیم کرده‌اید.

این اختلاف ۶ نسخه‌ی جزئی است و ممکن است در بعضی دستورات یا ویژگی‌ها با خطا مواجه شوید.



-  چون نیاز هست که یک پوشه داشته باشیم و درونش فایل kubeconfig.yaml هم باشه قبل اجرا با این ایمیج میشه این کار رو کرد
- چون که داکر برای این کار مجوز نداره
`
  init-kubeconfig:
    image: busybox
    volumes:
      - ./output:/output
    entrypoint: ["sh", "-c", "mkdir -p /output && touch /output/kubeconfig.yaml"]
    `

  - روش دیگه اینه که قبل از اجر دستور زیر رو بزنیم و نیازی به اینچیز هانباشه
   `
        mkdir -p output && touch output/kubeconfig.yaml
        docker compose down -v
        docker compose up -d
        docker compose run --rm kubectl kubectl get nodes
  `