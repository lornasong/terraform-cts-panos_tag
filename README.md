# PANOS Tag Module for Consul Terraform Sync

This Terraform module creates tags in a Palo Alto FW. Using this module in automation with [Consul Terraform Sync (CTS)](https://www.consul.io/docs/nia) will dynamically create or delete tags based off of configured services. This module is useful for testing CTS to observe how changes in service instances play out in a Palo Alto instance.

## Feature

The module uses the `panos` Terraform provider to create tags. The tags are named after the monitored Consul service instances.

## Requirements

### Ecosystem Requirements

| Ecosystem | Version |
|-----------|---------|
| [consul](https://www.consul.io/downloads) | >= 1.7 |
| [consul-terraform-sync](https://www.consul.io/docs/nia) | >= 0.1.0 |
| [terraform](https://www.terraform.io) | >= 0.13 |

### Terraform Providers

| Name | Version |
|------|---------|
| panos | >= 1.8.0 |

## Setup

This module expects that the user has already setup a PANOS firewall with a username and password / token.

## Usage

**User Config for Consul Terraform Sync**

See [Securely Configure Terraform Providers](https://www.consul.io/docs/nia/configuration#securely-configure-terraform-providers) for alternatives to directly inserting token in config file.

example.hcl
```hcl
task {
  name           = "task_d"
  services       = ["api"]
  providers      = ["panos"]
  version        = "0.0.1"
  source         = "lornasong/panos_tag/cts"
}

terraform_provider "panos" {
  hostname = "ZZ.ZZ.ZZ.ZZ"
  username = "YYYY"
  api_key = "XXXX"
}
```
