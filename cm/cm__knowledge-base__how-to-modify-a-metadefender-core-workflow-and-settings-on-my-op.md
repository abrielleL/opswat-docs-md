<!-- source: https://www.opswat.com/docs/cm/knowledge-base/how-to-modify-a-metadefender-core-workflow-and-settings-on-my-op -->

# How to modify a MetaDefender Core workflow and settings on My OPSWAT Central Management?

> **Check Your Version:**
>
> This article applies to all My OPSWAT Central Management releases deployed on Windows and Linux systems.

## **How to modify an individual MetaDefender Core workflow without a Policy:**

1. Navigate to Inventory > Service > Core > Click into the desired MetaDefender Core

   ![](https://uploads.developerhub.io/prod/97qW/4ww24z5de78mpc1pikd6yckdrf4fxjvrpmyv18y00fzh4jox3e23ezqaimoi7i0m.png)
2. Click “Edit” and select the desired setting to modify and save

   ![](https://uploads.developerhub.io/prod/97qW/1xmpkln7849jdap0aw4born98woxku2skjdo8t8dwcro7bx4jzo78pqu7xm45ob9.png)

 

## **How to modify a policy and assign it to MetaDefender Core:**

1. Select Policies > File Security > Core. If you have not imported a policy from one of the connected cores, please select “Import Policy from Instance”

   ![](https://uploads.developerhub.io/prod/97qW/7lx7v68is0g61skz30oignbv224d764w6v69xmzwgy6bbi2x8fumlltekiwkyv6x.png)

   ![](https://uploads.developerhub.io/prod/97qW/a7c7ldmhpxm8khezeqd5twt0t70mo8ezwv58bi6zoaockiyfjc9aj5227s6q1biz.png)

    
2. Hit edit on the imported workflows and save.
3. Navigate to Inventory > Groups > select groups or add cores to a new group > Assign the new policy created to the group of Cores.

![](https://uploads.developerhub.io/prod/97qW/3wa17t16dn4xwwumqoerfpg7f6uvkh3u76k7ouwv5vxby5ra08612a05u9krp84m.png)

4. By default, the policy will not be pushed automatically to the cores when a change it made to the policy. If you want all workflow and setting changes pushed to the group of Cores automatically, please enable auto sync.

   ![](https://uploads.developerhub.io/prod/97qW/gfef8qyr651eskp0verzbsyxc23zgmlivuevuon27mugfj8hfdtld0rqpzznjl4e.png)

   ![](https://uploads.developerhub.io/prod/97qW/j5os0gp6ejgo45nmu2myqsu57fsb9lwaopkx7c7sqeph169fj6mav5nuxpjbhh7d.png)

    

> **Support:**
>
> If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).
