# netflix spinnaker templates

Spinnaker is a centrally run product at Netflix, which we deploy continuously
as development happens. These are templates that closely mimic the ones our team
uses to deploy the Spinnaker services. Our clouddriver deployment pipelines are 
different enough from the other services that it is not represented here.

Internally, we manage our own Redis instances rather than use ElastiCache. Since
this is an implementation detail of our deployment which depends on Netflix-only
infrastructure features, so we're not including these pipelines.

You'll find 4 different templates:

1. Bake & Tag
2. Deploy to Env Root
3. Deploy From Cluster (extends 2)
4. Deploy From Image Tags (extends from 2)

The end-result pipelines that are created from these templates look like so:

```
1. Bake & Tag (triggered from Jenkins)
2. Deploy to Test, uses Deploy from Image Tags (triggered by #1)
3. Promote to Staging, uses Deploy from Cluster (triggered by #2)
4. Promote to Prod, uses Deploy from Cluster (manually trigger)
4b. Promote to Failover (this is part of the Env Root template, but is not
    currently present in these examples)
```
