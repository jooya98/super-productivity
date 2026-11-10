# Persian Localization Mission

## Mission

Improve the Persian (Farsi) localization of Super Productivity in a way that follows the project's existing internationalization workflow and is maintainable across future upstream releases.

The goal is not to create a private translation fork. The intended outcome is a reviewed, consistent Persian locale that can eventually be proposed to the upstream project through a pull request.

## Source files and project guidance

- [English source locale — `en.json`](../src/assets/i18n/en.json)
- [Persian locale — `fa.json`](../src/assets/i18n/fa.json)
- [Translation Guide](TRANSLATING.md)
- [i18n script usage](i18n-script-usage.md)
- [Translation consistency test](../tools/test-lng-files.js)
- [Translation management script](../tools/add-missing-i18n-variables.js)

The English locale is the reference and fallback language. Keep the nested key structure and interpolation placeholders intact.

## Current baseline

- Upstream repository: `super-productivity/super-productivity`
- Upstream default branch: `master`
- Fork: `jooya98/super-productivity`
- Working branch: `i18n/persian-localization`
- Baseline commit: `3650a6647797ed70260f13c39245d46c39afa2f6`
- The Persian locale already exists. This mission focuses on improving its terminology, writing quality, completeness, and consistency.
- This branch currently contains mission documentation only. Neither `en.json` nor `fa.json` has been changed as part of the setup.

## Work plan

### Phase 1 — Repository preparation

- [x] Create a public fork of the upstream repository.
- [x] Create a dedicated branch from the current upstream `master`.
- [x] Document this mission and its workflow.
- [x] Link the reference locale files and the upstream translation instructions.

### Phase 2 — Persian terminology and style guide

Prepare a consistent glossary and writing policy before editing the locale.

Cover at least:

- Preferred Persian equivalents for recurring product concepts (for example task, project, tag, backlog, time tracking, estimate, schedule, focus mode, and sync).
- Formality and tone appropriate for a productivity application.
- Persian typography: half-spaces, punctuation, quotation marks, digits, and spacing around Latin product names.
- Rules for technical terms, product names, abbreviations, and mixed Persian/English strings.
- UI brevity and consistency across menus, buttons, dialogs, notifications, and help text.

Do not treat the example terms above as a finalized glossary; agree on their exact equivalents during this phase.

### Phase 3 — Audit and improve the Persian locale

Compare `fa.json` with `en.json` and review the Persian strings in context.

Check for:

- Inaccurate, awkward, ambiguous, or inconsistent translations.
- Untranslated or outdated text.
- Grammar, spelling, half-space, punctuation, and typography problems.
- Inconsistent product terminology.
- Missing, altered, or malformed interpolation placeholders such as `{{count}}`, `{{title}}`, and `{{version}}`.
- Differences in meaning, warnings, confirmation prompts, and data-loss or recovery messages.

Preserve JSON validity, key names, nesting, and the meaning of the English source. Do not translate product names or technical identifiers blindly. An untranslated key should use the documented English fallback rather than an empty string or a copied English value in `fa.json`.

#### Follow the upstream i18n workflow

- For improvements to the Persian wording of existing keys, update only the corresponding string values in `fa.json`; do not rename, move, or restructure keys.
- Do not manually invent or add missing locale keys. Use the project's WIP workflow:
  1. `node tools/add-missing-i18n-variables.js extract fa`
  2. Translate the missing entries in the generated `fa-wip.json`.
  3. `node tools/add-missing-i18n-variables.js merge fa`
- When an existing English source string gains or changes a placeholder, update the corresponding Persian string to preserve that placeholder too.
- If English keys are added or changed, follow [Translation Guide](TRANSLATING.md); regenerate translation constants with `npm run int` when required.
- Do not run the legacy script mode casually: it updates missing keys across all locale files, not only Persian.

### Phase 4 — Validation and upstream contribution

This phase starts only after the translation and review work is ready and the repository owner explicitly asks to proceed.

- Validate JSON syntax and compare the key structure with the English source.
- Run `npm run int:test` (the project's locale and placeholder consistency checks).
- Review the final diff to ensure only intended localization files and agreed documentation are included.
- Launch the application and inspect representative screens in Persian/RTL. Check clipping, alignment, punctuation, mixed-direction text, numbers, dates, tooltips, dialogs, and notifications.
- Separate any genuine application-level RTL/layout defect from translation wording; do not silently expand a translation-only change into unrelated UI or calendar work.
- Prepare a focused pull request from `jooya98/super-productivity:i18n/persian-localization` to `super-productivity/super-productivity:master`.
- Do not open or merge the pull request until explicitly requested.

## Completion criteria

The localization is ready for upstream review when:

1. The glossary and style rules are consistent and documented.
2. Persian strings are accurate, natural, concise, and consistent with the product's terminology.
3. Key paths and all interpolation placeholders are preserved.
4. The locale consistency checks pass.
5. Representative UI screens have been reviewed in Persian/RTL.
6. The proposed diff is focused, reviewable, and does not include unrelated application changes.

---

## راهنمای اجرایی فارسی

### هدف

بهبود ترجمهٔ فارسی Super Productivity با رعایت سازوکار رسمی i18n پروژه؛ به شکلی که نتیجه قابل نگهداری باشد و در نسخه‌های بعدی با تغییرات upstream از بین نرود. هدف نهایی، آماده‌سازی مشارکت برای ارسال Pull Request به مخزن اصلی است، نه نگهداری یک Fork مستقل.

### فایل‌های مرجع

- [فایل انگلیسی `en.json`](../src/assets/i18n/en.json)
- [فایل فارسی `fa.json`](../src/assets/i18n/fa.json)
- [راهنمای رسمی ترجمه](TRANSLATING.md)
- [راهنمای اسکریپت مدیریت ترجمه‌ها](i18n-script-usage.md)

### ترتیب کار

1. ابتدا واژه‌نامه و دستورالعمل نگارشی فارسی را مشخص کنید.
2. سپس ترجمهٔ فعلی را با فایل انگلیسی مقایسه و عبارت‌های نامناسب، مبهم، ناقص یا ترجمه‌نشده را شناسایی کنید.
3. ترجمهٔ کلیدهای موجود را با حفظ ساختار JSON و تمام Placeholderها اصلاح کنید.
4. برای کلیدهای جدید یا جاافتاده از فایل موقت `fa-wip.json` و دستورات رسمی `extract` و `merge` استفاده کنید؛ کلید جدید را دستی به فایل اصلی فارسی اضافه نکنید.
5. پس از آماده‌شدن ترجمه، مرحلهٔ اعتبارسنجی و آماده‌سازی Pull Request انجام می‌شود؛ این مرحله تا اعلام صریح مالک مخزن آغاز نخواهد شد.

### قواعد مهم

- زبان انگلیسی مرجع و fallback است.
- رشتهٔ خالی یا کپی انگلیسی را برای ترجمهٔ انجام‌نشده در `fa.json` قرار ندهید.
- نام کلیدها، ساختار تو‌در‌تو و Placeholderها را تغییر ندهید.
- یک مفهوم واحد باید در سراسر برنامه معادل فارسی یکسانی داشته باشد.
- اصلاح مشکلات واقعی RTL در رابط کاربری، در صورت نیاز، باید جدا از تغییرات ترجمه بررسی شود.

**وضعیت فعلی:** فقط Fork، شاخه و این سند مأموریت ایجاد شده‌اند. هنوز هیچ تغییری در `en.json` یا `fa.json` اعمال نشده و Pull Request نیز ساخته نشده است.
