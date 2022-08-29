---
# generated by https://github.com/hashicorp/terraform-plugin-docs
page_title: "citrixadm_apigw_proxy Resource - terraform-provider-citrixadm"
subcategory: ""
description: |-
  Configure API Proxy endpoint on API Gateway
---

# citrixadm_apigw_proxy (Resource)

Configure API Proxy endpoint on API Gateway

## Example Usage

```terraform
data "citrixadm_managed_device" "device1" {
  ip_address = "10.0.1.42"
}
resource "citrixadm_apigw_proxy" "proxy1" {
  proxy_name           = "tf_proxy101"
  host                 = "2.2.2.2"
  port                 = 22
  protocol             = "https"
  deploy               = "false"
  service_fqdns        = ["api.example.com"]
  tls_security_profile = "High Security"
  tls_certkey_objref {
    adm_certkey {
      id = "abcdefgh-1234-5678-ijkl-mnopqrstuvwx"
    }
  }
  target_apigw {
    target_device {
      id           = data.citrixadm_managed_device.device1.id
      display_name = data.citrixadm_managed_device.device1.ip_address
    }
  }
}
```

<!-- schema generated by tfplugindocs -->
## Schema

### Required

- `deploy` (Boolean)
- `host` (String) Hostname or IP address (Citrix ADC VIP) where API traffic will be received by Citrix ADC from API clients.
- `port` (Number) API Proxy Port number
- `protocol` (String) Protocol: http/https
- `proxy_name` (String) API Proxy name
- `target_apigw` (Block List, Min: 1, Max: 1) Target ADC instance acting as API GW (see [below for nested schema](#nestedblock--target_apigw))

### Optional

- `service_fqdns` (List of String) Service FQDNs where API traffic will be received from api clients
- `tls_certkey_objref` (Block List, Max: 1) Reference to existing TLS certkey object in ADM (see [below for nested schema](#nestedblock--tls_certkey_objref))
- `tls_security_profile` (String) TLS Security profile

### Read-Only

- `id` (String) The ID of this resource.

<a id="nestedblock--target_apigw"></a>
### Nested Schema for `target_apigw`

Required:

- `target_device` (Block List, Min: 1, Max: 1) ADC device details (see [below for nested schema](#nestedblock--target_apigw--target_device))

<a id="nestedblock--target_apigw--target_device"></a>
### Nested Schema for `target_apigw.target_device`

Required:

- `display_name` (String) ADC Instance Name(IP-Address)
- `id` (String) ADC Instance Id



<a id="nestedblock--tls_certkey_objref"></a>
### Nested Schema for `tls_certkey_objref`

Optional:

- `adm_certkey` (Block List, Max: 1) Reference to existing TLS certkey object in ADM (see [below for nested schema](#nestedblock--tls_certkey_objref--adm_certkey))

<a id="nestedblock--tls_certkey_objref--adm_certkey"></a>
### Nested Schema for `tls_certkey_objref.adm_certkey`

Optional:

- `id` (String) Cert File Id

