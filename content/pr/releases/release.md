---
title: Kubernetes Release Cycle
type: docs
auto_generated: true
---
<!-- این محتوا به صورت خودکار تولید می‌شود از طریق https://github.com/kubernetes/website/blob/main/scripts/releng/update-release-info.sh -->

{{% pageinfo color="light" %}}
این محتوا به صورت خودکار تولید می‌شود و ممکن است لینک‌ها کار نکنند. منبع سند مشخص شده است.
[اینجا](https://github.com/kubernetes/community/blob/master/contributors/devel/sig-release/release.md).
{{% /pageinfo %}}
<!-- Lنکته محلی‌سازی: هنگام محلی‌سازی، بلوک pageinfo را حذف کنید -->

## هدف قرار دادن پیشرفت‌ها، مشکلات و روابط عمومی‌ها برای انتشار نقاط عطف

این سند بر توسعه‌دهندگان و مشارکت‌کنندگان Kubernetes متمرکز است که نیاز به ایجاد یک بهبود، مشکل یا درخواست pull دارند که یک نقطه عطف انتشار خاص را هدف قرار می‌دهد.

- [TL;DR](#tldr)
  - [Normal Dev (Weeks 1-11)](#normal-dev-weeks-1-11)
  - [Code Freeze (Weeks 12-14)](#code-freeze-weeks-12-14)
  - [Post-Release (Weeks 14+)](#post-release-weeks-14+)
- [Definitions](#definitions)
- [The Release Cycle](#the-release-cycle)
- [Removal Of Items From The Milestone](#removal-of-items-from-the-milestone)
- [Adding An Item To The Milestone](#adding-an-item-to-the-milestone)
  - [Milestone Maintainers](#milestone-maintainers)
  - [Feature additions](#feature-additions)
  - [Issue additions](#issue-additions)
  - [PR Additions](#pr-additions)
- [Other Required Labels](#other-required-labels)
  - [SIG Owner Label](#sig-owner-label)
  - [Priority Label](#priority-label)
  - [Issue/PR Kind Label](#issuepr-kind-label)

فرآیند هدایت بهبودها، مشکلات و درخواست‌های pull به یک نسخه Kubernetes، ذینفعان متعددی را در بر می‌گیرد:

- مالکان مربوط به بهبود، انتشار و درخواست pull
- رهبری SIG
- [تیم انتشار][release-team]

اطلاعات مربوط به گردش کار و تعاملات در زیر شرح داده شده است.

به عنوان مالک یک توسعه، انتشار یا درخواست pull ، it is your
مسئولیت اطمینان از برآورده شدن الزامات مربوط به نقاط عطف انتشار. در صورت نیاز به به‌روزرسانی، تیم اتوماسیون و انتشار با شما تماس خواهند گرفت., اما عدم اقدام می‌تواند منجر به حذف کار شما از مرحله‌ی مهم شود.. Additional
الزامات زمانی وجود دارند که نقطه عطف هدف، یک نسخه قبلی باشد.مشاهده کنید لینک پیوست شده را 
[cherry pick process][cherry-picks] .

## TL;DR

اگر می‌خواهید PR شما ادغام شود، به برچسب‌ها و مراحل مهم زیر نیاز دارد که در اینجا با Prow/commands نشان داده شده‌اند و برای اضافه کردن آنها لازم است:

### Normal Dev (Weeks 1-11)

- /sig {name}
- /kind {type}
- /lgtm
- /approved

### [Code Freeze][code-freeze] (هفته 12-14)

- /milestone {v1.y}
- /sig {name}
- /kind {bug, failing-test}
- /lgtm
- /approved

### پس از انتشار (هفته 14+)

بازگشت به الزامات مرحله 'Normal Dev':

- /sig {name}
- /kind {type}
- /lgtm
- /approved

ادغام‌ها در شاخه ۱.y اکنون [از طریق انتخاب‌های گیلاس] انجام می‌شوند.[cherry-picks], تأیید شده توسط [مدیران انتشار][release-managers].

در گذشته، برای درخواست‌های pull که با هدف تعیین نقطه عطف (milestone-targeted) انجام می‌شدند، الزام باز بودن یک issue مرتبط در GitHub وجود داشت، اما دیگر این‌طور نیست.
ویژگی‌ها یا بهبودها عملاً مشکلات گیت‌هاب یا [KEPها] هستند.[keps] که منجر به PR های بعدی می شود.

فرآیند کلی برچسب‌گذاری باید در بین انواع مصنوعات سازگار باشد.

## تعاریف

- *صاحبان مسئله*: ایجادکننده، واگذارکنندگان و کاربری که مسئله را به مرحله انتشار رسانده است

- *تیم انتشار*: هر نسخه Kubernetes دارای تیمی است که مدیریت پروژه را انجام می‌دهد.
  وظایف شرح داده شده [اینجا][release-team].

  Tاطلاعات تماس تیم مرتبط با هر نسخه منتشر شده را می‌توان یافت.
  [اینجا](https://git.k8s.io/sig-release/releases/).

- *Y days*: مربوط به روزهای کاری است

- *افزایش*: ببینید "[آیا «چیز من» یک پیشرفت است؟](https://git.k8s.io/enhancements/README.md#is-my-thing-an-enhancement)"

- *[enhancements-freeze][enhancements-freeze]*:
  مهلتی که [KEPs][keps] برای اینکه پیشرفت‌ها بخشی از نسخه فعلی باشند، باید تکمیل شوند

- *[exceptions][exceptions]*:
  فرآیند درخواست تمدید مهلت برای یک مورد خاص
ارتقاء 

- *[code-freeze][code-freeze]*:
  دوره حدود ۴ هفته‌ای قبل از تاریخ انتشار نهایی، که در طی آن فقط رفع اشکالات حیاتی در نسخه نهایی ادغام می‌شوند.

- *[Pruning](https://git.k8s.io/sig-release/releases/release_phases.md#pruning)*:
  فرآیند حذف یک بهبود از یک نقطه عطف انتشار، در صورتی که ... نباشد
  کاملاً پیاده‌سازی شده یا در غیر این صورت پایدار تلقی نمی‌شود.

- *release milestone*: رشته نسخه معنایی یا
  [نقطه عطف گیت‌هاب](https://help.github.com/en/github/managing-your-work-on-github/associating-milestones-with-issues-and-pull-requests)
  اشاره به نسخهٔ اصلی.جزئی `vX.Y` از انتشار.

  همچنین ببینید
  [انتشار نسخه](https://git.k8s.io/sig-release/release-engineering/versioning.md).

- *شاخه رهاسازی*: شاخه گیت `release-X.Y` برای مرحله `vX.Y` ایجاد شده است.

  در زمان انتشار `vX.Y-rc.0` ایجاد شده و پس از انتشار تقریباً به مدت ۱۲ ماه با انتشار وصله‌های `vX.Y.Z` حفظ شده است.

توجه: نسخه‌های ۱.۱۹ و جدیدتر، ۱ سال پشتیبانی انتشار وصله دریافت می‌کنند و نسخه‌های ۱.۱۸ و قبل از آن، ۹ ماه پشتیبانی انتشار وصله دریافت می‌کنند.

## چرخه انتشار

![ایمیج یک چرخه انتشار Kubernetes](/images/releases/release-cycle.jpg)

انتشارهای Kubernetes در حال حاضر تقریباً سه بار در سال اتفاق می‌افتد.

فرآیند انتشار را می‌توان شامل سه مرحله اصلی دانست:

- تعریف افزایش
- پیاده سازی
- تثبیت

اما در واقعیت، این یک پروژه متن‌باز و چابک است که برنامه‌ریزی و پیاده‌سازی ویژگی‌ها در آن همواره در حال انجام است. با توجه به مقیاس پروژه و پایگاه توسعه‌دهندگان توزیع‌شده در سطح جهانی، برای سرعت پروژه بسیار مهم است که به یک مرحله تثبیت دنباله‌دار متکی نباشد و در عوض آزمایش یکپارچه‌سازی مداوم داشته باشد که تضمین می‌کند پروژه همیشه پایدار است، به طوری که بتوان کامیت‌های فردی را به عنوان چیزی که خراب شده است، علامت‌گذاری کرد.

با تعریف مداوم ویژگی‌ها در طول سال، مجموعه‌ای از موارد به صورت حبابی ظاهر می‌شوند که هدفشان انتشار یک نسخه خاص است. **[توقف پیشرفت‌ها][enhancements-freeze]**
تقریباً ۴ هفته پس از شروع چرخه انتشار شروع می‌شود. تا این مرحله، تمام کارهای مربوط به ویژگی‌های مورد نظر برای انتشار مورد نظر، در مصنوعات برنامه‌ریزی مناسب، همراه با [سرپرست بهبودها] تیم انتشار، تعریف شده‌اند.(https://git.k8s.io/sig-release/release-team/role-handbooks/enhancements/README.md).

After Enhancements Freeze, tracking milestones on PRs and issues is important.
Items within the milestone are used as a punchdown list to complete the
release. *On issues*, milestones must be applied correctly, via triage by the
SIG, so that [Release Team][release-team] can track bugs and enhancements (any
enhancement-related issue needs a milestone).

There is some automation in place to help automatically assign milestones to
PRs.

This automation currently applies to the following repos:

- `kubernetes/enhancements`
- `kubernetes/kubernetes`
- `kubernetes/release`
- `kubernetes/sig-release`
- `kubernetes/test-infra`

At creation time, PRs against the `master` branch need humans to hint at which
milestone they might want the PR to target. Once merged, PRs against the
`master` branch have milestones auto-applied so from that time onward human
management of that PR's milestone is less necessary. On PRs against release
branches, milestones are auto-applied when the PR is created so no human
management of the milestone is ever necessary.

Any other effort that should be tracked by the Release Team that doesn't fall
under that automation umbrella should be have a milestone applied.

Implementation and bug fixing is ongoing across the cycle, but culminates in a
code freeze period.

**[Code Freeze][code-freeze]** starts in week ~12 and continues for ~2 weeks.
Only critical bug fixes are accepted into the release codebase during this
time.

There are approximately two weeks following Code Freeze, and preceding release,
during which all remaining critical issues must be resolved before release.
This also gives time for documentation finalization.

When the code base is sufficiently stable, the master branch re-opens for
general development and work begins there for the next release milestone. Any
remaining modifications for the current release are cherry picked from master
back to the release branch. The release is built from the release branch.

Each release is part of a broader Kubernetes lifecycle:

![Image of Kubernetes release lifecycle spanning three releases](/images/releases/release-lifecycle.jpg)

## Removal Of Items From The Milestone

Before getting too far into the process for adding an item to the milestone,
please note:

Members of the [Release Team][release-team] may remove issues from the
milestone if they or the responsible SIG determine that the issue is not
actually blocking the release and is unlikely to be resolved in a timely
fashion.

Members of the Release Team may remove PRs from the milestone for any of the
following, or similar, reasons:

- PR is potentially de-stabilizing and is not needed to resolve a blocking
  issue
- PR is a new, late feature PR and has not gone through the enhancements
  process or the [exception process][exceptions]
- There is no responsible SIG willing to take ownership of the PR and resolve
  any follow-up issues with it
- PR is not correctly labelled
- Work has visibly halted on the PR and delivery dates are uncertain or late

While members of the Release Team will help with labelling and contacting
SIG(s), it is the responsibility of the submitter to categorize PRs, and to
secure support from the relevant SIG to guarantee that any breakage caused by
the PR will be rapidly resolved.

Where additional action is required, an attempt at human to human escalation
will be made by the Release Team through the following channels:

- Comment in GitHub mentioning the SIG team and SIG members as appropriate for
  the issue type
- Emailing the SIG mailing list
  - bootstrapped with group email addresses from the
    [community sig list][sig-list]
  - optionally also directly addressing SIG leadership or other SIG members
- Messaging the SIG's Slack channel
  - bootstrapped with the slackchannel and SIG leadership from the
    [community sig list][sig-list]
  - optionally directly "@" mentioning SIG leadership or others by handle

## Adding An Item To The Milestone

### Milestone Maintainers

The members of the [`milestone-maintainers`](https://github.com/orgs/kubernetes/teams/milestone-maintainers/members)
GitHub team are entrusted with the responsibility of specifying the release
milestone on GitHub artifacts.

This group is [maintained](https://git.k8s.io/sig-release/release-team/README.md#milestone-maintainers)
by SIG Release and has representation from the various SIGs' leadership.

Adding the in-progress release milestone to pull requests after the Code Freeze is strictly prohibited, as it can compromise the stability of the release. Prior to making such changes, approval must be obtained from both the Release Team Lead and the Emeritus Advisor(s).

### Feature additions

Feature planning and definition takes many forms today, but a typical example
might be a large piece of work described in a [KEP][keps], with associated task
issues in GitHub. When the plan has reached an implementable state and work is
underway, the enhancement or parts thereof are targeted for an upcoming milestone
by creating GitHub issues and marking them with the Prow "/milestone" command.

For the first ~4 weeks into the release cycle, the Release Team's Enhancements
Lead will interact with SIGs and feature owners via GitHub, Slack, and SIG
meetings to capture all required planning artifacts.

If you have an enhancement to target for an upcoming release milestone, begin a
conversation with your SIG leadership and with that release's Enhancements
Lead.

### Issue additions

Issues are marked as targeting a milestone via the Prow "/milestone" command.

The Release Team's [Bug Triage Lead](https://git.k8s.io/sig-release/release-team/role-handbooks/bug-triage/README.md)
and overall community watch incoming issues and triage them, as described in
the contributor guide section on
[issue triage](https://k8s.dev/docs/guide/issue-triage/).

Marking issues with the milestone provides the community better visibility
regarding when an issue was observed and by when the community feels it must be
resolved. During [Code Freeze][code-freeze], a milestone must be set to merge
a PR.

An open issue is no longer required for a PR, but open issues and associated
PRs should have synchronized labels. For example a high priority bug issue
might not have its associated PR merged if the PR is only marked as lower
priority.

### PR Additions

PRs are marked as targeting a milestone via the Prow "/milestone" command.

This is a blocking requirement during Code Freeze as described above.

## Other Required Labels

[Here is the list of labels and their use and purpose.](https://git.k8s.io/test-infra/label_sync/labels.md#labels-that-apply-to-all-repos-for-both-issues-and-prs)

### SIG Owner Label

The SIG owner label defines the SIG to which we escalate if a milestone issue
is languishing or needs additional attention. If there are no updates after
escalation, the issue may be automatically removed from the milestone.

These are added with the Prow "/sig" command. For example to add the label
indicating SIG Storage is responsible, comment with `/sig storage`.

### Priority Label

Priority labels are used to determine an escalation path before moving issues
out of the release milestone. They are also used to determine whether or not a
release should be blocked on the resolution of the issue.

- `priority/critical-urgent`: Never automatically move out of a release
  milestone; continually escalate to contributor and SIG through all available
  channels.
  - considered a release blocking issue
  - requires daily updates from issue owners during [Code Freeze][code-freeze]
  - would require a patch release if left undiscovered until after the minor
    release
- `priority/important-soon`: Escalate to the issue owners and SIG owner; move
  out of milestone after several unsuccessful escalation attempts.
  - not considered a release blocking issue
  - would not require a patch release
  - will automatically be moved out of the release milestone at Code Freeze
    after a 4 day grace period
- `priority/important-longterm`: Escalate to the issue owners; move out of the
  milestone after 1 attempt.
  - even less urgent / critical than `priority/important-soon`
  - moved out of milestone more aggressively than `priority/important-soon`

### Issue/PR Kind Label

The issue kind is used to help identify the types of changes going into the
release over time. This may allow the Release Team to develop a better
understanding of what sorts of issues we would miss with a faster release
cadence.

For release targeted issues, including pull requests, one of the following
issue kind labels must be set:

- `kind/api-change`: Adds, removes, or changes an API
- `kind/bug`: Fixes a newly discovered bug.
- `kind/cleanup`: Adding tests, refactoring, fixing old bugs.
- `kind/design`: Related to design
- `kind/documentation`: Adds documentation
- `kind/failing-test`: CI test case is failing consistently.
- `kind/feature`: New functionality.
- `kind/flake`: CI test case is showing intermittent failures.

[cherry-picks]: https://git.k8s.io/community/contributors/devel/sig-release/cherry-picks.md
[code-freeze]: https://git.k8s.io/sig-release/releases/release_phases.md#code-freeze
[enhancements-freeze]: https://git.k8s.io/sig-release/releases/release_phases.md#enhancements-freeze
[exceptions]: https://git.k8s.io/sig-release/releases/release_phases.md#exceptions
[keps]: https://git.k8s.io/enhancements/keps
[release-managers]: /releases/release-managers/
[release-team]: https://git.k8s.io/sig-release/release-team
[sig-list]: https://k8s.dev/sigs
