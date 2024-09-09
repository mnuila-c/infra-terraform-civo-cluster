# Civo Cluster Template

Terraform module which deploys Civo kubernetes cluster on CIVO provider.

## Usage

```hcl
module "civo_k8s_cluster" {
  source = "./modules/civo-k8s-cluster"

  cluster_name           = "civo-cluster"
  network_label          = "civo-network"
  firewall_name          = "civo-fw-rule"
  node_pool_label        = "civo-node-pool"
  network_cidr_v4        = "192.168.0.0/24"
  network_nameservers_v4 = ["8.8.8.8", "1.1.1.1"]
  kubernetes_version     = "1.27.0"
  region                 = "NYC1"
  cluster_type           = "talos"
  cni                    = "flannel"
  node_size              = "g4s.kube.small"
  node_count             = 3
  local_cidr             = ["192.168.0.0/24"]
  external_network       = ["0.0.0.0/0"]
  default_cidr           = ["0.0.0.0/0"]
}
```

## Examples

- ...
- ...

## Contributing

Please read our [contributing guide](./docs/CONTRIBUTING.md) if you're interested in contributing to Walrus template.

<!-- BEGIN_TF_DOCS -->
## Requirements

| Name | Version |
|------|---------|
| <a name="requirement_terraform"></a> [terraform](#requirement\_terraform) | >= 1.5.7 |
| <a name="requirement_kubernetes"></a> [kubernetes](#requirement\_kubernetes) | >= 2.23.0 |
| <a name="requirement_helm"></a> [helm](#requirement\_helm) | >= 2.11.0 |

## Providers

| Name | Version |
|------|---------|
| <a name="provider_civo"></a> [civo](#provider\_civo) | >= 1.0.49 |
| <a name="provider_kubernetes"></a> [kubernetes](#provider\_kubernetes) | >= 2.23.0 |
| <a name="provider_helm"></a> [helm](#provider\_helm) | >= 2.11.0 |

## Modules

No modules.

## Resources

| Name | Type |
|------|------|
| [civo_kubernetes_cluster.my-cluster](https://registry.terraform.io/providers/civo/civo/latest/docs/resources/kubernetes_cluster) | resource |
| [civo_network.custom_net](https://registry.terraform.io/providers/civo/civo/latest/docs/resources/network) | resource |
| [civo_firewall.custom_rule](https://registry.terraform.io/providers/civo/civo/latest/docs/resources/firewall) | resource |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| <a name="input_namespace_name"></a> [namespace_name](#input\_namespace_name) | Specify the deployment namespace name, default value netris-operator. | `string` | `"standalone"` | no |
| <a name="input_context"></a> [context](#input\_context) | Receive contextual information. When Walrus deploys, Walrus will inject specific contextual information into this field.<br><br>Examples:<pre>context:<br>  project:<br>    name: string<br>    id: string<br>  environment:<br>    name: string<br>    id: string<br>  resource:<br>    name: string<br>    id: string</pre> | `map(any)` | `{}` | no |
| <a name="input_engine_parameters"></a> [engine\_parameters](#input\_engine\_parameters) | Specify the deployment parameters, see https://docs.aws.amazon.com/AmazonElastiCache/latest/red-ug/ParameterGroups.Redis.html. | <pre>list(object({<br>    name  = string<br>    value = string<br>  }))</pre> | `[]` | no |
| <a name="input_engine_version"></a> [engine\_version](#input\_engine\_version) | Specify the deployment engine version. | `string` | `"7.0"` | no |
| <a name="input_infrastructure"></a> [infrastructure](#input\_infrastructure) | Specify the infrastructure information for deploying.<br><br>Examples:<pre>infrastructure:<br>  vpc_id: string, optional             # the ID of the VPC where the Redis service applies<br>  kms_key_id: string, optional         # the ID of the KMS key which to encrypt the Redis data<br>  domain_suffix: string, optional      # a private DNS namespace of the CloudMap where to register the applied Redis service</pre> | <pre>object({<br>    vpc_id        = optional(string)<br>    kms_key_id    = optional(string)<br>    domain_suffix = optional(string)<br>  })</pre> | `{}` | no |
| <a name="input_password"></a> [password](#input\_password) | Specify the account password. The password must be 16-32 characters long and start with any letter, number, or the following symbols: ! # $ % ^ & * ( ) \_ + - =.<br>If not specified, it will generate a random password. | `string` | `null` | no |
| <a name="input_replication_readonly_replicas"></a> [replication\_readonly\_replicas](#input\_replication\_readonly\_replicas) | Specify the number of read-only replicas under the replication deployment. | `number` | `1` | no |
| <a name="input_resources"></a> [resources](#input\_resources) | Specify the computing resources.<br>Examples:<pre>resources:<br>  class: string, optional      # https://docs.aws.amazon.com/AmazonElastiCache/latest/red-ug/CacheNodes.SupportedTypes.html</pre> | <pre>object({<br>    class = optional(string, "cache.t3.micro")<br>  })</pre> | <pre>{<br>  "class": "cache.t3.micro"<br>}</pre> | no |

## Outputs

| Name | Description |
|------|-------------|
| <a name="output_submodule"></a> [submodule](#output\_submodule) | The message from submodule. |
| <a name="output_walrus_environment_id"></a> [walrus\_environment\_id](#output\_walrus\_environment\_id) | The id of environment where deployed in Walrus. |
| <a name="output_walrus_environment_name"></a> [walrus\_environment\_name](#output\_walrus\_environment\_name) | The name of environment where deployed in Walrus. |
| <a name="output_walrus_project_id"></a> [walrus\_project\_id](#output\_walrus\_project\_id) | The id of project where deployed in Walrus. |
| <a name="output_walrus_project_name"></a> [walrus\_project\_name](#output\_walrus\_project\_name) | The name of project where deployed in Walrus. |
| <a name="output_walrus_resource_id"></a> [walrus\_resource\_id](#output\_walrus\_resource\_id) | The id of resource where deployed in Walrus. |
| <a name="output_walrus_resource_name"></a> [walrus\_resource\_name](#output\_walrus\_resource\_name) | The name of resource where deployed in Walrus. |
<!-- END_TF_DOCS -->

## License

Copyright (c) 2023 [Seal, Inc.](https://seal.io)

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at [LICENSE](./LICENSE) file for details.

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
