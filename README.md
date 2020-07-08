# Example of Using The Custom Resource InSpec Profile For AWS 

The resource pack repository is here: https://github.com/skpaterson/example_aws_custom_resource_pack

Included in this resource pack is the following:

```
.
├── README.md
├── attributes.yml
├── controls
│   └── use_custom_resource_and_inspec_aws.rb
└── inspec.yml
```

Note that the controls directory here contains a test that uses both the custom resource from the resource pack and InSpec AWS resources.

The inspec.yml file in this repository declares the dependency on the resource pack:

```
depends:
- name: example_aws_custom_resource_pack
  url: https://github.com/skpaterson/example_aws_custom_resource_pack/archive/master.tar.gz
```

The dependency on InSpec AWS therefore comes from the inspec.yml file in the resource pack repository.

From the root of this repository this is an outline of what the execution would look like e.g. 

```
example_using_custom_resource_pack spaterson$ bundle exec inspec exec . -t aws://

Profile: AWS InSpec Profile (example_using_aws_custom_resource_pack)
Version: 0.1.0
Target:  aws://eu-west-2

  ↺  aws-single-vpc-exists-check: Check to see if custom VPC exists.
     ↺  Skipped control due to only_if condition.
  ✔  aws-vpcs-check: Check in all the VPCs for default sg not allowing 22 inwards
     ✔  EC2 Security Group ID: sg-12345 Name: default VPC ID: vpc-12345  is expected to allow in {:port=>22}
  ✔  aws-vpcs-multi-region-status-check: Check AWS VPCs in all regions have status "available"
     ✔  VPC vpc-12345 in eu-north-1 is expected to exist
     ✔  VPC vpc-12345 in eu-north-1 is expected to be available
     ✔  VPC vpc-54321 in eu-north-1 is expected to exist
     ✔  VPC vpc-54321 in eu-north-1 is expected to be available
    ...

  AWS Custom Resource
     ✔  is expected to exist

Profile: Example AWS InSpec Custom Resource Pack (example_aws_custom_resource_pack)
Version: 0.1.0
Target:  aws://eu-west-2

     No tests executed.

Profile: Amazon Web Services  Resource Pack (inspec-aws)
Version: 1.26.1
Target:  aws://eu-west-2

     No tests executed.

Profile Summary: 2 successful controls, 0 control failures, 1 control skipped
Test Summary: 72 successful, 0 failures, 1 skipped
```