---
page_title: "solidserver_ip_subnet Resource - SOLIDserver"
subcategory: ""
description: |-
  IP Subnet resource allows to create and manage IPAM networks that are key to organize the IP space
  Subnet can be blocks or subnets. Blocks reflect the assigned IP ranges (RFC1918 or public prefixes).
  Subnets reflect the internal sub-division of your network.
---

# solidserver_ip_subnet (Resource)

IP Subnet resource allows to create and manage IPAM networks that are key to organize the IP space
Subnet can be blocks or subnets. Blocks reflect the assigned IP ranges (RFC1918 or public prefixes).
Subnets reflect the internal sub-division of your network.

## Example Usage

```terraform
resource "solidserver_ip_subnet" "myFirstIPBlock" {
  space            = "${solidserver_ip_space.myFirstSpace.name}"
  request_ip       = "10.0.0.0"
  prefix_size      = 8
  name             = "myFirstIPBlock"
  terminal         = false
}

resource "solidserver_ip_subnet" "myFirstIPSubnet" {
  space            = "${solidserver_ip_space.myFirstSpace.name}"
  block            = "${solidserver_ip_subnet.myFirstIPBlock.name}"
  prefix_size      = 24
  name             = "myFirstIPSubnet"
  gateway_offset   = -1
  class            = "VIRTUAL"
  class_parameters = {
    vnid = "12666"
  }
}
```
<!-- schema generated by tfplugindocs -->
## Schema

### Required

- `name` (String) The name of the IP subnet to create.
- `prefix_size` (Number) The expected IP subnet's prefix length (ex: 24 for a '/24').
- `space` (String) The name of the space into which creating the subnet.

### Optional

- `block` (String) The name of the parent IP block/subnet into which creating the IP subnet.
- `class` (String) The class associated to the IP subnet.
- `class_parameters` (Map of String) The class parameters associated to the IP subnet.
- `gateway_offset` (Number) Offset for creating the gateway. Default is 0 (No gateway).
- `request_ip` (String) The optionally requested subnet IP address.
- `terminal` (Boolean) The terminal property of the IP subnet.

### Read-Only

- `address` (String) The provisionned IP network address.
- `gateway` (String) The subnet's computed gateway.
- `id` (String) The ID of this resource.
- `netmask` (String) The provisionned IP address netmask.
- `prefix` (String) The provisionned IP prefix.
