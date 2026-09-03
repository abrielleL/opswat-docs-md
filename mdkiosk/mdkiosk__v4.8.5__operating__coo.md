<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.5/operating/coo -->

# Country of Origin

Kiosk is able to detect source country where files are created from. The Country of Origin (COO) feature helps the Kiosk admin add more restrictions on the scanning result by specifying countries, which the publisher resides in, as forbidden. Files published from forbidden countries are considered as blocked, even they are clean from Metadefender Core scan result. Kiosk keeps scan result from Metadefender Core if no COO associates with the files.

Due to performance priority, only executable files (.exe, .dll) are supported for COO detection. Files reported by Metadefender Core as blocked is not processed with COO.

To support COO, the admin needs to enable COO and add countries to the forbidden list. Empty forbidden list equals to COO disabling.

Notes: Kiosk bases on internal database to identify COO of files. Files from companies not existing in the internal database might result as no COO.
