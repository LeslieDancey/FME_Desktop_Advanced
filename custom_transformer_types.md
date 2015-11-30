# Custom Transformer Types

Custom Transformers come in two flavors: Embedded and Linked.

**Custom Transformer Types**

There are two types of custom transformers: Embedded and Linked.

An embedded transformer is one that exists only in the workspace itself. Its definition is stored (embedded) inside the workspace file and it is not available to any other workspace.

A linked transformer is one that exists outside of a workspace. Its definition is stored in its own file and it is available to any other workspace, which reference it through a link.

On a workspace canvas, embedded transformers are identified by their green color, while linked transformers are colored cyan:

**Linked vs Embedded Transformers**

Both type of transformer can be used in an FME workspace, and there are various advantages and disadvantages to each type.

**Embedded Transformers**