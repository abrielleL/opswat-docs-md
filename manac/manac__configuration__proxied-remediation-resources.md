<!-- source: https://www.opswat.com/docs/manac/configuration/proxied-remediation-resources -->

# Proxied Remediation Resources

NAC allows blocked users to access various resources on the web, mainly for the purposes of registering new devices, or updating the software necessary to comply with your institution’s policies. NAC provides this access by way of a transparent HTTP proxy that inspects the desired URL, and serves those pages whose URLs contain one of the regular expressions below. By the nature of a transparent proxy, this method does not allow for presentation of pages served over HTTPs.

Any HTTPs remediation resources should be addressed via networking configuration changes. Please contact [opswat.com/support](https://opswat.com/support/) for more details.

## [ANTIVIRUS RESOURCES](/docs/manac/configuration/proxied-remediation-resources#antivirus-resources)

| Vendor | Regular Expression Patterns |
| --- | --- |
| AdAware / Lavasoft AV | lavasoft .[adaware.com](http://adaware.com) |
| Authentium | .[authentium.com](http://authentium.com) |
| Avast | .[avast.com](http://avast.com) progmac vpsmac |
| AVG | avg grisoft i...[com.com](http://com.com) |
| Avira | .[free-av.com](http://free-av.com) .[avgate.net](http://avgate.net) avira |
| BitDefender | bitdefender |
| Clam | [clamav.net](http://clamav.net) clamxav |
| Comodo | comodo |
| F-Secure | .[f-secure.com](http://f-secure.com) |
| Faronics | faronics |
| Fortinet | fdsupdate fortinet |
| GDATA | gdatasecurity gdata-software gdatasoftware |
| iAntivirus | iantivirus |
| Intego | integodownload update.intego |
| Kaspersky | Kaspersky .[kaspersky-labs.com](http://kaspersky-labs.com) .[kaspersky.com](http://kaspersky.com) |
| LANDesk | landesk |
| MacKeeper | mackeeper |
| Malwarebytes | [malwarebytes.org](http://malwarebytes.org)[mbamupdates.com](http://mbamupdates.com) |
| Mcafee | mcafee [data.hackerwatch.org](http://data.hackerwatch.org) .[nai.com](http://nai.com) |
| Microsoft | [ajax.aspnetcdn.com](http://ajax.aspnetcdn.com)[banners.spiceworks.com](http://banners.spiceworks.com)[code.jquery.com](http://code.jquery.com)[community.spiceworks.com](http://community.spiceworks.com) MSSecurityEssentials [ots.optimize.webtrends.com](http://ots.optimize.webtrends.com) onecare [spe.atdmt.com](http://spe.atdmt.com)[view.atdmt.com](http://view.atdmt.com) |
| ESET/NOD-32 | [eset.com](http://eset.com)[nod32-av.com](http://nod32-av.com) |
| Panda | pandasecurity pandasoftware [cloudantivirus.com](http://cloudantivirus.com) |
| PC Tools/ Threatfire | pctools threatfire |
| SecureIT | [securitycoverage.com](http://securitycoverage.com) secureitdirect |
| Sophos | sophos [sophosx1.net](http://sophosx1.net) .[sophos.com](http://sophos.com) |
| Spybot | safer-networking .[security.kolla.de](http://security.kolla.de) .[securitywonks.org](http://securitywonks.org) .[see-cure.de](http://see-cure.de) spybot |
| SpySweeper | spysweeper .[webroot.com](http://webroot.com) Webrootcloudav |
| Super Antispyware | [superantispyware.com](http://superantispyware.com) |
| Symantec / Norton | .[digitalriver.com](http://digitalriver.com) norton .[sarc.com](http://sarc.com) symantec |
| Trend | .[housecall.antivirus.com](http://housecall.antivirus.com) trendmicro |
| Vipre | [sunbeltsoftware.com](http://sunbeltsoftware.com)[vipreantivirus.com](http://vipreantivirus.com) |
| ZoneAlarm | [zonealarm.com](http://zonealarm.com)[zonelabs.com](http://zonelabs.com) |

## [DEVICE REGISTRATION, CERTIFICATE CHECKING AND OTHER OS-SPECIFIC ACCESS](/docs/manac/configuration/proxied-remediation-resources#device-registration-certificate-checking-and-other-os-specific-access)

| Vendor | Regular Expression Patterns |
| --- | --- |
| Adobe | .[adobe.com](http://adobe.com) |
| Apple | [www.apple.com/library/test/success.html](http://www.apple.com/library/test/success.html)[init.ess.apple.com](http://init.ess.apple.com)[static.ess.apple.com](http://static.ess.apple.com)[appleid.apple.com](http://appleid.apple.com)[osrecovery.apple.com](http://osrecovery.apple.com)[swscan.apple.com](http://swscan.apple.com)[swquery.apple.com](http://swquery.apple.com)[swdownload.apple.com](http://swdownload.apple.com)[swcdn.apple.com](http://swcdn.apple.com)[crl.apple.com](http://crl.apple.com)[configuration.apple.com](http://configuration.apple.com)[mesu.apple.com/assets/com_apple_MobileAsset_TimeZoneUpdate](http://mesu.apple.com/assets/com_apple_MobileAsset_TimeZoneUpdate) |
| Certificate Validation | .[ca.com](http://ca.com) .[My-eTrust.com](http://My-eTrust.com)[crl.usertrust.com](http://crl.usertrust.com)[crt.usertrust.com](http://crt.usertrust.com)[crl.incommon.org](http://crl.incommon.org)[cert.incommon.org](http://cert.incommon.org)[globalsign.net](http://globalsign.net) godaddy ocsp thawte verisign |
| Google Analytics | [www.google-analytics.com](http://www.google-analytics.com) |
| Java | [java.com](http://java.com) java.*.[sun.com](http://sun.com) |
| Microsoft | [g.msn.com](http://g.msn.com) .[microsoft.com](http://microsoft.com) .[windows.com](http://windows.com) .[windowsupdate.com](http://windowsupdate.com)[view.atdmt.com](http://view.atdmt.com)[spe.atdmt.com](http://spe.atdmt.com)[community.spiceworks.com](http://community.spiceworks.com)[banners.spiceworks.com](http://banners.spiceworks.com)[code.jquery.com](http://code.jquery.com)[ots.optimize.webtrends.com](http://ots.optimize.webtrends.com)[code.jquery.com/jquery-1.5.1.min.js](http://code.jquery.com/jquery-1.5.1.min.js)[ajax.aspnetcdn.com](http://ajax.aspnetcdn.com) |
| Nintendo / Wii | [conntest.nintendowifi.net](http://conntest.nintendowifi.net)[wii.com](http://wii.com) |
| Ninite | [ninite.com](http://ninite.com) |
| Online Testing | [pearsoned.com](http://pearsoned.com) |
| XBOX | [assets.xbox.com](http://assets.xbox.com)[msftncsi.com](http://msftncsi.com)[notice.xbox.com](http://notice.xbox.com) |

##
