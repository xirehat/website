---
reviewers:
- liggitt
- lavalamp
- thockin
- smarterclayton
title: "Deprecated API Migration Guide"
weight: 45
content_type: reference
---

<!-- overview -->

با تکامل API کوبرنتیز، APIها به صورت دوره‌ای سازماندهی مجدد یا ارتقا می‌یابند.
هنگامی که APIها تکامل می‌یابند، API قدیمی منسوخ شده و در نهایت حذف می‌شود.
این صفحه حاوی اطلاعاتی است که هنگام مهاجرت از نسخه‌های API منسوخ شده به نسخه‌های API جدیدتر و پایدارتر باید بدانید.

<!-- body -->

## Removed APIs by release

### v1.32

نسخه **v1.32** ارائه نسخه‌های API منسوخ‌شده زیر را متوقف کرد:

#### Flow control resources {#flowcontrol-resources-v132}

نسخه API مربوط به FlowSchema و PriorityLevelConfiguration از نسخه ۱.۳۲ به بعد دیگر ارائه نمی‌شود. **flowcontrol.apiserver.k8s.io/v1beta3**

* مانیفست‌ها و کلاینت‌های API را برای استفاده از نسخه API **flowcontrol.apiserver.k8s.io/v1** که از نسخه ۱.۲۹ در دسترس است، منتقل کنید.

* همه اشیاء موجود از طریق API جدید قابل دسترسی هستند.
* تغییرات قابل توجه در **flowcontrol.apiserver.k8s.io/v1**:
* فیلد PriorityLevelConfiguration `spec.limited.nominalConcurrencyShares` فقط در صورت عدم تعیین، به طور پیش‌فرض روی ۳۰ قرار می‌گیرد و مقدار صریح ۰ به ۳۰ تغییر نمی‌کند.

### v1.29

نسخه **v1.29** ارائه نسخه‌های API منسوخ‌شده زیر را متوقف کرد:

#### Flow control resources {#flowcontrol-resources-v129}

نسخه API مربوط به FlowSchema و PriorityLevelConfiguration از نسخه ۱.۲۹ به بعد دیگر ارائه نمی‌شود. **flowcontrol.apiserver.k8s.io/v1beta2**

* مانیفست‌ها و کلاینت‌های API را برای استفاده از نسخه API **flowcontrol.apiserver.k8s.io/v1** که از نسخه ۱.۲۹ در دسترس است، یا نسخه API **flowcontrol.apiserver.k8s.io/v1beta3** که از نسخه ۱.۲۶ در دسترس است، منتقل کنید.
* همه اشیاء موجودِ ذخیره‌شده از طریق API جدید قابل دسترسی هستند

* تغییرات قابل توجه در **flowcontrol.apiserver.k8s.io/v1**:
* فیلد PriorityLevelConfiguration `spec.limited.assuredConcurrencyShares` به `spec.limited.nominalConcurrencyShares` تغییر نام داده است و فقط در صورت عدم تعیین مقدار پیش‌فرض آن 30 است و مقدار صریح 0 به 30 تغییر نمی‌کند.
* Notable changes in **flowcontrol.apiserver.k8s**. تغییرات قابل توجه در **flowcontrol.apiserver**.

k8s.io/v1beta3**:
* فیلد PriorityLevelConfiguration `spec.limited.assuredConcurrencyShares` به `spec.limited.nominalConcurrencyShares` تغییر نام داده است.

### v1.27

نسخه **v1.27** ارائه نسخه‌های API منسوخ‌شده زیر را متوقف کرد:

#### CSIStorageCapacity {#csistoragecapacity-v127}

نسخه API **storage.k8s.io/v1beta1** از CSIStorageCapacity از نسخه ۱.۲۷ دیگر ارائه نمی‌شود.

* مانیفست‌ها و کلاینت‌های API را برای استفاده از نسخه API **storage.k8s.io/v1** که از نسخه ۱.۲۴ در دسترس است، منتقل کنید.

* همه اشیاء موجود از طریق API جدید قابل دسترسی هستند.
* هیچ تغییر قابل توجهی وجود ندارد

### v1.26

The **v1.26** release stopped serving the following deprecated API versions:

#### Flow control resources {#flowcontrol-resources-v126}

نسخه API **flowcontrol.apiserver.k8s.io/v1beta1** از FlowSchema و PriorityLevelConfiguration از نسخه ۱.۲۶ دیگر ارائه نمی‌شود.

* مانیفست‌ها و کلاینت‌های API را برای استفاده از نسخه API **flowcontrol.apiserver.k8s.io/v1beta2** منتقل کنید.

* همه اشیاء موجود از طریق API جدید قابل دسترسی هستند.
* هیچ تغییر قابل توجهی وجود ندارد

#### HorizontalPodAutoscaler {#horizontalpodautoscaler-v126}

نسخه API **autoscaling/v2beta2** از HorizontalPodAutoscaler از نسخه ۱.۲۶ دیگر ارائه نمی‌شود.

* مانیفست‌ها و کلاینت‌های API را برای استفاده از نسخه API **autoscaling/v2** که از نسخه ۱.۲۳ در دسترس است، منتقل کنید.

* همه اشیاء موجود از طریق API جدید قابل دسترسی هستند.
* تغییرات قابل توجه:

* `targetAverageUtilization` با `target.averageUtilization` و `target.type: Utilization` جایگزین شده است. به [Autoscaling on multiple metrics and custom metrics](/docs/tasks/run-application/horizontal-pod-autoscale-walkthrough/#autoscaling-on-multiple-metrics-and-custom-metrics) مراجعه کنید.
### v1.25

نسخه **v1.25** ارائه نسخه‌های API منسوخ‌شده زیر را متوقف کرد:

#### CronJob {#cronjob-v125}

نسخه API **batch/v1beta1** از CronJob دیگر از نسخه ۱.۲۵ ارائه نمی‌شود.

* مانیفست‌ها و کلاینت‌های API را برای استفاده از نسخه API **batch/v1** که از نسخه ۱.۲۱ در دسترس است، منتقل کنید.

* همه اشیاء موجود از طریق API جدید قابل دسترسی هستند.
* هیچ تغییر قابل توجهی وجود ندارد

#### EndpointSlice {#endpointslice-v125}

نسخه API **discovery.k8s.io/v1beta1** از EndpointSlice دیگر از نسخه ۱.۲۵ ارائه نمی‌شود.

* مانیفست‌ها و کلاینت‌های API را برای استفاده از نسخه API **discovery.k8s.io/v1** که از نسخه ۱.۲۱ در دسترس است، منتقل کنید.

* همه اشیاء موجود از طریق API جدید قابل دسترسی هستند.
* تغییرات قابل توجه در **discovery.k8s.io/v1**:

* استفاده از فیلد `nodeName` برای هر Endpoint به جای فیلد منسوخ شده `topology["kubernetes.io/hostname"]`

* استفاده از فیلد `zone` برای هر Endpoint به جای فیلد منسوخ شده `topology["topology.kubernetes.io/zone"]`

* `topology` با فیلد `deprecatedTopology` جایگزین شده است که در نسخه ۱ قابل نوشتن نیست.

#### Event {#event-v125}

نسخه API **events.k8s.io/v1beta1** از Event دیگر از نسخه ۱.۲۵ ارائه نمی‌شود.

* برای استفاده از نسخه API **events.k8s.io/v1** که از نسخه ۱.۱۹ در دسترس است، مانیفست‌ها و کلاینت‌های API را منتقل کنید. * همه اشیاء موجود از طریق API جدید قابل دسترسی هستند
* تغییرات قابل توجه در **events.k8s.io/v1**:
* `type` به `Normal` و `Warning` محدود شده است
* `involvedObject` به `regarding` تغییر نام داده است
* `action`، `reason`، `reportingController` و `reportingInstance` هنگام ایجاد رویدادهای جدید **events.k8s.io/v1** الزامی هستند
* به جای فیلد منسوخ شده `firstTimestamp` (که به `deprecatedFirstTimestamp` تغییر نام داده شده و در رویدادهای جدید **events.k8s.io/v1** مجاز نیست) از `eventTime` استفاده کنید
* به جای فیلد منسوخ شده `lastTimestamp` از `series.lastObservedTime` استفاده کنید
(که به `deprecatedLastTimestamp` تغییر نام داده شده و در رویدادهای جدید مجاز نیست) **events.k8s.io/v1** Events)
* به جای فیلد منسوخ شده `count` (که به `deprecatedCount` تغییر نام داده شده و در رویدادهای جدید **events.k8s.io/v1** مجاز نیست) از `series.count` استفاده کنید.

* به جای فیلد منسوخ شده `source.component` (که به `deprecatedSource.component` تغییر نام داده شده و در رویدادهای جدید **events.k8s.io/v1** مجاز نیست) از `reportingController` استفاده کنید.

* به جای فیلد منسوخ شده `source.host` (که به `deprecatedSource.host` تغییر نام داده شده و در رویدادهای جدید **events.k8s.io/v1** مجاز نیست) از `reportingInstance` استفاده کنید.

#### HorizontalPodAutoscaler {#horizontalpodautoscaler-v125}

نسخه API **autoscaling/v2beta1** از HorizontalPodAutoscaler از نسخه ۱.۲۵ دیگر ارائه نمی‌شود.

* مانیفست‌ها و کلاینت‌های API را برای استفاده از نسخه API **autoscaling/v2** که از نسخه ۱.۲۳ در دسترس است، منتقل کنید.

* همه اشیاء موجود از طریق API جدید قابل دسترسی هستند.
* تغییرات قابل توجه:

* `targetAverageUtilization` با `target.averageUtilization` و `target.type: Utilization` جایگزین شده است. به [Autoscaling on multiple metrics and custom metrics](/docs/tasks/run-application/horizontal-pod-autoscale-walkthrough/#autoscaling-on-multiple-metrics-and-custom-metrics) مراجعه کنید.

#### PodDisruptionBudget {#poddisruptionbudget-v125}

نسخه API **policy/v1beta1** از PodDisruptionBudget دیگر از نسخه ۱.۲۵ ارائه نمی‌شود.

* مانیفست‌ها و کلاینت‌های API را برای استفاده از نسخه API **policy/v1** که از نسخه ۱.۲۱ در دسترس است، منتقل کنید.

* همه اشیاء موجود از طریق API جدید قابل دسترسی هستند.
* تغییرات قابل توجه در **policy/v1**:

* یک `spec.selector` خالی (`{}`) که در `policy/v1` نوشته شده است، همه پادها را در فضای نام انتخاب می‌کند (در `policy/v1beta1` یک `spec.selector` خالی هیچ پادی را انتخاب نکرده است).

یک `spec.selector` تنظیم نشده، هیچ پادی را در هیچ یک از نسخه‌های API انتخاب نمی‌کند.

#### PodSecurityPolicy {#psp-v125}


PodSecurityPolicy در نسخه API **policy/v1beta1** از نسخه ۱.۲۵ دیگر ارائه نمی‌شود و کنترل‌کننده پذیرش PodSecurityPolicy حذف خواهد شد.

به [Pod Security Admission](/docs/concepts/security/pod-security-admission/) یا یک [3rd party admission webhook](/docs/reference/access-authn-authz/extensible-admission-controllers/). مهاجرت کنید.

برای راهنمای مهاجرت، به [Migrate from PodSecurityPolicy to the Built-In PodSecurity Admission Controller](/docs/tasks/configure-pod-container/migrate-from-psp/) مراجعه کنید. برای اطلاعات بیشتر در مورد منسوخ شدن، به [Migrate from PodSecurityPolicy to the Built-In PodSecurity Admission Controller](/docs/tasks/configure-pod-container/migrate-from-psp/). مراجعه کنید.

PodSecurityPolicy in the **policy/v1beta1** API version is no longer served as of v1.25,
and the PodSecurityPolicy admission controller will be removed.

#### RuntimeClass {#runtimeclass-v125}

کلاس RuntimeClass در نسخه API **node.k8s.io/v1beta1** از نسخه ۱.۲۵ دیگر ارائه نمی‌شود.

* مانیفست‌ها و کلاینت‌های API را برای استفاده از نسخه API **node.k8s.io/v1** که از نسخه ۱.۲۰ در دسترس است، منتقل کنید.

* همه اشیاء موجود از طریق API جدید قابل دسترسی هستند.
* هیچ تغییر قابل توجهی وجود ندارد

### v1.22

نسخه **v1.22** ارائه نسخه‌های API منسوخ‌شده زیر را متوقف کرد:

#### Webhook resources {#webhook-resources-v122}

نسخه API مربوط به MutatingWebhookConfiguration و ValidatingWebhookConfiguration از نسخه ۱.۲۲ دیگر ارائه نمی‌شود. **admissionregistration.k8s.io/v1beta1**

* مانیفست‌ها و کلاینت‌های API را برای استفاده از نسخه API **admissionregistration.k8s.io/v1** که از نسخه ۱.۱۶ در دسترس است، منتقل کنید. * همه اشیاء موجود از طریق API های جدید قابل دسترسی هستند
* تغییرات قابل توجه:
* مقدار پیش‌فرض `webhooks[*].failurePolicy` برای نسخه ۱ از `Ignore` به `Fail` تغییر کرد.
* مقدار پیش‌فرض `webhooks[*].matchPolicy` از `Exact` به `Equivalent` برای نسخه ۱ تغییر کرد.
* مقدار پیش‌فرض `webhooks[*].timeoutSeconds` از `30s` به `10s` برای نسخه ۱ تغییر کرد.
* مقدار پیش‌فرض `webhooks[*].sideEffects` حذف شد و فیلد مورد نیاز شد، و فقط `None` و `NoneOnDryRun` برای نسخه ۱ مجاز هستند.
* مقدار پیش‌فرض `webhooks[*].admissionReviewVersions` حذف شد و فیلد مورد نیاز شد. (نسخه‌های پشتیبانی شده برای AdmissionReview عبارتند از `v1` و `v1beta1`)
* مقدار پیش‌فرض `webhooks[*].name` باید باشد. برای اشیاء ایجاد شده از طریق `admissionregistration.k8s.io/v1` در لیست منحصر به فرد باشد

#### CustomResourceDefinition {#customresourcedefinition-v122}

The **apiextensions.k8s.io/v1beta1** API version of CustomResourceDefinition is no longer served as of v1.22.

* Migrate manifests and API clients to use the **apiextensions.k8s.io/v1** API version, available since v1.16.
* All existing persisted objects are accessible via the new API
* Notable changes:
  * `spec.scope` is no longer defaulted to `Namespaced` and must be explicitly specified
  * `spec.version` is removed in v1; use `spec.versions` instead
  * `spec.validation` is removed in v1; use `spec.versions[*].schema` instead
  * `spec.subresources` is removed in v1; use `spec.versions[*].subresources` instead
  * `spec.additionalPrinterColumns` is removed in v1; use `spec.versions[*].additionalPrinterColumns` instead
  * `spec.conversion.webhookClientConfig` is moved to `spec.conversion.webhook.clientConfig` in v1
  * `spec.conversion.conversionReviewVersions` is moved to `spec.conversion.webhook.conversionReviewVersions` in v1
  * `spec.versions[*].schema.openAPIV3Schema` is now required when creating v1 CustomResourceDefinition objects,
    and must be a [structural schema](/docs/tasks/extend-kubernetes/custom-resources/custom-resource-definitions/#specifying-a-structural-schema)
  * `spec.preserveUnknownFields: true` is disallowed when creating v1 CustomResourceDefinition objects;
    it must be specified within schema definitions as `x-kubernetes-preserve-unknown-fields: true`
  * In `additionalPrinterColumns` items, the `JSONPath` field was renamed to `jsonPath` in v1
    (fixes [#66531](https://github.com/kubernetes/kubernetes/issues/66531))

#### APIService {#apiservice-v122}

The **apiregistration.k8s.io/v1beta1** API version of APIService is no longer served as of v1.22.

* Migrate manifests and API clients to use the **apiregistration.k8s.io/v1** API version, available since v1.10.
* All existing persisted objects are accessible via the new API
* No notable changes

#### TokenReview {#tokenreview-v122}

The **authentication.k8s.io/v1beta1** API version of TokenReview is no longer served as of v1.22.

* Migrate manifests and API clients to use the **authentication.k8s.io/v1** API version, available since v1.6.
* No notable changes

#### SubjectAccessReview resources {#subjectaccessreview-resources-v122}

The **authorization.k8s.io/v1beta1** API version of LocalSubjectAccessReview,
SelfSubjectAccessReview, SubjectAccessReview, and SelfSubjectRulesReview is no longer served as of v1.22.

* Migrate manifests and API clients to use the **authorization.k8s.io/v1** API version, available since v1.6.
* Notable changes:
  * `spec.group` was renamed to `spec.groups` in v1 (fixes [#32709](https://github.com/kubernetes/kubernetes/issues/32709))

#### CertificateSigningRequest {#certificatesigningrequest-v122}

The **certificates.k8s.io/v1beta1** API version of CertificateSigningRequest is no longer served as of v1.22.

* Migrate manifests and API clients to use the **certificates.k8s.io/v1** API version, available since v1.19.
* All existing persisted objects are accessible via the new API
* Notable changes in `certificates.k8s.io/v1`:
  * For API clients requesting certificates:
    * `spec.signerName` is now required
      (see [known Kubernetes signers](/docs/reference/access-authn-authz/certificate-signing-requests/#kubernetes-signers)),
      and requests for `kubernetes.io/legacy-unknown` are not allowed to be created via the `certificates.k8s.io/v1` API
    * `spec.usages` is now required, may not contain duplicate values, and must only contain known usages
  * For API clients approving or signing certificates:
    * `status.conditions` may not contain duplicate types
    * `status.conditions[*].status` is now required
    * `status.certificate` must be PEM-encoded, and contain only `CERTIFICATE` blocks

#### Lease {#lease-v122}

The **coordination.k8s.io/v1beta1** API version of Lease is no longer served as of v1.22.

* Migrate manifests and API clients to use the **coordination.k8s.io/v1** API version, available since v1.14.
* All existing persisted objects are accessible via the new API
* No notable changes

#### Ingress {#ingress-v122}

The **extensions/v1beta1** and **networking.k8s.io/v1beta1** API versions of Ingress is no longer served as of v1.22.

* Migrate manifests and API clients to use the **networking.k8s.io/v1** API version, available since v1.19.
* All existing persisted objects are accessible via the new API
* Notable changes:
  * `spec.backend` is renamed to `spec.defaultBackend`
  * The backend `serviceName` field is renamed to `service.name`
  * Numeric backend `servicePort` fields are renamed to `service.port.number`
  * String backend `servicePort` fields are renamed to `service.port.name`
  * `pathType` is now required for each specified path. Options are `Prefix`,
    `Exact`, and `ImplementationSpecific`. To match the undefined `v1beta1` behavior, use `ImplementationSpecific`.

#### IngressClass {#ingressclass-v122}

The **networking.k8s.io/v1beta1** API version of IngressClass is no longer served as of v1.22.

* Migrate manifests and API clients to use the **networking.k8s.io/v1** API version, available since v1.19.
* All existing persisted objects are accessible via the new API
* No notable changes

#### RBAC resources {#rbac-resources-v122}

The **rbac.authorization.k8s.io/v1beta1** API version of ClusterRole, ClusterRoleBinding,
Role, and RoleBinding is no longer served as of v1.22.

* Migrate manifests and API clients to use the **rbac.authorization.k8s.io/v1** API version, available since v1.8.
* All existing persisted objects are accessible via the new APIs
* No notable changes

#### PriorityClass {#priorityclass-v122}

The **scheduling.k8s.io/v1beta1** API version of PriorityClass is no longer served as of v1.22.

* Migrate manifests and API clients to use the **scheduling.k8s.io/v1** API version, available since v1.14.
* All existing persisted objects are accessible via the new API
* No notable changes

#### Storage resources {#storage-resources-v122}

The **storage.k8s.io/v1beta1** API version of CSIDriver, CSINode, StorageClass, and VolumeAttachment is no longer served as of v1.22.

* Migrate manifests and API clients to use the **storage.k8s.io/v1** API version
  * CSIDriver is available in **storage.k8s.io/v1** since v1.19.
  * CSINode is available in **storage.k8s.io/v1** since v1.17
  * StorageClass is available in **storage.k8s.io/v1** since v1.6
  * VolumeAttachment is available in **storage.k8s.io/v1** v1.13
* All existing persisted objects are accessible via the new APIs
* No notable changes

### v1.16

The **v1.16** release stopped serving the following deprecated API versions:

#### NetworkPolicy {#networkpolicy-v116}

The **extensions/v1beta1** API version of NetworkPolicy is no longer served as of v1.16.

* Migrate manifests and API clients to use the **networking.k8s.io/v1** API version, available since v1.8.
* All existing persisted objects are accessible via the new API

#### DaemonSet {#daemonset-v116}

The **extensions/v1beta1** and **apps/v1beta2** API versions of DaemonSet are no longer served as of v1.16.

* Migrate manifests and API clients to use the **apps/v1** API version, available since v1.9.
* All existing persisted objects are accessible via the new API
* Notable changes:
  * `spec.templateGeneration` is removed
  * `spec.selector` is now required and immutable after creation; use the existing
    template labels as the selector for seamless upgrades
  * `spec.updateStrategy.type` now defaults to `RollingUpdate`
    (the default in `extensions/v1beta1` was `OnDelete`)

#### Deployment {#deployment-v116}

The **extensions/v1beta1**, **apps/v1beta1**, and **apps/v1beta2** API versions of Deployment are no longer served as of v1.16.

* Migrate manifests and API clients to use the **apps/v1** API version, available since v1.9.
* All existing persisted objects are accessible via the new API
* Notable changes:
  * `spec.rollbackTo` is removed
  * `spec.selector` is now required and immutable after creation; use the existing
    template labels as the selector for seamless upgrades
  * `spec.progressDeadlineSeconds` now defaults to `600` seconds
    (the default in `extensions/v1beta1` was no deadline)
  * `spec.revisionHistoryLimit` now defaults to `10`
    (the default in `apps/v1beta1` was `2`, the default in `extensions/v1beta1` was to retain all)
  * `maxSurge` and `maxUnavailable` now default to `25%`
    (the default in `extensions/v1beta1` was `1`)

#### StatefulSet {#statefulset-v116}

The **apps/v1beta1** and **apps/v1beta2** API versions of StatefulSet are no longer served as of v1.16.

* Migrate manifests and API clients to use the **apps/v1** API version, available since v1.9.
* All existing persisted objects are accessible via the new API
* Notable changes:
  * `spec.selector` is now required and immutable after creation;
    use the existing template labels as the selector for seamless upgrades
  * `spec.updateStrategy.type` now defaults to `RollingUpdate`
    (the default in `apps/v1beta1` was `OnDelete`)

#### ReplicaSet {#replicaset-v116}

The **extensions/v1beta1**, **apps/v1beta1**, and **apps/v1beta2** API versions of ReplicaSet are no longer served as of v1.16.

* Migrate manifests and API clients to use the **apps/v1** API version, available since v1.9.
* All existing persisted objects are accessible via the new API
* Notable changes:
  * `spec.selector` is now required and immutable after creation; use the existing template labels as the selector for seamless upgrades

#### PodSecurityPolicy {#psp-v116}

The **extensions/v1beta1** API version of PodSecurityPolicy is no longer served as of v1.16.

* Migrate manifests and API client to use the **policy/v1beta1** API version, available since v1.10.
* Note that the **policy/v1beta1** API version of PodSecurityPolicy will be removed in v1.25.

## What to do

### Test with deprecated APIs disabled

You can test your clusters by starting an API server with specific API versions disabled
to simulate upcoming removals. Add the following flag to the API server startup arguments:

`--runtime-config=<group>/<version>=false`

For example:

`--runtime-config=admissionregistration.k8s.io/v1beta1=false,apiextensions.k8s.io/v1beta1,...`

### Locate use of deprecated APIs

Use [client warnings, metrics, and audit information available in 1.19+](/blog/2020/09/03/warnings/#deprecation-warnings)
to locate use of deprecated APIs.

### Migrate to non-deprecated APIs

* Update custom integrations and controllers to call the non-deprecated APIs
* Change YAML files to reference the non-deprecated APIs

  You can use the `kubectl convert` command to automatically convert an existing object:

  `kubectl convert -f <file> --output-version <group>/<version>`.

  For example, to convert an older Deployment to `apps/v1`, you can run:

  `kubectl convert -f ./my-deployment.yaml --output-version apps/v1`

  This conversion may use non-ideal default values. To learn more about a specific
  resource, check the Kubernetes [API reference](/docs/reference/kubernetes-api/).
  
  {{< note >}}
  The `kubectl convert` tool is not installed by default, although
  in fact it once was part of `kubectl` itself. For more details, you can read the
  [deprecation and removal issue](https://github.com/kubernetes/kubectl/issues/725)
  for the built-in subcommand.
  
  To learn how to set up `kubectl convert` on your computer, visit the page that is right for your 
  operating system:
  [Linux](/docs/tasks/tools/install-kubectl-linux/#install-kubectl-convert-plugin),
  [macOS](/docs/tasks/tools/install-kubectl-macos/#install-kubectl-convert-plugin), or
  [Windows](/docs/tasks/tools/install-kubectl-windows/#install-kubectl-convert-plugin).
  {{< /note >}}
