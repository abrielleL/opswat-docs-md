<!-- source: https://www.opswat.com/docs/mdkiosk-linux/v5.7.4/setup/management---island-mode -->

# Management - Island Mode

At least one Kiosk already connected to Central Management via `Ethernet / Wi-Fi Mode` is required to onboard other Kiosks via `Island Mode`.

Only Central Management is supported for Island Mode.

## [Connecting to Central Management](/docs/mdkiosk-linux/v5.7.4/setup/management---island-mode#connecting-to-central-management)

If Kiosk will not have a network connection to the Central Management server, then Island Mode should be selected in the `Operation Mode` section.

Onboarding in Island Mode is a 4 step process carried out with another Kiosk already managed via Ethernet / Wi-Fi Mode by walking a Transfer USB between both systems.

### [Step 1](/docs/mdkiosk-linux/v5.7.4/setup/management---island-mode#step-1)

`Kiosk Name` specifies the Kiosk instance name that is displayed in Central Management for identification.

Insert a USB when prompted.

Info

A USB with a minimum size of 32GB is recommended.

A Transfer USB is tied to one specific Island Kiosk.

Each Island Kiosk requires its own Transfer USB.

Kiosk will initialize the USB for transfer and export the initial system details for onboarding.

When prompted, unplug the Transfer USB and walk it over to the Managed Kiosk.

### [Step 2](/docs/mdkiosk-linux/v5.7.4/setup/management---island-mode#step-2)

Insert the Transfer USB to the the Managed Kiosk.

The Managed Kiosk will import all the Island Kiosk system details and display the onboarding form.

To validate the onboarding, input the `Registration Code` of the Central Management server.

The Managed Kiosk will submit the onboarding information to Central Management and export items necessary to activate the Island Kiosk.

When prompted, unplug the Transfer USB and walk it over to the Island Kiosk.

### [Step 3](/docs/mdkiosk-linux/v5.7.4/setup/management---island-mode#step-3)

Insert the Transfer USB to the the Island Kiosk.

The Island Kiosk will import the items necessary for activation and export the result back to the transfer USB.

Once import is successful, the Island Kiosk is activated and ready for use.

When prompted, unplug the Transfer USB and walk it over to the Managed Kiosk.

### [Step 4](/docs/mdkiosk-linux/v5.7.4/setup/management---island-mode#step-4)

Insert the Transfer USB to the the Managed Kiosk.

The Managed Kiosk will import the Island Kiosk's activation result and notify Central Management.

When prompted, unplug the Transfer USB.

Congratulations, the Island Kiosk is now fully operational!

---

## [Operational Flow](/docs/mdkiosk-linux/v5.7.4/setup/management---island-mode#operational-flow)

Once an Island Kiosk is activated, it is recommended to keep moving the Transfer USB back and forth between the Island and Managed Kiosk on a regular basis to ensure the Island Kiosk is kept up to date and status is reflected accordingly on Central Management.

---

## [Re-creating a Transfer USB](/docs/mdkiosk-linux/v5.7.4/setup/management---island-mode#re-creating-a-transfer-usb)

In the event the Transfer USB is lost, another USB can be utilized as a Transfer USB.

On the Island Kiosk, touch the MetaDefender Kiosk logo and hit `Create Transfer USB`.

Follow the on-screen prompts and re-insert afterwards to capture the Island Kiosk export.

---

## [Modifying a Transfer USB](/docs/mdkiosk-linux/v5.7.4/setup/management---island-mode#modifying-a-transfer-usb)

Inserting the Transfer USB to another system and adding files to it is not allowed.

If a Transfer USB is identified with having more files on it than what is expected, Kiosk will identify and alert the user.

Unexpected files found on transfer media

The modified Transfer USB will be rejected until it is restored back to its original state.

To resolve, remove the additional files or re-create the Transfer USB.
