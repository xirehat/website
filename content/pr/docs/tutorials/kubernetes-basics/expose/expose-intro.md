---
title: استفاده از یک سرویس برای نمایش برنامه شما
weight: 10
---

## {{% heading "objectives" %}}

* آشنایی با سرویس‌ها در Kubernetes.
* آشنایی با نحوه ارتباط برچسب‌ها و انتخابگرها با یک سرویس.
* نمایش یک برنامه در خارج از کلاستر Kubernetes.

## Overview of Kubernetes Services


Kubernetes [Pods](/docs/concepts/workloads/pods/) فانی هستند. Podها دارای یک چرخه حیات (/docs/concepts/workloads/pods/pod-lifecycle/) هستند. هنگامی که یکworker node از بین می‌رود، Podهایی که روی node اجرا می‌شوند نیز از بین می‌روند. یک [Replicaset](/docs/concepts/workloads/controllers/replicaset/) ممکن است به صورت پویا cluster را از طریق ایجاد Podهای جدید به حالت مطلوب برگرداند تا برنامه شما در حال اجرا بماند. به عنوان مثال دیگر، یک backend پردازش تصویر با 3 replicas را در نظر بگیرید. این replicas قابل تعویض هستند. سیستم front-end نباید به کپی‌های back-end یا حتی اگر یک Pod از بین رفته و دوباره ایجاد شود، اهمیتی دهد. با این اوصاف، هر Pod در یک cluster Kubernetes یک آدرس IP منحصر به فرد دارد، حتی Pod های روی یک Node، بنابراین باید راهی برای تطبیق خودکار تغییرات بین Pod ها وجود داشته باشد تا برنامه‌های شما به کار خود ادامه دهند.

{{% alert %}}

_Kubernetes Service یک لایه انتزاعی است که مجموعه‌ای منطقی از Podها را تعریف می‌کند و امکان نمایش ترافیک خارجی، متعادل‌سازی بار و کشف سرویس را برای آن Podها فراهم می‌کند.._
{{% /alert %}}


یک [Service](/docs/concepts/services-networking/service/) در Kubernetes یک انتزاع است که مجموعه‌ای منطقی از Podها و سیاستی را برای دسترسی به آنها تعریف می‌کند. سرویس‌ها
یک اتصال سست بین Podهای وابسته را فعال می‌کنند. یک سرویس با استفاده از YAML یا JSON تعریف می‌شود،
مانند تمام مانیفست‌های شیء Kubernetes. مجموعه Podهایی که توسط یک سرویس هدف قرار می‌گیرند، معمولاً
توسط یک _label selector_ تعیین می‌شود (برای اینکه بدانید چرا ممکن است یک سرویس را بدون
شامل کردن `selector` در مشخصات بخواهید، به زیر مراجعه کنید).

اگرچه هر Pod یک آدرس IP منحصر به فرد دارد، اما این IPها بدون وجود سرویس، خارج از خو clusterشه در معرض دید قرار نمی‌گیرند. سرویس‌ها به برنامه‌های شما اجازه می‌دهند ترافیک دریافت کنند. سرویس‌ها را می‌توان با مشخص کردن `type` در `spec` سرویس، به روش‌های مختلف در معرض دید قرار داد:


* _ClusterIP_ (default) - سرویس را روی یک IP داخلی در کلاستر نمایش می‌دهد. این نوع باعث می‌شود سرویس فقط از داخل کلاستر قابل دسترسی باشد.

* _NodePort_ - سرویس را با استفاده از NAT روی پورت یکسان هر Node انتخاب شده در خوشه قرار می‌دهد.

با استفاده از `NodeIP:NodePort`، دسترسی به یک سرویس را از خارج از خوشه امکان‌پذیر می‌کند.Superset of ClusterIP.

* _LoadBalancer_ - یک متعادل‌کننده بار خارجی در cloud فعلی (در صورت پشتیبانی) ایجاد می‌کند و یک IP خارجی ثابت به سرویس اختصاص می‌دهد. Superset of NodePort.


* _ExternalName_ - سرویس را با برگرداندن یک رکورد `CNAME` به همراه مقدار آن، به محتویات فیلد `externalName` (مثلاً `foo.bar.example.com`) نگاشت می‌کند. هیچ نوع پروکسی تنظیم نشده است. این نوع به نسخه ۱.۷ یا بالاتر `kube-dns` یا CoreDNS نسخه ۰.۰.۸ یا بالاتر نیاز دارد.

اطلاعات بیشتر در مورد انواع مختلف سرویس‌ها را می‌توانید در آموزش [Using Source IP](/docs/tutorials/services/source-ip/)  بیابید. همچنین به [Connecting Applications with Services](/docs/tutorials/services/connect-applications-service/). مراجعه کنید.



علاوه بر این، توجه داشته باشید که برخی موارد استفاده از سرویس‌ها شامل عدم تعریف یک `selector` در مشخصات است. سرویسی که بدون `selector`ایجاد شود، شیء Endpoints مربوطه را نیز ایجاد نخواهد کرد. این به کاربران اجازه می‌دهد تا به صورت دستی یک سرویس را به نقاط انتهایی خاص نگاشت کنند. احتمال دیگر اینکه چرا ممکن است هیچ انتخابگری وجود نداشته باشد این است که شما صرفاً از `type: ExternalName` استفاده می‌کنید.


## Services و Labels

یک سرویس، ترافیک را در مجموعه‌ای از Podها مسیریابی می‌کند. سرویس‌ها انتزاعی هستند که به Podها اجازه می‌دهند بدون تأثیر بر برنامه شما، در Kubernetes از بین بروند و تکثیر شوند. کشف و مسیریابی بین Podهای وابسته (مانند اجزای frontend و backend در یک برنامه) توسط Kubernetes Services انجام می‌شود.



سرویس‌ها با استفاده از [labels and selectors](/docs/concepts/overview/working-with-objects/labels)، یک گروه‌بندی اولیه که امکان عملیات منطقی روی اشیاء در Kubernetes را فراهم می‌کند، مجموعه‌ای از Podها را تطبیق می‌دهند. برچسب‌ها جفت‌های کلید/مقدار متصل به اشیاء هستند و می‌توانند به روش‌های مختلفی مورد استفاده قرار گیرند:

* تعیین اشیاء برای توسعه، آزمایش و تولید
* جاسازی برچسب‌های نسخه
* طبقه‌بندی یک شیء با استفاده از برچسب‌ها




{{< figure src="/docs/tutorials/kubernetes-basics/public/images/module_04_labels.svg" class="diagram-medium" >}}


برچسب‌ها را می‌توان در زمان ایجاد یا بعداً به اشیاء متصل کرد. آن‌ها را می‌توان در هر زمانی تغییر داد. بیایید اکنون برنامه خود را با استفاده از یک سرویس نمایش دهیم و چند برچسب اعمال کنیم.



### Step 1: ایجاد یک سرویس جدید

بیایید تأیید کنیم که برنامه ما در حال اجرا است. ما از دستور `kubectl get` استفاده خواهیم کرد و به دنبال Pod های موجود خواهیم گشت:

```shell
kubectl get pods
```

اگر هیچ پادی در حال اجرا نباشد، به این معنی است که اشیاء از آموزش‌های قبلی پاک‌سازی شده‌اند. در این صورت، به عقب برگردید و استقرار را از آموزش [Using kubectl to create a Deployment](/docs/tutorials/kubernetes-basics/deploy-app/deploy-intro#deploy-an-app) دوباره ایجاد کنید. لطفاً چند ثانیه صبر کنید و دوباره پادها را فهرست کنید. وقتی پاد در حال اجرا را مشاهده کردید، می‌توانید ادامه دهید.





در مرحله بعد، بیایید سرویس‌های فعلی را از کلاستر خود لیست کنیم:

```shell
kubectl get services
```

برای نمایش استقرار به ترافیک خارجی، از دستور kubectl expose با گزینه --type=NodePort استفاده خواهیم کرد:

```shell
kubectl expose deployment/kubernetes-bootcamp --type="NodePort" --port 8080
```

اکنون یک سرویس در حال اجرا به نام kubernetes-bootcamp داریم. در اینجا می‌بینیم که این سرویس یک cluster-IP منحصر به فرد، یک پورت داخلی و یک external-IP (IP گره) دریافت کرده است.

برای فهمیدن اینکه چه پورتی به صورت خارجی باز شده است (برای سرویس `type: NodePort`)، زیردستور `describe service` را اجرا خواهیم کرد:


```shell
kubectl describe services/kubernetes-bootcamp
```

یک متغیر محیطی به نام `NODE_PORT` ایجاد کنید که مقدار پورت گره را داشته باشد:

```shell
export NODE_PORT="$(kubectl get services/kubernetes-bootcamp -o go-template='{{(index .spec.ports 0).nodePort}}')"
echo "NODE_PORT=$NODE_PORT"
```

اکنون می‌توانیم با استفاده از `curl`، آدرس IP گره و پورت خارجی، بررسی کنیم که آیا برنامه در خارج از کلاستر در دسترس است یا خیر:

```shell
curl http://"$(minikube ip):$NODE_PORT"
```
{{< note >}}
اگر minikube را با Docker Desktop به عنوان درایور کانتینر اجرا می‌کنید، به یک تونل minikube نیاز دارید. دلیل این امر این است که کانتینرهای داخل Docker Desktop از رایانه میزبان شما جدا هستند.


در یک پنجره ترمینال جداگانه، دستور زیر را اجرا کنید:

```shell
minikube service kubernetes-bootcamp --url
```

خروجی به این شکل است:

```
http://127.0.0.1:51082
!  از آنجا که شما از درایور داکر روی darwin استفاده می‌کنید، برای اجرای آن باید ترمینال باز باشد.
```

سپس از آدرس اینترنتی داده شده برای دسترسی به برنامه استفاده کنید:

```shell
curl 127.0.0.1:51082
```
{{< /note >}}

و ما از سرور پاسخی دریافت می‌کنیم. سرویس در معرض دید قرار می‌گیرد.

### Step 2: با استفاده از labels

Deployment به طور خودکار یک برچسب برای Pod ما ایجاد کرد. با زیردستور `describe deployment` می‌توانید نام (_key_) آن برچسب را ببینید:


```shell
kubectl describe deployment
```

بیایید از این برچسب برای جستجوی لیست پادها استفاده کنیم. ما از دستور `kubectl get pods` به همراه پارامتر `-l` و به دنبال آن مقادیر برچسب استفاده خواهیم کرد:

```shell
kubectl get pods -l app=kubernetes-bootcamp
```
شما می‌توانید همین کار را برای فهرست کردن سرویس‌های موجود انجام دهید:

```shell
kubectl get services -l app=kubernetes-bootcamp
```

نام پاد را دریافت کرده و آن را در متغیر محیطی POD_NAME ذخیره کنید:


```shell
export POD_NAME="$(kubectl get pods -o go-template --template '{{range .items}}{{.metadata.name}}{{"\n"}}{{end}}')"
echo "Name of the Pod: $POD_NAME"
```

برای اعمال یک برچسب جدید، از زیردستور label و به دنبال آن نوع شیء، نام شیء و برچسب جدید استفاده می‌کنیم:

```shell
kubectl label pods "$POD_NAME" version=v1
```

این یک برچسب جدید به پاد ما اعمال می‌کند (ما نسخه برنامه را به پاد پین کرده‌ایم) و می‌توانیم آن را با دستور `describe pod` بررسی کنیم:

```shell
kubectl describe pods "$POD_NAME"
```

اینجا می‌بینیم که برچسب اکنون به پاد ما متصل شده است. و اکنون می‌توانیم با استفاده از برچسب جدید، لیست پادها را جستجو کنیم:

```shell
kubectl get pods -l version=v1
```
و ما پاد را می‌بینیم.


### Step 3: حذف service

برای حذف سرویس‌ها می‌توانید از زیردستور «حذف سرویس» استفاده کنید. برچسب‌ها را نیز می‌توان در اینجا استفاده کرد:


```shell
kubectl delete service -l app=kubernetes-bootcamp
```

تأیید کنید که سرویس از بین رفته است:

```shell
kubectl get services
```

این تأیید می‌کند که سرویس ما حذف شده است. برای تأیید اینکه مسیر دیگر در معرض دید نیست، می‌توانید IP و پورت قبلاً در معرض دید را «curl» کنید:

```shell
curl http://"$(minikube ip):$NODE_PORT"
```

این ثابت می‌کند که برنامه دیگر از خارج از کلاستر قابل دسترسی نیست. می‌توانید با استفاده از دستور `curl` از داخل pod تأیید کنید که برنامه هنوز در حال اجرا است:

```shell
kubectl exec -ti $POD_NAME -- curl http://localhost:8080
```

در اینجا می‌بینیم که برنامه اجرا شده است. دلیل این امر مدیریت برنامه توسط Deployment است. برای خاموش کردن برنامه، باید Deployment را نیز حذف کنید.


## {{% heading "whatsnext" %}}

* آموزش
[Running Multiple Instances of Your App](/docs/tutorials/kubernetes-basics/scale/scale-intro/).
* Learn more about [Service](/docs/concepts/services-networking/service/).
