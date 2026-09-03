<!-- source: https://www.opswat.com/docs/manac/nac-v8.1.1/installation/layer-3-network-integration-scripts -->

# Layer 3 Network Integration Scripts

## [Introduction](/docs/manac/nac-v8.1.1/installation/layer-3-network-integration-scripts#introduction)

## [Layer 3 Router/Switch Integration Scripts](/docs/manac/nac-v8.1.1/installation/layer-3-network-integration-scripts#layer-3-routerswitch-integration-scripts)

The following scripts are provided to integrate Layer 3 routers/switches with NAC . For information on supported makes/models/versions, please refer to the article below and review the Network Integration Requirements section.

[Technical Requirements](https://app.developerhub.io/metaaccess-nac/nac-v8.0.5/installation/technical-requirements)

If any errors are encountered or there are questions regarding the script, email opswat-support@opswat.com with the make/model of the device along with a screenshot of the errors and a support ticket will be generated.

Info

NOTE - In order for PBR to function properly, the router must have a Layer 3 interface in the subnet the NAC system resides in.

NOTE - Scripts provided below are designed to be cut and paste and non-disruptive, however, organizations are encouraged to followed existing change control guidelines.

NOTE - Scripts provided below are designed to only be modified in designated areas where variables are listed. Making other modifications to the scripts may cause the script not to function and/or impact production network traffic. __Be sure to remove all comments in () before applying the script**\

NOTE - Do not run scripts from behind Layer 3 interfaces that will be under NAC policy as terminal session connectivity loss may occur.

NOTE – Ensure routing on the test subnet for which the script is applied has already been validated before applying the script.

## [Alcatel-Lucent](/docs/manac/nac-v8.1.1/installation/layer-3-network-integration-scripts#alcatel-lucent)

### [Alcatel-Lucent Layer 3 Integration Script (6850/6900)](/docs/manac/nac-v8.1.1/installation/layer-3-network-integration-scripts#alcatel-lucent-layer-3-integration-script-68506900)

[Integration Script - Alcatel-Lucent Layer 3 Switch Integration Script (6850 or 6900).pdf](https://onlinehelp.opswat.com/safeconnect-enforcer/attachments_4085114_1_SafeConnect_Integration_Script_-_Alcatel-Lucent_Layer_3_Switch_Integration_Script_(6850_or_6900).pdf)

### [Alcatel-Lucent Layer 3 Integration Script (9700)](/docs/manac/nac-v8.1.1/installation/layer-3-network-integration-scripts#alcatel-lucent-layer-3-integration-script-9700)

[Integration Script - Alcatel-Lucent Layer 3 Switch Integration Script (9700).pdf](https://onlinehelp.opswat.com/safeconnect-enforcer/attachments_4085115_1_SafeConnect_Integration_Script_-_Alcatel-Lucent_Layer_3_Switch_Integration_Script_(9700).pdf)

## [Brocade/Ruckus/Arris/Extreme (ICX and MLX Series)](/docs/manac/nac-v8.1.1/installation/layer-3-network-integration-scripts#brocaderuckusarrisextreme-icx-and-mlx-series)

### [Brocade/Ruckus/Arris Layer 3 Integration Script (ICX)](/docs/manac/nac-v8.1.1/installation/layer-3-network-integration-scripts#brocaderuckusarris-layer-3-integration-script-icx)

[Integration Script - Brocade+Ruckus+Arris Layer 3 Switch Integration Script (ICX).pdf](https://onlinehelp.opswat.com/safeconnect-enforcer/attachments_4085128_1_SafeConnect_Integration_Script_-_Brocade+Ruckus+Arris_Layer_3_Switch_Integration_Script_(ICX).pdf)

### [Brocade/Extreme Layer 3 Integration Script (MLX)](/docs/manac/nac-v8.1.1/installation/layer-3-network-integration-scripts#brocadeextreme-layer-3-integration-script-mlx)

[Integration Script - Brocade+Ruckus+Arris Layer 3 Switch Integration Script (MLX).pdf](https://onlinehelp.opswat.com/safeconnect-enforcer/attachments_4085109_1_SafeConnect_Integration_Script_-_Brocade+Ruckus+Arris_Layer_3_Switch_Integration_Script_(MLX).pdf)

## [Cisco](/docs/manac/nac-v8.1.1/installation/layer-3-network-integration-scripts#cisco)

### [Cisco Router Integration Script (2800)](/docs/manac/nac-v8.1.1/installation/layer-3-network-integration-scripts#cisco-router-integration-script-2800)

[Integration Script - Cisco Router Integration Script (2800).pdf](https://onlinehelp.opswat.com/safeconnect-enforcer/attachments_4085108_1_SafeConnect_Integration_Script_-_Cisco_Router_Integration_Script_(2800).pdf)

### [Cisco Layer 3 Switch Integration Script (2960X/XR)](/docs/manac/nac-v8.1.1/installation/layer-3-network-integration-scripts#cisco-layer-3-switch-integration-script-2960xxr)

[Integration Script - Cisco Layer 3 Switch Integration Script (2960X or XR).pdf](https://onlinehelp.opswat.com/safeconnect-enforcer/attachments_4085107_1_SafeConnect_Integration_Script_-_Cisco_Layer_3_Switch_Integration_Script_(2960X_or_XR).pdf)

### [Cisco Layer 3 Switch Integration Script (3750X)](/docs/manac/nac-v8.1.1/installation/layer-3-network-integration-scripts#cisco-layer-3-switch-integration-script-3750x)

[Integration Script - Cisco Layer 3 Switch Integration Script (3750X).pdf](https://onlinehelp.opswat.com/safeconnect-enforcer/attachments_4085112_1_SafeConnect_Integration_Script_-_Cisco_Layer_3_Switch_Integration_Script_(3750X).pdf)

### [Cisco Layer 3 Switch Integration Script (3850/4500 SUP7-8/4500X)](/docs/manac/nac-v8.1.1/installation/layer-3-network-integration-scripts#cisco-layer-3-switch-integration-script-38504500-sup7-84500x)

[Integration Script - Cisco Layer 3 Switch Integration Script (3850 or 4500 SUP7-8 or 4500X).pdf](https://onlinehelp.opswat.com/safeconnect-enforcer/attachments_4085105_1_SafeConnect_Integration_Script_-_Cisco_Layer_3_Switch_Integration_Script_(3850_or_4500_SUP7-8_or_4500X).pdf)

### [Cisco Layer 3 Switch Integration Script (4500 SUP4-5)](/docs/manac/nac-v8.1.1/installation/layer-3-network-integration-scripts#cisco-layer-3-switch-integration-script-4500-sup4-5)

[Integration Script - Cisco Layer 3 Switch Integration Script (4500 SUP4-5).pdf](https://onlinehelp.opswat.com/safeconnect-enforcer/attachments_4085099_1_SafeConnect_Integration_Script_-_Cisco_Layer_3_Switch_Integration_Script_(4500_SUP4-5).pdf)

### [Cisco Layer 3 Switch Integration Script (6500 SUP720)](/docs/manac/nac-v8.1.1/installation/layer-3-network-integration-scripts#cisco-layer-3-switch-integration-script-6500-sup720)

[Integration Script - Cisco Layer 3 Switch Integration Script (6500 SUP720).pdf](https://onlinehelp.opswat.com/safeconnect-enforcer/attachments_4085104_1_SafeConnect_Integration_Script_-_Cisco_Layer_3_Switch_Integration_Script_(6500_SUP720).pdf)

### [Cisco Layer 3 Switch Integration Script (6500/6800 SUP2T)](/docs/manac/nac-v8.1.1/installation/layer-3-network-integration-scripts#cisco-layer-3-switch-integration-script-65006800-sup2t)

[Integration Script - Cisco Layer 3 Switch Integration Script (6500 or 6800 SUP-2T).pdf](https://onlinehelp.opswat.com/safeconnect-enforcer/attachments_4085130_1_SafeConnect_Integration_Script_-_Cisco_Layer_3_Switch_Integration_Script_(6500_or_6800_SUP-2T).pdf)

### [Cisco Layer 3 Switch Integration Script (Nexus 7000)](/docs/manac/nac-v8.1.1/installation/layer-3-network-integration-scripts#cisco-layer-3-switch-integration-script-nexus-7000)

[Integration Script - Cisco Layer 3 Switch Integration Script (Nexus 7000).pdf](https://onlinehelp.opswat.com/safeconnect-enforcer/attachments_4085103_1_SafeConnect_Integration_Script_-_Cisco_Layer_3_Switch_Integration_Script_(Nexus_7000).pdf)

### [Cisco Layer 3 Switch Integration Script (Nexus 7000 F2/3 Module)](/docs/manac/nac-v8.1.1/installation/layer-3-network-integration-scripts#cisco-layer-3-switch-integration-script-nexus-7000-f23-module)

[Integration Script - Cisco Layer 3 Switch Integration Script (Nexus 7000 F2 or 3 Module).pdf](https://onlinehelp.opswat.com/safeconnect-enforcer/attachments_4085102_1_SafeConnect_Integration_Script_-_Cisco_Layer_3_Switch_Integration_Script_(Nexus_7000_F2_or_3_Module).pdf)

### [Cisco Layer 3 Switch Integration Script (Nexus 9300/9500)](/docs/manac/nac-v8.1.1/installation/layer-3-network-integration-scripts#cisco-layer-3-switch-integration-script-nexus-93009500)

[Integration Script - Cisco Layer 3 Switch Integration Script (Nexus 9300 or 9500).pdf](https://onlinehelp.opswat.com/safeconnect-enforcer/attachments_4085113_1_SafeConnect_Integration_Script_-_Cisco_Layer_3_Switch_Integration_Script_(Nexus_9300_or_9500).pdf)

### [Cisco Layer 3 Switch Integration Script (Catalyst 9500)](/docs/manac/nac-v8.1.1/installation/layer-3-network-integration-scripts#cisco-layer-3-switch-integration-script-catalyst-9500)

[Integration Script - Cisco Layer 3 Switch Integration Script (Catalyst 9500).pdf](https://onlinehelp.opswat.com/safeconnect-enforcer/attachments_4085131_1_SafeConnect_Integration_Script_-_Cisco_Layer_3_Switch_Integration_Script_(Catalyst_9500).pdf)

## [Dell](/docs/manac/nac-v8.1.1/installation/layer-3-network-integration-scripts#dell)

### [Dell N-Series/OS6 Layer 3 Integration Script](/docs/manac/nac-v8.1.1/installation/layer-3-network-integration-scripts#dell-n-seriesos6-layer-3-integration-script)

[Integration Script - Dell-EMC N-Series OS6 Layer 3 Integration.pdf](https://onlinehelp.opswat.com/safeconnect-enforcer/attachments_4085132_1_SafeConnect_Integration_Script_-_Dell-EMC_N-Series_OS6_Layer_3_Integration.pdf)

### [Dell S-Series/OS9 Layer 3 Integration Script](/docs/manac/nac-v8.1.1/installation/layer-3-network-integration-scripts#dell-s-seriesos9-layer-3-integration-script)

[Integration Script - Dell-EMC S-Series OS9 Layer 3 Integration.pdf](https://onlinehelp.opswat.com/safeconnect-enforcer/attachments_4085098_1_SafeConnect_Integration_Script_-_Dell-EMC_S-Series_OS9_Layer_3_Integration.pdf)

## [HP](/docs/manac/nac-v8.1.1/installation/layer-3-network-integration-scripts#hp)

### [HP Layer 3 Integration Script (3800)](/docs/manac/nac-v8.1.1/installation/layer-3-network-integration-scripts#hp-layer-3-integration-script-3800)

[Integration Script - HP Layer 3 Switch Integration Script (3800).pdf](https://onlinehelp.opswat.com/safeconnect-enforcer/attachments_4085110_1_SafeConnect_Integration_Script_-_HP_Layer_3_Switch_Integration_Script_(3800).pdf)

### [HP Layer 3 Integration Script (5400/8200)](/docs/manac/nac-v8.1.1/installation/layer-3-network-integration-scripts#hp-layer-3-integration-script-54008200)

[Integration Script - HP Layer 3 Switch Integration Script (5400 or 8200).pdf](https://onlinehelp.opswat.com/safeconnect-enforcer/attachments_4085111_1_SafeConnect_Integration_Script_-_HP_Layer_3_Switch_Integration_Script_(5400_or_8200).pdf)
