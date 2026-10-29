# renovate-config

Shared Renovate preset for Wild Roar's Bedrock WordPress sites. Each site's `renovate.json` extends it and adds only its own `hostRules` (private composer repo auth):

```json
{
  "$schema": "https://docs.renovatebot.com/renovate-schema.json",
  "extends": ["github>wildroar/renovate-config"],
  "hostRules": []
}
```

What it does (`default.json`):

- Composer only. Every `composer.json` in the repo except `vendor/`, `node_modules/`, `web/wp/`, and composer-installed plugins/mu-plugins.
- One grouped PR (`renovate/composer-non-major`) for all minor/patch updates, on the 1st and 15th (America/Denver, midnight to 6am).
- Monthly lock file maintenance on the 1st.
- Majors are never opened automatically. Approve them from the Dependency Dashboard once the site is ready. phpcs 4 is disabled entirely (WPCS 3 needs phpcs 3).
- Security fixes open immediately, outside the schedule and the group.
- Composer resolves with PHP `8.3.*` (`constraints.php`). A site on a different server version overrides `constraints` in its own `renovate.json`.
- Nothing automerges.

This repo is public on purpose: the sites live under more than one GitHub account, and the Mend Renovate app can only read presets across accounts when they're public. Never put secrets here.
