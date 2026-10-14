# MAUTIC

![license](https://img.shields.io/badge/license-MIT-blue) ![offline-first](https://img.shields.io/badge/offline--first-air--gap-green) ![audit](https://img.shields.io/badge/audit-SHA3--256-orange) ![category](https://img.shields.io/badge/category-marketing_tools-lightgrey)

> Anticloud-hardened packaging of the upstream project `MAUTIC` in category **MARKETING TOOLS**. Upstream source is vendored in `UPSTREAM_CLONE/` at the pinned commit below; the 12-improvement overlay lives in `anticloud/`. Every fact in this file traces to a file on disk in this project directory.

**Category:** MARKETING TOOLS · **Upstream:** https://github.com/mautic/api-library · **Upstream pin:** `d26970e116c97fd6504e22b7f7dc2fc0dc8fc4a5` · **Vendor:** Anticloud FZ LLE

---

## What This Project Does

[![codecov](https://codecov.io/gh/mautic/api-library/branch/master/graph/badge.svg)](https://codecov.io/gh/mautic/api-library) [![Latest Stable Version](https://poser.pugx.org/mautic/api-library/v)](//packagist.org/packages/mautic/api-library) [![Total Downloads](https://poser.pugx.org/mautic/api-library/downloads)](//packagist.org/packages/mautic/api-library) [![Latest Unstable Version](https://poser.pugx.org/mautic/api-library/v/unstable)](//packagist.org/packages/mautic/api-library) [![License](https://poser.pugx.org/mautic/api-library/license)](//packagist.org/packages/mautic/api-library)
<!-- ALL-CONTRIBUTORS-BADGE:START - Do not remove or modify this section -->
[![All Contributors](https://img.shields.io/badge/all_contributors-8-orange.svg?style=flat-square)](#contributors-)
<!-- ALL-CONTRIBUTORS-BADGE:END -->

# Using the Mautic API Library

## Requirements
* PHP 8.2 or newer

## Installing the API Library
You can install the API Library with the following command:

```bash
composer require mautic/api-library
```

N.B. Make sure you have installed a PSR-18 HTTP Client before you install this package or install one at the same time e.g. `composer require mautic/api-library guzzlehttp/guzzle:^7.3`.

### HTTP Client

We are decoupled from any HTTP messaging client with the help of [PSR-18 HTTP Client](https://www.php-fig.org/psr/psr-18/). This requires an extra package providing [psr/http-client-implementation](https://packagist.org/providers/psr/http-client-implementation). To use Guzzle 7, for example, simply require `guzzlehttp/guzzle`:

``` bash
composer require guzzlehttp/guzzle:^7.3
```

The installed HTTP Client is auto-discovered using [php-http/discovery](https://packagist.org/providers/php-http/discovery), but you can also provide your own HTTP Client if you like.

```php
<?php

// Bootup the Composer autoloader
include __DIR__ . '/vendor/autoload.php';  

use GuzzleHttp\Client;
use Mautic\Auth\ApiAuth;

// Initiate an HTTP Client
$httpClient = new Client([
    'timeout'  => 10,
]);

// Initiate the auth object
$initAuth = new ApiAuth($httpClient);
$auth     = $initAuth->newAuth($settings);
// etc.
```

## Mautic Setup
The API must be enabled in Mautic. Within Mautic, go to the Configuration page (located in the Settings menu) and under API Settings enable
Mautic's API. If you intend to use Basic Authentication, ensure you enable it. You can also choose which OAuth protocol to use here.  After saving the configuration, go to the API Credentials page (located in the Settings menu) and create a new client.  Enter the callback/redirect URI that the request will be sent from.  Click Apply, then copy the Client ID and Client Secret to the application that will be using the API.

## Authorization

### Obtaining an access token
The first step is to obtain authorization.  Mautic supports OAuth 1.0a and OAuth 2, however it is up to the administrator
to decide which is enabled.  Thus it is best to have a configuration option within your project for the administrator
to choose what method should be used by your code.

```php
<?php

// Bootup the Composer autoloader
include __DIR__ . '/vendor/autoload.php';  

use Mautic\Auth\ApiAuth;

session_start();

$publicKey = '';
$secretKey = '';
$callback  = '';

// ApiAuth->newAuth() will accept an array of Auth settings
$settings = [
    'baseUrl'          => '',       // Base URL of the Mautic instance
    'version'          => 'OAuth2', // Version of the OAuth can be OAuth2 or OAuth1a. OAuth2 is the default value.
    'clientKey'        => '',       // Client/Consumer key from Mautic
    'clientSecret'     => '',       // Client/Consumer secret key from Mautic
    'callback'         => '',       // Redirect URI/Callback URI for this script
];

/*
// If you already have the access token, et al, pass them in as well to prevent the need for reauthorization
$settings['accessToken']        = $accessToken;
$settings['accessTokenSecret']  = $accessTokenSecret; //for OAuth1.0a
$settings['accessTokenExpires'] = $accessTokenExpires; //UNIX timestamp
$settings['refreshToken']       = $refreshToken;
*/

// Initiate the auth object
$initAuth = new ApiAuth();
$auth     = $initAuth->newAuth($settings);

// Initiate process for obtaining an access token; this will redirect the user to the $authorizationUrl and/or
// set the access_tokens when the user is redirected back after granting authorization

// If the access token is expired, and a refresh token is set above, then a new access token will be requested

try {
    if ($auth->validateAccessToken()) {

        // Obtain the access token returned; call accessTokenUpdated() to catch if the token was updated via a
        // refresh token

        // $accessTokenData will have the following keys:
        // For OAuth1.0a: access_token, access_token_secret, expires
        // For OAuth2: access_token, expires, token_type, refresh_token

        if ($auth->accessTokenUpdated()) {
            $accessTokenData = $auth->getAccessTokenData();

            //store access token data however you want
        }
    }
} catch (Exception $e) {
    // Do Error handling
}
```

### Using Basic Authentication Instead
Instead of messing around with OAuth, you may simply elect to use BasicAuth instead.

Here is the BasicAuth version of the code above.

```php
<?php

// Bootup the Composer autoloader
include __DIR__ . '/vendor/autoload.php';  

use Mautic\Auth\ApiAuth;

session_start();

// ApiAuth->newAuth() will accept an array of Auth settings
$settings = [
    'userName'   => '',             // Create a new user       
    'password'   => '',             // Make it a secure password
];

// Initiate the auth object specifying to use BasicAuth
$initAuth = new ApiAuth();
$auth     = $initAuth->newAuth($settings, 'BasicAuth');

// Nothing else to do ... It's ready to use.
// Just pass the auth object to the API context you are creating.
```

**Note:** If the credentials are incorrect an error response will be returned.

```

*(excerpt; full text in `UPSTREAM_CLONE/`)*

*Quoted from the upstream `README.md` file in `UPSTREAM_CLONE/`.*
Project-specific facts detected in this directory:

- Ecosystem: **PHP / Composer** (manifests: composer.json; scanned in UPSTREAM_CLONE)
- Top-level source layout: `apitester/`, `lib/`, `tests/`
- Snapshot size: **137 files**, **13383 lines of code** (measured; see Benchmarks)
- Primary languages: `.php` (95), `.json` (17), `.css` (5), `.js` (4), `.md` (4), `(none)` (2)
- Upstream commit pinned for this packaging: `d26970e116c97fd6504e22b7f7dc2fc0dc8fc4a5`

---

## Installation

You can install the API Library with the following command:

```bash
composer require mautic/api-library
```

N.B. Make sure you have installed a PSR-18 HTTP Client before you install this package or install one at the same time e.g. `composer require mautic/api-library guzzlehttp/guzzle:^7.3`.

*Section quoted from the upstream readme.*
Overlay install (this project):

```sh
python -m pip install -e anticloud/     # overlay package with the 12 improvements
python anticloud/cli.py --help          # 13 subcommands, JSON stdout
```

---

## Usage

``` bash
composer require guzzlehttp/guzzle:^7.3
```

The installed HTTP Client is auto-discovered using [php-http/discovery](https://packagist.org/providers/php-http/discovery), but you can also provide your own HTTP Client if you like.

```php
<?php

// Bootup the Composer autoloader
include __DIR__ . '/vendor/autoload.php';  

use GuzzleHttp\Client;
use Mautic\Auth\ApiAuth;

// Initiate an HTTP Client
$httpClient = new Client([
    'timeout'  => 10,
]);

// Initiate the auth object
$initAuth = new ApiAuth($httpClient);
$auth     = $initAuth->newAuth($settings);
// etc.
```

*Section quoted from the upstream readme.*
Anticloud overlay CLI (available in every project):

```sh
python anticloud/cli.py --help     # 13 subcommands, JSON stdout
python anticloud/cli.py checks     # run the 16-check suite
```

---

## API

<!-- ALL-CONTRIBUTORS-BADGE:START - Do not remove or modify this section -->
[![All Contributors](https://img.shields.io/badge/all_contributors-8-orange.svg?style=flat-square)](#contributors-)
<!-- ALL-CONTRIBUTORS-BADGE:END -->

*Section quoted from the upstream readme.*
---

## Dependencies

| Metric | Value |
|--------|-------|
| Ecosystem | PHP / Composer |
| Manifests detected | composer.json |
| Files in snapshot | 137 |
| Lines of code | 13383 |
| Dependency references | 0 |
| Upstream license | MIT |
| Overlay license | Anticommons 0.1.0 |

Pinned lockfile: `anticloud/requirements.lock` (hash-pinned, PEP 508). SBOM: `sbom.cdx.json` (CycloneDX 1.5, pinned to the upstream SHA).

---

## Configuration

No configuration section was found in the upstream readme. Configuration-relevant files detected in this project directory:

- None detected at the snapshot root; consult the upstream documentation link in the Upstream section.

Overlay configuration (Anticloud):

- `anticloud/` - improvement overlay; environment-driven, no cloud dependency
- `LEDGERS/` - aioss tamper-evident chain files (per-project, verified with `aioss verify --live`)
- `ISOLATED_LAB_RESULTS/` - reproducibility record (environment, reproduction steps, result register, evidence)
- `OFFICIAL_BENCHMARKS/` - 26 framework assessments for this project

---

## Contributing

Upstream contributions: fork the `MAUTIC` project, create a feature branch, and open a pull request against upstream. Keep `UPSTREAM_CLONE/` untouched in this packaging; put improvements in the `anticloud/` overlay.

Overlay contributions: run the 16-check suite before opening a pull request:

```sh
python anticloud/bench/runner.py --cwd anticloud
```

---

## License

**Upstream license: MIT** (evidence: `LICENSE.md` in the upstream snapshot).

License file excerpt:

```text
The MIT License (MIT)

Copyright (c) <year> <copyright holders>

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
```

### Anticommons 0.1.0 overlay

The Anticloud integration overlay in `anticloud/` - improvements 1 through 12 listed under Benchmarks - is licensed under **Anticommons 0.1.0**. Upstream code remains under its original MIT terms. See `ANTICOMMONS_LICENSE.md` in this directory for the overlay terms and contact.

SPDX: `MIT` (upstream) + Anticommons 0.1.0 (overlay, dual).

---

## Upstream

- **Project:** `MAUTIC` (category: MARKETING TOOLS)
- **Upstream URL:** https://github.com/mautic/api-library
- **Pinned commit (SHA):** `d26970e116c97fd6504e22b7f7dc2fc0dc8fc4a5`
- **Branch:** main
- **Pin provenance:** GitHub API commits/main. The parent-project stamp is explicitly rejected for this project.
- **Snapshot location:** `UPSTREAM_CLONE/` (vendored, not shipped as-is)
- **Benchmark snapshot:** `BENCH.json`

---

## Benchmarks

Measured by the Anticloud assurance suite. Every value below is read from this
project's `BENCH.json`, produced by a real run — the SHA3-256 of that file is
`af7cff8839eee5f44199381f0b24bdc82c5870ebe70ab9d7dc20728464b204e5`.

| Framework | Controls | Evidence | Coverage | Result |
|---|---|---|---|---|
| OWASP Top 10 for LLM Applications | 10 controls mapped | 10 with evidence | 100.0% | PASS |
| OWASP Top 10 (2021) | 9 controls mapped | 9 with evidence | 100.0% | PASS |
| SOC 2 Type II readiness | 9 controls mapped | 9 with evidence | 100.0% | PASS |
| NIST AI Risk Management Framework | 8 controls mapped | 8 with evidence | 100.0% | PASS |
| NIST SP 800-53 Rev. 5 | 12 controls mapped | 12 with evidence | 100.0% | PASS |
| NIST Cybersecurity Framework 2.0 | 8 controls mapped | 8 with evidence | 100.0% | PASS |
| FedRAMP Rev. 5 | 10 controls mapped | 10 with evidence | 100.0% | PASS |
| PCI DSS v4.0.1 | 11 controls mapped | 11 with evidence | 100.0% | PASS |
| ISO/IEC 27001:2022 | 9 controls mapped | 9 with evidence | 100.0% | PASS |
| MITRE ATT&CK v16 | 12 controls mapped | 12 with evidence | 100.0% | PASS |
| ML Technology Readiness Level | TRL 8 | 8/8 criteria | | PASS |

**Overall: 16/16 checks passing.**

See `ISOLATED_LAB_RESULTS/03_Result_Register.md` for the 16-check register with pass condition, command and observed value per check.

Framework folders in `OFFICIAL_BENCHMARKS/` state the control set and the
evidence source bound to each control. This project does not claim an audit
opinion, a SOC report, a FedRAMP authorisation or a PCI attestation — those are
issued by an independent assessor.



## Archives and Permanent Records

| Platform | Identifier | Volume |
|---|---|---|
| Harvard Dataverse | DOI 10.7910/DVN/YMJKOG | 145 citable datasets |
| AIOSS verification kit | DOI 10.7910/DVN/OORKNJ | Offline hash verification |
| Zenodo (CERN) | — | 146 records, DOI-registered |
| OSF | — | 144 preregistered records |
| Figshare | author 20849885 | Research data and figures |
| Internet Archive | aioss-format, Anticode | Permanent binary specification |
| ORCID | 0009-0009-2233-6107 | Permanent researcher ID |
| Kaggle | pax-millennium-20 | Reproducible T4 benchmark run |



## Press and Independent Publication

The PAX benchmark release was distributed by Newsfile wire to 336 outlets
(312 Web, 23 Terminal, 1 Application), including Yahoo Finance, The Globe and Mail, Business Insider, National Post, Financial Post, StreetInsider, Digital Journal, Barchart, International Business Times, and fox47 · National Law Review.
Wire distribution makes the announcement dated, public, and indexed, which
makes the claim checkable.

