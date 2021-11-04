# This is the changelog for NCBI specific modifications
## v2.70.0-ncbi - November 2021
### Option to suppress route table creation for intra network
The module is useful because it works around TF inability to nest for_each statements when creating multiple (for instance) subnets for multiple vpcs.

Ordinarily the module will force create a route table for each intra (no NAT) subnet.  However we want the default route table for all the intra subnets so they can be routed to shared service for out and inbound.  

Introduces a new variable `create_intra_subnet_route_table`, default true to maintain original behaviour.  We set it to `false` and get the desired subnets without an unwanted set of subnet-specific RTBs and associations.

Also note, since the default label `intra` is inaccurate for our private subnets that are inspected by shared services, we use the existing `intra_subnet_suffix` and change to `inspected`
