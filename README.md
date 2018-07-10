# uk.co.vedaconsulting.mosaico

This extension integrates a responsive email template editor, [Mosaico](http://mosaico.io/), with CiviCRM.

 * [Initial Blog Post](https://civicrm.org/blogs/parvez/a-new-beginning-for-civimail)
 * [Beta Blog Post](https://civicrm.org/blog/deepaksrivastava/email-template-builder-civimosaico-is-now-beta)
 * [Initial Video](https://vimeo.com/156633077)
 * [v1.0 Stable Release](https://github.com/veda-consulting/uk.co.vedaconsulting.mosaico/releases/tag/1.0)
 * [v2.0 Plans](https://civicrm.org/blog/jamienovick/email-template-builder-mosaico-phase-2-plans)
 * [v2.0 and Styling Blog Post](https://civicrm.org/blog/jamienovick/extreme-makeovers-civicrm-style-introducing-the-shoreditch-theme-civicrms-new-user)

## Requirements

* CiviCRM
    * Recommended: `v4.7.{latest}`
    * Unofficial: `v4.6.26+` with [backports patch #9555](https://github.com/civicrm/civicrm-core/pull/9555)
* PHP-ImageMagick
* [FlexMailer](https://docs.civicrm.org/flexmailer/en/latest/) `v0.2-alpha5+`

## Installation

A CiviCRM extensions folder (In new sites since CiviCRM v4.7.0, this defaults to `files/civicrm/ext`. For older systems, see [the wiki](https://wiki.civicrm.org/confluence/display/CRMDOC/Extensions).)

#### Option 1: Download via Web

The official download URLs for Mosaico and related extensions are published on the CiviCRM.org Extension Directory. Download the latest releases of these extensions:

1. [`Shoreditch Theme`](https://civicrm.org/extensions/shoreditch)
2. [`FlexMailer`](https://civicrm.org/extensions/flexmailer)
3. [`Mosaico CiviCRM Integration`](https://civicrm.org/extensions/email-template-builder)

> __TIP__: `civicrm.org` downloads are intended for normal installations, and `github.com` downloads are intended for development. Downloads on `civicrm.org` and `github.com` are *often* the same -- but not always.

#### Option 2: Download via CLI

> This option requires command line tool [`cv`](https://github.com/civicrm/cv).

To download the current alpha/beta versions of Mosaico and its dependencies, run this one command:

```
cv dl --dev flexmailer shoreditch mosaico
```

Alternatively, you can download the latest nightly:

```
cv dl --dev flexmailer shoreditch
cv dl uk.co.vedaconsulting.mosaico@https://download.civicrm.org/extension/uk.co.vedaconsulting.mosaico/latest/uk.co.vedaconsulting.mosaico-latest.zip
```

> __TIP__: If you're using v4.6.x with backports, then `cv dl` will require an
> extra argument: "`--filter-ver=4.7.16`".  This enables it to download the
> latest extensions intended for v4.7.x (even if they aren't officially
> compatible with v4.6.x).

#### Option 3: Download via Git (preferred for development)

This option requires several command-line tools:

 * [`git`](https://git-scm.com/)
 * [`nodejs`](https://nodejs.org/en)
 * [`npm`](https://www.npmjs.com)
 * [`grunt-cli`](http://gruntjs.com/getting-started)
 * [`cv`](https://github.com/civicrm/cv)

Once these are installed, you should:

```
## Navigate to your extension directory, e.g.
cd sites/default/files/civicrm/ext

## Download the extensions
git clone https://github.com/civicrm/org.civicrm.flexmailer
git clone https://github.com/civicrm/org.civicrm.shoreditch
git clone https://github.com/veda-consulting/uk.co.vedaconsulting.mosaico

## Download additional dependencies
cd uk.co.vedaconsulting.mosaico
./bin/setup.sh -D
```

## Getting started (Usage)

If you haven't used Mosaico before, consult the the demo and tutorial materials from http://mosaico.io/index.html.

To send a new mailing, simply navigate to "Mailings => New Mailing". The CiviMail-Mosaico UI should appear.

Optionally, you may design reusable templates by navigating to "Mailings => Mosaico Templates".

When composing a new mailing with Mosaico, the screen may be configured as a three-step wizard or as a single-step form. To
choose a layout, navigate to "Administer => CiviMail => Mosaico Settings".

If you would like to compose mailings with the *old* CiviMail screen, navigate to "Mailings => New Mailing (Traditional)".

## Having issues with this extension?

Please make sure you have followed installation instructions.

Open issues on [github](https://github.com/veda-consulting/uk.co.vedaconsulting.mosaico/issues) with:
- screenshot of failure with any possible errors in firebug or js console
- any related logs or backtrace from civicrm
- tell us what version of CiviCRM and extension, you using.
- tell us the browser you are using (name and version) and test at least a second browser to tell us if this happen in both or only one (tell us the details about the second browser too).

## Development

#### Setup.sh

The script `bin/setup.sh` handles various build activities:

```
## Download dependencies
./bin/setup.sh -D

## Regenerate DAOs
./bin/setup.sh -g

## Build zip archive
./bin/setup.sh -z
```

#### Styling Changes

We use Gulp and Sass for styling and handle different running tasks. Firstly, you should install node packages using npm package manager:
```
npm install
```

Styling changes should go into `sass` directory and compiled to CSS using the following command:
```
gulp sass
```

#### Backstop Test suite

Backstop is integrated into the gulp architecture to give support for visual regression tesing. After installing node packages following commands will be available.

    ```shell
    gulp backstopjs:reference
    ```

    ```shell
    gulp backstopjs:test
    ```

For understanding and setting up the test suite see [TESTING.md](TESTING.md)

#### Patching Mosaico

This extensions ships with a patched version of Mosaico. The patches are maintained as a fork
in https://github.com/civicrm/mosaico using [Twigflow (Rebase)](https://gist.github.com/totten/39e932e5d10bc9e73e82790b2475eff2).

#### Testing

See [TESTING.md](TESTING.md)

#### Publication

Whenever a change is merged or pushed to `uk.co.vedaconsulting.mosaico`, a bot automatically builds a new `zip` archive
and publishes [uk.co.vedaconsulting.mosaico-latest.zip](https://download.civicrm.org/extension/uk.co.vedaconsulting.mosaico/latest/uk.co.vedaconsulting.mosaico-latest.zip).

The build/publish process has a few properties:
 * It combines [`uk.co.vedaconsulting.mosaico`](https://github.com/veda-consulting/uk.co.vedaconsulting.mosaico),
   [`civicrm/mosaico`](https://github.com/civicrm/mosaico), and any other runtime dependencies into one `zip` file.
 * The version number is determined by reading `info.xml` (`<version>`) and appending the current Unix timestamp.
   * Example: If the `version` is declared as `1.0.beta1`, then it will be published as `1.0.beta1.1478151288`.
 * Three files are published:
   * The `zip` archive
   * The new `info.xml` file
   * A JSON document describing the build.
 * An alias is provided under the folder `latest`.

The bot does *not* publish the new version to `civicrm.org`.  To do this, take the new `info.xml` file and manually
upload it.  Since `civicrm.org` provides a directory of past and current versions, be sure to specify the download-URL
for a specific version number (e.g.  `1.0.beta1.1478151288`) rather than an alias (`latest`).
