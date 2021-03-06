---
layout: "heroku"
page_title: "Heroku: heroku_space"
sidebar_current: "docs-heroku-resource-space"
description: |-
  Provides a Heroku Space resource for running apps in isolated, highly available, secure app execution environments.
---

# heroku\_space

Provides a Heroku Space resource for running apps in isolated, highly available, secure app execution environments.

## Example Usage

```hcl
// Create a new Heroku space
resource "heroku_space" "default" {
  name = "test-space"
  organization = "my-company"
  region = "virginia"
}

// Create a new Heroku app in test-space
resource "heroku_app" "default" {
  name = "test-app"
  space = "${heroku_space.default.name}"
  organization = {
    name = "my-company"
  }
}
```

## Argument Reference

The following arguments are supported:

* `name` - (Required) The name of the space.
* `organization` - (Required) The name of the organization which will own the space.
* `region` - (Optional) The region that the space should be created in.
* `shield` - (Optional) Whether or not the private space should be [shielded](https://devcenter.heroku.com/articles/private-spaces#shield-private-spaces).

## Attributes Reference

The following attributes are exported:

* `id` - The ID of the space.
* `name` - The space's name.
* `organization` - The space's organization.
* `region` - The space's region.
* `outbound_ips` - The space's stable outbound [NAT IPs](https://devcenter.heroku.com/articles/platform-api-reference#space-network-address-translation).

## Import

Spaces can be imported using the space `id`, e.g.

```
$ terraform import heroku_space.foobar MySpace
```
