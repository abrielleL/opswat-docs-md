<!-- source: https://www.opswat.com/docs/filescan/installation/domains-contacted-during-installation -->

# Domains Contacted During Installation & Operation

During the installation and operation of **MetaDefender Aether** (previously known as MetaDefender Sandbox), the following domains will be contacted. Please note that this may change over time.

| Domains | Purpose | Usage Type | MetaDefender Aether Layer |
| --- | --- | --- | --- |
| <api.metadefender.com> | MetaDefender Cloud Reputation API | Operation | Layer 1 - Threat Reputation  Layer 4 - Threat Hunting |
| <opswat.com>  <update.dl.opswat.com>  <activation.dl.opswat.com> | OPSWAT Activation Server and Update Infrastructure - Used for product activation and for downloading threat database updates | Operation | Layer 1 - Threat Reputation  Layer 2 - Dynamic Analysis  Layer 3 - Threat Scoring |
| <my.opswat.com> | MyOPSWAT Portal used for OCM Integration | Operation | N/A |
| <api.nuget.org>  <data.mcr.microsoft.com>  [mcr.microsoft.com](http://mcr.microsoft.com/)  [packages.microsoft.com](http://packages.microsoft.com/)  <a-0016.a-msedge.net> | Microsoft Container Registry and repository for .NET packages - Used by the Powershell emulator | Installation | N/A |
| [archive.ubuntu.com](http://archive.ubuntu.com)  [deb.debian.org](http://deb.debian.org)  <debian.map.fastlydns.net>  [security.ubuntu.com](http://security.ubuntu.com) | Repositories of Ubuntu and Debian packages (can be any regional or local mirror) - Used directly for Ubuntu installations and used in Docker containers for both Ubuntu and RHEL installs | Installation | N/A |
| <auth.docker.io>  [docker.io](http://docker.io)  [download.docker.com](http://download.docker.com)  <registry-1.docker.io>  <production.cloudflare.docker.com> | Used for Docker installation and downloading base images for Sandbox components | Installation | N/A |
| [bootstrap.pypa.io](http://bootstrap.pypa.io)  <files.pythonhosted.org>  [pypi.org](http://pypi.org) | Python package repositories - Used when building the Docker image for the Sandbox webservice component | Installation | N/A |
| [codecs.fedoraproject.org](http://codecs.fedoraproject.org)  [mirrors.fedoraproject.org](http://mirrors.fedoraproject.org) | Fedora’s geographically optimized mirror server that hosts Fedora packages | Installation | N/A |
| [d2h67oheeuigaw.cloudfront.net](http://d2h67oheeuigaw.cloudfront.net)  [d2lzkl7pfhq30w.cloudfront.net](http://d2lzkl7pfhq30w.cloudfront.net)  [artifact.sandbox-prod.metadefender.com](http://artifact.sandbox-prod.metadefender.com/) | Used for downloading phishpedia package from <artifact.sandbox-prod.metadefender.com> - Required for phishing detection ML model | Installation | N/A |
| [dl-ssl.google.com](http://dl-ssl.google.com)  [dl.google.com](http://dl.google.com) | Used for downloading Google Chrome - Required for URL rendering in the Sandbox transform Docker container | Installation | N/A |
| [github.com](http://github.com) | Used for getting YARA rules from OPSWAT fsYara repository: <https://github.com/filescanio/fsYara> | Operation | Layer 2 - Dynamic Analysis |
| [google.com](http://google.com)  [www.google.com](http://www.google.com) | Used for basic connectivity check | Installation | N/A |
| <ntp.ubuntu.com>  <time-a-g.nist.gov>  <time-a.nist.gov> | NTP and time servers | Operation | N/A |
| <pki.goog> | Google Public Key Infrastructure | Installation Operation | N/A |
| <playwright.azureedge.net> | Used for installing playwright in the Sandbox webservice docker image | Installation | N/A |
| <rhui.us-west-2.aws.ce.redhat.com> | RHEL package repository (can be any regional or local mirror) | Installation | N/A |

For convenience, the same domains are also listed here:

api.metadefender.com
opswat.com
update.dl.opswat.com
activation.dl.opswat.com
my.opswat.com
api.nuget.org
data.mcr.microsoft.com
mcr.microsoft.com
packages.microsoft.com
a-0016.a-msedge.net
archive.ubuntu.com
deb.debian.org
debian.map.fastlydns.net
security.ubuntu.com
auth.docker.io
docker.io
download.docker.com
registry-1.docker.io
production.cloudflare.docker.com
bootstrap.pypa.io
files.pythonhosted.org
pypi.org
codecs.fedoraproject.org
mirrors.fedoraproject.org
d2h67oheeuigaw.cloudfront.net
d2lzkl7pfhq30w.cloudfront.net
artifact.sandbox-prod.metadefender.com
dl-ssl.google.com
dl.google.com
github.com
google.com
www.google.com
ntp.ubuntu.com
time-a-g.nist.gov
time-a.nist.gov
pki.goog
playwright.azureedge.net
rhui.us-west-2.aws.ce.redhat.com

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
