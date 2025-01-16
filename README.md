# Microsoft365-Hunting
This is just a dumping ground for my brain, if it helped you I am glad it did.

## Joining alertinfo and alertevidence

The `alertinfo` table contains the incidents you see in Defender, the alertevidence contains the information about the various entities like:

* files
* ip addresses
* urls
* users
* devices

You can link these two tables together on the AlertId:

```Text
AlertInfo
| join AlertEvidence on $left.AlertId == $right.AlertId
```
