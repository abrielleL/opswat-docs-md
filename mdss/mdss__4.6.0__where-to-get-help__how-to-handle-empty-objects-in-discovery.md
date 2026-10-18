<!-- source: https://www.opswat.com/docs/mdss/4.6.0/where-to-get-help/how-to-handle-empty-objects-in-discovery -->

# How to handle empty objects in Discovery?

To skip the discovery of empty objects, please add the following property in your `customer.env` file:

```bash
DISCOVERY_SERVICE_IGNORE_EMPTY_OBJECTS=1
```

By default, this value is set to 0, which means we will **not** ignore empty objects.

After the property is added in your `customer.env`  file, please restart MetaDefender Storage Security for changes to take effect.

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
