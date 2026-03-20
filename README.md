# CrawlerProtection

Protect wikis against crawler bots. CrawlerProtection denies **anonymous** user
access to certain MediaWiki action URLs and SpecialPages which are resource
intensive.

# Configuration

* `$wgCrawlerProtectedSpecialPages` - array of special pages to protect
  (default: `[ 'mobilediff', 'recentchangeslinked', 'whatlinkshere' ]`).
  Supported values are special page names or their aliases regardless of case.
  You do not need to use the 'Special:' prefix. Note that you can fetch a full
  list of SpecialPages defined by your wiki using the API and jq with a simple
  bash one-liner like
  `curl -s "[YOURWIKI]api.php?action=query&meta=siteinfo&siprop=specialpagealiases&format=json" | jq -r '.query.specialpagealiases[].aliases[]' | sort`
  Of course certain Specials MUST be allowed like Special:Login so do not block
  everything.
* `$wgCrawlerProtectionUse418` - drop denied requests in a quick way via
  `die();` with
  [418 I'm a teapot](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Status/418)
  code (default: `false`)
* `$wgCrawlerProtectedActions` - add a list of actions to be denied
  (default: `[ 'history' ]`).

#  Version history

1.0.0

* MyWikis LLC

1.1.0 (Jun 30, 2025)

* add: ProtectionUse418
* 1.43 compatibility

1.2.0 (Aug 13, 2025)

* Fix 403 handling and add login links to prevent nginx 404 fallthrough

1.3.0 (Oct 11, 2025)

* Add oldid parameter blocking to special pages and comprehensive tests

1.4.0 (Feb 19, 2026)

* Add configurable action protection with $wgCrawlerProtectedActions

1.5.0 (Mar 4, 2026)

* Add custom header and text settings for access-denial display
