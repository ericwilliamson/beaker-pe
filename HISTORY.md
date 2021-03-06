# default - History
## Tags
* [LATEST - 15 Jun, 2016 (985fe231)](#LATEST)
* [0.4.0 - 1 Jun, 2016 (f5ad1884)](#0.4.0)
* [0.3.0 - 26 May, 2016 (0d6b6d4c)](#0.3.0)
* [0.2.0 - 18 May, 2016 (a65f2083)](#0.2.0)
* [0.1.2 - 4 Apr, 2016 (a6fd7bef)](#0.1.2)
* [0.1.1 - 4 Apr, 2016 (8203d928)](#0.1.1)
* [0.1.0 - 29 Feb, 2016 (4fc88d8c)](#0.1.0)

## Details
### <a name = "LATEST">LATEST - 15 Jun, 2016 (985fe231)

* (GEM) update beaker-pe version to 0.5.0 (985fe231)

* Merge pull request #11 from highb/cutover/pe-14555 (1b21288a)


```
Merge pull request #11 from highb/cutover/pe-14555

(PE-14555) Always use MEEP for >= 2016.2.0
```
* (PE-14555) Always use MEEP for >= 2016.2.0 (de3a5050)


```
(PE-14555) Always use MEEP for >= 2016.2.0

Prior to this commit pe-beaker would use `INSTALLER_TYPE` to
specify whether to run a MEEP (new) or legacy install.
This commit changes pe-beaker to always use MEEP if the PE
version being installed is >= 2016.2.0, and legacy otherwise.

No ENV parameters will be passed to specify which to use, as we
are now relying on the installer itself to default to using MEEP
by default in all 2016.2.0 builds going forward.
```
### <a name = "0.4.0">0.4.0 - 1 Jun, 2016 (f5ad1884)

* (HISTORY) update beaker-pe history for gem release 0.4.0 (f5ad1884)

* (GEM) update beaker-pe version to 0.4.0 (e04b1f64)

* Merge pull request #9 from jpartlow/issue/master/pe-14554-switch-default-to-meep (c9eff0ea)


```
Merge pull request #9 from jpartlow/issue/master/pe-14554-switch-default-to-meep

(PE-14554) Switch default to meep
```
* (PE-14554) Switch default to meep (f234e5fc)


```
(PE-14554) Switch default to meep

If INSTALLER_TYPE is not set, beaker-pe will now default to a meep
install.  You must set INSTALLER_TYPE to 'legacy' to get a legacy
install out of Beaker with this patch.
```
### <a name = "0.3.0">0.3.0 - 26 May, 2016 (0d6b6d4c)

* (HISTORY) update beaker-pe history for gem release 0.3.0 (0d6b6d4c)

* (GEM) update beaker-pe version to 0.3.0 (d58ed99e)

* Merge pull request #5 from jpartlow/issue/master/pe-14271-wire-for-meep (55aa098f)


```
Merge pull request #5 from jpartlow/issue/master/pe-14271-wire-for-meep

(PE-14271) Wire beaker-pe for meep
```
* (maint) Add some logging context for sign and agent shutdown (398882f4)


```
(maint) Add some logging context for sign and agent shutdown

...steps.
```
* (PE-14271) Do not try to sign certificate for meep core hosts (e485c423)


```
(PE-14271) Do not try to sign certificate for meep core hosts

Certificate is generated by meep.  Step is redundant and produces failed
puppet agent run and puppet cert sign in log.
```
* (PE-15259) Inform BeakerAnswers if we need legacy database defaults (7ef0347d)


```
(PE-15259) Inform BeakerAnswers if we need legacy database defaults

Based on this setting, BeakerAnswers can provide legacy bash default
values for database user parameters in the meep hiera config.  This is
necessary if we are upgrading from an older pe that beaker just
installed using the legacy script/answer defaults.

Also logs the actual answers/pe.conf file that was generated so we can
see what is going on.
```
* (maint) Remove unused variables from spec (61134529)


```
(maint) Remove unused variables from spec

Marked by static analysis; specs continue to pass after removal.
```
* (PE-14271) Have mock hosts return a hostname (53e90212)


```
(PE-14271) Have mock hosts return a hostname

Because BeakerAnswers sets hiera host parameters from Host#hostname, so
the method needs to exist in our mocks.
```
* (maint) Make the previous_pe_ver available on upgrade (0f72aaab)


```
(maint) Make the previous_pe_ver available on upgrade

Sometimes during PE upgrades we need to be able to determine what
version we upgraded from, to know what behavior we expect from the
upgrade.  Prior to this change, that could only be determined by probing
into the original host.cfg yaml. This patch just sets it explicitly in
each host prior to overwriting the pe_ver with pe_upgrade_ver.
```
* (PE-14271) Adjust higgs commands to provide correct answer (f7cc8d9a)


```
(PE-14271) Adjust higgs commands to provide correct answer

...for both legacy and meep installers.  The former prompts to continue
expecting 'Y' and the later prompts with options where '1' is intended
to kick off Higgs.

Also added spec coverage for these methods.
```
* (PE-14271) Adjust BeakerAnswers call for meep (6bc392ff)


```
(PE-14271) Adjust BeakerAnswers call for meep

Based on changes pending in puppetlabs/beaker-answers#16, change the
generate_installer_conf_file_for() method to submit the expected :format
option temporarily.  This will go away when we cutover to meep and no
longer have to have both installer scripts operational in the same
build.

Fleshes out the specs that verify the method returns expected answer or
pe.conf data from BeakerAnswers, as written out via scp.
```
* (PE-14271) Prepare host installer options based on version/env (616612a6)


```
(PE-14271) Prepare host installer options based on version/env

The addition of a use_meep? query allows setting host options for either
legacy or meep installer.  This enables installer_cmd to invoke the
correct installer.
```
* (maint) Remove remaining version_is_less mocks (7ea8fbcf)


```
(maint) Remove remaining version_is_less mocks

For consistency, removed the rest of the version_is_less mocks.

In the three cases where this had an impact on the specs, replaced
them with a concrete version setting on the test host object.
```
* (maint) Stop mocking version_is_less in do_install tests (d3e09cc1)


```
(maint) Stop mocking version_is_less in do_install tests

Each change to do_install and supporting methods involving a
version_is_less call was requiring additional mocking simulating
version_is_less's behavior.  This is unnecessary given that hosts are
being set with a version, and actually masks behavior of the class.
Removing these specifically because it was causing churn when
introducing meep functionality.
```
* (PE-14271) Extract installer configuration methods (3071c5e9)


```
(PE-14271) Extract installer configuration methods

...from the existing code to generate answers and expand it to
generalize the installer settings and configuration file.  Passes
existing specs.  Will be further specialized to handle legacy/meep
cases.
```
* (PE-14934) Fix specs to cover changes from PE-14934 (b22c3790)


```
(PE-14934) Fix specs to cover changes from PE-14934

Introduced chagnes to the do_install method, but specs were failing
because of the tight coupling between expectations and counts of command
execution.

The need to initialize metadata comes from the fact that the previous
PR #3 added step() calls, which reference the TestCase metadata attr.
Since we aren't using an actual TestCase instance, this had to be
initalized separately.
```
### <a name = "0.2.0">0.2.0 - 18 May, 2016 (a65f2083)

* (HISTORY) update beaker-pe history for gem release 0.2.0 (a65f2083)

* (GEM) update beaker-pe version to 0.2.0 (d9a052a4)

* Merge pull request #1 from Renelast/fix/windows_masterless (ef4be9a2)


```
Merge pull request #1 from Renelast/fix/windows_masterless

Fixes windows masterless installation
```
* Merge branch 'master' of https://github.com/puppetlabs/beaker-pe into fix/windows_masterless (f1a96fb2)

* Merge pull request #7 from tvpartytonight/BKR-656 (aa566657)


```
Merge pull request #7 from tvpartytonight/BKR-656

(maint) Remove leftover comments
```
* (maint) Remove leftover comments (c7ce982b)


```
(maint) Remove leftover comments

This removes some straggling comments and adds a comment to the new
metadata object in the `ClassMixedWithDSLInstallUtils` class.
```
* Merge pull request #6 from tvpartytonight/BKR-656 (c1ea366b)


```
Merge pull request #6 from tvpartytonight/BKR-656

BKR-656
```
* (BKR-656) refactor pe_ver setting into independent method (0d918c46)


```
(BKR-656) refactor pe_ver setting into independent method

Previous to this commit, transforming a host object prior to upgrading
was handled in the upgrade_pe_on method. This change removes that logic
from that method and allows for independent transformation to happen in
a new prep_host_for_upgrade method.
```
* (BKR-656) Update spec tests for do_install (b602661f)


```
(BKR-656) Update spec tests for do_install

Commit 7112971ac7b14b8c3e9703523bbb8526af6fdfbe introduced changes to
the do_install method but did not have any updates for the spec tests.
This commit adds those tests in.
```
* Adds type defaults and runs puppet agent on masterless windows (e7d06a3f)

* Fixes windows masterless installation (9ff54261)


```
Fixes windows masterless installation

Setting up a masterless windows client would fail with the following error:

Exited: 1
/usr/local/rvm/gems/ruby-2.2.1/gems/beaker-2.37.0/lib/beaker/host.rb:330:in `exec': Host 'sxrwjhkia9gzo03' exited with 1 running: (Beaker::Host::CommandFailure)
 cmd.exe /c puppet config set server
Last 10 lines of output were:
        Error: puppet config set takes 2 arguments, but you gave 1
        Error: Try 'puppet help config set' for usage

As far as I could see this error is caused by the 'setup_defaults_and_config_helper_on' function which tries to set the master configuration setting in puppet.conf. But since there is no master varaible available this failes.

This patch should fix that by only calling setup_defaults_and_config_helper_on whern we're not doing a masterless installation.
```
### <a name = "0.1.2">0.1.2 - 4 Apr, 2016 (a6fd7bef)

* (HISTORY) update beaker-pe history for gem release 0.1.2 (a6fd7bef)

* (GEM) update beaker-pe version to 0.1.2 (b3175863)

* Merge pull request #3 from demophoon/fix/master/pe-14934-robust-puppetdb-check (c3bebe59)


```
Merge pull request #3 from demophoon/fix/master/pe-14934-robust-puppetdb-check

(PE-14934) Add more robust puppetdb check
```
* (PE-14934) Add more robust puppetdb check (7112971a)


```
(PE-14934) Add more robust puppetdb check

Before this commit we were still failing before the last puppet agent
run in do_install because we also run puppet agent in some cases before
the last run. This commit adds in the wait during that agent run as well
as a check on the status endpoint in puppetdb to be sure that it is
running in the case that the port is open but puppetdb is not ready for
requests.
```
### <a name = "0.1.1">0.1.1 - 4 Apr, 2016 (8203d928)

* (HISTORY) update beaker-pe history for gem release 0.1.1 (8203d928)

* (GEM) update beaker-pe version to 0.1.1 (6ccb5a59)

* Merge pull request #2 from demophoon/fix/master/pe-14934 (4e0b668e)


```
Merge pull request #2 from demophoon/fix/master/pe-14934

(PE-14934) Test if puppetdb is up when running puppet agent on pdb node
```
* (PE-14934) Test if puppetdb is up when running puppet agent on pdb node (882ca94f)


```
(PE-14934) Test if puppetdb is up when running puppet agent on pdb node

Before this commit we were running into an issue where puppetdb would
sometimes not be up and running after puppet agent restarted the
service. This commit waits for the puppetdb service to be up after
running puppet agent on the database node so that the next agent run
doesn't fail.
```
### <a name = "0.1.0">0.1.0 - 29 Feb, 2016 (4fc88d8c)

* Initial release.
