---
reviewers:
- چرخه حیات cluster sig

title: ایجاد یک کلاستر با kubeadm
content_type: وظیفه
weight: 30
---

<!-- overview -->

<img src="/images/kubeadm-stacked-color.png" align="right" width="150px"></img>
با استفاده از `kubeadm`، می‌توانید یک کلاستر Kubernetes با حداقل قابلیت اجرا ایجاد کنید که با بهترین شیوه‌ها مطابقت داشته باشد.

در واقع، می‌توانید از `kubeadm` برای راه‌اندازی کلاستری استفاده کنید که آزمون‌های انطباق [Kubernetes Conformance tests](/blog/2017/10/software-conformance-certification/). را با موفقیت پشت سر بگذارد.

`kubeadm` همچنین از سایر توابع چرخه عمر کلاستر، مانند `[bootstrap tokens](/docs/reference/access-authn-authz/bootstrap-tokens/) و ارتقاء کلاستر پشتیبانی می‌کند.


ابزار `kubeadm` در صورت نیاز به موارد زیر مفید است:

- روشی ساده برای شما تا احتمالاً برای اولین بار Kubernetes را امتحان کنید.
- روشی برای کاربران فعلی تا راه‌اندازی یک کلاستر را خودکار کرده و برنامه خود را آزمایش کنند.
- یک بلوک سازنده در سایر اکوسیستم‌ها و/یا ابزارهای نصب با دامنه وسیع‌تر.

شما می‌توانید `kubeadm` را روی دستگاه‌های مختلفی نصب و استفاده کنید: لپ‌تاپ، مجموعه‌ای از سرورهای ابری، رزبری پای و موارد دیگر. چه در حال استقرار در فضای ابری باشید و چه در محل، می‌توانید `kubeadm` را در سیستم‌های آماده‌سازی مانند Ansible یا Terraform ادغام کنید.

## {{% heading "prerequisites" %}}

برای دنبال کردن این راهنما، شما نیاز دارید به:

- One or more machines running a deb/rpm-compatible Linux OS; - یک یا چند دستگاه که سیستم عامل لینوکس سازگار با deb/rpm را اجرا می‌کنند؛ به عنوان مثال: اوبونتو یا CentOS.


۲ گیگابایت یا بیشتر رم برای هر دستگاه - کمتر از این مقدار، فضای کمی برای برنامه‌های شما باقی می‌گذارد.


حداقل ۲ پردازنده روی دستگاهی که به عنوان گره صفحه کنترل استفاده می‌کنید.


اتصال کامل شبکه بین تمام دستگاه‌های موجود در خوشه. می‌توانید از یک شبکه عمومی یا خصوصی استفاده کنید.

همچنین باید از نسخه‌ای از `kubeadm` استفاده کنید که بتواند نسخه Kubernetes مورد نظر شما را در کلاستر جدیدتان مستقر کند.

[Kubernetes' version and version skew support policy](/docs/setup/release/version-skew-policy/#supported-versions)
هم برای `kubeadm` و هم برای کل Kubernetes اعمال می‌شود.

برای اطلاع از نسخه‌های Kubernetes و `kubeadm` که پشتیبانی می‌شوند، این سیاست را بررسی کنید. این صفحه برای Kubernetes نوشته شده است {{< param "version" >}}.


وضعیت کلی ویژگی ابزار `kubeadm` در حالت دسترسی عمومی (GA) است. برخی از زیرویژگی‌ها هنوز در دست توسعه فعال هستند. پیاده‌سازی ایجاد خوشه ممکن است با تکامل ابزار کمی تغییر کند، اما پیاده‌سازی کلی باید کاملاً پایدار باشد.

{{< note >}}
هر دستوری که تحت `kubeadm alpha` باشد، طبق تعریف، در سطح آلفا پشتیبانی می‌شود.
{{< /note >}}

<!-- steps -->

## Objectives

* نصب یک کلاستر Kubernetes با صفحه کنترل واحد
* نصب یک شبکه Pod روی کلاستر به طوری که Pod های شما بتوانند با یکدیگر ارتباط برقرار کنند

## دستورالعمل ها

### آماده سازی میزبانان

#### نصب کامپوننت

یک {{< glossary_tooltip term_id="container-runtime" text="container runtime" >}}
و kubeadm را روی همه میزبان‌ها نصب کنید. برای دستورالعمل‌های دقیق و سایر پیش‌نیازها، به [Installing kubeadm](/docs/setup/production-environment/tools/kubeadm/install-kubeadm/). مراجعه کنید.


{{< note >}}
اگر قبلاً kubeadm را نصب کرده‌اید، برای دستورالعمل‌های مربوط به نحوه‌ی ارتقاء kubeadm، به دو مرحله‌ی اول سند [Upgrading Linux nodes](/docs/tasks/administer-cluster/kubeadm/upgrading-linux-nodes) مراجعه کنید.



وقتی شما ارتقا می‌دهید، kubelet هر چند ثانیه یک بار مجدداً راه‌اندازی می‌شود و در یک حلقه‌ی خرابی منتظر می‌ماند تا kubeadm به آن بگوید چه کاری انجام دهد. این حلقه‌ی خرابی مورد انتظار و طبیعی است.
پس از اینکه صفحه کنترل خود را مقداردهی اولیه کردید، kubelet به طور عادی اجرا می‌شود.
{{< /note >}}

#### Network setup

kubeadm مشابه سایر اجزای Kubernetes سعی می‌کند یک IP قابل استفاده در رابط‌های شبکه مرتبط با یک دروازه پیش‌فرض روی یک میزبان پیدا کند. سپس چنین IP برای تبلیغات و/یا شنود انجام شده توسط یک جزء استفاده می‌شود.

برای فهمیدن اینکه این IP در هاست لینوکس چیست، می‌توانید از دستور زیر استفاده کنید:

```shell
ip route show # Look for a line starting with "default via"
```

{{< note >}}
اگر دو یا چند default gateways روی میزبان وجود داشته باشد، یک جزء Kubernetes سعی می‌کند از اولین default gateways که با آن مواجه می‌شود و دارای یک آدرس IP جهانی تک‌پخشی مناسب است، استفاده کند. هنگام انجام این انتخاب، ترتیب دقیق default gateways ممکن است بین سیستم‌عامل‌ها و نسخه‌های هسته مختلف متفاوت باشد.
{{< /note >}}

اجزای Kubernetes رابط شبکه سفارشی را به عنوان یک گزینه نمی‌پذیرند، بنابراین یک آدرس IP سفارشی باید به عنوان یک پرچم به تمام نمونه‌های اجزایی که به چنین پیکربندی سفارشی نیاز دارند، ارسال شود.

{{< note >}}
اگر میزبان دروازه پیش‌فرض نداشته باشد و اگر یک آدرس IP سفارشی به یک جزء Kubernetes ارسال نشود، ممکن است آن جزء با خطا خارج شود.
{{< /note >}}

برای پیکربندی آدرس تبلیغ سرور API برای گره‌های صفحه کنترل که با هر دو `init` و `join` ایجاد شده‌اند، می‌توان از پرچم `--apiserver-advertise-address` استفاده کرد.

ترجیحاً، این گزینه می‌تواند در [kubeadm API](/docs/reference/config-api/kubeadm-config.v1beta4) به صورت `InitConfiguration.localAPIEndpoint` و `JoinConfiguration.controlPlane.localAPIEndpoint` تنظیم شود.

برای kubeletها روی همه گره‌ها، گزینه `--node-ip` را می‌توان در `.nodeRegistration.kubeletExtraArgs` درون یک فایل پیکربندی kubeadm (`InitConfiguration` یا `JoinConfiguration`) ارسال کرد.



برای دو پشته‌سازی به [Dual-stack support with kubeadm](/docs/setup/production-environment/tools/kubeadm/dual-stack-support).مراجعه کنید.

آدرس‌های IP که به اجزای صفحه کنترل اختصاص می‌دهید، بخشی از فیلدهای نام جایگزین موضوع گواهی‌های X.509 آنها می‌شوند. تغییر این آدرس‌های IP نیاز به امضای گواهی‌های جدید و راه‌اندازی مجدد اجزای آسیب‌دیده دارد، به طوری که تغییر در فایل‌های گواهی منعکس شود. برای جزئیات بیشتر در مورد این موضوع به [Manual certificate renewal](/docs/tasks/administer-cluster/kubeadm/kubeadm-certs/#manual-certificate-renewal) مراجعه کنید.


{{< warning >}}
پروژه Kubernetes این رویکرد (پیکربندی تمام نمونه‌های کامپوننت با آدرس‌های IP سفارشی) را توصیه نمی‌کند. در عوض، نگهدارندگان Kubernetes توصیه می‌کنند شبکه میزبان را طوری تنظیم کنید که IP ,default gateway  IP باشد که اجزای Kubernetes به طور خودکار آن را شناسایی و استفاده می‌کنند.
در گره‌های لینوکس، می‌توانید از دستوراتی مانند `ip route` برای پیکربندی شبکه استفاده کنید. سیستم عامل شما ممکن است ابزارهای مدیریت شبکه سطح بالاتری را نیز ارائه دهد. اگر دروازه پیش‌فرض گره شما یک آدرس IP عمومی است، باید فیلتر کردن بسته‌ها یا سایر اقدامات امنیتی را که از گره‌ها و خوشه شما محافظت می‌کند، پیکربندی کنید.
{{< /warning >}}

### آماده‌سازیcontainer images مورد نیاز

این مرحله اختیاری است و فقط در صورتی اعمال می‌شود که شما نخواهید `kubeadm init` و `kubeadm join` تصاویر کانتینر پیش‌فرض را که در `registry.k8s.io` میزبانی می‌شوند، دانلود کنند.


Kubeadm دستوراتی دارد که می‌تواند به شما در پیش‌دریافت تصاویر مورد نیاز هنگام ایجاد یک کلاستر بدون اتصال اینترنت روی گره‌های آن کمک کند.
برای جزئیات بیشتر به [Running kubeadm without an internet connection](/docs/reference/setup-tools/kubeadm/kubeadm-init#without-internet-connection) مراجعه کنید.


Kubeadm به شما امکان می‌دهد از یک مخزن image سفارشی برای تصاویر مورد نیاز استفاده کنید.
برای جزئیات بیشتر به [Using custom images](/docs/reference/setup-tools/kubeadm/kubeadm-init#custom-images)مراجعه کنید.

.

### مقداردهی اولیه control-plane node

control-plane node, ماشینی است که اجزای صفحه کنترل، از جمله {{< glossary_tooltip term_id="etcd" >}} (پایگاه داده خوشه‌ای) و {{< glossary_tooltip text="API Server" term_id="kube-apiserver" >}} (که ابزار خط فرمان {{< glossary_tooltip text="kubectl" term_id="kubectl" >}} با آن ارتباط برقرار می‌کند) در آن اجرا می‌شوند.

دارید این کلاستر واحد `kubeadm` در صفحه کنترل را به [high availability](/docs/setup/production-environment/tools/kubeadm/high-availability/) ارتقا دهید، باید `--control-plane-endpoint` را برای تنظیم endpoint مشترک برای همهcontrol-plane مشخص کنید. چنین نقطه پایانی می‌تواند یک نام DNS یا یک آدرس IP از یک load-balancer باشد.


1. .دارید این کلاستر واحد `kubeadm` در صفحه کنترل را به [high availability](/docs/setup/production-environment/tools/kubeadm/high-availability/) ارتقا دهید، باید `--control-plane-endpoint` را برای تنظیم endpoint مشترک برای همهcontrol-plane مشخص کنید. چنین نقطه پایانی می‌تواند یک نام DNS یا یک آدرس IP از یک load-balancer باشد.

یک افزونه شبکه Pod انتخاب کنید و بررسی کنید که آیا نیاز به ارسال آرگومان به `kubeadm init` دارد یا خیر. بسته به اینکه کدام ارائه‌دهنده شخص ثالث را انتخاب می‌کنید، ممکن است لازم باشد `--pod-network-cidr` را روی یک مقدار خاص ارائه‌دهنده تنظیم کنید. به [Installing a Pod network add-on](#pod-network) مراجعه کنید.
1. Cیک افزونه شبکه Pod انتخاب کنید و بررسی کنید که آیا نیاز به ارسال آرگومان به `kubeadm init` دارد یا خیر. بسته به اینکه کدام ارائه‌دهنده شخص ثالث را انتخاب می‌کنید، ممکن است لازم باشد `--pod-network-cidr` را روی یک مقدار خاص ارائه‌دهنده تنظیم کنید. به [Installing a Pod network add-on](#pod-network) مراجعه کنید.

۱. (اختیاری) `kubeadm` سعی می‌کند با استفاده از فهرستی از نقاط پایانی شناخته‌شده، زمان اجرای کانتینر را شناسایی کند. برای استفاده از زمان اجرای کانتینرهای مختلف یا اگر بیش از یک زمان اجرای کانتینر روی گره تأمین‌شده نصب شده است، آرگومان `--cri-socket` را برای `kubeadm` مشخص کنید. به [Installing a runtime](/docs/setup/production-environment/tools/kubeadm/install-kubeadm/#installing-runtime) مراجعه کنید.

برای مقداردهی اولیه گره صفحه کنترل، دستور زیر را اجرا کنید:

```bash
kubeadm init <args>
```

### ملاحظاتی در مورد apiserver-advertise-address و ControlPlaneEndpoint

در حالی که می‌توان از `--apiserver-advertise-address` برای تنظیم آدرس تبلیغ‌شده برای سرور API این گره صفحه کنترل خاص استفاده کرد، `--control-plane-endpoint` می‌تواند برای تنظیم نقطه پایانی مشترک برای همهcontrol-plane nodes  استفاده شود.


`--control-plane-endpoint` به آدرس‌های IP و نام‌های DNS اجازه می‌دهد تا به آدرس‌های IP نگاشت شوند. لطفاً برای ارزیابی راه‌حل‌های ممکن در رابطه با چنین نگاشتی، با مدیر شبکه خود تماس بگیرید.


در اینجا یک نمونه نقشه برداری آورده شده است:


```
192.168.0.102 cluster-endpoint
```

که در آن `192.168.0.102` آدرس IP این گره و `cluster-endpoint` یک نام DNS سفارشی است که به این IP نگاشت می‌شود.
این به شما امکان می‌دهد `--control-plane-endpoint=cluster-endpoint` را به `kubeadm init` ارسال کنید و همان نام DNS را به `kubeadm join` ارسال کنید. بعداً می‌توانید `cluster-endpoint` را تغییر دهید تا در سناریوی دسترسی بالا به آدرس متعادل‌کننده بار شما اشاره کند.

تبدیل یک کلاستر صفحه کنترل که بدون `--control-plane-endpoint` ایجاد شده است به یک کلاستر با دسترسی بالا توسط kubeadm پشتیبانی نمی‌شود.


### اطلاعات بیشتر

برای اطلاعات بیشتر در مورد آرگومان‌های `kubeadm init`، به [Using kubeadm init with a configuration file](/docs/reference/setup-tools/kubeadm/kubeadm-init/#config-file).مراجعه کنید.


برای سفارشی‌سازی اجزای صفحه کنترل، از جمله تخصیص اختیاری IPv6 به کاوشگر زنده بودن برای اجزای صفحه کنترل و سرور etcd، آرگومان‌های اضافی را برای هر جزء ارائه دهید، همانطور که در [custom arguments](/docs/setup/production-environment/tools/kubeadm/control-plane-flags/) مستند شده است.


برای پیکربندی مجدد کلاستری که قبلاً ایجاد شده است، به [Reconfiguring a kubeadm cluster](/docs/tasks/administer-cluster/kubeadm/kubeadm-reconfigure). مراجعه کنید.


برای اجرای مجدد `kubeadm init`، ابتدا باید [tear down the cluster](#tear-down).


اگر به node با معماری متفاوت با کلاستر خود متصل می‌شوید، مطمئن شوید که DaemonSetهای مستقر شده شما از image کانتینر برای این معماری پشتیبانی می‌کنند.


`kubeadm init` ابتدا یک سری پیش‌بررسی انجام می‌دهد تا مطمئن شود که دستگاه برای اجرای Kubernetes آماده است. این پیش‌بررسی‌ها هشدارها را نمایش می‌دهند و در صورت بروز خطا از سیستم خارج می‌شوند. `kubeadm init` سپس اجزای صفحه کنترل کلاستر را دانلود و نصب می‌کند. این کار ممکن است چند دقیقه طول بکشد.

بعد از اتمام باید ببینید:


```none

control-plane Kubernetes شما با موفقیت راه‌اندازی شد!

برای شروع استفاده از کلاستر خود، باید دستور زیر را به عنوان یک کاربر معمولی اجرا کنید:


  mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config


اکنون باید یک شبکه پاد (Pod network) را در کلاستر مستقر کنید. دستور "kubectl apply -f [podnetwork].yaml" را با یکی از گزینه‌های ذکر شده در آدرس زیر اجرا کنید:
  /docs/concepts/cluster-administration/addons/


اکنون باید یک شبکه پاد (Pod network) را در کلاستر مستقر کنید. دستور "kubectl apply -f [podnetwork].yaml" را با یکی از گزینه‌های ذکر شده در آدرس زیر اجرا کنید:
  /docs/concepts/cluster-administration/addons/


اکنون می‌توانید با اجرای دستور زیر روی هر گره به عنوان کاربر root هر تعداد ماشین را به هم متصل کنید:


  kubeadm join <control-plane-host>:<control-plane-port> --token <token> --discovery-token-ca-cert-hash sha256:<hash>
```

برای اینکه kubectl برای کاربر غیر ریشه شما کار کند، این دستورات را اجرا کنید که بخشی از خروجی `kubeadm init` نیز هستند:


```bash
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

Alternatively, if you are the `root` user, you can run:

```bash
export KUBECONFIG=/etc/kubernetes/admin.conf
```

{{< warning >}}
The kubeconfig file `admin.conf` that `kubeadm init` generates contains a certificate with
`Subject: O = kubeadm:cluster-admins, CN = kubernetes-admin`. The group `kubeadm:cluster-admins`
is bound to the built-in `cluster-admin` ClusterRole.
Do not share the `admin.conf` file with anyone.

`kubeadm init` generates another kubeconfig file `super-admin.conf` that contains a certificate with
`Subject: O = system:masters, CN = kubernetes-super-admin`.
`system:masters` is a break-glass, super user group that bypasses the authorization layer (for example RBAC).
Do not share the `super-admin.conf` file with anyone. It is recommended to move the file to a safe location.

See
[Generating kubeconfig files for additional users](/docs/tasks/administer-cluster/kubeadm/kubeadm-certs#kubeconfig-additional-users)
on how to use `kubeadm kubeconfig user` to generate kubeconfig files for additional users.
{{< /warning >}}

Make a record of the `kubeadm join` command that `kubeadm init` outputs. You
need this command to [join nodes to your cluster](#join-nodes).

The token is used for mutual authentication between the control-plane node and the joining
nodes. The token included here is secret. Keep it safe, because anyone with this
token can add authenticated nodes to your cluster. These tokens can be listed,
created, and deleted with the `kubeadm token` command. See the
[kubeadm reference guide](/docs/reference/setup-tools/kubeadm/kubeadm-token/).

### Installing a Pod network add-on {#pod-network}

{{< caution >}}
This section contains important information about networking setup and
deployment order.
Read all of this advice carefully before proceeding.

**You must deploy a
{{< glossary_tooltip text="Container Network Interface" term_id="cni" >}}
(CNI) based Pod network add-on so that your Pods can communicate with each other.
Cluster DNS (CoreDNS) will not start up before a network is installed.**

- Take care that your Pod network must not overlap with any of the host
  networks: you are likely to see problems if there is any overlap.
  (If you find a collision between your network plugin's preferred Pod
  network and some of your host networks, you should think of a suitable
  CIDR block to use instead, then use that during `kubeadm init` with
  `--pod-network-cidr` and as a replacement in your network plugin's YAML).

- By default, `kubeadm` sets up your cluster to use and enforce use of
  [RBAC](/docs/reference/access-authn-authz/rbac/) (role based access
  control).
  Make sure that your Pod network plugin supports RBAC, and so do any manifests
  that you use to deploy it.

- If you want to use IPv6--either dual-stack, or single-stack IPv6 only
  networking--for your cluster, make sure that your Pod network plugin
  supports IPv6.
  IPv6 support was added to CNI in [v0.6.0](https://github.com/containernetworking/cni/releases/tag/v0.6.0).

{{< /caution >}}

{{< note >}}
Kubeadm should be CNI agnostic and the validation of CNI providers is out of the scope of our current e2e testing.
If you find an issue related to a CNI plugin you should log a ticket in its respective issue
tracker instead of the kubeadm or kubernetes issue trackers.
{{< /note >}}

Several external projects provide Kubernetes Pod networks using CNI, some of which also
support [Network Policy](/docs/concepts/services-networking/network-policies/).

See a list of add-ons that implement the
[Kubernetes networking model](/docs/concepts/cluster-administration/networking/#how-to-implement-the-kubernetes-network-model).

Please refer to the [Installing Addons](/docs/concepts/cluster-administration/addons/#networking-and-network-policy)
page for a non-exhaustive list of networking addons supported by Kubernetes.
You can install a Pod network add-on with the following command on the
control-plane node or a node that has the kubeconfig credentials:

```bash
kubectl apply -f <add-on.yaml>
```

{{< note >}}
Only a few CNI plugins support Windows. More details and setup instructions can be found
in [Adding Windows worker nodes](/docs/tasks/administer-cluster/kubeadm/adding-windows-nodes/#network-config).
{{< /note >}}

You can install only one Pod network per cluster.

Once a Pod network has been installed, you can confirm that it is working by
checking that the CoreDNS Pod is `Running` in the output of `kubectl get pods --all-namespaces`.
And once the CoreDNS Pod is up and running, you can continue by joining your nodes.

If your network is not working or CoreDNS is not in the `Running` state, check out the
[troubleshooting guide](/docs/setup/production-environment/tools/kubeadm/troubleshooting-kubeadm/)
for `kubeadm`.

### Managed node labels

By default, kubeadm enables the [NodeRestriction](/docs/reference/access-authn-authz/admission-controllers/#noderestriction)
admission controller that restricts what labels can be self-applied by kubelets on node registration.
The admission controller documentation covers what labels are permitted to be used with the kubelet `--node-labels` option.
The `node-role.kubernetes.io/control-plane` label is such a restricted label and kubeadm manually applies it using
a privileged client after a node has been created. To do that manually you can do the same by using `kubectl label`
and ensure it is using a privileged kubeconfig such as the kubeadm managed `/etc/kubernetes/admin.conf`.

### Control plane node isolation

By default, your cluster will not schedule Pods on the control plane nodes for security
reasons. If you want to be able to schedule Pods on the control plane nodes,
for example for a single machine Kubernetes cluster, run:

```bash
kubectl taint nodes --all node-role.kubernetes.io/control-plane-
```

The output will look something like:

```
node "test-01" untainted
...
```

This will remove the `node-role.kubernetes.io/control-plane:NoSchedule` taint
from any nodes that have it, including the control plane nodes, meaning that the
scheduler will then be able to schedule Pods everywhere.

Additionally, you can execute the following command to remove the
[`node.kubernetes.io/exclude-from-external-load-balancers`](/docs/reference/labels-annotations-taints/#node-kubernetes-io-exclude-from-external-load-balancers) label
from the control plane node, which excludes it from the list of backend servers:

```bash
kubectl label nodes --all node.kubernetes.io/exclude-from-external-load-balancers-
```

### Adding more control plane nodes

See [Creating Highly Available Clusters with kubeadm](/docs/setup/production-environment/tools/kubeadm/high-availability/)
for steps on creating a high availability kubeadm cluster by adding more control plane nodes.

### Adding worker nodes {#join-nodes}

The worker nodes are where your workloads run.

The following pages show how to add Linux and Windows worker nodes to the cluster by using
the `kubeadm join` command:

* [Adding Linux worker nodes](/docs/tasks/administer-cluster/kubeadm/adding-linux-nodes/)
* [Adding Windows worker nodes](/docs/tasks/administer-cluster/kubeadm/adding-windows-nodes/)

### (Optional) Controlling your cluster from machines other than the control-plane node

In order to get a kubectl on some other computer (e.g. laptop) to talk to your
cluster, you need to copy the administrator kubeconfig file from your control-plane node
to your workstation like this:

```bash
scp root@<control-plane-host>:/etc/kubernetes/admin.conf .
kubectl --kubeconfig ./admin.conf get nodes
```

{{< note >}}
The example above assumes SSH access is enabled for root. If that is not the
case, you can copy the `admin.conf` file to be accessible by some other user
and `scp` using that other user instead.

The `admin.conf` file gives the user _superuser_ privileges over the cluster.
This file should be used sparingly. For normal users, it's recommended to
generate an unique credential to which you grant privileges. You can do
this with the `kubeadm kubeconfig user --client-name <CN>`
command. That command will print out a KubeConfig file to STDOUT which you
should save to a file and distribute to your user. After that, grant
privileges by using `kubectl create (cluster)rolebinding`.
{{< /note >}}

### (Optional) Proxying API Server to localhost

If you want to connect to the API Server from outside the cluster, you can use
`kubectl proxy`:

```bash
scp root@<control-plane-host>:/etc/kubernetes/admin.conf .
kubectl --kubeconfig ./admin.conf proxy
```

You can now access the API Server locally at `http://localhost:8001/api/v1`

## Clean up {#tear-down}

If you used disposable servers for your cluster, for testing, you can
switch those off and do no further clean up. You can use
`kubectl config delete-cluster` to delete your local references to the
cluster.

However, if you want to deprovision your cluster more cleanly, you should
first [drain the node](/docs/reference/generated/kubectl/kubectl-commands#drain)
and make sure that the node is empty, then deconfigure the node.

### Remove the node

Talking to the control-plane node with the appropriate credentials, run:

```bash
kubectl drain <node name> --delete-emptydir-data --force --ignore-daemonsets
```

Before removing the node, reset the state installed by `kubeadm`:

```bash
kubeadm reset
```

The reset process does not reset or clean up iptables rules or IPVS tables.
If you wish to reset iptables, you must do so manually:

```bash
iptables -F && iptables -t nat -F && iptables -t mangle -F && iptables -X
```

If you want to reset the IPVS tables, you must run the following command:

```bash
ipvsadm -C
```

Now remove the node:

```bash
kubectl delete node <node name>
```

If you wish to start over, run `kubeadm init` or `kubeadm join` with the
appropriate arguments.

### Clean up the control plane

You can use `kubeadm reset` on the control plane host to trigger a best-effort
clean up.

See the [`kubeadm reset`](/docs/reference/setup-tools/kubeadm/kubeadm-reset/)
reference documentation for more information about this subcommand and its
options.

## Version skew policy {#version-skew-policy}

While kubeadm allows version skew against some components that it manages, it is recommended that you
match the kubeadm version with the versions of the control plane components, kube-proxy and kubelet.

### kubeadm's skew against the Kubernetes version

kubeadm can be used with Kubernetes components that are the same version as kubeadm
or one version older. The Kubernetes version can be specified to kubeadm by using the
`--kubernetes-version` flag of `kubeadm init` or the
[`ClusterConfiguration.kubernetesVersion`](/docs/reference/config-api/kubeadm-config.v1beta4/)
field when using `--config`. This option will control the versions
of kube-apiserver, kube-controller-manager, kube-scheduler and kube-proxy.

Example:

* kubeadm is at {{< skew currentVersion >}}
* `kubernetesVersion` must be at {{< skew currentVersion >}} or {{< skew currentVersionAddMinor -1 >}}

### kubeadm's skew against the kubelet

Similarly to the Kubernetes version, kubeadm can be used with a kubelet version that is
the same version as kubeadm or three versions older.

Example:

* kubeadm is at {{< skew currentVersion >}}
* kubelet on the host must be at {{< skew currentVersion >}}, {{< skew currentVersionAddMinor -1 >}},
  {{< skew currentVersionAddMinor -2 >}} or {{< skew currentVersionAddMinor -3 >}}

### kubeadm's skew against kubeadm

There are certain limitations on how kubeadm commands can operate on existing nodes or whole clusters
managed by kubeadm.

If new nodes are joined to the cluster, the kubeadm binary used for `kubeadm join` must match
the last version of kubeadm used to either create the cluster with `kubeadm init` or to upgrade
the same node with `kubeadm upgrade`. Similar rules apply to the rest of the kubeadm commands
with the exception of `kubeadm upgrade`.

Example for `kubeadm join`:

* kubeadm version {{< skew currentVersion >}} was used to create a cluster with `kubeadm init`
* Joining nodes must use a kubeadm binary that is at version {{< skew currentVersion >}}

Nodes that are being upgraded must use a version of kubeadm that is the same MINOR
version or one MINOR version newer than the version of kubeadm used for managing the
node.

Example for `kubeadm upgrade`:

* kubeadm version {{< skew currentVersionAddMinor -1 >}} was used to create or upgrade the node
* The version of kubeadm used for upgrading the node must be at {{< skew currentVersionAddMinor -1 >}}
  or {{< skew currentVersion >}}

To learn more about the version skew between the different Kubernetes component see
the [Version Skew Policy](/releases/version-skew-policy/).

## Limitations {#limitations}

### Cluster resilience {#resilience}

The cluster created here has a single control-plane node, with a single etcd database
running on it. This means that if the control-plane node fails, your cluster may lose
data and may need to be recreated from scratch.

Workarounds:

* Regularly [back up etcd](https://etcd.io/docs/v3.5/op-guide/recovery/). The
  etcd data directory configured by kubeadm is at `/var/lib/etcd` on the control-plane node.

* Use multiple control-plane nodes. You can read
  [Options for Highly Available topology](/docs/setup/production-environment/tools/kubeadm/ha-topology/) to pick a cluster
  topology that provides [high-availability](/docs/setup/production-environment/tools/kubeadm/high-availability/).

### Platform compatibility {#multi-platform}

kubeadm deb/rpm packages and binaries are built for amd64, arm (32-bit), arm64, ppc64le, and s390x
following the [multi-platform proposal](https://git.k8s.io/design-proposals-archive/multi-platform.md).

Multiplatform container images for the control plane and addons are also supported since v1.12.

Only some of the network providers offer solutions for all platforms. Please consult the list of
network providers above or the documentation from each provider to figure out whether the provider
supports your chosen platform.

## Troubleshooting {#troubleshooting}

If you are running into difficulties with kubeadm, please consult our
[troubleshooting docs](/docs/setup/production-environment/tools/kubeadm/troubleshooting-kubeadm/).

<!-- discussion -->

## {{% heading "whatsnext" %}}

* Verify that your cluster is running properly with [Sonobuoy](https://github.com/heptio/sonobuoy)
* <a id="lifecycle" />See [Upgrading kubeadm clusters](/docs/tasks/administer-cluster/kubeadm/kubeadm-upgrade/)
  for details about upgrading your cluster using `kubeadm`.
* Learn about advanced `kubeadm` usage in the [kubeadm reference documentation](/docs/reference/setup-tools/kubeadm/)
* Learn more about Kubernetes [concepts](/docs/concepts/) and [`kubectl`](/docs/reference/kubectl/).
* See the [Cluster Networking](/docs/concepts/cluster-administration/networking/) page for a bigger list
  of Pod network add-ons.
* <a id="other-addons" />See the [list of add-ons](/docs/concepts/cluster-administration/addons/) to
  explore other add-ons, including tools for logging, monitoring, network policy, visualization &amp;
  control of your Kubernetes cluster.
* Configure how your cluster handles logs for cluster events and from
  applications running in Pods.
  See [Logging Architecture](/docs/concepts/cluster-administration/logging/) for
  an overview of what is involved.

### Feedback {#feedback}

* For bugs, visit the [kubeadm GitHub issue tracker](https://github.com/kubernetes/kubeadm/issues)
* For support, visit the
  [#kubeadm](https://kubernetes.slack.com/messages/kubeadm/) Slack channel
* General SIG Cluster Lifecycle development Slack channel:
  [#sig-cluster-lifecycle](https://kubernetes.slack.com/messages/sig-cluster-lifecycle/)
* SIG Cluster Lifecycle [SIG information](https://github.com/kubernetes/community/tree/master/sig-cluster-lifecycle#readme)
* SIG Cluster Lifecycle mailing list:
  [kubernetes-sig-cluster-lifecycle](https://groups.google.com/forum/#!forum/kubernetes-sig-cluster-lifecycle)
