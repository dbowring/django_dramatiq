# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](http://keepachangelog.com/en/1.0.0/)
and this project adheres to [Semantic Versioning](http://semver.org/spec/v2.0.0.html).

## [0.13.0] - 2025-02-24

### Added
Set number of processes/threads through DRAMATIQ_NPROCS, DRAMATIQ_NTHREADS. ([m000], [#186])

[m000]: https://github.com/m000
[#186]: https://github.com/Bogdanp/django_dramatiq/pull/186

## [0.12.0] - 2024-12-29
### Changed
- Set thread count to 8 as per dramatiq default. Fix [#153]. ([@andrewgy8], [#170])
- Use ArgumentDefaultsHelpFormatter to show the defaults for rundramatiq options. (#167)

[@andrewgy8]: https://github.com/andrewgy8
[#153]: https://github.com/Bogdanp/django_dramatiq/issues/153
[#170]: https://github.com/Bogdanp/django_dramatiq/pull/170

### Added
- Display task details in the admin when JSONEncoder is not used. Fix [#135]. ([@huubbouma], [#136])
- Support for Python 3.13
- Support for Django 5.1

[@huubbouma]: https://github.com/huubbouma
[#135]: https://github.com/Bogdanp/django_dramatiq/issues/135
[#136]: https://github.com/Bogdanp/django_dramatiq/pull/136

### Dropped
- Support for Python 3.8
- Support for Django 3.2

## [0.11.6] - 2023-12-12
### Added
- Support for Python 3.12
- Support for Django 5.0

## [0.11.5] - 2023-08-11
### Added
- Fix exception traceback on Python 3.8

## [0.11.4] - 2023-07-05
### Added
- Support for Django 4.2
- Add skip-logging flag to `rundramatiq` command

## [0.11.3] - 2023-07-04
### Added
- Store traceback in django admin even when retries=0

### Dropped
- Support for Python 3.7
- Support for Django 4.0

## [0.11.2] - 2022-11-18
### Changed
- Replaced `AppConfig.ready` workaround with `__init__` to fix [#133]. ([@amureki], [#137])

[@amureki]:  https://github.com/amureki
[#133]: https://github.com/Bogdanp/django_dramatiq/issues/133
[#137]: https://github.com/Bogdanp/django_dramatiq/pull/137

## [0.11.1] - 2022-11-11
### Added
- Support for Python 3.10 and 3.11
- Support for Django 4.0 and 4.1

### Changed
- Fixed issue [#123] in deferred `DjangoDramatiqConfig` initialization. 
  Dramatiq configuration now happens before loading importing all Django apps models,
  so loaded tasks will use the correct Dramatiq settings. ([@amureki], [#126])

### Dropped
- Support for Python 3.6
- Support for Django 2.2 and 3.1

[@amureki]:  https://github.com/amureki
[#123]: https://github.com/Bogdanp/django_dramatiq/issues/123
[#126]: https://github.com/Bogdanp/django_dramatiq/pull/126

## [0.11.0] - 2022-06-11
### Added

- The `DRAMATIQ_AUTODISCOVER_MODULES` setting. ([@thebjorn], [#97], [#98], [#99])
- The `--worker-shutdown-timeout` flag to `rundramatiq`. ([@b1ngz], [#110])

### Changed

- Initialization is now deferred until the application is ready.  This
  is somewhat of a major change to how configuration works, but it's
  more in line with what Django expects from apps. If you run into
  issues importing your tasks, consider deferring your imports as much
  as you can (eg. import tasks in your methods instead of at the top
  level). ([#103])

[@b1ngz]: https://github.com/b1ngz
[@thebjorn]: https://github.com/thebjorn
[#97]: https://github.com/Bogdanp/django_dramatiq/issues/97
[#98]: https://github.com/Bogdanp/django_dramatiq/issues/98
[#99]: https://github.com/Bogdanp/django_dramatiq/issues/99
[#103]: https://github.com/Bogdanp/django_dramatiq/pull/103
[#110]: https://github.com/Bogdanp/django_dramatiq/pull/110

## [0.10.0] - 2021-03-21
### Added

- Added the `--fork-function` flag to `rundramatiq`. ([@timdrijvers], [#63])
- Added support for setting middleware kwargs at runtime. ([@dnmellen], [#83])

[@dnmellen]: https://github.com/dnmellen
[@timdrijvers]: https://github.com/timdrijvers
[#63]: https://github.com/Bogdanp/django_dramatiq/issues/63
[#83]: https://github.com/Bogdanp/django_dramatiq/issues/83

## [0.9.1] - 2020-02-04
### Fixed

- Added a missing migration for the Tasks table. ([#60])

[#60]: https://github.com/Bogdanp/django_dramatiq/issues/60

## [0.9.0] - 2020-02-01
### Changed

- The admin middleware now stores the queue and actor name in the
  database, improving filtering performance for databases containing
  lots of tasks.  ([@Sovetnikov], [#56])

### Fixed

- Skipped messages are now properly handled by the admin
  middleware. ([@Sovetnikov], [#59])
- `rundramatiq` now properly respects `DRAMATIQ_IGNORED_MODULES`.
  ([@OrazioPirataDelloSpazio], [#57])

[@OrazioPirataDelloSpazio]: https://github.com/OrazioPirataDelloSpazio
[@Sovetnikov]: https://github.com/Sovetnikov
[#56]: https://github.com/Bogdanp/django_dramatiq/pull/56
[#57]: https://github.com/Bogdanp/django_dramatiq/pull/57
[#59]: https://github.com/Bogdanp/django_dramatiq/pull/59

## [0.8.0] - 2019-08-31
### Added

- `rundramatiq` now discovers task packages.  ([@AceFire6], [#46])
- Tasks in the admin can now be filtered by `queue_name` and
  `actor_name`. ([@jcass77], [#50])

[@AceFire6]: https://github.com/AceFire6
[#46]: https://github.com/Bogdanp/django_dramatiq/pull/46
[@jcass77]: https://github.com/jcass77
[#50]: https://github.com/Bogdanp/django_dramatiq/pull/50

### Changed

- `--no-reload` command line flag has been changed to `--reload`.
  This is a breaking change to the `rundramatiq` command.
  ([@ramonsaraiva], [#42])

[@ramonsaraiva]: https://github.com/ramonsaraiva
[#42]: https://github.com/Bogdanp/django_dramatiq/pull/42

### Fixed

- The 'ETA' column for Tasks in the admin now checks the Django
  `USE_TZ` configuration setting to ensure that dates are displayed
  using the same timezone as the Django standard columns. ([#51],
  [@jcass77])

[@jcass77]: https://github.com/jcass77
[#51]: https://github.com/Bogdanp/django_dramatiq/pull/51

## [0.7.1] - 2019-06-06
### Added

- Tasks in the admin can now be filtered by `status`. ([@MightySCollins], [#37])
- The build now includes Django-specific classifiers. ([@OmenApps], [#39])

[@MightySCollins]: https://github.com/MightySCollins
[#37]: https://github.com/Bogdanp/django_dramatiq/pull/37
[@OmenApps]: https://github.com/OmenApps
[#39]: https://github.com/Bogdanp/django_dramatiq/pull/39

## [0.7.0] - 2019-03-28
### Added

- `DRAMATIQ_IGNORED_MODULES` setting.  ([@denizdogan], [#33], [#34])

[@denizdogan]: https://github.com/denizdogan
[#33]: https://github.com/Bogdanp/django_dramatiq/issues/33
[#34]: https://github.com/Bogdanp/django_dramatiq/pull/34

### Changed

- Tasks are now read-only.  ([@CapedHero], [#29], [#30])

[@CapedHero]: https://github.com/CapedHero
[#29]: https://github.com/Bogdanp/django_dramatiq/issues/29
[#30]: https://github.com/Bogdanp/django_dramatiq/issues/30

## [0.6.0] - 2019-02-21
### Changed

- The broker is set up as soon as the `django_dramatiq` application is
  loaded.  This fixes issue [#26] and is technically a breaking change
  for middleware writers.

[#26]: https://github.com/Bogdanp/django_dramatiq/issues/26

## [0.5.3] - 2019-01-31
### Changed

- A default rate limiter backend can now be configured.  ([#25], [@StasEvseev])

[#25]: https://github.com/Bogdanp/django_dramatiq/pull/25
[@StasEvseev]: https://github.com/StasEvseev

## [0.5.2] - 2019-01-05
### Fixed

- Expired connections are now closed before and after each message. ([#19])

[#19]: https://github.com/Bogdanp/django_dramatiq/issues/19

## [0.5.1] - 2018-11-10
### Fixed

- Tasks are now upserted more safely. ([#23], [@aericson])

[#23]: https://github.com/Bogdanp/django_dramatiq/pull/23
[#@aericson]: https://github.com/aericson

## [0.5.0] - 2018-09-22
### Added

- Support for configuring result backends in settings via
  `DRAMATIQ_RESULT_BACKEND`. ([#18], [@xdmiodz])
- `--queue`, `--pid-file` and `--log-file` arguments are now passed
  through to the `dramatiq` command.  ([#20], [@MattBlack85])

[#18]: https://github.com/Bogdanp/django_dramatiq/pull/18
[#20]: https://github.com/Bogdanp/django_dramatiq/pull/20
[@MattBlack85]: https://github.com/MattBlack85
[@xdmiodz]: https://github.com/xdmiodz

## [0.4.1] - 2018-07-15
### Fixed

- Instances can now be passed to middleware list in settings.  ([#14])

[#14]: https://github.com/Bogdanp/django_dramatiq/issues/14

## [0.4.0] - 2018-07-11
### Added

- `DRAMATIQ_ENCODER` setting.

## [0.3.0] - 2018-04-14
### Added

- `DramatiqTestCase`

## [0.2.2] - 2018-01-06
### Fixed

- `--path` is now the first to be passed to `dramatiq`.  This fixes an
  issue where the workers wouldn't boot when the `-no-reload` flag was
  set.

## [0.2.0] - 2018-01-06
### Added

- `--path` command line argument.

### Changed

- The broker is now set up by `DjangoDramatiqConfig.ready`.
- The minimum dramatiq version is now 0.18.
- `BASE_DIR` is no longer a required setting.

### Fixed

- `Task.message` no handles `memoryview`s properly.

## [0.1.5] - 2017-12-22
### Fixed

- Python 3.5 is now supported.

## [0.1.4] - 2017-12-08
### Fixed

- Fixed use of `tobytes()` in `Task.message` for Django 2.0.

## [0.1.3] - 2017-11-20
### Added

- `--reload-use-polling` flag to force a poll-based file watcher
  instead of a OS-native one.  This is useful inside of Vagrant and
  Docker. ([Dramatiq #18])

[Dramatiq #18]: https://github.com/Bogdanp/dramatiq/issues/18

## [0.1.2] - 2017-11-20
### Fixed

- Tasks modules and packages are now detected using Django's built-in
  `module_has_submodule` helper. ([@rakanalh])

[@rakanalh]: https://github.com/rakanalh

## [0.1.1] - 2017-11-15
### Fixed

- `dramatiq` and `dramatiq-gevent` are now resolved according to
  `sys.executable` ([@rakanalh]).

[@rakanalh]: https://github.com/rakanalh


[Unreleased]: https://github.com/Bogdanp/django_dramatiq/compare/v0.12.0...HEAD
[0.12.0]: https://github.com/Bogdanp/django_dramatiq/compare/v0.11.6...v0.12.0
[0.10.0]: https://github.com/Bogdanp/django_dramatiq/compare/v0.9.1...v0.10.0
[0.9.1]: https://github.com/Bogdanp/django_dramatiq/compare/v0.9.0...v0.9.1
[0.9.0]: https://github.com/Bogdanp/django_dramatiq/compare/v0.8.0...v0.9.0
[0.8.0]: https://github.com/Bogdanp/django_dramatiq/compare/v0.7.1...v0.8.0
[0.7.1]: https://github.com/Bogdanp/django_dramatiq/compare/v0.7.0...v0.7.1
[0.7.0]: https://github.com/Bogdanp/django_dramatiq/compare/v0.6.0...v0.7.0
[0.6.0]: https://github.com/Bogdanp/django_dramatiq/compare/v0.5.3...v0.6.0
[0.5.3]: https://github.com/Bogdanp/django_dramatiq/compare/v0.5.2...v0.5.3
[0.5.2]: https://github.com/Bogdanp/django_dramatiq/compare/v0.5.1...v0.5.2
[0.5.1]: https://github.com/Bogdanp/django_dramatiq/compare/v0.5.0...v0.5.1
[0.5.0]: https://github.com/Bogdanp/django_dramatiq/compare/v0.4.1...v0.5.0
[0.4.1]: https://github.com/Bogdanp/django_dramatiq/compare/v0.4.0...v0.4.1
[0.4.0]: https://github.com/Bogdanp/django_dramatiq/compare/v0.3.0...v0.4.0
[0.3.0]: https://github.com/Bogdanp/django_dramatiq/compare/v0.2.2...v0.3.0
[0.2.2]: https://github.com/Bogdanp/django_dramatiq/compare/v0.2.1...v0.2.2
[0.2.1]: https://github.com/Bogdanp/django_dramatiq/compare/v0.2.0...v0.2.1
[0.1.5]: https://github.com/Bogdanp/django_dramatiq/compare/v0.1.4...v0.1.5
[0.1.4]: https://github.com/Bogdanp/django_dramatiq/compare/v0.1.3...v0.1.4
[0.1.3]: https://github.com/Bogdanp/django_dramatiq/compare/v0.1.2...v0.1.3
[0.1.2]: https://github.com/Bogdanp/django_dramatiq/compare/v0.1.1...v0.1.2
[0.1.1]: https://github.com/Bogdanp/django_dramatiq/compare/v0.1.0...v0.1.1
