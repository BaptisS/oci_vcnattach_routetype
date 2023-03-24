# oci_vcnattach_routetype


```

#!/bin/sh
complist=$(oci iam compartment list --all --compartment-id-in-subtree true) 
complistcur=$(echo $complist | jq .data | jq -r '.[] | ."id"')
rm -f vcnattach.log
for compocid in $complistcur; do oci network drg-attachment list --compartment-id $compocid --all --attachment-type VCN >> vcnattach.log ; done
vcnattachlistcur=$(cat vcnattach.log | jq .data | jq -r '.[] | ."id"')
for drgattach in $vcnattachlistcur; do oci network drg-attachment update --drg-attachment-id  $drgattach --network-details "{'type':'VCN','vcnRouteType':'VCN_CIDRS'}" --force ; done


```
