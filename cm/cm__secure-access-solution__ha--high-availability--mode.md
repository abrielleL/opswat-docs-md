<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/ha--high-availability--mode -->

# HA (High Availability) Mode

HA (High Availability) Mode is all about keeping your systems running, come what may. It's that redundancy, that safety net, that ensures minimal downtime. Think of it as having a backup plan for your entire infrastructure. If one server goes belly up, another seamlessly takes over, keeping the lights on and the data flowing.

## How to Enable

### Setup Master node

1. Login to your 1st NAC VM as **admin** user
2. Navigate to **HA Mode**
3. Input your VIP (Virtual IP)
4. Select state as Master
5. Select Enable HA Mode

![](https://uploads.developerhub.io/prod/97qW/xi26rvmfy29jcz4bktchalcd4ws0psst4hmpdy3dd1f1zj3huberzostiwmyivk6.png)

### Setup Backup node

1. Login to your 2nd NAC VM as **admin** user
2. Navigate to **HA Mode**
3. Input your VIP (Virtual IP)
4. Select state as Backup
5. Select Enable HA Mode

![](https://uploads.developerhub.io/prod/97qW/j9teu5gtcyj96zdq2qhnhb12stf1kjetvgb7uif17mdk1bvmprajy53pbbl8dmdv.png)
