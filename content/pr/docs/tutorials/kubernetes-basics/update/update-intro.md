---
title: انجام یک به‌روزرسانی رو به بالا
weight: 10
---

## {{% heading "objectives" %}}

با استفاده از kubectl یک به‌روزرسانی غلتان انجام دهید.

## به‌روزرسانی یک برنامه


{{% alert %}}
_به‌ Rolling updates با به‌روزرسانی تدریجی نمونه‌های Pods با موارد جدید، امکان به‌روزرسانی Deployments را بدون هیچ‌گونه قطعی فراهم می‌کند.._
{{% /alert %}}

کاربران انتظار دارند که برنامه‌ها همیشه در دسترس باشند و از توسعه‌دهندگان انتظار می‌رود که نسخه‌های جدید آنها را چندین بار در روز مستقر کنند. در Kubernetes این کار با «به‌روزرسانی‌های غلتان» انجام می‌شود. **rolling updates** اجازه می‌دهد تا به‌روزرسانی استقرار بدون هیچ گونه خرابی انجام شود. این کار با جایگزینی تدریجی پادهای فعلی با پادهای جدید انجام می‌شود. پادهای جدید روی گره‌هایی با منابع موجود برنامه‌ریزی می‌شوند و Kubernetes قبل از حذف پادهای قدیمی، منتظر شروع به کار پادهای جدید می‌ماند.

در ماژول قبلی، برنامه خود را برای اجرای چندین نمونه مقیاس‌بندی کردیم. این یک الزام برای انجام به‌روزرسانی‌ها بدون تأثیر بر در دسترس بودن برنامه است.
به طور پیش‌فرض، حداکثر تعداد پادهایی که می‌توانند در طول به‌روزرسانی در دسترس نباشند
و حداکثر تعداد پادهای جدیدی که می‌توانند ایجاد شوند، یکی است. هر دو گزینه را می‌توان به تعداد یا درصد (از پادها) پیکربندی کرد. در Kubernetes، به‌روزرسانی‌ها
نسخه‌بندی می‌شوند و هرگونه به‌روزرسانی Deployment را می‌توان به نسخه قبلی (پایدار) برگرداند.

## Rolling updates نمای کلی

<!-- animation -->
<div class="col-md-8">
  <div id="myCarousel" class="carousel" data-ride="carousel" data-interval="3000">
    <div class="carousel-inner" role="listbox">
      <div class="item carousel-item active">
        <img src="/docs/tutorials/kubernetes-basics/public/images/module_06_rollingupdates1.svg">
      </div>
      <div class="item carousel-item">
        <img src="/docs/tutorials/kubernetes-basics/public/images/module_06_rollingupdates2.svg">
      </div>
      <div class="item carousel-item">
        <img src="/docs/tutorials/kubernetes-basics/public/images/module_06_rollingupdates3.svg">
      </div>
      <div class="item carousel-item">
        <img src="/docs/tutorials/kubernetes-basics/public/images/module_06_rollingupdates4.svg">
      </div>
    </div>
  </div>
</div>

{{% alert %}}
_اگر یک Deployment به صورت عمومی در معرض دید عموم قرار گیرد، سرویس در طول به‌روزرسانی، ترافیک را فقط به Podهای موجود متعادل می‌کند.._
{{% /alert %}}

مشابه مقیاس‌پذیری برنامه، اگر یک Deployment به صورت عمومی در معرض دید عموم قرار گیرد، سرویس در طول به‌روزرسانی، ترافیک را فقط به Podهای موجود متعادل می‌کند. Pod موجود، نمونه‌ای است که برای کاربران برنامه در دسترس است.

Rolling update اقدامات زیر را امکان‌پذیر می‌کنند:

* انتقال یک برنامه از یک محیط به محیط دیگر (از طریق به‌روزرسانی‌هایcontainer image)
* بازگشت به نسخه‌های قبلی
* ادغام مداوم و تحویل مداوم برنامه‌ها با عدم خرابی


در آموزش تعاملی زیر، برنامه خود را به نسخه جدید به‌روزرسانی می‌کنیم و همچنین یک بازگشت به نسخه قبل انجام می‌دهیم.


### نسخه برنامه را به‌روزرسانی کنید

برای فهرست کردن Deployment های خود، زیردستور `get deployments` را اجرا کنید:

```shell
kubectl get deployments
```

برای فهرست کردن پادهای در حال اجرا، دستور فرعی `get pods` را اجرا کنید:


```shell
kubectl get pods
```
برای مشاهده نسخه image فعلی برنامه، زیردستور `describe pods` را اجرا کنید و به دنبال فیلد `Image` بگردید:

```shell
kubectl describe pods
```
برای به‌روزرسانی image برنامه به نسخه ۲، از زیردستور `set image` استفاده کنید و به دنبال آن نام استقرار و نسخه جدید image را بنویسید:

```shell
kubectl set image deployments/kubernetes-bootcamp kubernetes-bootcamp=docker.io/jocatalin/kubernetes-bootcamp:v2
```
این دستور به Deployment اطلاع داد که از یک image متفاوت برای برنامه شما استفاده کند و یک به‌روزرسانی مداوم را آغاز کرد. وضعیت Podهای جدید را بررسی کنید و با استفاده از زیردستور `get pods`، پایان Podهای قدیمی را مشاهده کنید:

```shell
kubectl get pods
```

### یک به‌روزرسانی را تأیید کنید

ابتدا، بررسی کنید که سرویس در حال اجرا باشد، زیرا ممکن است آن را در مرحله آموزش قبلی حذف کرده باشید، دستور `describe services/kubernetes-bootcamp` را اجرا کنید. اگر از دست رفته است، می‌توانید دوباره آن را با دستور زیر ایجاد کنید:


```shell
kubectl expose deployment/kubernetes-bootcamp --type="NodePort" --port 8080
```

یک متغیر محیطی به نام `NODE_PORT` ایجاد کنید که مقدار پورت گره را داشته باشد:

```shell
export NODE_PORT="$(kubectl get services/kubernetes-bootcamp -o go-template='{{(index .spec.ports 0).nodePort}}')"
echo "NODE_PORT=$NODE_PORT"
```

در مرحله بعد، یک `curl` به IP و پورتِ در معرضِ دسترسی انجام دهید:

```shell
curl http://"$(minikube ip):$NODE_PORT"
```

هر بار که دستور `curl` را اجرا می‌کنید، به یک Pod متفاوت برخورد خواهید کرد. توجه داشته باشید که اکنون همه Podها آخرین نسخه (`v2`) را اجرا می‌کنند.

همچنین می‌توانید با اجرای زیردستور `rollout status` به‌روزرسانی را تأیید کنید:

```shell
kubectl rollout status deployments/kubernetes-bootcamp
```

برای مشاهده نسخه تصویر فعلی برنامه، زیردستور describe pods را اجرا کنید:

```shell
kubectl describe pods
```

در فیلد `Image` خروجی، تأیید کنید که از آخرین نسخه Image (`v2`) استفاده می‌کنید.


### یک به‌روزرسانی را برگردانید

بیایید یک به‌روزرسانی دیگر انجام دهیم و سعی کنیم image با برچسب `v10` را مستقر کنیم:


```shell
kubectl set image deployments/kubernetes-bootcamp kubernetes-bootcamp=gcr.io/google-samples/kubernetes-bootcamp:v10
```

برای مشاهده وضعیت استقرار از دستور `get deployments` استفاده کنید:

```shell
kubectl get deployments
```

توجه داشته باشید که خروجی تعداد دلخواه Pod های موجود را فهرست نمی‌کند. برای فهرست کردن همه Pod ها، زیردستور `get pods` را اجرا کنید:


```shell
kubectl get pods
```

توجه کنید که برخی از پادها وضعیت  دارند
`ImagePullBackOff`.

برای درک بیشتر مشکل، زیردستور `describe pods` را اجرا کنید:


```shell
kubectl describe pods
```

در بخش `Events` در خروجی مربوط به پادهای آسیب‌دیده، توجه کنید که نسخه `v10` ایمیج در مخزن وجود ندارد.



برای بازگرداندن آخرین نسخه فعال به حالت اولیه، از زیردستور rollout undo استفاده کنید:

```shell
kubectl rollout undo deployments/kubernetes-bootcamp
```
دستور `rollout undo`، استقرار را به حالت شناخته شده قبلی (`v2` از تصویر) برمی‌گرداند. به‌روزرسانی‌ها نسخه‌بندی می‌شوند و می‌توانید به هر حالت شناخته شده قبلی از استقرار برگردید.

از زیردستور `get pods` برای فهرست کردن مجدد Podها استفاده کنید:

دستور `rollout undo`، استقرار را به حالت شناخته شده قبلی (`v2` از image) برمی‌گرداند. به‌روزرسانی‌ها نسخه‌بندی می‌شوند و می‌توانید به هر حالت شناخته شده قبلی از استقرار برگردید.

از زیردستور `get pods` برای فهرست کردن مجدد Podها استفاده کنید:


```shell
kubectl get pods
```

برای بررسی ایمیج مستقر شده روی پادهای در حال اجرا، از زیردستور `describe pods` استفاده کنید:


```shell
kubectl describe pods
```

استقرار دوباره از نسخه پایدار برنامه (`v2`) استفاده می‌کند. بازگشت به نسخه قبلی با موفقیت انجام شد.

به یاد داشته باشید که cluster محلی خود را تمیز کنید.

```shell
kubectl delete deployments/kubernetes-bootcamp services/kubernetes-bootcamp
```

## {{% heading "whatsnext" %}}

* درباره [Deployments](/docs/concepts/workloads/controllers/deployment/). بیشتر بدانید.