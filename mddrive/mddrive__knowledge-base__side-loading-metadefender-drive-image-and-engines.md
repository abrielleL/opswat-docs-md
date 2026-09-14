<!-- source: https://www.opswat.com/docs/mddrive/knowledge-base/side-loading-metadefender-drive-image-and-engines -->

# Side-loading MetaDefender Drive Image and Engines for Drive Toolkit

#### [Overview:](/docs/mddrive/knowledge-base/side-loading-metadefender-drive-image-and-engines#overview)

MetaDefender Drive image and engines have been downloaded and updated completely from a Toolkit that has internet access. There is the need to copy the image and engines from that online Toolkit to another Drive Toolkit running on an air-gapped workstation.

#### [MetaDefender Drive Image location:](/docs/mddrive/knowledge-base/side-loading-metadefender-drive-image-and-engines#metadefender-drive-image-location)

- Navigate to the location where MetaDefender Drive Toolkit is extracted
- Find the "*../../MetaDefenderDriveToolkit/current*" folder (1)
- Make sure there are the following files

  - *release-note.html*
  - *mdd-dd.yml*
  - *mdd-pkg.dd*
  - *partition-layout-info*

#### [MetaDefender Drive engines location:](/docs/mddrive/knowledge-base/side-loading-metadefender-drive-image-and-engines#metadefender-drive-engines-location)

- Navigate to the location where MetaDefender Drive Toolkit is extracted
- Find the "*../../MetaDefenderDriveToolkit/engines*" folder (1)
- There are the engines definitions and databases (2) that will be used for Boot Scan session

- Navigate to "*../../MetaDefenderDriveToolkit/win_defs*" folder (1)
- There are databases for In-Session scan (2)

#### [Side loading Image and Engines:](/docs/mddrive/knowledge-base/side-loading-metadefender-drive-image-and-engines#side-loading-image-and-engines)

After finding the location of MetaDefender Drive Image and its engines, you can simply use an secure USB storage to copy them to the isolated MetaDefender Drive Toolkit, under the corresponding directories

- *"../../MetaDefenderDriveToolkit/current":* this directory is for the Image
- *"../../MetaDefenderDriveToolkit/engines":* this directory is for the Boot Scan engines
- *"../../MetaDefenderDriveToolkit/win_defs":* this directory is for the In-Session engines
