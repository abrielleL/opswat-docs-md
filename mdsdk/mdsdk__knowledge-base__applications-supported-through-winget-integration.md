<!-- source: https://www.opswat.com/docs/mdsdk/knowledge-base/applications-supported-through-winget-integration -->

# Applications Supported through WinGet Integration

View as Markdown Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

The OESIS Framework expands its patching catalog every month with applications onboarded from the WinGet source. This article lists the applications added through WinGet integration, grouped by the monthly SDK News edition that announced them, with the signature ID of each application as published in the OESIS Framework support chart.

## [How WinGet-sourced applications are delivered](/docs/mdsdk/knowledge-base/applications-supported-through-winget-integration#how-winget-sourced-applications-are-delivered)

Applications onboarded from WinGet are delivered as a data update, so no engine update is required to receive new entries. Every detected product and patch carries a `data_source` field, which is `winget` for these applications and `opswat` for OPSWAT-curated signatures, so you can tell the two apart in `DetectProducts`, `GetLatestInstaller` and the server-side data files (`products.json`, `patch_aggregation.json` and `moby.json`).

WinGet-sourced products are returned by `DetectProducts` when the `enable_winget_source` option is enabled. Leaving the option off preserves the existing, OPSWAT-only behavior.

Each monthly table below is sorted alphabetically by product name. Use the search box in the Product column to find an application.

## [November 2026](/docs/mdsdk/knowledge-base/applications-supported-through-winget-integration#november-2026)

This update added patching support for **287 applications** (287 signatures in total).

| Product | Signature |
| --- | --- |
| 4KWALL | 4708 |
| ABDownloadManager | 4796 |
| Achievements | 4669 |
| AI Usage Dashboard | 4582 |
| AirPodsDesktop | 5041 |
| AlienFX Tools | 5237 |
| Alloy | 5038 |
| Altair GraphQL Client | 4980 |
| AltSnap | 4987 |
| Altus | 5266 |
| Amethyst | 5148 |
| AMLL TTML Tool | 4659 |
| Anki | 4770 |
| Ant Commander Personal | 4567 |
| AnxReader | 4898 |
| AnymeX | 5183 |
| Aptakube | 5233 |
| ATV Desktop Remote | 5277 |
| Audacious | 5179 |
| AWS Loggy | 4679 |
| Bdash | 5157 |
| Beetroot | 4569 |
| BentoDesk | 4734 |
| Better-CrewLink | 5203 |
| Bitcoin Core | 4742 |
| Blockbench | 4963 |
| Blur-AutoClicker | 5114 |
| BOINC | 5088 |
| BSManager | 5186 |
| BumbleHive | 4716 |
| CC Desktop Switch | 5250 |
| CC Switch | 4736 |
| ChatLab | 4923 |
| Chia | 4870 |
| Chiri | 4663 |
| Chocolatey GUI | 5134 |
| Cinny desktop | 5238 |
| cloudflared | 4812 |
| CopyQ | 4858 |
| CopyTranslator | 4797 |
| CrowdSec | 4823 |
| Dangerzone | 4968 |
| DbGate | 4932 |
| DBX | 4781 |
| DeltaChat | 5142 |
| Dev HUD | 4673 |
| Dev Janitor | 5236 |
| dev-sidecar | 4448 |
| DevWit | 4462 |
| digiKam | 5248 |
| Discrakt | 4732 |
| Display Driver Uninstaller | 5229 |
| DLSS Updater | 5190 |
| Dorion | 5081 |
| dotsider-mcp | 4711 |
| Dune 3D | 5110 |
| Echophrase | 4497 |
| EcoPaste | 4924 |
| EnsoAI | 4501 |
| Erlang OTP | 4857 |
| eSearch | 4936 |
| ExifCleaner | 5066 |
| ExpressLRS Configurator | 5239 |
| F3D | 5005 |
| FanFolder | 4594 |
| FeedFlow | 5180 |
| Feishin | 4883 |
| fend | 5213 |
| FFmpeg Batch AV Converter | 5151 |
| File Converter | 4819 |
| Firezone | 4896 |
| Flameshot | 4771 |
| Fluent Reader | 4887 |
| Fluent Search | 5106 |
| fluent-bit | 4906 |
| FreeShow | 5172 |
| FxSound | 5011 |
| Gale | 5244 |
| Game Cheats Manager | 4825 |
| Game Save Manager | 5156 |
| Gephi | 4947 |
| GitButler | 4789 |
| GitHub Stars Manager | 5035 |
| Gitify | 4982 |
| Glyph | 4485 |
| GnuCash | 5019 |
| GodotHub | 4654 |
| GR2Analyst 3 | 4481 |
| Grok App | 4650 |
| Headlamp | 4928 |
| Heroic | 4856 |
| Hoppscotch Agent | 4489 |
| Horizon EDA | 5171 |
| HTTP Toolkit | 5259 |
| Hubble.md | 5160 |
| Hydra | 4804 |
| Hydrogen (Advanced drum machine for GNU/Linux) | 5170 |
| IdeaShare | 4490 |
| IIViewer | 4514 |
| Immich Folder Watch | 4706 |
| IndepenDesk | 4486 |
| InferenceHub | 4498 |
| Infinite Algebra 1 | 4556 |
| Infinite Algebra 2 | 4557 |
| Infinite Calculus | 4558 |
| Infinite Geometry | 4559 |
| Infinite Grade 6 Math | 4560 |
| Infinite Pre-Algebra | 4562 |
| Infinite Precalculus | 4563 |
| Intel(R) PresentMon | 5083 |
| IPFS Desktop | 4953 |
| IPTVnator | 4934 |
| Jackett | 4811 |
| Joplin | 4748 |
| JYYCode | 4647 |
| Kai | 4666 |
| Kalker | 5124 |
| Karing | 4816 |
| Kdenlive | 4967 |
| KDiff3 | 5271 |
| KeyEcho | 5234 |
| keymapper | 5192 |
| Keyviz | 4888 |
| KiCad | 5055 |
| Kiro | 5020 |
| Klayout - Layout Viewer And Editor | 5184 |
| Koinkat | 4540 |
| Koodo Reader | 4773 |
| KopiaUI | 4834 |
| Lepton | 4879 |
| LibrePCB | 5054 |
| Local MCP Tunnel | 4707 |
| Lody | 4526 |
| Logisim-evolution | 4917 |
| Logseq | 4758 |
| Lore Desktop | 4901 |
| LRCGET | 5046 |
| lx-music-desktop | 4747 |
| Markpad | 5187 |
| MarkText | 4745 |
| mathom | 4480 |
| Mattermost | 5097 |
| MD Plus | 4729 |
| Meru | 5215 |
| MinerU | 4743 |
| Mixxx | 4938 |
| Monet | 4731 |
| muffon | 5102 |
| Mullvad VPN | 4918 |
| Multica | 4741 |
| murmure | 5205 |
| MuseScore | 4822 |
| Music Presence | 5040 |
| MusicFree | 4899 |
| Namida | 4956 |
| Nebula Terminal | 4554 |
| NeeView | 5212 |
| NegPy | 4538 |
| Netbird | 4772 |
| Netcatty | 4957 |
| NetPad | 5092 |
| NetPad vNext | 5093 |
| NexusShell | 4545 |
| NitTray | 4524 |
| NordLayer | 4583 |
| Nostr VPN | 4568 |
| Notepad3 | 4946 |
| Notesnook | 4826 |
| NSwagStudio | 4930 |
| Nyrna | 5175 |
| OnionShare | 4939 |
| ontime | 5222 |
| Onyx Code | 4528 |
| Open Design | 4737 |
| Open-Shell | 4892 |
| OpenAudible | 5130 |
| OpenCode | 4677 |
| OpenCodex | 5263 |
| OpenComic | 5120 |
| OpenLogiNet | 4529 |
| OpenMPT | 5251 |
| OpenShot Video Editor | 4951 |
| OpenToonz | 4915 |
| Orca | 4738 |
| osquery | 4784 |
| Outline | 4761 |
| P3X Redis UI | 5246 |
| Packet Sender | 5068 |
| Pane | 4609 |
| PanWriter | 5174 |
| PCSX2 | 4814 |
| Penpot Desktop | 5191 |
| PicView | 5037 |
| Pixelorama | 4876 |
| PixPin | 4617 |
| Polar | 5240 |
| PolyMC | 5111 |
| Portmaster | 4838 |
| Positron | 5022 |
| PrintBridge | 4703 |
| Processing | 4627 |
| Proton Mail Bridge | 5152 |
| ProxyBridge | 4952 |
| Pulsebar | 4724 |
| Qalculate! | 5067 |
| Quadrant | 4638 |
| QuickLook | 4780 |
| qutebrowser | 4866 |
| Rai Pal | 5261 |
| RapidRAW | 4878 |
| Rare | 5224 |
| Raudo IPTV | 4643 |
| Rayburst | 4872 |
| Reqable | 4942 |
| RimSort | 5178 |
| rubick | 4885 |
| RunJS | 5107 |
| SABnzbd | 5051 |
| Scalar | 4809 |
| SceneBuilder | 5243 |
| Scratch | 5149 |
| ScreenToGif | 4774 |
| Servy | 5117 |
| Session | 5276 |
| SFMC Data Loader | 4507 |
| Shotcut | 4818 |
| SimpleFixAI | 4662 |
| Simplenote | 4986 |
| SimpleX Chat | 4794 |
| SiYuan | 4756 |
| Skriuw | 4644 |
| sleek | 5116 |
| Snoop | 5087 |
| Snow Shot | 4975 |
| Sparkle | 4911 |
| Spokenly | 4676 |
| SQL Plan For Dummies | 4657 |
| SQLiteStudio | 4944 |
| Stremio Community v5 | 5235 |
| Stremio Enhanced | 5241 |
| Stretchly | 4955 |
| Sunshine | 4759 |
| SwitchHosts | 4775 |
| TagSpaces | 4984 |
| TaskExplorer | 5028 |
| TeXworks | 5252 |
| Tier1Suite | 4693 |
| TimeScribe | 5227 |
| tldraw offline | 4695 |
| Tolaria | 4791 |
| Trezor Suite | 5209 |
| TrguiNG | 5249 |
| TurboWarp | 5272 |
| TweakHub | 4624 |
| Twinkle Tray | 4895 |
| ueli | 5009 |
| UniClipboard | 5131 |
| Universal Radio Hacker | 4855 |
| Unsloth | 4701 |
| Vega | 4488 |
| VidBee | 4581 |
| Voltius | 5258 |
| Wasabi Wallet | 5082 |
| Weasis | 5169 |
| webOS Dev Manager | 5080 |
| Webstudio | 4897 |
| Windhawk | 4893 |
| Windows Battery Life Tool | 4552 |
| WindowTop | 5155 |
| Windscribe | 5200 |
| Wing | 4713 |
| WinScript | 5058 |
| WinSetView | 5119 |
| WiX Toolset Additional Tools | 5195 |
| Word Hunter | 4499 |
| WSL Dashboard | 5026 |
| XerahS | 4660 |
| Yaak | 4795 |
| YAKC | 4493 |
| yasb | 4972 |
| YouTube Music | 4765 |
| YouTube Music for Desktop | 5207 |
| Zeal | 4846 |
| Zellij | 4764 |
| ZeroWhats | 4730 |
| ZohoVoice-Desktop | 4733 |
| Zuno | 4584 |

## [October 2026](/docs/mdsdk/knowledge-base/applications-supported-through-winget-integration#october-2026)

This update added patching support for **31 applications** (31 signatures in total).

| Product | Signature |
| --- | --- |
| Accident Reconstruction Professional | 4432 |
| Antigravity | 4213 |
| Anytype | 4396 |
| AutoHotkey | 4390 |
| Azure Connected Machine Agent | 4384 |
| balena-cli | 4397 |
| CyberHive Connect | 4403 |
| DiscoverWorthy Scratchpad | 4434 |
| Ditto | 4435 |
| DMMGamePlayer | 4442 |
| Duo Desktop | 4345 |
| Envarly | 4466 |
| Executor | 4531 |
| FastTube Pro | 4470 |
| fullfetch | 4273 |
| KakaoTalk | 4393 |
| Karuzip | 4515 |
| memoir | 4544 |
| Microsoft Azure Storage Explorer | 4372 |
| nu | 4404 |
| Password Safe | 4347 |
| PW Auto Login | 4415 |
| qbPortWeaver | 4533 |
| SASM | 4440 |
| SnippingTool | 4428 |
| Tenebra | 4437 |
| ToeRings | 4296 |
| VSCodium | 4365 |
| Wazuh Agent | 4363 |
| znote | 4210 |
| Zotero | 4421 |

## [September 2026](/docs/mdsdk/knowledge-base/applications-supported-through-winget-integration#september-2026)

This update added patching support for **13 applications** (15 signatures in total).

| Product | Signature |
| --- | --- |
| 3DF Zephyr Free | 4287 |
| Arelle | 4294 |
| BurnAware Free | 1614 |
| BurnAware Pro | 1917 |
| Endstate | 4246 |
| Go | 3789 |
| Hardware Visualizer | 4244 |
| HWMonitor | 1939 |
| Markdown Studio | 4247 |
| Notion | 4175 |
| PeaZip | 268, 3558 |
| PowerShell | 3504, 3503 |
| Writ | 4288 |

## [August 2026](/docs/mdsdk/knowledge-base/applications-supported-through-winget-integration#august-2026)

This update added patching support for **67 applications** (81 signatures in total).

| Product | Signature |
| --- | --- |
| 010 Editor | 1931 |
| Advanced SystemCare | 242 |
| Angry IP Scanner | 3909 |
| AnyBurn | 2031 |
| AnyToISO | 1073 |
| AusweisApp | 4270 |
| Azul Zulu JDK 23 | 3972 |
| Azul Zulu JRE 8 | 4009 |
| Backupper | 297 |
| Chromium | 4172 |
| CloneSpy | 1518 |
| Convertilla | 2401 |
| Cppcheck | 1572 |
| Doxygen | 292 |
| EaseUS Todo Backup | 120 |
| Eclipse Temurin JDK with Hotspot 17 | 3588 |
| Eclipse Temurin JDK with Hotspot 19 | 3657, 3652 |
| Eclipse Temurin JDK with Hotspot 25 | 4087 |
| Eclipse Temurin JDK with Hotspot 8 | 3578 |
| Eclipse Temurin JRE with Hotspot 19 | 3653, 3654 |
| Everything | 2890, 3560, 3844, 3845 |
| Exact Audio Copy | 1969 |
| ExamDiff | 1067 |
| ExtractNow | 799 |
| Find and Mount | 2496 |
| Flock | 3238 |
| foobar2000 | 1358 |
| Gajim | 718 |
| Geany | 1906 |
| Jabra Direct | 3324 |
| JetBrains WebStorm | 1104 |
| Karen's Replicator | 451 |
| Kodi | 1948 |
| Lightscreen | 2874 |
| Lightshot | 2878 |
| Microsoft .NET Runtime 6.0 | 3737, 3745 |
| Microsoft .NET Runtime 7.0 | 3746, 3736 |
| Microsoft .NET Runtime 9.0 | 3993, 3991 |
| Microsoft .NET SDK 6.0 | 3735, 3749 |
| Microsoft .NET SDK 7.0 | 3747, 3734 |
| Microsoft .NET SDK 8.0 | 3876, 3877 |
| Microsoft .NET SDK 9.0 | 3989, 3990 |
| Microsoft ASP.NET Core Runtime 6.0 | 3751, 3740 |
| Microsoft ASP.NET Core Runtime 9.0 | 3994, 4093 |
| MKVToolNix | 2900 |
| MyPhoneExplorer | 2064 |
| NetSpeedTray | 4268 |
| OBS Studio | 4174 |
| Obsidian | 4177 |
| Partition Assistant | 299 |
| Power Automate for desktop | 4056 |
| PyCharm Community | 1133 |
| PyCharm Professional | 1132 |
| Rclone UI | 4274 |
| Reg Organizer | 1456 |
| Registry Life | 2237 |
| Resource Hacker | 915 |
| Secure IT | 1169 |
| Softros LAN Messenger | 773 |
| Splashtop Streamer | 3901 |
| Uninstall Tool | 1594 |
| UrBackup | 1091 |
| VeraCrypt | 2334 |
| Vim | 4171 |
| Wireless Network Watcher | 917 |
| Wise Game Booster | 981 |
| Wise JetSearch | 980 |

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
