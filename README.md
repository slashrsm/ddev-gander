[![tests](https://github.com/tag1consulting/ddev-gander/actions/workflows/tests.yml/badge.svg)](https://github.com/tag1consulting/ddev-gander/actions/workflows/tests.yml) ![project is maintained](https://img.shields.io/maintenance/yes/2024.svg)

# ddev-gander <!-- omit in toc -->

* [What is gander?](#what-is-ddev-gander)
* [Prerequisites?](#prerequisites)
* [Getting started?](#getting-started)

## What is Gander?

Gander is a preconfigured Open Telemetry stack relying on Prometheus, Grafana, and Grafana Tempo.

`ddev get tag1consulting/ddev-gander`, run Drupal core's OpenTelemetry phpunit tests, and immediately see performance metrics and traces in a Grafana dashboard. Or add PerformanceTestBase coverage to an existing project with a few lines of code if you already have phpunit functional test coverage of your project.

For more information on the phpunit side of things, see [the Drupal core change record](https://www.drupal.org/node/3366904).


## Prerequisites:
* [Install ddev](https://ddev.readthedocs.io/en/latest/users/install/ddev-installation/) if you haven't already.
* Enable ddev on your local Drupal project.
* Ensure you can already run functional JavaScript tests in the ddev environment. This requires a working chromedriver container as part of your ddev installation. You can run any core functional javascript test without having Gander installed to confirm.

If you are running on an M1 or M2 Mac, add the following steps to get chromedriver working, this may also be the most reliable method on other platforms.

```
cd .ddev
rm docker-compose.chromedriver.yml
ddev get ddev/ddev-selenium-standalone-chrome
```

Or see [Matt Glaman's guide](https://mglaman.dev/blog/running-drupals-functionaljavascript-tests-ddev) 

And if you have issues with both of these methods, check [resources linked from this ddev issue](https://github.com/ddev/ddev/issues/3578).

## Getting started
Add Gander and run Drupal's performance tests via a git clone of Drupal core:
* ddev get tag1consulting/ddev-gander
* ddev restart
* ddev ssh
* To run a single test: `vendor/bin/phpunit -c core/phpunit.xml profiles/demo_umami/tests/src/FunctionalJavascript/OpenTelemetryNodePagePerformanceTest.php`
* To run all Gander tests: `vendor/bin/phpunit -c core/phpunit.xml --group OpenTelemetry`
* Check the Grafana dashboard via: http://localhost:3000/
* You might need to run the test a few times for the data to start appearing on the dashboard. For example: `for run in 1..3; do vendor/bin/phpunit -c core/phpunit.xml profiles/demo_umami/tests/src/FunctionalJavascript/OpenTelemetryNodePagePerformanceTest.php --filter hot; done;`
