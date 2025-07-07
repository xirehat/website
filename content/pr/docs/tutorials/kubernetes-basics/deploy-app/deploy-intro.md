---
title: استفاده از kubectl  برای ساختن Deployment
weight: 10
---

## {{% heading "objectives" %}}

* در بارهapplication Deployments. بیاموزید .
* اولین برنامتون رو در kuberntes با kubectl  اجرا کنید با .

## Kubernetes Deployments

{{% alert %}}
_یک Deployment در کوبرنتیز مسئول ایجاد و به‌روزرسانی  instances از برنامه‌ی شما است.._
{{% /alert %}}



{{< note >}}
این آموزش از کانتینری استفاده می‌کند که به معماری AMD64 نیاز دارد. اگر از Minikube روی سیستمی با معماری CPU متفاوت استفاده می‌کنید، می‌توانید سعی کنید Minikube را با درایوری اجرا کنید که قادر به شبیه‌سازی معماری AMD64 باشد.
برای مثال، درایور Docker Desktop می‌تواند این کار را انجام دهد.
{{< /note >}}

وقتی یک [running Kubernetes cluster](/docs/tutorials/kubernetes-basics/create-cluster/cluster-intro/), دارید، می‌توانید برنامه‌های کانتینر شده خود را روی آن مستقر کنید. برای انجام این کار، یک Kubernetes **Deployment** ایجاد می‌کنید. Deployment به Kubernetes دستور می‌دهد که چگونه نمونه‌هایی از برنامه شما را ایجاد و به‌روزرسانی کند. پس از ایجاد یک Deployment،  Kubernetes
control plane نمونه‌های برنامه موجود در آن Deployment را برای اجرا روی node در کلاستر برنامه‌ریزی می‌کند.




پس از ایجاد instances برنامه، یک کنترل‌کننده‌ی Kubernetes  controller Deployment به طور مداوم آن نمونه‌ها را رصد می‌کند. اگر گره‌ای که میزبان یک نمونه است از کار بیفتد یا حذف شود، Deployment controller instance را با instances در node دیگری در cluster جایگزین می‌کند. **این یک مکانیسم خود-ترمیمی برای رسیدگی به خرابی یا تعمیر و نگهداری cluster فراهم می‌کند.**

در دنیای pre-orchestration، اسکریپت‌های نصب اغلب برای شروع برنامه‌ها استفاده می‌شدند، اما امکان بازیابی از خرابی دستگاه را فراهم نمی‌کردند. Kubernetes Deployments با ایجاد instances برنامه شما و همچنین اجرای آنها در Nodes رویکردی اساساً متفاوت برای مدیریت برنامه ارائه می‌دهد

## استقرار اولین برنامه شما در Kubernetes

{{% alert %}}
_برای اینکه برنامه‌ها روی Kubernetes مستقر شوند، باید در یکی از قالب‌های container پشتیبانی‌شده بسته‌بندی شوند.._
{{% /alert %}}

{{< figure src="/docs/tutorials/kubernetes-basics/public/images/module_02_first_app.svg" class="diagram-medium" >}}

شما می‌توانید با استفاده از رابط خط فرمان Kubernetes، [kubectl](/docs/reference/kubectl/)، یک Deployment ایجاد و مدیریت کنید. `kubectl` از API Kubernetes برای تعامل با کلاستر استفاده می‌کند. در این ماژول، رایج‌ترین دستورات `kubectl` مورد نیاز برای ایجاد Deploymentهایی که برنامه‌های شما را روی یک cluster Kubernetes اجرا می‌کنند، را خواهید آموخت.

هنگام ایجاد یک Deployment، باید container image را برای برنامه خود و تعداد replicas که می‌خواهید اجرا کنید، مشخص کنید. می‌توانید این اطلاعات را بعداً با به‌روزرسانی Deployment خود تغییر دهید؛ [Module 5](/docs/tutorials/kubernetes-basics/scale/scale-intro/)
و [Module 6](/docs/tutorials/kubernetes-basics/update/update-intro/) از بوت کمپ
در مورد چگونگی مقیاس‌بندی و به‌روزرسانی Deploymentهای خود بحث کنید.


برای اولین استقرار خود، از یک برنامه hello-node که در یک کانتینر Docker بسته‌بندی شده است و از NGINX برای بازگرداندن همه درخواست‌ها استفاده می‌کند، استفاده خواهید کرد. (اگر قبلاً سعی نکرده‌اید یک برنامه hello-node ایجاد کنید و آن را با استفاده از یک کانتینر مستقر کنید، می‌توانید ابتدا با دنبال کردن دستورالعمل‌های [learn Hello Minikube](/docs/tutorials/hello-minikube/) این کار را انجام دهید.

شما همچنین باید kubectl را نصب کرده باشید. در صورت نیاز به نصب آن، به [install tools](/docs/tasks/tools/#kubectl) مراجعه کنید.

حالا که می‌دانید Deploymentها چه هستند، بیایید اولین برنامه‌مان را Deploy کنیم!

### kubectl رستورات اولیه 

قالب رایج یک دستور kubectl عبارت است از: `kubectl action resource`.

این دستور، _action_  (مانند `create`، `describe` یا `delete`) را روی _resource_ (مانند `node` یا `deployment`) انجام می‌دهد. می‌توانید از `--help` بعد از زیردستور برای دریافت اطلاعات بیشتر در مورد پارامترهای ممکن استفاده کنید (برای مثال: `kubectl get nodes --help`).



با اجرای دستور `kubectl version` بررسی کنید که kubectl برای ارتباط با کلاستر شما پیکربندی شده باشد.

بررسی کنید که kubectl نصب شده باشد و بتوانید نسخه‌های کلاینت و سرور را ببینید.

برای مشاهده nodes موجود در cluster دستور `kubectl get nodes` را اجرا کنید.

nodes موجود را مشاهده خواهید کرد. بعداً، Kubernetes بر اساس منابع موجود Node، محل استقرار برنامه ما را انتخاب خواهد کرد.

### استقرار یک برنامه


Let’s deploy our first app on Kubernetes with the `kubectl create بیایید اولین برنامه خود را با دستور `kubectl create deployment` در Kubernetes مستقر کنیم.

ما باید نام استقرار و مکان image برنامه را ارائه دهیم (آدرس کامل مخزن برای تصاویر میزبانی شده در خارج از Docker Hub را نیز شامل شود).

```shell
kubectl create deployment kubernetes-bootcamp --image=gcr.io/google-samples/kubernetes-bootcamp:v1
```



Great! You just deployed your first application by creating a deployment. This performed a few things for you:

* searched for a suitable node where an instance of the application could be run (we have only 1 available node)
* scheduled the application to run on that Node
* configured the cluster to reschedule the instance on a new Node when needed

To list your deployments use the `kubectl get deployments` command:

```shell
kubectl get deployments
```

می‌بینیم که یک instance از برنامه شما در حال اجرا است. این instance درون یک کانتینر روی گره شما در حال اجرا است.

### برنامه را مشاهده کنید

[Pods](/docs/concepts/workloads/pods/) که درون Kubernetes در حال اجرا هستند، روی یک شبکه خصوصی و ایزوله اجرا می‌شوند. به طور پیش‌فرض، آنها از سایر podها و سرویس‌های درون همان cluster Kubernetes قابل مشاهده هستند، اما خارج از آن شبکه قابل مشاهده نیستند. وقتی از `kubectl` استفاده می‌کنیم، از طریق یک نقطه پایانی API برای ارتباط با برنامه خود در تعامل هستیم.


ما گزینه‌های دیگری در مورد نحوه نمایش برنامه شما در خارج از cluster Kubernetes را بعداً، در [Module 4](/docs/tutorials/kubernetes-basics/expose/) پوشش خواهیم داد.

همچنین به عنوان یک آموزش پایه، ما در اینجا به هیچ وجه توضیح نمی‌دهیم که «Pods» چیستند، این موضوع در مباحث بعدی پوشش داده خواهد شد.

دستور `kubectl proxy` می‌تواند یک پروکسی ایجاد کند که ارتباطات را به شبکه خصوصی در سطح کلاستر هدایت کند. این پروکسی را می‌توان با فشار دادن کلیدهای `control-C` خاتمه داد و در حین اجرا هیچ خروجی نشان نمی‌دهد.

**برای اجرای پروکسی باید یک پنجره ترمینال دوم باز کنید.**

```shell
kubectl proxy
```

اکنون ما ارتباطی بین میزبان خود (ترمینال) و cluster Kubernetes داریم.

پروکسی امکان دسترسی مستقیم به API را از این ترمینال‌ها فراهم می‌کند.

شما می‌توانید تمام APIهای میزبانی شده را از طریق نقطه پایانی پروکسی مشاهده کنید. به عنوان مثال، می‌توانیم نسخه را مستقیماً از طریق API با استفاده از دستور `curl` جستجو کنیم:


```shell
curl http://localhost:8001/version
```

{{< note >}}
اگر پورت ۸۰۰۱ قابل دسترسی نیست، مطمئن شوید که `kubectl proxy`  که در بالا شروع کردید، در ترمینال دوم در حال اجرا باشد.
{{< /note >}}

سرور API به طور خودکار برای هر پاد، بر اساس نام پاد، یک  endpoint ایجاد می‌کند که از طریق پروکسی نیز قابل دسترسی است.

ابتدا باید نام POD را دریافت کنیم و آن را در  environment variable `POD_NAME` ذخیره خواهیم کرد.

```shell
export POD_NAME=$(kubectl get pods -o go-template --template '{{range .items}}{{.metadata.name}}{{"\n"}}{{end}}')
echo Name of the Pod: $POD_NAME
```

شما می‌توانید از طریق API پروکسی شده و با اجرای دستور زیر به Pod دسترسی پیدا کنید:

```shell
curl http://localhost:8001/api/v1/namespaces/default/pods/$POD_NAME:8080/proxy/
```

برای اینکه بتوان بدون استفاده از پروکسی به Deployment جدید دسترسی داشت، به یک سرویس نیاز است که در [Module ۴](/docs/tutorials/kubernetes-basics/expose/) توضیح داده خواهد شد.

## {{% heading "whatsnext" %}}

* آموزش [Viewing Pods and Nodes](/docs/tutorials/kubernetes-basics/explore/explore-intro/).
* بیشتر بدانید[Deployments](/docs/concepts/workloads/controllers/deployment/).