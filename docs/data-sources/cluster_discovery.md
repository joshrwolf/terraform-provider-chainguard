---
# generated by https://github.com/hashicorp/terraform-plugin-docs
page_title: "chainguard_cluster_discovery Data Source - terraform-provider-chainguard"
subcategory: ""
description: |-
  Potential clusters to install found via Enforce cluster discovery.
---

# chainguard_cluster_discovery (Data Source)

Potential clusters to install found via Enforce cluster discovery.

## Example Usage

```terraform
data "chainguard_cluster_discovery" "example" {
  id        = "foo/bar"
  profiles  = ["observer"]
  providers = ["CLOUD_RUN"]
}
```

<!-- schema generated by tfplugindocs -->
## Schema

### Required

- `id` (String) Exact UIDP of the IAM Group to use for impersonation when discovering clusters
- `profiles` (List of String) List of profiles to verify compatibility with. Allowed values are "observer", "enforcer"
- `providers` (List of String) List of provider types to check. Allowed value are "APP_RUNNER", "CLOUD_RUN", "ECS", "EKS", "GKE", "KIND", "UNKNOWN"

### Optional

- `states` (List of String) A filter on the discovered cluster states to return. Allowed value are "ELIGIBLE", "ENROLLED", "NEEDS_WORK", "UNKNOWN", "UNSUPPORTED" (if unspecified, this defaults to ELIGIBLE and ENROLLED)

### Read-Only

- `results` (Attributes List) Discovered clusters. (see [below for nested schema](#nestedatt--results))

<a id="nestedatt--results"></a>
### Nested Schema for `results`

Read-Only:

- `account` (String) Cloud account where cluster was discovered
- `location` (String) Cluster location
- `name` (String) Cluster name
- `provider` (String) Cluster provider type
- `state` (Attributes List) Cluster state (see [below for nested schema](#nestedatt--results--state))

<a id="nestedatt--results--state"></a>
### Nested Schema for `results.state`

Optional:

- `certificate_authority_data` (String) If state is eligible or enrolled, this is the PEM encoded CA chain for the api-server
- `id` (String) If state is enrolled, this is the UIDP of the cluster
- `profiles` (List of String) If state is enrolled, these are the installed profiles
- `reason` (String) If state is unsupported this is why
- `server` (String) If state is eligible or enrolled, this is the cluster api-server URL
- `steps` (List of String) If state is needswork, this are remediation steps

Read-Only:

- `state` (String) State of discovered cluster