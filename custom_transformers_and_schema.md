# Custom Transformers and Schema

Schema Handling is one of the most misunderstood components in Custom Transformers.

**Attribute Schema**

The main consequence of making a reusable custom transformer is that the author (and FME) cannot be sure where the transformer will be used and whether the schema will always match what is required.

For example, in this workspace a custom transformer carries out processing on incoming data using an attribute called AddressID as a key field.

However, if – in the same workspace – that transformer is duplicated and connected to a different Reader feature type, there is no guarantee that AddressID will exist.

For example, here it is connected to a feature type where the field is in upper case, which will cause the workspace to fail when run: