---
title: شرایط پذیرشWebhookMatch
content_type: feature_gate
_build:
  list: never
  render: false

stages:
  - stage: آلفا
    defaultValue: false
    fromVersion: "1.27"
    toVersion: "1.27"
  - stage: بتا
    defaultValue: true
    fromVersion: "1.28"
    toVersion: "1.29"
  - stage: پایدار
    defaultValue: true
    fromVersion: "1.30"
    toVersion: "1.32"

removed: true
---
فعال کردن [match conditions](/docs/reference/access-authn-authz/extensible-admission-controllers/#matching-requests-matchconditions)
برای تغییر و اعتبارسنجی وب‌هوک‌های پذیرش.