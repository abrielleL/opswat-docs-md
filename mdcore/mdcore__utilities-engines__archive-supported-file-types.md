<!-- source: https://www.opswat.com/docs/mdcore/utilities-engines/archive-supported-file-types -->

# Supported file types

The archive engine can extract 171 file types:

| File type | Note |
| --- | --- |
| 7z | a password protected file can be extracted with a given password |
| ACE |  |
| ALZ |  |
| AR |  |
| ARJ |  |
| BZ2 |  |
| CAB | all split CAB files can be extracted |
| CPIO |  |
| CRX |  |
| DEB |  |
| UDEB |  |
| DSD |  |
| EGG |  |
| GEM |  |
| GZ |  |
| JAR |  |
| JARCS |  |
| JMOD |  |
| LHA |  |
| LZH |  |
| LZMA |  |
| NAR |  |
| PCK |  |
| RAR | all split RAR files can be extracted. A password protected file can be extracted with a given password |
| RPM |  |
| SPF |  |
| STORY |  |
| TAR | if a TAR is a split archive, only the first file can be extracted |
| TAZ |  |
| TBZ |  |
| TGZ |  |
| TSE |  |
| TSEC |  |
| TSEZ |  |
| VIB |  |
| VTAR |  |
| WAR |  |
| WSP |  |
| XAR |  |
| XZ |  |
| YZ1 |  |
| ZIP | if a ZIP is a split archive, only the first file can be extracted. A password protected file can be extracted with a given password |
| MDZIP |  |
| XPI |  |
| UUE |  |
| ZSTD |  |
| ASICE |  |
| ASICS |  |
| DOCM |  |
| DOCX |  |
| DOTM |  |
| DOTX |  |
| HPWX |  |
| ODP |  |
| ODS |  |
| ODT |  |
| OTP |  |
| OTS |  |
| OTT |  |
| OXPS |  |
| PBIX |  |
| PBIT |  |
| POTM |  |
| POTX |  |
| PPAM |  |
| PPSM |  |
| PPSX |  |
| PPTM |  |
| PPTX |  |
| RIBC |  |
| SHOW |  |
| SLDM |  |
| SLDX |  |
| SCDOC |  |
| STC |  |
| STD |  |
| STI |  |
| STW |  |
| SXC |  |
| SXD |  |
| SXI |  |
| SXM |  |
| SXW |  |
| SXG |  |
| TWBX |  |
| UTIB |  |
| VSDM |  |
| VSDX |  |
| VSSM |  |
| VSSX |  |
| VSTM |  |
| VSTX |  |
| XLAM |  |
| XLSB |  |
| XLSM |  |
| XLSX |  |
| XLTM |  |
| XLTX |  |
| XPS |  |
| GPG | please see the details [here](https://www.opswat.com/docs/mdcore/utilities-engines/gpg-decryption) |
| APK |  |
| APPX |  |
| DLL |  |
| SFX | includes 7z SFX (created by 7-Zip), CAB SFX (created by IExpress), RAR SFX (created by WinRAR), ZIP SFX (created by PKZip) |
| IPA |  |
| MSI |  |
| MSIX |  |
| PKG |  |
| DMG | supported file systems: APFS, HFS, FAT |
| ISO |  |
| UDF |  |
| VDI |  |
| VHD | partition Styles: GPT, MBR; File Systems: FAT16, FAT32, NTFS, EXT32, HFS |
| VHDX | partition Styles: GPT, MBR; File Systems: FAT16, FAT32, NTFS, EXT32, HFS |
| VMDK | partition Styles: GPT, MBR; File Systems: NTFS, HFS, FAT12, FAT16, FAT32, EXT2, EXT3, EXT4. |
| WIM |  |
| E01 |  |
| NTFS |  |
| FAT |  |
| HFS |  |
| EXT |  |
| MBR |  |
| OVA |  |
| RAW | NTFS file system only |
| 3DML |  |
| CHM |  |
| MSM |  |
| P7M |  |
| SMIME | Support multipart SMIME |
| GIT BUNDLE |  |
| MS OLE |  |
| B3DM |  |
| GPKG |  |
| ZLIB |  |
| GIT PACK |  |
| VSIX |  |
| NUPKG |  |
| NPZ | detected and extracted as ZIP file |
| OEX | detected and extracted as ZIP file |
| WHL | detected and extracted as ZIP file |
| ICS |  |
| X12EDI |  |
| ESZ |  |
| MHT |  |
| EML | extracted to header, body, attachments |
| MSG | extracted to header, body, attachments |
| OFT |  |
| OST |  |
| PST |  |
| TNEF |  |
| MBX |  |
| DWF |  |
| DWFX |  |
| PCAP | with http, ftp, imap protocol |
| INNO | support Inno version 6.4.0 or older only |
| PYZ |  |
| ASAR |  |
| AppImg |  |
| QCOW | support QCOW1, QCOW2, QCOW3 |
| LZ4 |  |
| MAR |  |
| UFDR |  |
| YENC |  |
| EDS |  |
| 3MF |  |
| BLZ |  |
| SquashFS |  |
| WARC |  |
| BLZ |  |
| X3P |  |
| Parquet |  |
| KM5 |  |

- Encrypted PDF, MS Word (DOC, DOCX, DOCM, DOTX, DOTM, DOT)/Excel (XLS, XLSX, XLSM, XLSB, XLTM)/PowerPoint (PPT, PPTX, PPTM, PPSM, POTX, POTM), ALZ, EGG.
- An encoded base64 file can be decoded by the archive extraction engine.
- The Parquet file format supports extracting only binary columns.
- Configure the archive extraction in the Workflow:
