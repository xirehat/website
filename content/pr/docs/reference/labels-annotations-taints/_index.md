---
title: برچسب‌ها، حاشیه‌نویسی‌ها و رنگ‌های شناخته‌شده
content_type: مفهوم
weight: 40
no_list: true
card:
  name: مرجع
  weight: 30
  anchors:
  - anchor: "#برچسب‌ها-حاشیه‌نویسی‌ها-و-رنگ‌های-استفاده‌شده-روی-اشیاء-api"
    title: برچسب‌ها، حاشیه‌نویسی‌ها و رنگ‌آمیزی‌ها
---

<!-- overview -->

کوبرنتیز تمام برچسب‌ها، حاشیه‌نویسی‌ها و رنگ‌ها را در فضاهای نام `kubernetes.io` و `k8s.io` محفوظ می‌دارد.


این سند هم به عنوان مرجعی برای مقادیر و هم به عنوان نقطه هماهنگی برای تعیین مقادیر عمل می‌کند.

<!-- body -->

## برچسب‌ها، حاشیه‌نویسی‌ها و رنگ‌های استفاده‌شده در اشیاء API


### apf.kubernetes.io/autoupdate-spec

نوع: حاشیه‌نویسی


مثال: `apf.kubernetes.io/autoupdate-spec: "true"`

مورد استفاده در: اشیاء [`FlowSchema` و `PriorityLevelConfiguration`](/docs/concepts/cluster-administration/flow-control/#defaults)

اگر این حاشیه‌نویسی در FlowSchema یا PriorityLevelConfiguration روی true تنظیم شده باشد، `spec` آن شیء توسط kube-apiserver مدیریت می‌شود. اگر سرور API یک شیء APF را تشخیص ندهد و شما آن را برای به‌روزرسانی خودکار حاشیه‌نویسی کنید، سرور API کل شیء را حذف می‌کند. در غیر این صورت، سرور API مشخصات شیء را مدیریت نمی‌کند. برای جزئیات بیشتر، [Maintenance of the Mandatory and Suggested Configuration Objects](/docs/concepts/cluster-administration/flow-control/#maintenance-of-the-mandatory-and-suggested-configuration-objects). را مطالعه کنید.


### app.kubernetes.io/component

نوع: برچسب


مثال: `app.kubernetes.io/component: "database"`

مورد استفاده در: همه اشیاء (معمولاً در [workload resources](/docs/reference/kubernetes-api/workload-resources/) استفاده می‌شود).

مولفه درون معماری برنامه.

یکی از [recommended labels](/docs/concepts/overview/working-with-objects/common-labels/#labels).



### app.kubernetes.io/created-by (deprecated)

نوع: برچسب


مثال: `app.kubernetes.io/created-by: "controller-manager"`

مورد استفاده در: همه اشیاء (معمولاً در [workload resources](/docs/reference/kubernetes-api/workload-resources/)).استفاده می‌شود.

کنترل‌کننده/کاربری که این منبع را ایجاد کرده است.



{{< note >}}
از نسخه ۱.۹ به بعد، این برچسب منسوخ شده است.
{{< /note >}}

### app.kubernetes.io/instance

نوع: برچسب

مثال: `app.kubernetes.io/instance: "mysql-abcxyz"`

مورد استفاده در: همه اشیاء (معمولاً در [workload resources](/docs/reference/kubernetes-api/workload-resources/)). استفاده می‌شود

نامی منحصر به فرد که نمونه یک برنامه را مشخص می‌کند.

برای اختصاص یک نام غیر منحصر به فرد، از [app.kubernetes.io/name](#app-kubernetes-io-name) استفاده کنید.

یکی از [recommended labels](/docs/concepts/overview/working-with-objects/common-labels/#labels).


### app.kubernetes.io/managed-by

نوع: برچسب

مثال: `app.kubernetes.io/managed-by: "helm"`

مورد استفاده در: همه اشیاء (معمولاً در [workload resources](/docs/reference/kubernetes-api/workload-resources/)). استفاده می‌شود

ابزاری که برای مدیریت عملکرد یک برنامه استفاده می‌شود.

یکی از [recommended labels](/docs/concepts/overview/working-with-objects/common-labels/#labels).



### app.kubernetes.io/name


نوع: برچسب

مثال: `app.kubernetes.io/name: "mysql"`

مورد استفاده در: همه اشیاء (معمولاً در [workload resources](/docs/reference/kubernetes-api/workload-resources/)). استفاده می‌شود

نام برنامه.

یکی از [recommended labels](/docs/concepts/overview/working-with-objects/common-labels/#labels).

### app.kubernetes.io/part-of


نوع: برچسب

مثال: `app.kubernetes.io/part-of: "wordpress"`

مورد استفاده در: همه اشیاء (معمولاً در [workload resources](/docs/reference/kubernetes-api/workload-resources/)). استفاده می‌شود

نام یک برنامه سطح بالاتر که این شیء بخشی از آن است.

یکی از [recommended labels](/docs/concepts/overview/working-with-objects/common-labels/#labels).

### app.kubernetes.io/version

نوع: برچسب

مثال: `app.kubernetes.io/version: "5.7.21"`

مورد استفاده در: همه اشیاء (معمولاً در [workload resources](/docs/reference/kubernetes-api/workload-resources/)). استفاده می‌شود

نسخه فعلی برنامه.

اشکال رایج مقادیر عبارتند از:

- [semantic version](https://semver.org/spec/v1.0.0.html)
- the Git [revision hash](https://git-scm.com/book/en/v2/Git-Tools-Revision-Selection#_single_revisions)
  for the source code.

برای کد منبع.

یکی از [recommended labels](/docs/concepts/overview/working-with-objects/common-labels/#labels).

نوع: حاشیه‌نویسی



مثال: `applyset.kubernetes.io/additional-namespaces: "namespace1,namespace2"`

مورد استفاده در: اشیاء به عنوان والدین ApplySet.
استفاده از این حاشیه‌نویسی Alpha است.
برای نسخه Kubernetes {{< skew currentVersion >}}، می‌توانید از این حاشیه‌نویسی روی Secrets، ConfigMaps یا منابع سفارشی استفاده کنید، اگر
{{< glossary_tooltip term_id="CustomResourceDefinition" text="CustomResourceDefinition" >}}
تعریف آنها دارای برچسب `applyset.kubernetes.io/is-parent-type` باشد.

بخشی از مشخصات مورد استفاده برای پیاده‌سازی [هرس مبتنی بر ApplySet در kubectl](/docs/tasks/manage-kubernetes-objects/declarative-config/#alternative-kubectl-apply-f-directory-prune).

این حاشیه‌نویسی به شیء والد مورد استفاده برای ردیابی یک ApplySet اعمال می‌شود تا دامنه ApplySet را فراتر از فضای نام خود شیء والد (در صورت وجود) گسترش دهد.

مقدار، فهرستی از نام‌های فضاهای نام غیر از فضای نام والد است که اشیاء در آن یافت می‌شوند و با کاما از هم جدا شده‌اند.

### applyset.kubernetes.io/contains-group-kinds (alpha) {#applyset-kubernetes-io-contains-group-kinds}

نوع: حاشیه‌نویسی

مورد استفاده در: اشیاء مورد استفاده به عنوان والدین ApplySet.

مورد استفاده در: اشیاء به عنوان والدین ApplySet.

مورد استفاده از این حاشیه‌نویسی Alpha است.

برای نسخه Kubernetes {{< skew currentVersion >}}، می‌توانید از این حاشیه‌نویسی روی Secrets، ConfigMaps یا منابع سفارشی استفاده کنید، اگر CustomResourceDefinition که آنها را تعریف می‌کند، دارای برچسب `applyset.kubernetes.io/is-parent-type` باشد.

بخشی از مشخصات مورد استفاده برای پیاده‌سازی [هرس مبتنی بر ApplySet در kubectl](/docs/tasks/manage-kubernetes-objects/declarative-config/#alternative-kubectl-apply-f-directory-prune).

این حاشیه‌نویسی به شیء والد مورد استفاده برای ردیابی یک ApplySet جهت بهینه‌سازی فهرست اشیاء عضو ApplySet اعمال می‌شود. این مورد در مشخصات ApplySet اختیاری است، زیرا ابزارها می‌توانند عملیات کشف را انجام دهند یا از بهینه‌سازی متفاوتی استفاده کنند. با این حال، از نسخه Kubernetes {{< skew currentVersion >}}،

توسط kubectl الزامی است. در صورت وجود، مقدار این حاشیه‌نویسی باید لیستی از انواع گروه باشد که با کاما از هم جدا شده‌اند، در قالب نام کاملاً واجد شرایط، یعنی`<resource>.<group>`.

### applyset.kubernetes.io/contains-group-resources (deprecated) {#applyset-kubernetes-io-contains-group-resources}

نوع: حاشیه‌نویسی


مثال: `applyset.kubernetes.io/contains-group-resources: "certificates.cert-manager.io,configmaps,deployments.apps,secrets,services"`


مورد استفاده در: اشیاء مورد استفاده به عنوان والدین ApplySet.

برای نسخه Kubernetes {{< skew currentVersion >}}، می‌توانید از این حاشیه‌نویسی روی Secrets، ConfigMaps یا منابع سفارشی استفاده کنید، اگر CustomResourceDefinition که آنها را تعریف می‌کند، دارای برچسب `applyset.kubernetes.io/is-parent-type` باشد.

بخشی از مشخصات مورد استفاده برای پیاده‌سازی [هرس مبتنی بر ApplySet در kubectl](/docs/tasks/manage-kubernetes-objects/declarative-config/#alternative-kubectl-apply-f-directory-prune).
این حاشیه‌نویسی به شیء والد مورد استفاده برای ردیابی یک ApplySet جهت بهینه‌سازی فهرست اشیاء عضو ApplySet اعمال می‌شود. این مورد در مشخصات ApplySet اختیاری است، زیرا ابزارها می‌توانند عملیات کشف را انجام دهند یا از بهینه‌سازی متفاوتی استفاده کنند. با این حال، در نسخه Kubernetes {{< skew currentVersion >}}،
توسط kubectl الزامی است. در صورت وجود، مقدار این حاشیه‌نویسی باید لیستی از انواع گروه باشد که با کاما از هم جدا شده‌اند، در قالب نام کاملاً واجد شرایط، یعنی`<resource>.<group>`.
{{< note >}}
این حاشیه‌نویسی در حال حاضر منسوخ شده و با [`applyset.kubernetes.io/contains-group-kinds`](#applyset-kubernetes-io-contains-group-kinds) جایگزین شده است، پشتیبانی از این مورد در نسخه بتا یا عمومی applyset حذف خواهد شد.
{{< /note >}}

### applyset.kubernetes.io/id (alpha) {#applyset-kubernetes-io-id}

نوع: برچسب



مثال: `applyset.kubernetes.io/id: "applyset-0eFHV8ySqp7XoShsGvyWFQD3s96yqwHmzc4e0HR1dsY-v1"`

مورد استفاده در: اشیاء به عنوان والدین ApplySet.

مورد استفاده از این برچسب Alpha است.

برای نسخه Kubernetes {{< skew currentVersion >}}، می‌توانید از این برچسب روی Secrets، ConfigMaps یا منابع سفارشی استفاده کنید، اگر CustomResourceDefinition که آنها را تعریف می‌کند، دارای برچسب `applyset.kubernetes.io/is-parent-type` باشد.


بخشی از مشخصات مورد استفاده برای پیاده‌سازی [ApplySet-based pruning in kubectl](/docs/tasks/manage-kubernetes-objects/declarative-config/#alternative-kubectl-apply-f-directory-prune).
این برچسب چیزی است که یک شیء را به شیء والد ApplySet تبدیل می‌کند.
مقدار آن، شناسه منحصر به فرد ApplySet است که از هویت خود شیء والد مشتق شده است. این شناسه **باید** کدگذاری base64 (با استفاده از کدگذاری امن URL از RFC4648) از هش group-kind-name-namespace شیء که روی آن قرار دارد، به شکل زیر باشد:
`<base64(sha256(<name>.<namespace>.<kind>.<group>))>`.
هیچ ارتباطی بین مقدار این برچسب و UID شیء وجود ندارد.


### applyset.kubernetes.io/is-parent-type (alpha) {#applyset-kubernetes-io-is-parent-type}

نوع: برچسب

مثال: `applyset.kubernetes.io/is-parent-type: "true"`

مورد استفاده در: تعریف منابع سفارشی (CRD)

مورد استفاده از این برچسب Alpha است.

بخشی از مشخصات مورد استفاده برای پیاده‌سازی
[ApplySet-based pruning in kubectl](/docs/tasks/manage-kubernetes-objects/declarative-config/#alternative-kubectl-apply-f-directory-prune).

شما می‌توانید این برچسب را روی یک CustomResourceDefinition (CRD) تنظیم کنید تا نوع منبع سفارشی که تعریف می‌کند (نه خود CRD) به عنوان والد مجاز برای یک ApplySet شناسایی شود.

تنها مقدار مجاز برای این برچسب `"true"` است؛ اگر می‌خواهید یک CRD را به عنوان والد معتبر برای ApplySets علامت‌گذاری کنید، این برچسب را حذف کنید.


### applyset.kubernetes.io/part-of (alpha) {#applyset-kubernetes-io-part-of}

نوع: برچسب

مثال: `applyset.kubernetes.io/part-of: "applyset-0eFHV8ySqp7XoShsGvyWFQD3s96yqwHmzc4e0HR1dsY-v1"`

مورد استفاده در: همه اشیاء.

مورد استفاده از این برچسب Alpha است.

بخشی از مشخصات مورد استفاده برای پیاده‌سازی
[ApplySet-based pruning in kubectl](/docs/tasks/manage-kubernetes-objects/declarative-config/#alternative-kubectl-apply-f-directory-prune).

این برچسب چیزی است که یک شیء را به عضوی از ApplySet تبدیل می‌کند.

مقدار برچسب **باید** با مقدار برچسب `applyset.kubernetes.io/id` روی شیء والد مطابقت داشته باشد.


### applyset.kubernetes.io/tooling (alpha) {#applyset-kubernetes-io-tooling}

نوع: حاشیه‌نویسی

مثال: `applyset.kubernetes.io/tooling: "kubectl/v{{< skew currentVersion >}}"`

مورد استفاده در: اشیاء مورد استفاده به عنوان والدین ApplySet.

مورد استفاده از این حاشیه‌نویسی Alpha است.

برای نسخه Kubernetes {{< skew currentVersion >}}، می‌توانید از این حاشیه‌نویسی روی Secrets، ConfigMaps یا منابع سفارشی استفاده کنید، اگر CustomResourceDefinition که آنها را تعریف می‌کند، دارای برچسب `applyset.kubernetes.io/is-parent-type` باشد.

بخشی از مشخصات مورد استفاده برای پیاده‌سازی 
[ApplySet-based pruning in kubectl](/docs/tasks/manage-kubernetes-objects/declarative-config/#alternative-kubectl-apply-f-directory-prune). این حاشیه‌نویسی به شیء والد مورد استفاده برای ردیابی یک ApplySet اعمال می‌شود تا نشان دهد کدام ابزار، آن ApplySet را مدیریت می‌کند. ابزارسازی باید از تغییر ApplySetهای متعلق به ابزارهای دیگر خودداری کند. مقدار باید در قالب `<toolname>/<semver>` باشد.
### apps.kubernetes.io/pod-index (beta) {#apps-kubernetes.io-pod-index}

نوع: برچسب

مثال: `apps.kubernetes.io/pod-index: "0"`

مورد استفاده در: پاد

وقتی یک کنترلر StatefulSet یک پاد برای StatefulSet ایجاد می‌کند، این برچسب را روی آن پاد تنظیم می‌کند.

مقدار برچسب، اندیس ترتیبی پاد در حال ایجاد است.

برای جزئیات بیشتر به [Pod Index Label](/docs/concepts/workloads/controllers/statefulset/#pod-index-label) در مبحث StatefulSet مراجعه کنید.

به [PodIndexLabel](/docs/reference/command-line-tools-reference/feature-gates/) توجه داشته باشید.

برای اضافه شدن این برچسب به پادها، باید گیت ویژگی فعال باشد.

### resource.kubernetes.io/pod-claim-name

نوع: حاشیه‌نویسی

مثال: `resource.kubernetes.io/pod-claim-name: "my-pod-claim"`

مورد استفاده در: ResourceClaim

این حاشیه‌نویسی به ResourceClaims تولید شده اختصاص داده می‌شود.

مقدار آن با نام ادعای منبع در `.spec` هر Pod(هایی) که ResourceClaim برای آنها ایجاد شده است، مطابقت دارد.

این حاشیه‌نویسی، جزئیات پیاده‌سازی داخلی [dynamic resource allocation](/docs/concepts/scheduling-eviction/dynamic-resource-allocation/). است

شما نیازی به خواندن یا تغییر مقدار این حاشیه‌نویسی ندارید.


### cluster-autoscaler.kubernetes.io/safe-to-evict

نوع: حاشیه‌نویسی

مثال: `cluster-autoscaler.kubernetes.io/safe-to-evict: "true"`

مورد استفاده در: Pod

وقتی این حاشیه‌نویسی روی `"true"` تنظیم شود، مقیاس‌پذیر خودکار کلاستر اجازه دارد یک Pod را حذف کند
حتی اگر سایر قوانین معمولاً از این کار جلوگیری کنند.
مقیاس‌پذیر خودکار کلاستر هرگز Podهایی را که این حاشیه‌نویسی به صراحت روی `"false"` تنظیم شده است، حذف نمی‌کند. می‌توانید آن را روی یک Pod مهم که می‌خواهید به اجرا ادامه دهد، تنظیم کنید.

### config.kubernetes.io/local-config

نوع: حاشیه‌نویسی

مثال: `config.kubernetes.io/local-config: "true"`

مورد استفاده در: همه اشیاء

این حاشیه‌نویسی در مانیفست‌ها برای علامت‌گذاری یک شیء به عنوان پیکربندی محلی که نباید به API Kubernetes ارسال شود، استفاده می‌شود.

مقدار `"true"` برای این حاشیه‌نویسی اعلام می‌کند که شیء فقط توسط ابزارهای سمت کلاینت مصرف می‌شود و نباید به سرور API ارسال شود.

مقدار `"false"` می‌تواند برای اعلام اینکه شیء باید به سرور API ارسال شود، حتی زمانی که در غیر این صورت محلی فرض می‌شود، استفاده شود.

این حاشیه‌نویسی بخشی از مشخصات توابع Kubernetes Resource Model (KRM) است که توسط Kustomize و ابزارهای شخص ثالث مشابه استفاده می‌شود.

به عنوان مثال، Kustomize اشیاء دارای این حاشیه‌نویسی را از خروجی ساخت نهایی خود حذف می‌کند.


### container.apparmor.security.beta.kubernetes.io/* (deprecated) {#container-apparmor-security-beta-kubernetes-io}

نوع: حاشیه‌نویسی

مثال: `container.apparmor.security.beta.kubernetes.io/my-container: my-custom-profile`

مورد استفاده در: Pods

این حاشیه‌نویسی به شما امکان می‌دهد تا پروفایل امنیتی AppArmor را برای یک کانتینر درون یک Pod Kubernetes مشخص کنید. از Kubernetes نسخه ۱.۳۰، این باید با فیلد `appArmorProfile` تنظیم شود.

برای کسب اطلاعات بیشتر، به آموزش [AppArmor](/docs/tutorials/security/apparmor/) مراجعه کنید.

این آموزش استفاده از AppArmor را برای محدود کردن توانایی‌ها و دسترسی‌های یک کانتینر نشان می‌دهد.

پروفایل مشخص شده، مجموعه‌ای از قوانین و محدودیت‌هایی را که فرآیند کانتینر شده باید رعایت کند، تعیین می‌کند. این به اجرای سیاست‌های امنیتی و جداسازی کانتینرهای شما کمک می‌کند.

### internal.config.kubernetes.io/* (reserved prefix) {#internal.config.kubernetes.io-reserved-wildcard}

نوع: حاشیه‌نویسی

مورد استفاده در: همه اشیاء

این پیشوند برای استفاده داخلی توسط ابزارهایی که به عنوان هماهنگ‌کننده مطابق با مشخصات توابع Kubernetes Resource Model (KRM) عمل می‌کنند، رزرو شده است.

حاشیه‌نویسی‌های با این پیشوند برای فرآیند هماهنگ‌سازی داخلی هستند و در مانیفست‌های سیستم فایل ذخیره نمی‌شوند. به عبارت دیگر، ابزار هماهنگ‌کننده باید این حاشیه‌نویسی‌ها را هنگام خواندن فایل‌ها از سیستم فایل محلی تنظیم کند و هنگام نوشتن خروجی توابع به سیستم فایل، آنها را حذف کند.

یک تابع KRM **نباید** حاشیه‌نویسی‌های دارای این پیشوند را تغییر دهد، مگر اینکه برای یک حاشیه‌نویسی مشخص شده، طور دیگری مشخص شده باشد. این امر به ابزارهای هماهنگ‌کننده امکان می‌دهد حاشیه‌نویسی‌های داخلی اضافی را بدون نیاز به تغییر در توابع موجود اضافه کنند.

### internal.config.kubernetes.io/path

نوع: حاشیه‌نویسی

مثال: `internal.config.kubernetes.io/path: "relative/file/path.yaml"`

مورد استفاده در: همه اشیاء

این حاشیه‌نویسی، مسیر نسبی فایل مانیفست که شیء از آن بارگذاری شده است را با جداکننده اسلش، مستقل از سیستم‌عامل و با فاصله مشخص ثبت می‌کند. این مسیر نسبت به یک مکان ثابت در سیستم فایل است که توسط ابزار هماهنگ‌کننده تعیین می‌شود.

این حاشیه‌نویسی بخشی از مشخصات توابع Kubernetes Resource Model (KRM) است که توسط Kustomize و ابزارهای شخص ثالث مشابه استفاده می‌شود.

یک تابع KRM **نباید** این حاشیه‌نویسی را روی اشیاء ورودی تغییر دهد، مگر اینکه فایل‌های ارجاع‌شده را تغییر دهد. یک تابع KRM **ممکن است** این حاشیه‌نویسی را روی اشیاء تولید شده خود نیز شامل کند.
### internal.config.kubernetes.io/index

نوع: حاشیه‌نویسی

مثال: `internal.config.kubernetes.io/index: "2"`

مورد استفاده در: همه اشیاء

این حاشیه‌نویسی، موقعیت صفر-ایندکس‌شده سند YAML حاوی شیء را در فایل مانیفستی که شیء از آن بارگذاری شده است، ثبت می‌کند. توجه داشته باشید که اسناد YAML با سه خط تیره (`---`) از هم جدا می‌شوند و هر کدام می‌توانند شامل یک شیء باشند. وقتی این حاشیه‌نویسی مشخص نشده باشد، مقدار 0 به طور ضمنی در نظر گرفته می‌شود.

این حاشیه‌نویسی بخشی از مشخصات توابع Kubernetes Resource Model (KRM) است که توسط Kustomize و ابزارهای شخص ثالث مشابه استفاده می‌شود.

یک تابع KRM **نباید** این حاشیه‌نویسی را روی اشیاء ورودی تغییر دهد، مگر اینکه فایل‌های ارجاع‌شده را تغییر دهد. یک تابع KRM **ممکن است** این حاشیه‌نویسی را روی اشیاء تولید شده خود نیز شامل کند.

### kube-scheduler-simulator.sigs.k8s.io/bind-result

نوع: حاشیه‌نویسی

مثال: `kube-scheduler-simulator.sigs.k8s.io/bind-result: '{"DefaultBinder":"success"}'`

مورد استفاده در: پاد

این حاشیه‌نویسی نتیجه افزونه‌های زمان‌بندی اتصال را که توسط https://sigs.k8s.io/kube-scheduler-simulator استفاده می‌شود، ثبت می‌کند.

### kube-scheduler-simulator.sigs.k8s.io/filter-result

نوع: حاشیه‌نویسی

مثال:

```yaml
kube-scheduler-simulator.sigs.k8s.io/filter-result: >-
      {"node-282x7":{"AzureDiskLimits":"passed","EBSLimits":"passed","GCEPDLimits":"passed","InterPodAffinity":"passed","NodeAffinity":"passed","NodeName":"passed","NodePorts":"passed","NodeResourcesFit":"passed","NodeUnschedulable":"passed","NodeVolumeLimits":"passed","PodTopologySpread":"passed","TaintToleration":"passed","VolumeBinding":"passed","VolumeRestrictions":"passed","VolumeZone":"passed"},"node-gp9t4":{"AzureDiskLimits":"passed","EBSLimits":"passed","GCEPDLimits":"passed","InterPodAffinity":"passed","NodeAffinity":"passed","NodeName":"passed","NodePorts":"passed","NodeResourcesFit":"passed","NodeUnschedulable":"passed","NodeVolumeLimits":"passed","PodTopologySpread":"passed","TaintToleration":"passed","VolumeBinding":"passed","VolumeRestrictions":"passed","VolumeZone":"passed"}}
```

ورد استفاده در: پاد

این حاشیه‌نویسی نتیجه افزونه‌های زمان‌بندی فیلتر را که توسط https://sigs.k8s.io/kube-scheduler-simulator استفاده می‌شود، ثبت می‌کند.

### kube-scheduler-simulator.sigs.k8s.io/finalscore-result

نوع: حاشیه‌نویسی

مثال:

```yaml
kube-scheduler-simulator.sigs.k8s.io/finalscore-result: >-
      {"node-282x7":{"ImageLocality":"0","InterPodAffinity":"0","NodeAffinity":"0","NodeNumber":"0","NodeResourcesBalancedAllocation":"76","NodeResourcesFit":"73","PodTopologySpread":"200","TaintToleration":"300","VolumeBinding":"0"},"node-gp9t4":{"ImageLocality":"0","InterPodAffinity":"0","NodeAffinity":"0","NodeNumber":"0","NodeResourcesBalancedAllocation":"76","NodeResourcesFit":"73","PodTopologySpread":"200","TaintToleration":"300","VolumeBinding":"0"}}
```

مورد استفاده در: پاد

این حاشیه‌نویسی، نمرات نهایی را که زمان‌بند از نمرات افزونه‌های زمان‌بند نمره محاسبه می‌کند، ثبت می‌کند.

مورد استفاده توسط https://sigs.k8s.io/kube-scheduler-simulator.
### kube-scheduler-simulator.sigs.k8s.io/permit-result

نوع: حاشیه‌نویسی

مثال: `kube-scheduler-simulator.sigs.k8s.io/permit-result: '{"CustomPermitPlugin":"success"}'`

مورد استفاده در: پاد

این حاشیه‌نویسی نتیجه افزونه‌های زمان‌بندی مجوز را که توسط https://sigs.k8s.io/kube-scheduler-simulator استفاده می‌شود، ثبت می‌کند

### kube-scheduler-simulator.sigs.k8s.io/permit-result-timeout

نوع: حاشیه‌نویسی

مثال: `kube-scheduler-simulator.sigs.k8s.io/permit-result-timeout: '{"CustomPermitPlugin":"10s"}'`

مورد استفاده در: پاد

این حاشیه‌نویسی، زمان‌های انقضای بازگشتی از افزونه‌های زمان‌بندی مجوز را ثبت می‌کند که توسط https://sigs.k8s.io/kube-scheduler-simulator استفاده می‌شود.

### kube-scheduler-simulator.sigs.k8s.io/postfilter-result

Type: Annotation

نوع: حاشیه‌نویسی

مثال: `kube-scheduler-simulator.sigs.k8s.io/postfilter-result: '{"DefaultPreemption":"success"}'`

مورد استفاده در: پاد

این حاشیه‌نویسی نتیجه افزونه‌های زمان‌بندی postfilter را که توسط https://sigs.k8s.io/kube-scheduler-simulator استفاده می‌شود، ثبت می‌کند.

### kube-scheduler-simulator.sigs.k8s.io/prebind-result

نوع: حاشیه‌نویسی

مثال: `kube-scheduler-simulator.sigs.k8s.io/prebind-result: '{"VolumeBinding":"success"}'`

مورد استفاده در: پاد

این حاشیه‌نویسی نتیجه افزونه‌های زمان‌بندی پیش‌اتصال را که توسط https://sigs.k8s.io/kube-scheduler-simulator استفاده می‌شود، ثبت می‌کند.

### kube-scheduler-simulator.sigs.k8s.io/prefilter-result

نوع: حاشیه‌نویسی

مثال: `kube-scheduler-simulator.sigs.k8s.io/prebind-result: '{"VolumeBinding":"success"}'`

مورد استفاده در: پاد

این حاشیه‌نویسی نتیجه افزونه‌های زمان‌بندی پیش‌اتصال را که توسط https://sigs.k8s.io/kube-scheduler-simulator استفاده می‌شود، ثبت می‌کند.

### kube-scheduler-simulator.sigs.k8s.io/prefilter-result-status

نوع: حاشیه‌نویسی


مثال:

```yaml
kube-scheduler-simulator.sigs.k8s.io/prefilter-result-status: >-
      {"InterPodAffinity":"success","NodeAffinity":"success","NodePorts":"success","NodeResourcesFit":"success","PodTopologySpread":"success","VolumeBinding":"success","VolumeRestrictions":"success"}
```

مورد استفاده در: پاد

این حاشیه‌نویسی نتیجه افزونه‌های زمان‌بندی پیش‌فیلتر را که توسط https://sigs.k8s.io/kube-scheduler-simulator استفاده می‌شود، ثبت می‌کند.

### kube-scheduler-simulator.sigs.k8s.io/prescore-result

نوع: حاشیه‌نویسی

مثال:

```yaml
    kube-scheduler-simulator.sigs.k8s.io/prescore-result: >-
      {"InterPodAffinity":"success","NodeAffinity":"success","NodeNumber":"success","PodTopologySpread":"success","TaintToleration":"success"}
```

مورد استفاده در: پاد

این حاشیه‌نویسی نتیجه افزونه‌های زمان‌بندی پیش‌فیلتر را که توسط https://sigs.k8s.io/kube-scheduler-simulator استفاده می‌شود، ثبت می‌کند.

### kube-scheduler-simulator.sigs.k8s.io/reserve-result

نوع: حاشیه‌نویسی

مثال: `kube-scheduler-simulator.sigs.k8s.io/reserve-result: '{"VolumeBinding":"success"}'`

مورد استفاده در: پاد

این حاشیه‌نویسی نتیجه‌ی افزونه‌های زمان‌بندی رزرو را که توسط https://sigs.k8s.io/kube-scheduler-simulator استفاده می‌شود، ثبت می‌کند.

### kube-scheduler-simulator.sigs.k8s.io/result-history

نوع: حاشیه‌نویسی

مثال: `kube-scheduler-simulator.sigs.k8s.io/result-history: '[]'`

مورد استفاده در: پاد

این حاشیه‌نویسی تمام نتایج برنامه‌ریزی گذشته از افزونه‌های زمان‌بندی را که توسط https://sigs.k8s.io/kube-scheduler-simulator استفاده می‌شود، ثبت می‌کند.

### kube-scheduler-simulator.sigs.k8s.io/score-result

نوع: حاشیه‌نویسی


```yaml
    kube-scheduler-simulator.sigs.k8s.io/score-result: >-
      {"node-282x7":{"ImageLocality":"0","InterPodAffinity":"0","NodeAffinity":"0","NodeNumber":"0","NodeResourcesBalancedAllocation":"76","NodeResourcesFit":"73","PodTopologySpread":"0","TaintToleration":"0","VolumeBinding":"0"},"node-gp9t4":{"ImageLocality":"0","InterPodAffinity":"0","NodeAffinity":"0","NodeNumber":"0","NodeResourcesBalancedAllocation":"76","NodeResourcesFit":"73","PodTopologySpread":"0","TaintToleration":"0","VolumeBinding":"0"}}
```

مورد استفاده در: پاد

این حاشیه‌نویسی نتیجه افزونه‌های زمان‌بندی امتیاز را ثبت می‌کند که توسط https://sigs.k8s.io/kube-scheduler-simulator استفاده می‌شود.

### kube-scheduler-simulator.sigs.k8s.io/selected-node

نوع: حاشیه‌نویسی

مثال: `kube-scheduler-simulator.sigs.k8s.io/selected-node: node-282x7`

مورد استفاده در: پاد

این حاشیه‌نویسی، گره‌ای را که توسط چرخه زمان‌بندی انتخاب می‌شود، ثبت می‌کند و توسط https://sigs.k8s.io/kube-scheduler-simulator استفاده می‌شود.

### kubernetes.io/arch

نوع: برچسب

مثال: `kubernetes.io/arch: "amd64"`

مورد استفاده در: Node

Kubelet این را با `runtime.GOARCH` مطابق تعریف Go پر می‌کند.

این می‌تواند در صورتی که گره‌های ARM و x86 را با هم ترکیب می‌کنید، مفید باشد.

### kubernetes.io/os

نوع: برچسب

مثال: `kubernetes.io/os: "linux"`

مورد استفاده در: Node، Pod

برای گره‌ها، kubelet این را با `runtime.GOOS` مطابق تعریف Go پر می‌کند. این می‌تواند در صورتی که در حال ترکیب سیستم‌های عامل در کلاستر خود هستید (مثلاً: ترکیب گره‌های لینوکس و ویندوز) مفید باشد.

همچنین می‌توانید این برچسب را روی یک Pod تنظیم کنید. Kubernetes به شما امکان می‌دهد هر مقداری را برای این برچسب تنظیم کنید. اگر از این برچسب استفاده می‌کنید، با این وجود باید آن را روی رشته Go `runtime.GOOS` برای سیستم عاملی که این Pod در واقع با آن کار می‌کند، تنظیم کنید.

هنگامی که مقدار برچسب `kubernetes.io/os` برای یک Pod با مقدار برچسب روی یک Node مطابقت نداشته باشد، kubelet روی گره، Pod را نمی‌پذیرد. با این حال، kube-scheduler این موضوع را در نظر نمی‌گیرد. از طرف دیگر، kubelet از اجرای Pod که در آن یک Pod OS مشخص کرده‌اید، خودداری می‌کند، اگر این سیستم عامل با سیستم عامل گره‌ای که kubelet در آن اجرا می‌شود، یکسان نباشد. برای جزئیات بیشتر، فقط به دنبال [Pods OS](/docs/concepts/workloads/pods/#pod-os) باشید.

### kubernetes.io/metadata.name

نوع: برچسب

مثال: `kubernetes.io/metadata.name: "mynamespace"`

مورد استفاده در: فضاهای نام

سرور Kubernetes API (بخشی از {{< glossary_tooltip text="control plane" term_id="control-plane" >}})
این برچسب را روی همه فضاهای نام تنظیم می‌کند. مقدار برچسب
روی نام فضای نام تنظیم می‌شود. شما نمی‌توانید مقدار این برچسب را تغییر دهید.

این در صورتی مفید است که بخواهید یک فضای نام خاص را با برچسب
{{< glossary_tooltip text="selector" term_id="selector" >}} هدف قرار دهید.

### kubernetes.io/limit-ranger

نوع: حاشیه‌نویسی

مثال: `kubernetes.io/limit-ranger: "مجموعه افزونه LimitRanger: پردازنده، درخواست حافظه برای کانتینر nginx؛ پردازنده، محدودیت حافظه برای کانتینر nginx"`

مورد استفاده در: پاد

کوبرنتس به طور پیش‌فرض هیچ محدودیتی برای منابع ارائه نمی‌دهد، به این معنی که مگر اینکه صریحاً محدودیت‌ها را تعریف کنید، کانتینر شما می‌تواند CPU و حافظه نامحدودی مصرف کند.

شما می‌توانید یک درخواست پیش‌فرض یا محدودیت پیش‌فرض برای پادها تعریف کنید. این کار را با ایجاد یک LimitRange در فضای نام مربوطه انجام می‌دهید. پادهایی که پس از تعریف LimitRange مستقر می‌شوند، این محدودیت‌ها را خواهند داشت.

حاشیه‌نویسی `kubernetes.io/limit-ranger` ثبت می‌کند که پیش‌فرض‌های منابع برای پاد مشخص شده‌اند و با موفقیت اعمال شده‌اند.

برای جزئیات بیشتر، درباره [LimitRanges](/docs/concepts/policy/limit-range) بخوانید.

### kubernetes.io/config.hash

نوع: حاشیه‌نویسی

مثال: `kubernetes.io/config.hash: "df7cc47f8477b6b1226d7d23a904867b"`

مورد استفاده در: پاد

هنگامی که kubelet یک پاد استاتیک بر اساس یک مانیفست داده شده ایجاد می‌کند، این حاشیه‌نویسی را به پاد استاتیک متصل می‌کند. مقدار حاشیه‌نویسی، شناسه کاربری (UID) پاد است.

توجه داشته باشید که kubelet همچنین `.spec.nodeName` را روی نام گره فعلی تنظیم می‌کند، گویی پاد

برای گره برنامه‌ریزی شده است.

### kubernetes.io/config.mirror

نوع: حاشیه‌نویسی

مثال: `kubernetes.io/config.mirror: "df7cc47f8477b6b1226d7d23a904867b"`

مورد استفاده در: پاد

برای یک پاد استاتیک که توسط kubelet روی یک گره ایجاد شده است، یک {{< glossary_tooltip text="mirror Pod" term_id="mirror-pod" >}}
در سرور API ایجاد می‌شود. kubelet یک حاشیه‌نویسی اضافه می‌کند تا نشان دهد که این پاد
در واقع یک پاد آینه‌ای است. مقدار حاشیه‌نویسی از حاشیه‌نویسی [`kubernetes.io/config.hash`](#kubernetes-io-config-hash)
کپی می‌شود که UID پاد است.

هنگام به‌روزرسانی یک پاد با این مجموعه حاشیه‌نویسی، حاشیه‌نویسی قابل تغییر یا حذف نیست. اگر یک Pod این حاشیه‌نویسی را نداشته باشد، نمی‌توان آن را در طول به‌روزرسانی Pod اضافه کرد.

### kubernetes.io/config.source

نوع: حاشیه‌نویسی

مثال: `kubernetes.io/config.source: "file"`

مورد استفاده در: پاد

این حاشیه‌نویسی توسط kubelet اضافه می‌شود تا نشان دهد پاد از کجا می‌آید.

برای پادهای استاتیک، مقدار حاشیه‌نویسی می‌تواند یکی از `file` یا `http` باشد، بسته به اینکه مانیفست پاد در کجا قرار دارد. برای پادی که در سرور API ایجاد شده و سپس در گره فعلی زمان‌بندی شده است، مقدار حاشیه‌نویسی `api` است.
### kubernetes.io/config.seen

نوع: حاشیه‌نویسی

مثال: `kubernetes.io/config.seen: "2023-10-27T04:04:56.011314488Z"`

مورد استفاده در: پاد

وقتی kubelet برای اولین بار یک پاد را می‌بیند، ممکن است این حاشیه‌نویسی را با مقداری از برچسب زمانی فعلی در قالب RFC3339 به پاد اضافه کند.

### addonmanager.kubernetes.io/mode

نوع: برچسب

مثال: `addonmanager.kubernetes.io/mode: "Reconcile"`

مورد استفاده در: همه اشیاء

برای مشخص کردن نحوه مدیریت یک افزونه، می‌توانید از برچسب `addonmanager.kubernetes.io/mode` استفاده کنید.

این برچسب می‌تواند یکی از سه مقدار زیر را داشته باشد: `Reconcile`، `EnsureExists` یا `Ignore`.

- `Reconcile`: منابع افزونه به صورت دوره‌ای با وضعیت مورد انتظار تطبیق داده می‌شوند.

در صورت وجود هرگونه اختلاف، مدیر افزونه منابع را در صورت نیاز دوباره ایجاد، پیکربندی یا حذف می‌کند. این حالت پیش‌فرض است اگر هیچ برچسبی مشخص نشده باشد.

- `EnsureExists`: منابع افزونه فقط از نظر وجود بررسی می‌شوند اما پس از ایجاد تغییر نمی‌کنند. مدیر افزونه منابع را زمانی که هیچ نمونه‌ای از منبع با آن نام وجود نداشته باشد، ایجاد یا دوباره ایجاد می‌کند.

- `Ignore`: منابع افزونه نادیده گرفته می‌شوند. این حالت برای افزونه‌هایی که با مدیر افزونه سازگار نیستند یا توسط کنترل‌کننده دیگری مدیریت می‌شوند، مفید است.

برای جزئیات بیشتر، به [Addon-manager](https://github.com/kubernetes/kubernetes/blob/master/cluster/addons/addon-manager/README.md) مراجعه کنید.

### beta.kubernetes.io/arch (deprecated)

نوع: برچسب

این برچسب منسوخ شده است. لطفاً به جای آن از [`kubernetes.io/arch`](#kubernetes-io-arch) استفاده کنید.

### beta.kubernetes.io/os (منسوخ شده)

نوع: برچسب

این برچسب منسوخ شده است. لطفاً به جای آن از [`kubernetes.io/os`](#kubernetes-io-os) استفاده کنید.

### kube-aggregator.kubernetes.io/automanaged {#kube-aggregator-kubernetesio-automanaged}

نوع: برچسب

مثال: `kube-aggregator.kubernetes.io/automanaged: "onstart"`

مورد استفاده در: APIService

`kube-apiserver` این برچسب را روی هر شیء APIService که سرور API به طور خودکار ایجاد کرده است، تنظیم می‌کند. این برچسب نحوه مدیریت آن APIService توسط صفحه کنترل را مشخص می‌کند. شما نباید خودتان این برچسب را اضافه، اصلاح یا حذف کنید.

{{< note >}}
اشیاء APIService مدیریت‌شده خودکار توسط kube-apiserver حذف می‌شوند زمانی که هیچ API منبع داخلی یا سفارشی مربوط به گروه/نسخه APIService نداشته باشد.
{{< /note >}}

دو مقدار ممکن وجود دارد:

- `onstart`: APIService باید هنگام راه‌اندازی یک سرور API تطبیق داده شود، اما در غیر این صورت خیر.
- `true`: سرور API باید این APIService را به طور مداوم تطبیق دهد.

### service.alpha.kubernetes.io/tolerate-unready-endpoints (deprecated)

نوع: حاشیه‌نویسی

مورد استفاده در: StatefulSet

این حاشیه‌نویسی در یک سرویس نشان می‌دهد که آیا کنترل‌کننده نقاط پایانی باید اقدام به ایجاد نقاط پایانی برای پادهای آماده‌نشده کند یا خیر. نقاط پایانی این سرویس‌ها رکوردهای DNS خود را حفظ می‌کنند و از لحظه‌ای که kubelet تمام کانتینرهای موجود در پاد را شروع می‌کند و آن را _Running_ علامت‌گذاری می‌کند، تا زمانی که kubelet تمام کانتینرها را متوقف کرده و پاد را از سرور API حذف کند، به دریافت ترافیک برای سرویس ادامه می‌دهند.

### autoscaling.alpha.kubernetes.io/behavior (deprecated) {#autoscaling-alpha-kubernetes-io-behavior}

نوع: حاشیه‌نویسی

مورد استفاده در: HorizontalPodAutoscaler

این حاشیه‌نویسی برای پیکربندی رفتار مقیاس‌بندی برای HorizontalPodAutoscaler (HPA) در نسخه‌های قبلی Kubernetes استفاده می‌شد.

این به شما امکان می‌داد مشخص کنید که HPA چگونه باید پادها را به بالا یا پایین مقیاس‌بندی کند، از جمله تنظیم پنجره‌های تثبیت و سیاست‌های مقیاس‌بندی.

تنظیم این حاشیه‌نویسی در هیچ یک از نسخه‌های پشتیبانی‌شده Kubernetes تأثیری ندارد.

### kubernetes.io/hostname {#kubernetesiohostname}

نوع: برچسب

مثال: `kubernetes.io/hostname: "ip-172-20-114-199.ec2.internal"`

مورد استفاده در: Node

Kubelet این برچسب را با نام میزبان گره پر می‌کند. توجه داشته باشید که نام میزبان
را می‌توان با ارسال پرچم `--hostname-override` به `kubelet` از نام میزبان "واقعی" تغییر داد.

این برچسب همچنین به عنوان بخشی از سلسله مراتب توپولوژی استفاده می‌شود.

برای اطلاعات بیشتر به [topology.kubernetes.io/zone](#topologykubernetesiozone) مراجعه کنید.

### kubernetes.io/change-cause {#change-cause}

نوع: حاشیه‌نویسی

مثال: `kubernetes.io/change-cause: "kubectl edit --record deployment foo"`

مورد استفاده در: همه اشیاء

این حاشیه‌نویسی بهترین حدس در مورد دلیل تغییر چیزی است.

هنگام اضافه کردن `--record` به دستور `kubectl` که ممکن است یک شیء را تغییر دهد، مقداردهی می‌شود.

### kubernetes.io/description {#description}

نوع: حاشیه‌نویسی

مثال: `kubernetes.io/description: "توضیحات شیء K8s."`

مورد استفاده در: همه اشیاء

این حاشیه‌نویسی برای توصیف رفتار خاص شیء مورد نظر استفاده می‌شود.

### kubernetes.io/enforce-mountable-secrets (deprecated) {#enforce-mountable-secrets}

نوع: حاشیه‌نویسی

مثال: `kubernetes.io/enforce-mountable-secrets: "true"`

مورد استفاده در: ServiceAccount

{{< note >}}
`kubernetes.io/enforce-mountable-secrets` از Kubernetes نسخه ۱.۳۲ منسوخ شده است. برای جداسازی دسترسی به secretهای mount شده، از namespaceهای جداگانه استفاده کنید.
{{< /note >}}

مقدار این حاشیه‌نویسی باید **true** باشد تا اعمال شود.
وقتی این حاشیه‌نویسی را روی «true» تنظیم می‌کنید، Kubernetes قوانین زیر را برای
Podهایی که به عنوان این ServiceAccount اجرا می‌شوند، اعمال می‌کند:

۱. اسراری که به عنوان ولوم‌ها (volumes) نصب شده‌اند باید در فیلد «اسرار» (secrets) سرویس‌اکانت (ServiceAccount) فهرست شوند.

۱. اسراری که در «envFrom» برای کانتینرها (شامل کانتینرهای سایدکار و کانتینرهای init) به آنها اشاره شده است، باید در فیلد اسرار سرویس‌اکانت نیز فهرست شوند.

اگر هر کانتینری در یک پاد به رازی اشاره کند که در فیلد «اسرار» سرویس‌اکانت فهرست نشده باشد (و حتی اگر این مرجع به عنوان «اختیاری» علامت‌گذاری شده باشد)، پاد شروع به کار نخواهد کرد، و خطایی مبنی بر عدم انطباق مرجع اسرار ایجاد خواهد شد.

۱. اسراری که در «imagePullSecrets» یک پاد به آنها اشاره شده است، باید در فیلد «imagePullSecrets» سرویس‌اکانت وجود داشته باشند، پاد شروع به کار نخواهد کرد، و خطایی مبنی بر عدم انطباق مرجع اسرار کشیدن تصویر ایجاد خواهد شد.

وقتی یک پاد ایجاد یا به‌روزرسانی می‌کنید، این قوانین بررسی می‌شوند. اگر پاد از آنها پیروی نکند، شروع به کار نمی‌کند و یک پیام خطا مشاهده خواهید کرد.

اگر یک پاد از قبل در حال اجرا باشد و حاشیه‌نویسی `kubernetes.io/enforce-mountable-secrets` را به true تغییر دهید، یا ServiceAccount مرتبط را ویرایش کنید تا ارجاع به یک راز که پاد از قبل از آن استفاده می‌کند را حذف کنید، پاد به اجرای خود ادامه می‌دهد.

### node.kubernetes.io/exclude-from-external-load-balancers

نوع: برچسب

مثال: `node.kubernetes.io/exclude-from-external-load-balancers`

مورد استفاده در: Node

شما می‌توانید به گره‌های کارگر خاص برچسب اضافه کنید تا آنها را از لیست سرورهای backend مورد استفاده توسط متعادل‌کننده‌های بار خارجی حذف کنید.

دستور زیر را می‌توان برای حذف یک گره کارگر از لیست سرورهای backend در یک مجموعه backend استفاده کرد:

```shell
kubectl label nodes <node-name> node.kubernetes.io/exclude-from-external-load-balancers=true
```

### controller.kubernetes.io/pod-deletion-cost {#pod-deletion-cost}
نوع: حاشیه‌نویسی

مثال: `controller.kubernetes.io/pod-deletion-cost: "10"`

مورد استفاده در: Pod

این حاشیه‌نویسی برای تنظیم [Pod Deletion Cost](/docs/concepts/workloads/controllers/replicaset/#pod-deletion-cost) استفاده می‌شود که به کاربران اجازه می‌دهد تا ترتیب کوچک‌سازی ReplicaSet را تحت تأثیر قرار دهند.

مقدار حاشیه‌نویسی به یک نوع `int32` تجزیه می‌شود.

### cluster-autoscaler.kubernetes.io/enable-ds-eviction

نوع: حاشیه‌نویسی

مثال: `cluster-autoscaler.kubernetes.io/enable-ds-eviction: "true"`

مورد استفاده در: پاد

این حاشیه‌نویسی کنترل می‌کند که آیا یک پاد DaemonSet باید توسط یک ClusterAutoscaler حذف شود یا خیر.

این حاشیه‌نویسی باید در پادهای DaemonSet در مانیفست DaemonSet مشخص شود.

وقتی این حاشیه‌نویسی روی `"true"` تنظیم شود، ClusterAutoscaler مجاز است یک پاد DaemonSet را حذف کند، حتی اگر سایر قوانین معمولاً مانع از این کار شوند.

برای اینکه ClusterAutoscaler نتواند پادهای DaemonSet را حذف کند، می‌توانید این حاشیه‌نویسی را برای پادهای مهم DaemonSet روی `"false"` تنظیم کنید. اگر این حاشیه‌نویسی تنظیم نشده باشد، ClusterAutoscaler از رفتار کلی خود پیروی می‌کند (یعنی DaemonSets را بر اساس پیکربندی خود حذف می‌کند).

{{< note >}}
این حاشیه‌نویسی فقط روی پادهای DaemonSet تأثیر می‌گذارد.
{{< /note >}}

### kubernetes.io/ingress-bandwidth

نوع: حاشیه‌نویسی

مثال: `kubernetes.io/ingress-bandwidth: 10M`

مورد استفاده در: پاد

شما می‌توانید شکل‌دهی ترافیک با کیفیت سرویس را به یک پاد اعمال کنید و پهنای باند موجود آن را به طور مؤثر محدود کنید. ترافیک ورودی به یک پاد با شکل‌دهی بسته‌های صف‌بندی شده برای مدیریت مؤثر داده‌ها مدیریت می‌شود. برای محدود کردن پهنای باند در یک پاد، یک فایل JSON با تعریف شیء بنویسید و سرعت ترافیک داده را با استفاده از حاشیه‌نویسی `kubernetes.io/ingress-bandwidth` مشخص کنید. واحد مورد استفاده برای تعیین نرخ ورودی، بیت در ثانیه است، به عنوان [مقدار](/docs/reference/kubernetes-api/common-definitions/quantity/). به عنوان مثال، `10M` به معنی 10 مگابیت در ثانیه است.

{{< note >}}
حاشیه‌نویسی شکل‌دهی ترافیک ورودی یک ویژگی آزمایشی است. اگر می‌خواهید پشتیبانی از شکل‌دهی ترافیک را فعال کنید، باید افزونه `bandwidth` را به فایل پیکربندی CNI خود (پیش‌فرض `/etc/cni/net.d`) اضافه کنید و مطمئن شوید که فایل باینری در پوشه CNI bin شما (پیش‌فرض `/opt/cni/bin`) گنجانده شده است.
hashiernevisi sheklde
{{< /note >}}

### kubernetes.io/egress-bandwidth

نوع: حاشیه‌نویسی

مثال: `kubernetes.io/egress-bandwidth: 10M`

مورد استفاده در: پاد

ترافیک خروجی از یک پاد توسط پلیس کنترل می‌شود، که به سادگی بسته‌های اضافی از نرخ پیکربندی شده را حذف می‌کند. محدودیت‌هایی که روی یک پاد اعمال می‌کنید، بر پهنای باند سایر پادها تأثیری ندارد.

برای محدود کردن پهنای باند روی یک پاد، یک فایل JSON تعریف شیء بنویسید و سرعت ترافیک داده را با استفاده از حاشیه‌نویسی `kubernetes.io/egress-bandwidth` مشخص کنید. واحد مورد استفاده برای تعیین نرخ خروجی، بیت در ثانیه است، به عنوان [مقدار](/docs/reference/kubernetes-api/common-definitions/quantity/).

به عنوان مثال، `10M` به معنی 10 مگابیت در ثانیه است.

{{< note >}}
حاشیه‌نویسی شکل‌دهی ترافیک خروجی یک ویژگی آزمایشی است. اگر می‌خواهید پشتیبانی از شکل‌دهی ترافیک را فعال کنید، باید افزونه‌ی `bandwidth` را به فایل پیکربندی CNI خود (پیش‌فرض `/etc/cni/net.d`) اضافه کنید و مطمئن شوید که فایل باینری در پوشه‌ی CNI bin شما (پیش‌فرض `/opt/cni/bin`) قرار دارد.
{{< /note >}}

### beta.kubernetes.io/instance-type (deprecated)

نوع: برچسب


{{< note >}}
از نسخه ۱.۱۷ به بعد، این برچسب منسوخ شده و به جای آن از ‎[node.kubernetes.io/instance-type](#nodekubernetesioinstance-type)‎ استفاده می‌شود.
{{< /note >}}

### node.kubernetes.io/instance-type {#nodekubernetesioinstance-type}

نوع: برچسب

مثال: `node.kubernetes.io/instance-type: "m3.medium"`

مورد استفاده در: Node

Kubelet این را با نوع نمونه‌ای که توسط ارائه‌دهنده ابر تعریف شده است، پر می‌کند.

این فقط در صورتی تنظیم می‌شود که از یک ارائه‌دهنده ابر استفاده کنید. این تنظیم مفید است

اگر می‌خواهید بارهای کاری خاصی را به انواع نمونه خاصی اختصاص دهید، اما معمولاً می‌خواهید

برای انجام برنامه‌ریزی مبتنی بر منابع به زمان‌بند Kubernetes تکیه کنید.

شما باید برنامه‌ریزی را بر اساس ویژگی‌ها انجام دهید نه بر اساس انواع نمونه

(برای مثال: به جای نیاز به یک `g2.2xlarge`، به یک GPU نیاز دارید).

### failure-domain.beta.kubernetes.io/region (deprecated) {#failure-domainbetakubernetesioregion}

نوع: برچسب

{{< note >}}
از نسخه ۱.۱۷ به بعد، این برچسب به نفع ‎[topology.kubernetes.io/region](#topologykubernetesioregion)‎ منسوخ شده است.
{{< /note >}}

### failure-domain.beta.kubernetes.io/zone (deprecated) {#failure-domainbetakubernetesiozone}

نوع: برچسب

{{< note >}}
از نسخه ۱.۱۷ به بعد، این برچسب به نفع برچسب [topology.kubernetes.io/zone](#topologykubernetesiozone) منسوخ شده است.
{{< /note >}}

### pv.kubernetes.io/bind-completed {#pv-kubernetesiobind-completed}

نوع: حاشیه‌نویسی
مثال: `pv.kubernetes.io/bind-completed: "yes"`

مورد استفاده در: PersistentVolumeClaim

هنگامی که این حاشیه‌نویسی روی یک PersistentVolumeClaim (PVC) تنظیم می‌شود، نشان می‌دهد که چرخه عمر PVC از تنظیمات اتصال اولیه عبور کرده است. در صورت وجود، این اطلاعات نحوه تفسیر وضعیت اشیاء PVC توسط صفحه کنترل را تغییر می‌دهد.

مقدار این حاشیه‌نویسی برای Kubernetes اهمیتی ندارد.

### pv.kubernetes.io/bound-by-controller {#pv-kubernetesioboundby-controller}

نوع: حاشیه‌نویسی

مثال: `pv.kubernetes.io/bound-by-controller: "yes"`

مورد استفاده در: PersistentVolume، PersistentVolumeClaim

اگر این حاشیه‌نویسی روی یک PersistentVolume یا PersistentVolumeClaim تنظیم شده باشد، نشان می‌دهد که یک اتصال ذخیره‌سازی (PersistentVolume → PersistentVolumeClaim، یا PersistentVolumeClaim → PersistentVolume) توسط {{< glossary_tooltip text="controller" term_id="controller" >}} نصب شده است.

اگر حاشیه‌نویسی تنظیم نشده باشد و یک اتصال ذخیره‌سازی وجود داشته باشد، عدم وجود آن حاشیه‌نویسی به این معنی است که اتصال به صورت دستی انجام شده است.

مقدار این حاشیه‌نویسی مهم نیست.

### pv.kubernetes.io/provisioned-by {#pv-kubernetesiodynamically-provisioned}

نوع: حاشیه‌نویسی

مثال: `pv.kubernetes.io/provisioned-by: "kubernetes.io/rbd"`

مورد استفاده در: PersistentVolume

این حاشیه‌نویسی به PersistentVolume(PV) که به صورت پویا توسط Kubernetes فراهم شده است، اضافه می‌شود.

مقدار آن نام افزونه volume است که volume را ایجاد کرده است. این annotation هم برای کاربران (برای نشان دادن اینکه یک PV از کجا می‌آید) و هم برای Kubernetes (برای تشخیص PVهای فراهم شده به صورت پویا در تصمیماتش) کاربرد دارد.

### pv.kubernetes.io/migrated-to {#pv-kubernetesio-migratedto}

نوع: حاشیه‌نویسی

مثال: `pv.kubernetes.io/migrated-to: pd.csi.storage.gke.io`

مورد استفاده در: PersistentVolume، PersistentVolumeClaim

این به PersistentVolume(PV) و PersistentVolumeClaim(PVC) اضافه می‌شود که قرار است توسط درایور CSI مربوطه از طریق دروازه ویژگی `CSIMigration` به صورت پویا تهیه/حذف شوند.

هنگامی که این حاشیه‌نویسی تنظیم می‌شود، اجزای Kubernetes "خاموش" می‌شوند و `external-provisioner` روی اشیاء عمل می‌کند.

### statefulset.kubernetes.io/pod-name {#statefulsetkubernetesiopod-name}

نوع: برچسب

مثال: `statefulset.kubernetes.io/pod-name: "mystatefulset-7"`

مورد استفاده در: Pod

هنگامی که یک کنترلر StatefulSet یک Pod برای StatefulSet ایجاد می‌کند، صفحه کنترل
این برچسب را روی آن Pod تنظیم می‌کند. مقدار برچسب، نام Pod در حال ایجاد است.

برای جزئیات بیشتر به [برچسب نام Pod](/docs/concepts/workloads/controllers/statefulset/#pod-name-label) در موضوع StatefulSet مراجعه کنید.
in the StatefulSet topic for more details.

### scheduler.alpha.kubernetes.io/node-selector {#schedulerkubernetesnode-selector}

نوع: حاشیه‌نویسی

مثال: `scheduler.alpha.kubernetes.io/node-selector: "name-of-node-selector"`

مورد استفاده در: فضای نام

[PodNodeSelector](/docs/reference/access-authn-authz/admission-controllers/#podnodeselector)

از این کلید حاشیه‌نویسی برای اختصاص انتخابگرهای گره به پادها در فضاهای نام استفاده می‌کند.

### topology.kubernetes.io/region {#topologykubernetesioregion}

نوع: برچسب

مثال: `topology.kubernetes.io/region: "us-east-1"`

مورد استفاده در: Node، PersistentVolume

به [topology.kubernetes.io/zone](#topologykubernetesiozone) مراجعه کنید.

### topology.kubernetes.io/zone {#topologykubernetesiozone}

نوع: برچسب

مثال: `topology.kubernetes.io/zone: "us-east-1c"`

مورد استفاده در: Node، PersistentVolume

**در Node**: `kubelet` یا `cloud-controller-manager` خارجی این را با اطلاعات ارائه دهنده ابر پر می‌کند. این فقط در صورتی تنظیم می‌شود که از یک ارائه دهنده ابر استفاده کنید. با این حال، اگر در توپولوژی شما منطقی باشد، می‌توانید تنظیم این را روی گره‌ها در نظر بگیرید.

**در PersistentVolume**: ارائه دهندگان حجم آگاه از توپولوژی به طور خودکار محدودیت‌های وابستگی گره را روی `PersistentVolume` تنظیم می‌کنند.

یک منطقه نشان دهنده یک دامنه خرابی منطقی است. برای خوشه‌های Kubernetes معمول است که برای افزایش دسترسی، چندین منطقه را در بر بگیرند. در حالی که تعریف دقیق یک منطقه به پیاده‌سازی‌های زیرساختی واگذار شده است، ویژگی‌های مشترک یک منطقه شامل موارد زیر است: تأخیر بسیار کم شبکه در یک منطقه، ترافیک شبکه بدون هزینه در یک منطقه و استقلال از خرابی از سایر مناطق. به عنوان مثال، گره‌های درون یک منطقه ممکن است یک سوئیچ شبکه را به اشتراک بگذارند، اما گره‌های مناطق مختلف نباید این کار را انجام دهند.

یک منطقه نشان دهنده یک دامنه بزرگتر است که از یک یا چند منطقه تشکیل شده است.

برای خوشه‌های Kubernetes غیرمعمول است که چندین منطقه را در بر بگیرند.

در حالی که تعریف دقیق یک منطقه یا منطقه به پیاده‌سازی زیرساخت‌ها واگذار شده است،

ویژگی‌های مشترک یک منطقه شامل تأخیر شبکه بالاتر بین آنها نسبت به درون آنها،

هزینه غیر صفر برای ترافیک شبکه بین آنها و عدم وابستگی به سایر مناطق یا مناطق در صورت خرابی است.

به عنوان مثال، گره‌های درون یک منطقه ممکن است زیرساخت برق (مثلاً یک UPS یا ژنراتور) را به اشتراک بگذارند،

اما گره‌های مناطق مختلف معمولاً این کار را نمی‌کنند.

Kubernetes چند فرض در مورد ساختار مناطق و مناطق در نظر می‌گیرد:



1. مناطق و زون‌ها سلسله مراتبی هستند: زون‌ها زیرمجموعه‌های دقیقی از مناطق هستند و هیچ منطقه‌ای نمی‌تواند در 2 منطقه باشد

2. نام مناطق در مناطق مختلف منحصر به فرد است؛ برای مثال، منطقه "africa-east-1" ممکن است از مناطق "africa-east-1a" و "africa-east-1b" تشکیل شده باشد.


می‌توان با اطمینان فرض کرد که برچسب‌های توپولوژی تغییر نمی‌کنند.
اگرچه برچسب‌ها کاملاً قابل تغییر هستند، مصرف‌کنندگان آنها می‌توانند فرض کنند که یک گره مشخص
بدون تخریب و ایجاد مجدد، بین مناطق جابجا نمی‌شود.


Kubernetes می‌تواند از این اطلاعات به روش‌های مختلفی استفاده کند.

برای مثال، زمانبند به طور خودکار سعی می‌کند Podها را در یک ReplicaSet در بین گره‌ها

در یک خوشه تک منطقه‌ای پخش کند (برای کاهش تأثیر خرابی گره‌ها، به [kubernetes.io/hostname](#kubernetesiohostname) مراجعه کنید).

با خوشه‌های چند منطقه‌ای، این رفتار پخش برای مناطق نیز اعمال می‌شود (برای کاهش تأثیر خرابی منطقه).

این امر از طریق _SelectorSpreadPriority_ حاصل می‌شود.



_SelectorSpreadPriority_ یک جایگذاری با بهترین تلاش است. اگر مناطق موجود در خوشه شما ناهمگن باشند (به عنوان مثال: تعداد گره‌های مختلف، انواع گره‌های مختلف یا نیازهای منابع مختلف pod)، این جایگذاری ممکن است از توزیع برابر podهای شما در مناطق جلوگیری کند. در صورت تمایل، می‌توانید از مناطق همگن (تعداد و نوع گره‌های یکسان) برای کاهش احتمال توزیع نابرابر استفاده کنید.



زمانبند (از طریق گزاره _VolumeZonePredicate_) همچنین تضمین می‌کند که پادهایی که یک حجم مشخص را در اختیار دارند، فقط در همان منطقه با آن حجم قرار گیرند. حجم‌ها را نمی‌توان بین مناطق مختلف متصل کرد.


اگر `PersistentVolumeLabel` از برچسب‌گذاری خودکار PersistentVolumeهای شما پشتیبانی نمی‌کند، باید اضافه کردن برچسب‌ها را به صورت دستی (یا اضافه کردن پشتیبانی از `PersistentVolumeLabel`) در نظر بگیرید.
با `PersistentVolumeLabel`، زمان‌بندی از نصب Podها در یک منطقه متفاوت جلوگیری می‌کند.
اگر زیرساخت شما این محدودیت را ندارد، اصلاً نیازی به اضافه کردن برچسب‌های منطقه به Volumeها ندارید.

### volume.beta.kubernetes.io/storage-provisioner (منسوخ شده)

نوع: حاشیه‌نویسی


مثال: `volume.beta.kubernetes.io/storage-provisioner: "k8s.io/minikube-hostpath"`

مورد استفاده در: PersistentVolumeClaim

این حاشیه‌نویسی از نسخه ۱.۲۳ منسوخ شده است. به [volume.kubernetes.io/storage-provisioner](#volume-kubernetes-io-storage-provisioner) مراجعه کنید.

### volume.beta.kubernetes.io/storage-class (منسوخ شده)

نوع: حاشیه‌نویسی

مثال: `volume.beta.kubernetes.io/storage-class: "example-class"`

مورد استفاده در: PersistentVolume، PersistentVolumeClaim

این حاشیه‌نویسی می‌تواند برای PersistentVolume(PV) یا PersistentVolumeClaim(PVC) استفاده شود تا نام [StorageClass](/docs/concepts/storage/storage-classes/) مشخص شود.
هنگامی که هم ویژگی `storageClassName` و هم حاشیه‌نویسی `volume.beta.kubernetes.io/storage-class` مشخص شده باشند، حاشیه‌نویسی `volume.beta.kubernetes.io/storage-class` بر ویژگی `storageClassName` اولویت دارد.

این حاشیه‌نویسی منسوخ شده است. در عوض، فیلد [`storageClassName`](/docs/concepts/storage/persistent-volumes/#class) را برای PersistentVolumeClaim یا PersistentVolume تنظیم کنید.

### volume.beta.kubernetes.io/mount-options (منسوخ شده) {#mount-options}

نوع: حاشیه‌نویسی

مثال : `volume.beta.kubernetes.io/mount-options: "ro,soft"`

 مورد استفاده در: PersistentVolume

یک مدیر Kubernetes می‌تواند گزینه‌های اضافی [mount options](/docs/concepts/storage/persistent-volumes/#mount-options) را برای زمانی که یک PersistentVolume روی یک گره mount می‌شود، مشخص کند.


### volume.kubernetes.io/storage-provisioner  {#volume-kubernetes-io-storage-provisioner}

نوع: حاشیه‌نویسی

Used on: PersistentVolumeClaim

This annotation is added to a PVC that is supposed to be dynamically provisioned.
Its value is the name of a volume plugin that is supposed to provision a volume
for this PVC.

### volume.kubernetes.io/selected-node



مورد استفاده در: PersistentVolumeClaim

این حاشیه‌نویسی به یک PVC اضافه می‌شود که توسط یک زمانبند فعال می‌شود تا به صورت پویا آماده‌سازی شود. مقدار آن نام گره انتخاب شده است.


### volumes.kubernetes.io/controller-managed-attach-detach

نوع: حاشیه‌نویسی

مورد استفاده در: گره


اگر یک گره دارای حاشیه‌نویسی `volumes.kubernetes.io/controller-managed-attach-detach` باشد، عملیات اتصال و جدا کردن حافظه آن توسط _volume attach/detach_ مدیریت می‌شود. {{< glossary_tooltip text="controller" term_id="controller" >}}

ارزش حاشیه‌نویسی مهم نیست.

### node.kubernetes.io/windows-build {#nodekubernetesiowindows-build}

نوع: برچسب

مثال :`node.kubernetes.io/windows-build: "10.0.17763"`

مورد استفاده در: Node

وقتی kubelet روی مایکروسافت ویندوز اجرا می‌شود، به‌طور خودکار گره خود را برچسب‌گذاری می‌کند تا نسخه ویندوز سرور مورد استفاده را ثبت کند.


مقدار برچسب در قالب "MajorVersion.MinorVersion.BuildNumber" است.

### storage.alpha.kubernetes.io/migrated-plugins {#storagealphakubernetesiomigrated-plugins}

نوع: حاشیه‌نویسی


مثال:`storage.alpha.kubernetes.io/migrated-plugins: "kubernetes.io/cinder"`


مورد استفاده در: CSINode (یک رابط برنامه‌نویسی API افزونه)
این حاشیه‌نویسی به طور خودکار برای شیء CSINode که به گره‌ای که CSIDriver را نصب می‌کند، نگاشت می‌شود، اضافه می‌شود. این حاشیه‌نویسی نام افزونه درون‌درختی افزونه منتقل شده را نشان می‌دهد. مقدار آن به نوع ذخیره‌سازی ارائه‌دهنده ابر درون‌درختی خوشه شما بستگی دارد.

برای مثال، اگر نوع ذخیره‌سازی ارائه‌دهنده ابر درون‌شاخه‌ای «CSIMigrationvSphere» باشد، نمونه CSINodes برای گره باید با این موارد به‌روزرسانی شود:
`storage.alpha.kubernetes.io/migrated-plugins: "kubernetes.io/vsphere-volume"`

### service.kubernetes.io/headless {#servicekubernetesioheadless}

نوع: برچسب


مثال: `service.kubernetes.io/headless: ""`

مورد استفاده در: Endpoints

صفحه کنترل این برچسب را به شیء Endpoints اضافه می‌کند وقتی که سرویس مالک Headless باشد.

برای کسب اطلاعات بیشتر، [Headless Services](/docs/concepts/services-networking/service/#headless-services) را مطالعه کنید.

### service.kubernetes.io/topology-aware-hints (منسوخ شده) {#servicekubernetesiotopology-aware-hints}

مثال: `service.kubernetes.io/topology-aware-hints: "Auto"`

مورد استفاده در: سرویس


این حاشیه‌نویسی برای فعال کردن _topology aware hints_ روی سرویس‌ها استفاده می‌شد. Topology aware hints از آن زمان تغییر نام داده است: این مفهوم اکنون [topology aware routing](/docs/concepts/services-networking/topology-aware-routing/) نامیده می‌شود.
تنظیم حاشیه‌نویسی روی `Auto`، روی یک سرویس، صفحه کنترل Kubernetes را پیکربندی کرد تا نکات توپولوژی را روی EndpointSlices مرتبط با آن سرویس اضافه کند. همچنین می‌توانید به صراحت حاشیه‌نویسی را روی `Disabled` تنظیم کنید.

اگر نسخه‌ای از Kubernetes قدیمی‌تر از {{< skew currentVersion >}} را اجرا می‌کنید، مستندات آن نسخه Kubernetes را بررسی کنید تا ببینید مسیریابی آگاه از توپولوژی در آن نسخه چگونه کار می‌کند.

هیچ مقدار معتبر دیگری برای این حاشیه‌نویسی وجود ندارد. اگر نمی‌خواهید نکات مربوط به توپولوژی برای یک سرویس وجود داشته باشد، این حاشیه‌نویسی را اضافه نکنید.

### service.kubernetes.io/topology-mode

نوع: حاشیه‌نویسی


مثال: `service.kubernetes.io/topology-mode: Auto`


مورد استفاده در: Service

این حاشیه‌نویسی روشی برای تعریف نحوه مدیریت توپولوژی شبکه توسط سرویس‌ها ارائه می‌دهد؛ برای مثال، می‌توانید یک سرویس را طوری پیکربندی کنید که Kubernetes ترجیح دهد ترافیک بین
کلاینت و سرور را در یک منطقه توپولوژی واحد نگه دارد.
در برخی موارد، این می‌تواند به کاهش هزینه‌ها یا بهبود عملکرد شبکه کمک کند.


برای جزئیات بیشتر به [Topology Aware Routing](/docs/concepts/services-networking/topology-aware-routing/) مراجعه کنید.

### kubernetes.io/service-name {#kubernetesioservice-name}

نوع: برچسب


مثال: `kubernetes.io/service-name: "my-website"`

مورد استفاده در: EndpointSlice

Kubernetes با استفاده از این برچسب، [EndpointSlices](/docs/concepts/services-networking/endpoint-slices/) را با [Services](/docs/concepts/services-networking/service/) مرتبط می‌کند.

این برچسب {{< glossary_tooltip term_id="name" text="name">}} از سرویسی را که EndpointSlice از آن پشتیبانی می‌کند، ثبت می‌کند. همه EndpointSliceها باید این برچسب را روی نام سرویس مرتبط خود تنظیم کنند.

### kubernetes.io/service-account.name

نوع: Annotation

مثال: `kubernetes.io/service-account.name: "sa-name"`

مورد استفاده در: راز

این حاشیه‌نویسی {{< glossary_tooltip term_id="name" text="name">}} از حساب سرویسی را ثبت می‌کند که توکن (ذخیره شده در راز از نوع `kubernetes.io/service-account-token`) نشان دهنده آن است.

### kubernetes.io/service-account.uid

نوع: Annotation

مثال: `kubernetes.io/service-account.uid: da68f9c6-9d26-11e7-b84e-002dc52800da`

Used on: Secret

مورد استفاده در: Secret

این حاشیه‌نویسی {{< glossary_tooltip term_id="uid" text="unique ID" >}} از حساب سرویسی که توکن (ذخیره شده در راز از نوع `kubernetes.io/service-account-token`) نشان می‌دهد را ثبت می‌کند.

### kubernetes.io/legacy-token-last-used

Type: Label

نوع: Label

مثال: `kubernetes.io/legacy-token-last-used: 2022-10-24`

مورد استفاده در: راز

صفحه کنترل فقط این برچسب را به رازهایی اضافه می‌کند که نوع آنها `kubernetes.io/service-account-token` باشد.

مقدار این برچسب، تاریخ (فرمت ISO 8601، منطقه زمانی UTC) را ثبت می‌کند که صفحه کنترل
آخرین درخواستی را مشاهده کرده است که در آن کلاینت با استفاده از توکن حساب سرویس احراز هویت شده است.

اگر یک توکن قدیمی آخرین بار قبل از اینکه کلاستر این ویژگی را دریافت کند (که در Kubernetes نسخه 1.26 اضافه شده است) استفاده شده باشد،

در این صورت برچسب تنظیم نشده است.

### kubernetes.io/legacy-token-invalid-since


نوع: Label

مثال: `kubernetes.io/legacy-token-invalid-since: 2023-10-27`

مورد استفاده در: راز

صفحه کنترل به طور خودکار این برچسب را به رازهای تولید شده خودکار که نوع `kubernetes.io/service-account-token` دارند اضافه می‌کند. این برچسب، توکن مبتنی بر راز را برای احراز هویت نامعتبر علامت‌گذاری می‌کند. مقدار این برچسب، تاریخ (فرمت ISO 8601، منطقه زمانی UTC) را ثبت می‌کند، زمانی که صفحه کنترل تشخیص می‌دهد که راز تولید شده خودکار برای مدت زمان مشخصی (به طور پیش‌فرض یک سال) استفاده نشده است.

### endpoints.kubernetes.io/managed-by (deprecated) {#endpoints-kubernetes-io-managed-by}

نوع: Label

مثال: `endpoints.kubernetes.io/managed-by: endpoint-controller`

مورد استفاده در: نقاط پایانی

این برچسب به صورت داخلی برای علامت‌گذاری اشیاء نقاط پایانی که توسط Kubernetes ایجاد شده‌اند (برخلاف نقاط پایانی ایجاد شده توسط کاربران یا کنترل‌کننده‌های خارجی) استفاده می‌شود.

{{< note >}}
API [Endpoints](/docs/reference/kubernetes-api/service-resources/endpoints-v1/) به نفع [EndpointSlice](/docs/reference/kubernetes-api/service-resources/endpoint-slice-v1/) منسوخ شده است.
{{< /note >}}

### endpointslice.kubernetes.io/managed-by {#endpointslicekubernetesiomanaged-by}

نوع: Label

مثال: `endpointslice.kubernetes.io/managed-by: endpointslice-controller.k8s.io`

مورد استفاده در: EndpointSlices

این برچسب برای نشان دادن کنترل‌کننده یا موجودیتی که EndpointSlice را مدیریت می‌کند، استفاده می‌شود. هدف این برچسب
فعال کردن مدیریت اشیاء EndpointSlice مختلف توسط کنترل‌کننده‌ها یا موجودیت‌های مختلف در یک خوشه است. مقدار `endpointslice-controller.k8s.io` نشان دهنده یک شیء EndpointSlice است که به طور خودکار توسط Kubernetes برای یک سرویس با {{< glossary_tooltip text="selectors" term_id="selector" >}} ایجاد شده است.

### endpointslice.kubernetes.io/skip-mirror {#endpointslicekubernetesioskip-mirror}


نوع: Label

مثال: `endpointslice.kubernetes.io/skip-mirror: "true"`

مورد استفاده در: نقاط پایانی

این برچسب را می‌توان روی یک منبع Endpoints روی `"true"` تنظیم کرد تا نشان دهد که کنترلر EndpointSliceMirroring نباید این منبع را با EndpointSlices منعکس کند.



### service.kubernetes.io/service-proxy-name {#servicekubernetesioservice-proxy-name}



نوع: Label

مثال: `service.kubernetes.io/service-proxy-name: "foo-bar"`

مورد استفاده در: سرویس

kube-proxy این برچسب را برای پروکسی سفارشی دارد که کنترل سرویس را به پروکسی سفارشی واگذار می‌کند.


### experimental.windows.kubernetes.io/isolation-type (deprecated) {#experimental-windows-kubernetes-io-isolation-type}

Type: Annotation

Example: `experimental.windows.kubernetes.io/isolation-type: "hyperv"`

Used on: Pod

The annotation is used to run Windows containers with Hyper-V isolation.

{{< note >}}
Starting from v1.20, this annotation is deprecated.
Experimental Hyper-V support was removed in 1.21.
{{< /note >}}

### ingressclass.kubernetes.io/is-default-class

Type: Annotation

Example: `ingressclass.kubernetes.io/is-default-class: "true"`

Used on: IngressClass

When a IngressClass resource has this annotation set to `"true"`, new Ingress resource
without a class specified will be assigned this default class.

### nginx.ingress.kubernetes.io/configuration-snippet

Type: Annotation

Example: `nginx.ingress.kubernetes.io/configuration-snippet: "  more_set_headers \"Request-Id: $req_id\";\nmore_set_headers \"Example: 42\";\n"`

Used on: Ingress

You can use this annotation to set extra configuration on an Ingress that
uses the [NGINX Ingress Controller](https://github.com/kubernetes/ingress-nginx/).
The `configuration-snippet` annotation is ignored
by default since version 1.9.0 of the ingress controller.
The NGINX ingress controller setting `allow-snippet-annotations.`
has to be explicitly enabled to use this annotation.
Enabling the annotation can be dangerous in a multi-tenant cluster, as it can lead people with otherwise
limited permissions being able to retrieve all Secrets in the cluster.

### kubernetes.io/ingress.class (deprecated)

Type: Annotation

Used on: Ingress

{{< note >}}
Starting in v1.18, this annotation is deprecated in favor of `spec.ingressClassName`.
{{< /note >}}

### kubernetes.io/cluster-service (deprecated) {#kubernetes-io-cluster-service}

Type: Label

Example: `kubernetes.io/cluster-service: "true"`

Used on: Service

This label indicates that the Service provides a service to the cluster, if the value is set to true.
When you run `kubectl cluster-info`, the tool queries for Services with this label set to true.

However, setting this label on any Service is deprecated.

### storageclass.kubernetes.io/is-default-class

Type: Annotation

Example: `storageclass.kubernetes.io/is-default-class: "true"`

Used on: StorageClass

When a single StorageClass resource has this annotation set to `"true"`, new PersistentVolumeClaim
resource without a class specified will be assigned this default class.

### alpha.kubernetes.io/provided-node-ip (alpha) {#alpha-kubernetes-io-provided-node-ip}

Type: Annotation

Example: `alpha.kubernetes.io/provided-node-ip: "10.0.0.1"`

Used on: Node

The kubelet can set this annotation on a Node to denote its configured IPv4 and/or IPv6 address.

When kubelet is started with the `--cloud-provider` flag set to any value (includes both external
and legacy in-tree cloud providers), it sets this annotation on the Node to denote an IP address
set from the command line flag (`--node-ip`). This IP is verified with the cloud provider as valid
by the cloud-controller-manager.

### batch.kubernetes.io/job-completion-index

Type: Annotation, Label

Example: `batch.kubernetes.io/job-completion-index: "3"`

Used on: Pod

The Job controller in the kube-controller-manager sets this as a label and annotation for Pods
created with Indexed [completion mode](/docs/concepts/workloads/controllers/job/#completion-mode).

Note the [PodIndexLabel](/docs/reference/command-line-tools-reference/feature-gates/)
feature gate must be enabled for this to be added as a pod **label**,
otherwise it will just be an annotation.

### batch.kubernetes.io/cronjob-scheduled-timestamp

Type: Annotation

Example: `batch.kubernetes.io/cronjob-scheduled-timestamp: "2016-05-19T03:00:00-07:00"`

Used on: Jobs and Pods controlled by CronJobs

This annotation is used to record the original (expected) creation timestamp for a Job,
when that Job is part of a CronJob.
The control plane sets the value to that timestamp in RFC3339 format. If the Job belongs to a CronJob
with a timezone specified, then the timestamp is in that timezone. Otherwise, the timestamp is in controller-manager's local time.

### kubectl.kubernetes.io/default-container

Type: Annotation

Example: `kubectl.kubernetes.io/default-container: "front-end-app"`

The value of the annotation is the container name that is default for this Pod.
For example, `kubectl logs` or `kubectl exec` without `-c` or `--container` flag
will use this default container.

### kubectl.kubernetes.io/default-logs-container (deprecated)

Type: Annotation

Example: `kubectl.kubernetes.io/default-logs-container: "front-end-app"`

The value of the annotation is the container name that is the default logging container for this
Pod. For example, `kubectl logs` without `-c` or `--container` flag will use this default
container.

{{< note >}}
This annotation is deprecated. You should use the
[`kubectl.kubernetes.io/default-container`](#kubectl-kubernetes-io-default-container)
annotation instead. Kubernetes versions 1.25 and newer ignore this annotation.
{{< /note >}}

### kubectl.kubernetes.io/last-applied-configuration

Type: Annotation

Example: _see following snippet_
```yaml
    kubectl.kubernetes.io/last-applied-configuration: >
      {"apiVersion":"apps/v1","kind":"Deployment","metadata":{"annotations":{},"name":"example","namespace":"default"},"spec":{"selector":{"matchLabels":{"app.kubernetes.io/name":foo}},"template":{"metadata":{"labels":{"app.kubernetes.io/name":"foo"}},"spec":{"containers":[{"image":"container-registry.example/foo-bar:1.42","name":"foo-bar","ports":[{"containerPort":42}]}]}}}}
```

Used on: all objects

The kubectl command line tool uses this annotation as a legacy mechanism
to track changes. That mechanism has been superseded by
[Server-side apply](/docs/reference/using-api/server-side-apply/).

### kubectl.kubernetes.io/restartedAt {#kubectl-k8s-io-restart-at}

Type: Annotation

Example: `kubectl.kubernetes.io/restartedAt: "2024-06-21T17:27:41Z"`

Used on: Deployment, ReplicaSet, StatefulSet, DaemonSet, Pod

This annotation contains the latest restart time of a resource (Deployment, ReplicaSet, StatefulSet or DaemonSet),
where kubectl triggered a rollout in order to force creation of new Pods.
The command `kubectl rollout restart <RESOURCE>` triggers a restart by patching the template
metadata of all the pods of resource with this annotation. In above example the latest restart time is shown as 21st June 2024 at 17:27:41 UTC.

You should not assume that this annotation represents the date / time of the most recent update;
a separate change could have been made since the last manually triggered rollout.

If you manually set this annotation on a Pod, nothing happens. The restarting side effect comes from
how workload management and Pod templating works.

### endpoints.kubernetes.io/over-capacity

Type: Annotation

Example: `endpoints.kubernetes.io/over-capacity:truncated`

Used on: Endpoints

The {{< glossary_tooltip text="control plane" term_id="control-plane" >}} adds this annotation to
an [Endpoints](/docs/concepts/services-networking/service/#endpoints) object if the associated
{{< glossary_tooltip term_id="service" >}} has more than 1000 backing endpoints.
The annotation indicates that the Endpoints object is over capacity and the number of endpoints
has been truncated to 1000.

If the number of backend endpoints falls below 1000, the control plane removes this annotation.

### endpoints.kubernetes.io/last-change-trigger-time

Type: Annotation

Example: `endpoints.kubernetes.io/last-change-trigger-time: "2023-07-20T04:45:21Z"`

Used on: Endpoints

This annotation set to an [Endpoints](/docs/concepts/services-networking/service/#endpoints) object that
represents the timestamp (The timestamp is stored in RFC 3339 date-time string format. For example, '2018-10-22T19:32:52.1Z'). This is timestamp
of the last change in some Pod or Service object, that triggered the change to the Endpoints object.

### control-plane.alpha.kubernetes.io/leader (deprecated) {#control-plane-alpha-kubernetes-io-leader}

Type: Annotation

Example: `control-plane.alpha.kubernetes.io/leader={"holderIdentity":"controller-0","leaseDurationSeconds":15,"acquireTime":"2023-01-19T13:12:57Z","renewTime":"2023-01-19T13:13:54Z","leaderTransitions":1}`

Used on: Endpoints

The {{< glossary_tooltip text="control plane" term_id="control-plane" >}} previously set annotation on
an [Endpoints](/docs/concepts/services-networking/service/#endpoints) object. This annotation provided
the following detail:

- Who is the current leader.
- The time when the current leadership was acquired.
- The duration of the lease (of the leadership) in seconds.
- The time the current lease (the current leadership) should be renewed.
- The number of leadership transitions that happened in the past.

Kubernetes now uses [Leases](/docs/concepts/architecture/leases/) to
manage leader assignment for the Kubernetes control plane.

### batch.kubernetes.io/job-tracking (deprecated) {#batch-kubernetes-io-job-tracking}

Type: Annotation

Example: `batch.kubernetes.io/job-tracking: ""`

Used on: Jobs

The presence of this annotation on a Job used to indicate that the control plane is
[tracking the Job status using finalizers](/docs/concepts/workloads/controllers/job/#job-tracking-with-finalizers).
Adding or removing this annotation no longer has an effect (Kubernetes v1.27 and later)
All Jobs are tracked with finalizers.

### job-name (deprecated) {#job-name}

Type: Label

Example: `job-name: "pi"`

Used on: Jobs and Pods controlled by Jobs

{{< note >}}
Starting from Kubernetes 1.27, this label is deprecated.
Kubernetes 1.27 and newer ignore this label and use the prefixed `job-name` label.
{{< /note >}}

### controller-uid (deprecated) {#controller-uid}

Type: Label

Example: `controller-uid: "$UID"`

Used on: Jobs and Pods controlled by Jobs

{{< note >}}
Starting from Kubernetes 1.27, this label is deprecated.
Kubernetes 1.27 and newer ignore this label and use the prefixed `controller-uid` label.
{{< /note >}}

### batch.kubernetes.io/job-name {#batchkubernetesio-job-name}

Type: Label

Example: `batch.kubernetes.io/job-name: "pi"`

Used on: Jobs and Pods controlled by Jobs

This label is used as a user-friendly way to get Pods corresponding to a Job.
The `job-name` comes from the `name` of the Job and allows for an easy way to
get Pods corresponding to the Job.

### batch.kubernetes.io/controller-uid {#batchkubernetesio-controller-uid}

Type: Label

Example: `batch.kubernetes.io/controller-uid: "$UID"`

Used on: Jobs and Pods controlled by Jobs

This label is used as a programmatic way to get all Pods corresponding to a Job.  
The `controller-uid` is a unique identifier that gets set in the `selector` field so the Job
controller can get all the corresponding Pods.

### scheduler.alpha.kubernetes.io/defaultTolerations {#scheduleralphakubernetesio-defaulttolerations}

Type: Annotation

Example: `scheduler.alpha.kubernetes.io/defaultTolerations: '[{"operator": "Equal", "value": "value1", "effect": "NoSchedule", "key": "dedicated-node"}]'`

Used on: Namespace

This annotation requires the [PodTolerationRestriction](/docs/reference/access-authn-authz/admission-controllers/#podtolerationrestriction)
admission controller to be enabled. This annotation key allows assigning tolerations to a
namespace and any new pods created in this namespace would get these tolerations added.

### scheduler.alpha.kubernetes.io/tolerationsWhitelist {#schedulerkubernetestolerations-whitelist}

Type: Annotation

Example: `scheduler.alpha.kubernetes.io/tolerationsWhitelist: '[{"operator": "Exists", "effect": "NoSchedule", "key": "dedicated-node"}]'`

Used on: Namespace

This annotation is only useful when the (Alpha)
[PodTolerationRestriction](/docs/reference/access-authn-authz/admission-controllers/#podtolerationrestriction)
admission controller is enabled. The annotation value is a JSON document that defines a list of
allowed tolerations for the namespace it annotates. When you create a Pod or modify its
tolerations, the API server checks the tolerations to see if they are mentioned in the allow list.
The pod is admitted only if the check succeeds.

### scheduler.alpha.kubernetes.io/preferAvoidPods (deprecated) {#scheduleralphakubernetesio-preferavoidpods}

Type: Annotation

Used on: Node

This annotation requires the [NodePreferAvoidPods scheduling plugin](/docs/reference/scheduling/config/#scheduling-plugins)
to be enabled. The plugin is deprecated since Kubernetes 1.22.
Use [Taints and Tolerations](/docs/concepts/scheduling-eviction/taint-and-toleration/) instead.

### node.kubernetes.io/not-ready

Type: Taint

Example: `node.kubernetes.io/not-ready: "NoExecute"`

Used on: Node

The Node controller detects whether a Node is ready by monitoring its health
and adds or removes this taint accordingly.

### node.kubernetes.io/unreachable

Type: Taint

Example: `node.kubernetes.io/unreachable: "NoExecute"`

Used on: Node

The Node controller adds the taint to a Node corresponding to the
[NodeCondition](/docs/concepts/architecture/nodes/#condition) `Ready` being `Unknown`.

### node.kubernetes.io/unschedulable

Type: Taint

Example: `node.kubernetes.io/unschedulable: "NoSchedule"`

Used on: Node

The taint will be added to a node when initializing the node to avoid race condition.

### node.kubernetes.io/memory-pressure

Type: Taint

Example: `node.kubernetes.io/memory-pressure: "NoSchedule"`

Used on: Node

The kubelet detects memory pressure based on `memory.available` and `allocatableMemory.available`
observed on a Node. The observed values are then compared to the corresponding thresholds that can
be set on the kubelet to determine if the Node condition and taint should be added/removed.

### node.kubernetes.io/disk-pressure

Type: Taint

Example: `node.kubernetes.io/disk-pressure :"NoSchedule"`

Used on: Node

The kubelet detects disk pressure based on `imagefs.available`, `imagefs.inodesFree`,
`nodefs.available` and `nodefs.inodesFree`(Linux only) observed on a Node.
The observed values are then compared to the corresponding thresholds that can be set on the
kubelet to determine if the Node condition and taint should be added/removed.

### node.kubernetes.io/network-unavailable

Type: Taint

Example: `node.kubernetes.io/network-unavailable: "NoSchedule"`

Used on: Node

This is initially set by the kubelet when the cloud provider used indicates a requirement for
additional network configuration. Only when the route on the cloud is configured properly will the
taint be removed by the cloud provider.

### node.kubernetes.io/pid-pressure

Type: Taint

Example: `node.kubernetes.io/pid-pressure: "NoSchedule"`

Used on: Node

The kubelet checks D-value of the size of `/proc/sys/kernel/pid_max` and the PIDs consumed by
Kubernetes on a node to get the number of available PIDs that referred to as the `pid.available`
metric. The metric is then compared to the corresponding threshold that can be set on the kubelet
to determine if the node condition and taint should be added/removed.

### node.kubernetes.io/out-of-service

Type: Taint

Example: `node.kubernetes.io/out-of-service:NoExecute`

Used on: Node

A user can manually add the taint to a Node marking it out-of-service.
If a Node is marked out-of-service with this taint, the Pods on the node 
will be forcefully deleted if there are no matching tolerations on it and
volume detach operations for the Pods terminating on the node will happen immediately.
This allows the Pods on the out-of-service node to recover quickly on a different node.

{{< caution >}}
Refer to [Non-graceful node shutdown](/docs/concepts/architecture/nodes/#non-graceful-node-shutdown)
for further details about when and how to use this taint.
{{< /caution >}}

### node.cloudprovider.kubernetes.io/uninitialized

Type: Taint

Example: `node.cloudprovider.kubernetes.io/uninitialized: "NoSchedule"`

Used on: Node

Sets this taint on a Node to mark it as unusable, when kubelet is started with the "external"
cloud provider, until a controller from the cloud-controller-manager initializes this Node, and
then removes the taint.

### node.cloudprovider.kubernetes.io/shutdown

Type: Taint

Example: `node.cloudprovider.kubernetes.io/shutdown: "NoSchedule"`

Used on: Node

If a Node is in a cloud provider specified shutdown state, the Node gets tainted accordingly
with `node.cloudprovider.kubernetes.io/shutdown` and the taint effect of `NoSchedule`.

### feature.node.kubernetes.io/*

Type: Label

Example: `feature.node.kubernetes.io/network-sriov.capable: "true"`

Used on: Node

These labels are used by the Node Feature Discovery (NFD) component to advertise
features on a node. All built-in labels use the `feature.node.kubernetes.io` label
namespace and have the format `feature.node.kubernetes.io/<feature-name>: "true"`.
NFD has many extension points for creating vendor and application-specific labels.
For details, see the [customization guide](https://kubernetes-sigs.github.io/node-feature-discovery/v0.12/usage/customization-guide).

### nfd.node.kubernetes.io/master.version

Type: Annotation

Example: `nfd.node.kubernetes.io/master.version: "v0.6.0"`

Used on: Node

For node(s) where the Node Feature Discovery (NFD)
[master](https://kubernetes-sigs.github.io/node-feature-discovery/stable/usage/nfd-master.html)
is scheduled, this annotation records the version of the NFD master.
It is used for informative use only.

### nfd.node.kubernetes.io/worker.version

Type: Annotation

Example: `nfd.node.kubernetes.io/worker.version: "v0.4.0"`

Used on: Nodes

This annotation records the version for a Node Feature Discovery's
[worker](https://kubernetes-sigs.github.io/node-feature-discovery/stable/usage/nfd-worker.html)
if there is one running on a node. It's used for informative use only.

### nfd.node.kubernetes.io/feature-labels

Type: Annotation

Example: `nfd.node.kubernetes.io/feature-labels: "cpu-cpuid.ADX,cpu-cpuid.AESNI,cpu-hardware_multithreading,kernel-version.full"`

Used on: Nodes

This annotation records a comma-separated list of node feature labels managed by
[Node Feature Discovery](https://kubernetes-sigs.github.io/node-feature-discovery/) (NFD).
NFD uses this for an internal mechanism. You should not edit this annotation yourself.

### nfd.node.kubernetes.io/extended-resources

Type: Annotation

Example: `nfd.node.kubernetes.io/extended-resources: "accelerator.acme.example/q500,example.com/coprocessor-fx5"`

Used on: Nodes

This annotation records a comma-separated list of
[extended resources](/docs/concepts/configuration/manage-resources-containers/#extended-resources)
managed by [Node Feature Discovery](https://kubernetes-sigs.github.io/node-feature-discovery/) (NFD).
NFD uses this for an internal mechanism. You should not edit this annotation yourself.

### nfd.node.kubernetes.io/node-name

Type: Label

Example: `nfd.node.kubernetes.io/node-name: node-1`

Used on: Nodes

It specifies which node the NodeFeature object is targeting.
Creators of NodeFeature objects must set this label and 
consumers of the objects are supposed to use the label for 
filtering features designated for a certain node.

{{< note >}}
These Node Feature Discovery (NFD) labels or annotations only apply to 
the nodes where NFD is running. To learn more about NFD and 
its components go to its official [documentation](https://kubernetes-sigs.github.io/node-feature-discovery/stable/get-started/).
{{< /note >}}

### service.beta.kubernetes.io/aws-load-balancer-access-log-emit-interval (beta) {#service-beta-kubernetes-io-aws-load-balancer-access-log-emit-interval}

Example: `service.beta.kubernetes.io/aws-load-balancer-access-log-emit-interval: "5"`

Used on: Service

The cloud controller manager integration with AWS elastic load balancing configures
the load balancer for a Service based on this annotation. The value determines
how often the load balancer writes log entries. For example, if you set the value
to 5, the log writes occur 5 seconds apart.

### service.beta.kubernetes.io/aws-load-balancer-access-log-enabled (beta) {#service-beta-kubernetes-io-aws-load-balancer-access-log-enabled}

Example: `service.beta.kubernetes.io/aws-load-balancer-access-log-enabled: "false"`

Used on: Service

The cloud controller manager integration with AWS elastic load balancing configures
the load balancer for a Service based on this annotation. Access logging is enabled
if you set the annotation to "true".

### service.beta.kubernetes.io/aws-load-balancer-access-log-s3-bucket-name (beta) {#service-beta-kubernetes-io-aws-load-balancer-access-log-s3-bucket-name}

Example: `service.beta.kubernetes.io/aws-load-balancer-access-log-enabled: example`

Used on: Service

The cloud controller manager integration with AWS elastic load balancing configures
the load balancer for a Service based on this annotation. The load balancer
writes logs to an S3 bucket with the name you specify.

### service.beta.kubernetes.io/aws-load-balancer-access-log-s3-bucket-prefix (beta) {#service-beta-kubernetes-io-aws-load-balancer-access-log-s3-bucket-prefix}

Example: `service.beta.kubernetes.io/aws-load-balancer-access-log-enabled: "/example"`

Used on: Service

The cloud controller manager integration with AWS elastic load balancing configures
the load balancer for a Service based on this annotation. The load balancer
writes log objects with the prefix that you specify.

### service.beta.kubernetes.io/aws-load-balancer-additional-resource-tags (beta) {#service-beta-kubernetes-io-aws-load-balancer-additional-resource-tags}

Example: `service.beta.kubernetes.io/aws-load-balancer-additional-resource-tags: "Environment=demo,Project=example"`

Used on: Service

The cloud controller manager integration with AWS elastic load balancing configures
tags (an AWS concept) for a load balancer based on the comma-separated key/value
pairs in the value of this annotation.

### service.beta.kubernetes.io/aws-load-balancer-alpn-policy (beta) {#service-beta-kubernetes-io-aws-load-balancer-alpn-policy}

Example: `service.beta.kubernetes.io/aws-load-balancer-alpn-policy: HTTP2Optional`

Used on: Service

The [AWS load balancer controller](https://kubernetes-sigs.github.io/aws-load-balancer-controller/)
uses this annotation.
See [annotations](https://kubernetes-sigs.github.io/aws-load-balancer-controller/latest/guide/service/annotations/)
in the AWS load balancer controller documentation.

### service.beta.kubernetes.io/aws-load-balancer-attributes (beta) {#service-beta-kubernetes-io-aws-load-balancer-attributes}

Example: `service.beta.kubernetes.io/aws-load-balancer-attributes: "deletion_protection.enabled=true"`

Used on: Service

The [AWS load balancer controller](https://kubernetes-sigs.github.io/aws-load-balancer-controller/)
uses this annotation.
See [annotations](https://kubernetes-sigs.github.io/aws-load-balancer-controller/latest/guide/service/annotations/)
in the AWS load balancer controller documentation.

### service.beta.kubernetes.io/aws-load-balancer-backend-protocol (beta) {#service-beta-kubernetes-io-aws-load-balancer-backend-protocol}

Example: `service.beta.kubernetes.io/aws-load-balancer-backend-protocol: tcp`

Used on: Service

The cloud controller manager integration with AWS elastic load balancing configures
the load balancer listener based on the value of this annotation.

### service.beta.kubernetes.io/aws-load-balancer-connection-draining-enabled (beta) {#service-beta-kubernetes-io-aws-load-balancer-connection-draining-enabled}

Example: `service.beta.kubernetes.io/aws-load-balancer-connection-draining-enabled: "false"`

Used on: Service

The cloud controller manager integration with AWS elastic load balancing configures
the load balancer based on this annotation. The load balancer's connection draining
setting depends on the value you set.

### service.beta.kubernetes.io/aws-load-balancer-connection-draining-timeout (beta) {#service-beta-kubernetes-io-aws-load-balancer-connection-draining-timeout}

Example: `service.beta.kubernetes.io/aws-load-balancer-connection-draining-timeout: "60"`

Used on: Service

If you configure [connection draining](#service-beta-kubernetes-io-aws-load-balancer-connection-draining-enabled)
for a Service of `type: LoadBalancer`, and you use the AWS cloud, the integration configures
the draining period based on this annotation. The value you set determines the draining
timeout in seconds.

### service.beta.kubernetes.io/aws-load-balancer-ip-address-type (beta) {#service-beta-kubernetes-io-aws-load-balancer-ip-address-type}

Example: `service.beta.kubernetes.io/aws-load-balancer-ip-address-type: ipv4`

Used on: Service

The [AWS load balancer controller](https://kubernetes-sigs.github.io/aws-load-balancer-controller/)
uses this annotation.
See [annotations](https://kubernetes-sigs.github.io/aws-load-balancer-controller/latest/guide/service/annotations/)
in the AWS load balancer controller documentation.

### service.beta.kubernetes.io/aws-load-balancer-connection-idle-timeout (beta) {#service-beta-kubernetes-io-aws-load-balancer-connection-idle-timeout}

Example: `service.beta.kubernetes.io/aws-load-balancer-connection-idle-timeout: "60"`

Used on: Service

The cloud controller manager integration with AWS elastic load balancing configures
a load balancer based on this annotation. The load balancer has a configured idle
timeout period (in seconds) that applies to its connections. If no data has been
sent or received by the time that the idle timeout period elapses, the load balancer
closes the connection.

### service.beta.kubernetes.io/aws-load-balancer-cross-zone-load-balancing-enabled (beta) {#service-beta-kubernetes-io-aws-load-balancer-cross-zone-load-balancing-enabled}

Example: `service.beta.kubernetes.io/aws-load-balancer-cross-zone-load-balancing-enabled: "true"`

Used on: Service

The cloud controller manager integration with AWS elastic load balancing configures
a load balancer based on this annotation. If you set this annotation to "true",
each load balancer node distributes requests evenly across the registered targets
in all enabled [availability zones](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-regions-availability-zones.html#concepts-availability-zones).
If you disable cross-zone load balancing, each load balancer node distributes requests
evenly across the registered targets in its availability zone only.

### service.beta.kubernetes.io/aws-load-balancer-eip-allocations (beta) {#service-beta-kubernetes-io-aws-load-balancer-eip-allocations}

Example: `service.beta.kubernetes.io/aws-load-balancer-eip-allocations: "eipalloc-01bcdef23bcdef456,eipalloc-def1234abc4567890"`

Used on: Service

The cloud controller manager integration with AWS elastic load balancing configures
a load balancer based on this annotation. The value is a comma-separated list
of elastic IP address allocation IDs.

This annotation is only relevant for Services of `type: LoadBalancer`, where
the load balancer is an AWS Network Load Balancer.

### service.beta.kubernetes.io/aws-load-balancer-extra-security-groups (beta) {#service-beta-kubernetes-io-aws-load-balancer-extra-security-groups}

Example: `service.beta.kubernetes.io/aws-load-balancer-extra-security-groups: "sg-12abcd3456,sg-34dcba6543"`

Used on: Service

The cloud controller manager integration with AWS elastic load balancing configures
a load balancer based on this annotation. The annotation value is a comma-separated
list of extra AWS VPC security groups to configure for the load balancer.

### service.beta.kubernetes.io/aws-load-balancer-healthcheck-healthy-threshold (beta) {#service-beta-kubernetes-io-aws-load-balancer-healthcheck-healthy-threshold}

Example: `service.beta.kubernetes.io/aws-load-balancer-healthcheck-healthy-threshold: "3"`

Used on: Service

The cloud controller manager integration with AWS elastic load balancing configures
a load balancer based on this annotation. The annotation value specifies the number of
successive successful health checks required for a backend to be considered healthy
for traffic.

### service.beta.kubernetes.io/aws-load-balancer-healthcheck-interval (beta) {#service-beta-kubernetes-io-aws-load-balancer-healthcheck-interval}

Example: `service.beta.kubernetes.io/aws-load-balancer-healthcheck-interval: "30"`

Used on: Service

The cloud controller manager integration with AWS elastic load balancing configures
a load balancer based on this annotation. The annotation value specifies the interval,
in seconds, between health check probes made by the load balancer.

### service.beta.kubernetes.io/aws-load-balancer-healthcheck-path (beta) {#service-beta-kubernetes-io-aws-load-balancer-healthcheck-papth}

Example: `service.beta.kubernetes.io/aws-load-balancer-healthcheck-path: /healthcheck`

Used on: Service

The cloud controller manager integration with AWS elastic load balancing configures
a load balancer based on this annotation. The annotation value determines the
path part of the URL that is used for HTTP health checks.

### service.beta.kubernetes.io/aws-load-balancer-healthcheck-port (beta) {#service-beta-kubernetes-io-aws-load-balancer-healthcheck-port}

Example: `service.beta.kubernetes.io/aws-load-balancer-healthcheck-port: "24"`

Used on: Service

The cloud controller manager integration with AWS elastic load balancing configures
a load balancer based on this annotation. The annotation value determines which
port the load balancer connects to when performing health checks.

### service.beta.kubernetes.io/aws-load-balancer-healthcheck-protocol (beta) {#service-beta-kubernetes-io-aws-load-balancer-healthcheck-protocol}

Example: `service.beta.kubernetes.io/aws-load-balancer-healthcheck-protocol: TCP`

Used on: Service

The cloud controller manager integration with AWS elastic load balancing configures
a load balancer based on this annotation. The annotation value determines how the
load balancer checks the health of backend targets.

### service.beta.kubernetes.io/aws-load-balancer-healthcheck-timeout (beta) {#service-beta-kubernetes-io-aws-load-balancer-healthcheck-timeout}

Example: `service.beta.kubernetes.io/aws-load-balancer-healthcheck-timeout: "3"`

Used on: Service

The cloud controller manager integration with AWS elastic load balancing configures
a load balancer based on this annotation. The annotation value specifies the number
of seconds before a probe that hasn't yet succeeded is automatically treated as
having failed.

### service.beta.kubernetes.io/aws-load-balancer-healthcheck-unhealthy-threshold (beta) {#service-beta-kubernetes-io-aws-load-balancer-healthcheck-unhealthy-threshold}

Example: `service.beta.kubernetes.io/aws-load-balancer-healthcheck-unhealthy-threshold: "3"`

Used on: Service

The cloud controller manager integration with AWS elastic load balancing configures
a load balancer based on this annotation. The annotation value specifies the number of
successive unsuccessful health checks required for a backend to be considered unhealthy
for traffic.

### service.beta.kubernetes.io/aws-load-balancer-internal (beta) {#service-beta-kubernetes-io-aws-load-balancer-internal}

Example: `service.beta.kubernetes.io/aws-load-balancer-internal: "true"`

Used on: Service

The cloud controller manager integration with AWS elastic load balancing configures
a load balancer based on this annotation. When you set this annotation to "true",
the integration configures an internal load balancer.

If you use the [AWS load balancer controller](https://kubernetes-sigs.github.io/aws-load-balancer-controller/),
see [`service.beta.kubernetes.io/aws-load-balancer-scheme`](#service-beta-kubernetes-io-aws-load-balancer-scheme).

### service.beta.kubernetes.io/aws-load-balancer-manage-backend-security-group-rules (beta) {#service-beta-kubernetes-io-aws-load-balancer-manage-backend-security-group-rules}

Example: `service.beta.kubernetes.io/aws-load-balancer-manage-backend-security-group-rules: "true"`

Used on: Service

The [AWS load balancer controller](https://kubernetes-sigs.github.io/aws-load-balancer-controller/)
uses this annotation.
See [annotations](https://kubernetes-sigs.github.io/aws-load-balancer-controller/latest/guide/service/annotations/)
in the AWS load balancer controller documentation.

### service.beta.kubernetes.io/aws-load-balancer-name (beta) {#service-beta-kubernetes-io-aws-load-balancer-name}

Example: `service.beta.kubernetes.io/aws-load-balancer-name: my-elb`

Used on: Service

If you set this annotation on a Service, and you also annotate that Service with
`service.beta.kubernetes.io/aws-load-balancer-type: "external"`, and you use the
[AWS load balancer controller](https://kubernetes-sigs.github.io/aws-load-balancer-controller/)
in your cluster, then the AWS load balancer controller sets the name of that load
balancer to the value you set for _this_ annotation.

See [annotations](https://kubernetes-sigs.github.io/aws-load-balancer-controller/latest/guide/service/annotations/)
in the AWS load balancer controller documentation.

### service.beta.kubernetes.io/aws-load-balancer-nlb-target-type (beta) {#service-beta-kubernetes-io-aws-load-balancer-nlb-target-type}

Example: `service.beta.kubernetes.io/aws-load-balancer-nlb-target-type: "true"`

Used on: Service

The [AWS load balancer controller](https://kubernetes-sigs.github.io/aws-load-balancer-controller/)
uses this annotation.
See [annotations](https://kubernetes-sigs.github.io/aws-load-balancer-controller/latest/guide/service/annotations/)
in the AWS load balancer controller documentation.

### service.beta.kubernetes.io/aws-load-balancer-private-ipv4-addresses (beta) {#service-beta-kubernetes-io-aws-load-balancer-private-ipv4-addresses}

Example: `service.beta.kubernetes.io/aws-load-balancer-private-ipv4-addresses: "198.51.100.0,198.51.100.64"`

Used on: Service

The [AWS load balancer controller](https://kubernetes-sigs.github.io/aws-load-balancer-controller/)
uses this annotation.
See [annotations](https://kubernetes-sigs.github.io/aws-load-balancer-controller/latest/guide/service/annotations/)
in the AWS load balancer controller documentation.

### service.beta.kubernetes.io/aws-load-balancer-proxy-protocol (beta) {#service-beta-kubernetes-io-aws-load-balancer-proxy-protocol}

Example: `service.beta.kubernetes.io/aws-load-balancer-proxy-protocol: "*"`

Used on: Service

The official Kubernetes integration with AWS elastic load balancing configures
a load balancer based on this annotation. The only permitted value is `"*"`,
which indicates that the load balancer should wrap TCP connections to the backend
Pod with the PROXY protocol.

### service.beta.kubernetes.io/aws-load-balancer-scheme (beta) {#service-beta-kubernetes-io-aws-load-balancer-scheme}

Example: `service.beta.kubernetes.io/aws-load-balancer-scheme: internal`

Used on: Service

The [AWS load balancer controller](https://kubernetes-sigs.github.io/aws-load-balancer-controller/)
uses this annotation.
See [annotations](https://kubernetes-sigs.github.io/aws-load-balancer-controller/latest/guide/service/annotations/)
in the AWS load balancer controller documentation.

### service.beta.kubernetes.io/aws-load-balancer-security-groups (deprecated) {#service-beta-kubernetes-io-aws-load-balancer-security-groups}

Example: `service.beta.kubernetes.io/aws-load-balancer-security-groups: "sg-53fae93f,sg-8725gr62r"`

Used on: Service

The AWS load balancer controller uses this annotation to specify a comma separated list
of security groups you want to attach to an AWS load balancer. Both name and ID of security
are supported where name matches a `Name` tag, not the `groupName` attribute.

When this annotation is added to a Service, the load-balancer controller attaches the security groups
referenced by the annotation to the load balancer. If you omit this annotation, the AWS load balancer
controller automatically creates a new security group and attaches it to the load balancer.

{{< note >}}
Kubernetes v1.27 and later do not directly set or read this annotation. However, the AWS
load balancer controller (part of the Kubernetes project) does still use the
`service.beta.kubernetes.io/aws-load-balancer-security-groups` annotation.
{{< /note >}}

### service.beta.kubernetes.io/load-balancer-source-ranges (deprecated) {#service-beta-kubernetes-io-load-balancer-source-ranges}

Example: `service.beta.kubernetes.io/load-balancer-source-ranges: "192.0.2.0/25"`

Used on: Service

The [AWS load balancer controller](https://kubernetes-sigs.github.io/aws-load-balancer-controller/)
uses this annotation. You should set `.spec.loadBalancerSourceRanges` for the Service instead.

### service.beta.kubernetes.io/aws-load-balancer-ssl-cert (beta) {#service-beta-kubernetes-io-aws-load-balancer-ssl-cert}

Example: `service.beta.kubernetes.io/aws-load-balancer-ssl-cert: "arn:aws:acm:us-east-1:123456789012:certificate/12345678-1234-1234-1234-123456789012"`

Used on: Service

The official integration with AWS elastic load balancing configures TLS for a Service of
`type: LoadBalancer` based on this annotation. The value of the annotation is the
AWS Resource Name (ARN) of the X.509 certificate that the load balancer listener should
use.

(The TLS protocol is based on an older technology that abbreviates to SSL.)

### service.beta.kubernetes.io/aws-load-balancer-ssl-negotiation-policy (beta) {#service-beta-kubernetes-io-aws-load-balancer-ssl-negotiation-policy}

Example: `service.beta.kubernetes.io/aws-load-balancer-ssl-negotiation-policy: ELBSecurityPolicy-TLS-1-2-2017-01`

The official integration with AWS elastic load balancing configures TLS for a Service of
`type: LoadBalancer` based on this annotation. The value of the annotation is the name
of an AWS policy for negotiating TLS with a client peer.

### service.beta.kubernetes.io/aws-load-balancer-ssl-ports (beta) {#service-beta-kubernetes-io-aws-load-balancer-ssl-ports}

Example: `service.beta.kubernetes.io/aws-load-balancer-ssl-ports: "*"`

The official integration with AWS elastic load balancing configures TLS for a Service of
`type: LoadBalancer` based on this annotation. The value of the annotation is either `"*"`,
which means that all the load balancer's ports should use TLS, or it is a comma separated
list of port numbers.

### service.beta.kubernetes.io/aws-load-balancer-subnets (beta) {#service-beta-kubernetes-io-aws-load-balancer-subnets}

Example: `service.beta.kubernetes.io/aws-load-balancer-subnets: "private-a,private-b"`

Kubernetes' official integration with AWS uses this annotation to configure a
load balancer and determine in which AWS availability zones to deploy the managed
load balancing service. The value is either a comma separated list of subnet names, or a
comma separated list of subnet IDs.

### service.beta.kubernetes.io/aws-load-balancer-target-group-attributes (beta) {#service-beta-kubernetes-io-aws-load-balancer-target-group-attributes}

Example: `service.beta.kubernetes.io/aws-load-balancer-target-group-attributes: "stickiness.enabled=true,stickiness.type=source_ip"`

Used on: Service

The [AWS load balancer controller](https://kubernetes-sigs.github.io/aws-load-balancer-controller/)
uses this annotation.
See [annotations](https://kubernetes-sigs.github.io/aws-load-balancer-controller/latest/guide/service/annotations/)
in the AWS load balancer controller documentation.

### service.beta.kubernetes.io/aws-load-balancer-target-node-labels (beta) {#service-beta-kubernetes-io-aws-target-node-labels}

Example: `service.beta.kubernetes.io/aws-load-balancer-target-node-labels: "kubernetes.io/os=Linux,topology.kubernetes.io/region=us-east-2"`

Kubernetes' official integration with AWS uses this annotation to determine which
nodes in your cluster should be considered as valid targets for the load balancer.

### service.beta.kubernetes.io/aws-load-balancer-type (beta) {#service-beta-kubernetes-io-aws-load-balancer-type}

Example: `service.beta.kubernetes.io/aws-load-balancer-type: external`

Kubernetes' official integrations with AWS use this annotation to determine
whether the AWS cloud provider integration should manage a Service of
`type: LoadBalancer`.

There are two permitted values:

`nlb`
: the cloud controller manager configures a Network Load Balancer

`external`
: the cloud controller manager does not configure any load balancer

If you deploy a Service of `type: LoadBalancer` on AWS, and you don't set any
`service.beta.kubernetes.io/aws-load-balancer-type` annotation,
the AWS integration deploys a classic Elastic Load Balancer. This behavior,
with no annotation present, is the default unless you specify otherwise.

When you set this annotation to `external` on a Service of `type: LoadBalancer`,
and your cluster has a working deployment of the AWS Load Balancer controller,
then the AWS Load Balancer controller attempts to deploy a load balancer based
on the Service specification.

{{< caution >}}
Do not modify or add the `service.beta.kubernetes.io/aws-load-balancer-type` annotation
on an existing Service object. See the AWS documentation on this topic for more
details.
{{< /caution >}}

### service.beta.kubernetes.io/azure-load-balancer-disable-tcp-reset (deprecated) {#service-beta-kubernetes-azure-load-balancer-disble-tcp-reset}

Example: `service.beta.kubernetes.io/azure-load-balancer-disable-tcp-reset: "false"`

Used on: Service

This annotation only works for Azure standard load balancer backed service.
This annotation is used on the Service to specify whether the load balancer
should disable or enable TCP reset on idle timeout. If enabled, it helps
applications to behave more predictably, to detect the termination of a connection,
remove expired connections and initiate new connections. 
You can set the value to be either true or false.

See [Load Balancer TCP Reset](https://learn.microsoft.com/en-gb/azure/load-balancer/load-balancer-tcp-reset) for more information.

{{< note >}} 
This annotation is deprecated.
{{< /note >}}

### pod-security.kubernetes.io/enforce

Type: Label

Example: `pod-security.kubernetes.io/enforce: "baseline"`

Used on: Namespace

Value **must** be one of `privileged`, `baseline`, or `restricted` which correspond to
[Pod Security Standard](/docs/concepts/security/pod-security-standards) levels.
Specifically, the `enforce` label _prohibits_ the creation of any Pod in the labeled
Namespace which does not meet the requirements outlined in the indicated level.

See [Enforcing Pod Security at the Namespace Level](/docs/concepts/security/pod-security-admission)
for more information.

### pod-security.kubernetes.io/enforce-version

Type: Label

Example: `pod-security.kubernetes.io/enforce-version: "{{< skew currentVersion >}}"`

Used on: Namespace

Value **must** be `latest` or a valid Kubernetes version in the format `v<major>.<minor>`.
This determines the version of the
[Pod Security Standard](/docs/concepts/security/pod-security-standards)
policies to apply when validating a Pod.

See [Enforcing Pod Security at the Namespace Level](/docs/concepts/security/pod-security-admission)
for more information.

### pod-security.kubernetes.io/audit

Type: Label

Example: `pod-security.kubernetes.io/audit: "baseline"`

Used on: Namespace

Value **must** be one of `privileged`, `baseline`, or `restricted` which correspond to
[Pod Security Standard](/docs/concepts/security/pod-security-standards) levels.
Specifically, the `audit` label does not prevent the creation of a Pod in the labeled
Namespace which does not meet the requirements outlined in the indicated level,
but adds an this annotation to the Pod.

See [Enforcing Pod Security at the Namespace Level](/docs/concepts/security/pod-security-admission)
for more information.

### pod-security.kubernetes.io/audit-version

Type: Label

Example: `pod-security.kubernetes.io/audit-version: "{{< skew currentVersion >}}"`

Used on: Namespace

Value **must** be `latest` or a valid Kubernetes version in the format `v<major>.<minor>`.
This determines the version of the
[Pod Security Standard](/docs/concepts/security/pod-security-standards)
policies to apply when validating a Pod.

See [Enforcing Pod Security at the Namespace Level](/docs/concepts/security/pod-security-admission)
for more information.

### pod-security.kubernetes.io/warn

Type: Label

Example: `pod-security.kubernetes.io/warn: "baseline"`

Used on: Namespace

Value **must** be one of `privileged`, `baseline`, or `restricted` which correspond to
[Pod Security Standard](/docs/concepts/security/pod-security-standards) levels.
Specifically, the `warn` label does not prevent the creation of a Pod in the labeled
Namespace which does not meet the requirements outlined in the indicated level,
but returns a warning to the user after doing so.
Note that warnings are also displayed when creating or updating objects that contain
Pod templates, such as Deployments, Jobs, StatefulSets, etc.

See [Enforcing Pod Security at the Namespace Level](/docs/concepts/security/pod-security-admission)
for more information.

### pod-security.kubernetes.io/warn-version

Type: Label

Example: `pod-security.kubernetes.io/warn-version: "{{< skew currentVersion >}}"`

Used on: Namespace

Value **must** be `latest` or a valid Kubernetes version in the format `v<major>.<minor>`.
This determines the version of the [Pod Security Standard](/docs/concepts/security/pod-security-standards)
policies to apply when validating a submitted Pod.
Note that warnings are also displayed when creating or updating objects that contain
Pod templates, such as Deployments, Jobs, StatefulSets, etc.

See [Enforcing Pod Security at the Namespace Level](/docs/concepts/security/pod-security-admission)
for more information.

### rbac.authorization.kubernetes.io/autoupdate

Type: Annotation

Example: `rbac.authorization.kubernetes.io/autoupdate: "false"`

Used on: ClusterRole, ClusterRoleBinding, Role, RoleBinding

When this annotation is set to `"true"` on default RBAC objects created by the API server,
they are automatically updated at server start to add missing permissions and subjects
(extra permissions and subjects are left in place).
To prevent autoupdating a particular role or rolebinding, set this annotation to `"false"`.
If you create your own RBAC objects and set this annotation to `"false"`, `kubectl auth reconcile`
(which allows reconciling arbitrary RBAC objects in a {{< glossary_tooltip text="manifest" term_id="manifest" >}})
respects this annotation and does not automatically add missing permissions and subjects.

### kubernetes.io/psp (deprecated) {#kubernetes-io-psp}

Type: Annotation

Example: `kubernetes.io/psp: restricted`

Used on: Pod

This annotation was only relevant if you were using
[PodSecurityPolicy](/docs/concepts/security/pod-security-policy/) objects.
Kubernetes v{{< skew currentVersion >}} does not support the PodSecurityPolicy API.

When the PodSecurityPolicy admission controller admitted a Pod, the admission controller
modified the Pod to have this annotation.
The value of the annotation was the name of the PodSecurityPolicy that was used for validation.

### seccomp.security.alpha.kubernetes.io/pod (non-functional) {#seccomp-security-alpha-kubernetes-io-pod}

Type: Annotation

Used on: Pod

Kubernetes before v1.25 allowed you to configure seccomp behavior using this annotation.
See [Restrict a Container's Syscalls with seccomp](/docs/tutorials/security/seccomp/) to
learn the supported way to specify seccomp restrictions for a Pod.

### container.seccomp.security.alpha.kubernetes.io/[NAME] (non-functional) {#container-seccomp-security-alpha-kubernetes-io}

Type: Annotation

Used on: Pod

Kubernetes before v1.25 allowed you to configure seccomp behavior using this annotation.
See [Restrict a Container's Syscalls with seccomp](/docs/tutorials/security/seccomp/) to
learn the supported way to specify seccomp restrictions for a Pod.

### snapshot.storage.kubernetes.io/allow-volume-mode-change

Type: Annotation

Example: `snapshot.storage.kubernetes.io/allow-volume-mode-change: "true"`

Used on: VolumeSnapshotContent

Value can either be `true` or `false`. This determines whether a user can modify
the mode of the source volume when a PersistentVolumeClaim is being created from
a VolumeSnapshot.

Refer to [Converting the volume mode of a Snapshot](/docs/concepts/storage/volume-snapshots/#convert-volume-mode)
and the [Kubernetes CSI Developer Documentation](https://kubernetes-csi.github.io/docs/)
for more information.

### scheduler.alpha.kubernetes.io/critical-pod (deprecated)

Type: Annotation

Example: `scheduler.alpha.kubernetes.io/critical-pod: ""`

Used on: Pod

This annotation lets Kubernetes control plane know about a Pod being a critical Pod
so that the descheduler will not remove this Pod.

{{< note >}}
Starting in v1.16, this annotation was removed in favor of
[Pod Priority](/docs/concepts/scheduling-eviction/pod-priority-preemption/).
{{< /note >}}

### jobset.sigs.k8s.io/jobset-name

Type: Label, Annotation

Example:  `jobset.sigs.k8s.io/jobset-name: "my-jobset"`

Used on: Jobs, Pods

This label/annotation is used to store the name of the JobSet that a Job or Pod belongs to.
[JobSet](https://jobset.sigs.k8s.io) is an extension API that you can deploy into your Kubernetes cluster.

### jobset.sigs.k8s.io/replicatedjob-replicas

Type: Label, Annotation

Example: `jobset.sigs.k8s.io/replicatedjob-replicas: "5"`

Used on: Jobs, Pods

This label/annotation specifies the number of replicas for a ReplicatedJob.

### jobset.sigs.k8s.io/replicatedjob-name

Type: Label, Annotation

Example: `jobset.sigs.k8s.io/replicatedjob-name: "my-replicatedjob"`

Used on: Jobs, Pods

This label or annotation stores the name of the replicated job that this Job or Pod is part of.

### jobset.sigs.k8s.io/job-index

Type: Label, Annotation

Example: `jobset.sigs.k8s.io/job-index: "0"`

Used on: Jobs, Pods

This label/annotation is set by the JobSet controller on child Jobs and Pods. It contains the index of the Job replica within its parent ReplicatedJob.

### jobset.sigs.k8s.io/job-key

Type: Label, Annotation

Example: `jobset.sigs.k8s.io/job-key: "0f1e93893c4cb372080804ddb9153093cb0d20cefdd37f653e739c232d363feb"`

Used on: Jobs, Pods

The JobSet controller sets this label (and also an annotation with the same key)  on child Jobs and
Pods of a JobSet. The value is the SHA256 hash of the namespaced Job name.

### alpha.jobset.sigs.k8s.io/exclusive-topology

Type: Annotation

Example: `alpha.jobset.sigs.k8s.io/exclusive-topology: "zone"`

Used on: JobSets, Jobs

You can set this label/annotation on a [JobSet](https://jobset.sigs.k8s.io) to ensure exclusive Job
placement per topology group. You can also define this label or annotation on a replicated job
template. Read the documentation for JobSet to learn more.

### alpha.jobset.sigs.k8s.io/node-selector

Type: Annotation

Example: `alpha.jobset.sigs.k8s.io/node-selector: "true"`

Used on: Jobs, Pods

This label/annotation can be applied to a JobSet. When it's set, the JobSet controller modifies the Jobs and their corresponding Pods by adding node selectors and tolerations. This ensures exclusive job placement per topology domain, restricting the scheduling of these Pods to specific nodes based on the strategy.

### alpha.jobset.sigs.k8s.io/namespaced-job

Type: Label

Example: `alpha.jobset.sigs.k8s.io/namespaced-job: "default_myjobset-replicatedjob-0"`

Used on: Nodes

This label is either set manually or automatically (for example, a cluster autoscaler) on the nodes. When `alpha.jobset.sigs.k8s.io/node-selector` is set to  `"true"`, the  JobSet controller adds a nodeSelector to this node label (along with the toleration to the taint `alpha.jobset.sigs.k8s.io/no-schedule` disucssed next).

### alpha.jobset.sigs.k8s.io/no-schedule

Type: Taint

Example: `alpha.jobset.sigs.k8s.io/no-schedule: "NoSchedule"`

Used on: Nodes

This taint is either set manually or automatically (for example, a cluster autoscaler) on the nodes. When `alpha.jobset.sigs.k8s.io/node-selector` is set to  `"true"`, the  JobSet controller adds a toleration to this node taint (along with the node selector to the label `alpha.jobset.sigs.k8s.io/namespaced-job` disucssed previously).

### jobset.sigs.k8s.io/coordinator

Type: Annotation, Label

Example: `jobset.sigs.k8s.io/coordinator: "myjobset-workers-0-0.headless-svc"`

Used on: Jobs, Pods

This annotation/label is used on Jobs and Pods to store a stable network endpoint where the coordinator
pod can be reached if the [JobSet](https://jobset.sigs.k8s.io) spec defines the `.spec.coordinator` field.

## Annotations used for audit

<!-- sorted by annotation -->
- [`authorization.k8s.io/decision`](/docs/reference/labels-annotations-taints/audit-annotations/#authorization-k8s-io-decision)
- [`authorization.k8s.io/reason`](/docs/reference/labels-annotations-taints/audit-annotations/#authorization-k8s-io-reason)
- [`insecure-sha1.invalid-cert.kubernetes.io/$hostname`](/docs/reference/labels-annotations-taints/audit-annotations/#insecure-sha1-invalid-cert-kubernetes-io-hostname)
- [`missing-san.invalid-cert.kubernetes.io/$hostname`](/docs/reference/labels-annotations-taints/audit-annotations/#missing-san-invalid-cert-kubernetes-io-hostname)
- [`pod-security.kubernetes.io/audit-violations`](/docs/reference/labels-annotations-taints/audit-annotations/#pod-security-kubernetes-io-audit-violations)
- [`pod-security.kubernetes.io/enforce-policy`](/docs/reference/labels-annotations-taints/audit-annotations/#pod-security-kubernetes-io-enforce-policy)
- [`pod-security.kubernetes.io/exempt`](/docs/reference/labels-annotations-taints/audit-annotations/#pod-security-kubernetes-io-exempt)
- [`validation.policy.admission.k8s.io/validation_failure`](/docs/reference/labels-annotations-taints/audit-annotations/#validation-policy-admission-k8s-io-validation-failure)
  
See more details on [Audit Annotations](/docs/reference/labels-annotations-taints/audit-annotations/).

## kubeadm

### kubeadm.alpha.kubernetes.io/cri-socket

Type: Annotation

Example: `kubeadm.alpha.kubernetes.io/cri-socket: unix:///run/containerd/container.sock`

Used on: Node

Annotation that kubeadm uses to preserve the CRI socket information given to kubeadm at
`init`/`join` time for later use. kubeadm annotates the Node object with this information.
The annotation remains "alpha", since ideally this should be a field in KubeletConfiguration
instead.

### kubeadm.kubernetes.io/etcd.advertise-client-urls

Type: Annotation

Example: `kubeadm.kubernetes.io/etcd.advertise-client-urls: https://172.17.0.18:2379`

Used on: Pod

Annotation that kubeadm places on locally managed etcd Pods to keep track of
a list of URLs where etcd clients should connect to.
This is used mainly for etcd cluster health check purposes.

### kubeadm.kubernetes.io/kube-apiserver.advertise-address.endpoint

Type: Annotation

Example: `kubeadm.kubernetes.io/kube-apiserver.advertise-address.endpoint: https://172.17.0.18:6443`

Used on: Pod

Annotation that kubeadm places on locally managed `kube-apiserver` Pods to keep track
of the exposed advertise address/port endpoint for that API server instance.

### kubeadm.kubernetes.io/component-config.hash

Type: Annotation

Example: `kubeadm.kubernetes.io/component-config.hash: 2c26b46b68ffc68ff99b453c1d30413413422d706483bfa0f98a5e886266e7ae`

Used on: ConfigMap

Annotation that kubeadm places on ConfigMaps that it manages for configuring components.
It contains a hash (SHA-256) used to determine if the user has applied settings different
from the kubeadm defaults for a particular component.

### node-role.kubernetes.io/control-plane

Type: Label

Used on: Node

A marker label to indicate that the node is used to run control plane components.
The kubeadm tool applies this label to the control plane nodes that it manages.
Other cluster management tools typically also set this taint.

You can label control plane nodes with this label to make it easier to schedule Pods
only onto these nodes, or to avoid running Pods on the control plane.
If this label is set, the [EndpointSlice controller](/docs/concepts/services-networking/topology-aware-routing/#implementation-control-plane)
ignores that node while calculating Topology Aware Hints.

### node-role.kubernetes.io/*

Type: Label

Example: `node-role.kubernetes.io/gpu: gpu`

Used on: Node

This optional label is applied to a node when you want to mark a node role. 
The node role (text following `/` in the label key) can be set, as long as the overall key follows the
[syntax](/docs/concepts/overview/working-with-objects/labels/#syntax-and-character-set) rules for
object labels.

Kubernetes defines one specific node role, **control-plane**. A label you can use to mark that node
role is [`node-role.kubernetes.io/control-plane`](#node-role-kubernetes-io-control-plane).

### node-role.kubernetes.io/control-plane {#node-role-kubernetes-io-control-plane-taint}

Type: Taint

Example: `node-role.kubernetes.io/control-plane:NoSchedule`

Used on: Node

Taint that kubeadm applies on control plane nodes to restrict placing Pods and
allow only specific pods to schedule on them.

If this Taint is applied, control plane nodes allow only critical workloads to
be scheduled onto them. You can manually remove this taint with the following
command on a specific node.

```shell
kubectl taint nodes <node-name> node-role.kubernetes.io/control-plane:NoSchedule-
```

### node-role.kubernetes.io/master (deprecated) {#node-role-kubernetes-io-master-taint}

Type: Taint

Used on: Node

Example: `node-role.kubernetes.io/master:NoSchedule`

Taint that kubeadm previously applied on control plane nodes to allow only critical
workloads to schedule on them. Replaced by the
[`node-role.kubernetes.io/control-plane`](#node-role-kubernetes-io-control-plane-taint)
taint. kubeadm no longer sets or uses this deprecated taint.

### resource.k8s.io/admin-access {resource-k8s-io-admin-access}

Type: Label

Example: `resource.k8s.io/admin-access: "true"`

Used on: Namespace

Used to grant administrative access to certain resource.k8s.io API types within
a namespace. When this label is set on a namespace with the value `"true"`
(case-sensitive), it allows the use of `adminAccess: true` in any namespaced
`resource.k8s.io` API types. Currently, this permission applies to
`ResourceClaim` and `ResourceClaimTemplate` objects.

See [Dynamic Resource Allocation Admin access](/docs/concepts/scheduling-eviction/dynamic-resource-allocation/#enabling-admin-access)
for more information.
