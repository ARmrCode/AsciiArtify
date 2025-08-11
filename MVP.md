
# MVP Demonstration

## Demo Video

<video src="../demo.mp4" controls autoplay loop muted width="800"></video>

---

## Опис MVP

MVP (Minimum Viable Product) — це мінімальний продукт з основними функціями, необхідними для того, щоб перевірити продукт на фокус-групі користувачів.  
На цьому етапі розробники додають додаткові функції, фіксять баги та вдосконалюють продукт на основі отриманого від користувачів фідбеку.

З боку DevOps для цього потрібно створити додаток у ArgoCD, який буде відслідковувати Git-репозиторій продукту  
[https://github.com/ARmrCode/AsciiArtify](https://github.com/ARmrCode/AsciiArtify)  
та налаштувати автоматичну синхронізацію.

Після успішного налаштування ArgoCD можна запустити повний цикл, щоб продемонструвати, як ArgoCD автоматично відслідковує та синхронізує зміни з Git-репозиторію та розгортає їх на Kubernetes-кластері.

---

## Виконані кроки

```bash
# Проксі доступ до ArgoCD
kubectl port-forward svc/argocd-server -n argocd 8080:443

# Отримання паролю адміністратора
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo

# Проксі доступ до сервісу demo/ambassador
kubectl port-forward -n demo svc/ambassador 8088:80

# Перевірка сервісів у namespace demo
kubectl get svc -n demo

# Проксі доступ повторно
kubectl port-forward -n demo svc/ambassador 8088:80

# Тестовий запит до сервісу
curl localhost:8088

# Завантаження тестового зображення Google
wget -O /tmp/g.png "https://www.google.com/images/branding/googlelogo/1x/googlelogo_color_272x92dp.png"

# Відкриття зображення
open /tmp/g.png 

# Відправка зображення у сервіс
curl -F 'image=@/tmp/g.png' localhost:8088/img/

# Завантаження зображення повторно
wget -O /tmp/g.png "https://www.google.com/images/branding/googlelogo/1x/googlelogo_color_272x92dp.png"

# Відкриття зображення повторно
open /tmp/g.png 

# Повторна відправка зображення у сервіс
curl -F 'image=@/tmp/g.png' localhost:8088/img/
```

---

## Результат
Налаштований додаток в ArgoCD автоматично синхронізує стан Kubernetes-кластера з Git-репозиторієм,  
а сервіс обробляє завантажені зображення, як показано у демо-відео.
