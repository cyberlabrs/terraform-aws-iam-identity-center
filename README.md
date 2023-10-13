<!-- BEGIN_TF_DOCS -->
## Requirements

| Name | Version |
|------|---------|
| <a name="requirement_terraform"></a> [terraform](#requirement\_terraform) | >= 1.3 |
| <a name="requirement_aws"></a> [aws](#requirement\_aws) | >= 4.65 |

## Providers

| Name | Version |
|------|---------|
| <a name="provider_aws"></a> [aws](#provider\_aws) | >= 4.65 |

## Modules

No modules.

## Resources

| Name | Type |
|------|------|
| [aws_identitystore_group.groups](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/identitystore_group) | resource |
| [aws_identitystore_group_membership.membership](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/identitystore_group_membership) | resource |
| [aws_identitystore_user.users](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/identitystore_user) | resource |
| [aws_ssoadmin_account_assignment.attachments](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/ssoadmin_account_assignment) | resource |
| [aws_ssoadmin_customer_managed_policy_attachment.customer_managed_policies](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/ssoadmin_customer_managed_policy_attachment) | resource |
| [aws_ssoadmin_managed_policy_attachment.managed_policies](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/ssoadmin_managed_policy_attachment) | resource |
| [aws_ssoadmin_permission_set.permission_sets](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/ssoadmin_permission_set) | resource |
| [aws_ssoadmin_permission_set_inline_policy.inline_policy](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/ssoadmin_permission_set_inline_policy) | resource |
| [aws_ssoadmin_permissions_boundary_attachment.customer_managed_boundary](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/ssoadmin_permissions_boundary_attachment) | resource |
| [aws_ssoadmin_permissions_boundary_attachment.managed_boundary](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/ssoadmin_permissions_boundary_attachment) | resource |
| [aws_ssoadmin_instances.this](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/ssoadmin_instances) | data source |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| <a name="input_attachments"></a> [attachments](#input\_attachments) | The list of attachments | <pre>list(object({<br>    permission_set_arn      = optional(string),<br>    permission_set_name     = optional(string),<br>    principal_type          = string,<br>    principal_id            = optional(string),<br>    principal_group_name    = optional(string),<br>    principal_user_username = optional(string),<br>    target_account_id       = string,<br>  }))</pre> | `[]` | no |
| <a name="input_groups"></a> [groups](#input\_groups) | The list of groups | <pre>list(object({<br>    name        = string,<br>    description = optional(string, null)<br>    users       = optional(list(string), [])<br>  }))</pre> | `[]` | no |
| <a name="input_permission_sets"></a> [permission\_sets](#input\_permission\_sets) | The list of permission sets | <pre>list(object({<br>    name                      = string,<br>    description               = optional(string, null)<br>    relay_state               = optional(string, null)<br>    session_duration          = optional(string, "PT1H")<br>    managed_policies          = optional(list(string), [])<br>    customer_managed_policies = optional(any, [])<br>    inline_policy             = optional(string, null)<br>    inline_policy_json_path   = optional(string, null)<br>    boundary_policy = optional(object({<br>      type                 = string<br>      managed_policy_arn   = optional(string)<br>      customer_policy_name = optional(string)<br>      customer_policy_path = optional(string)<br>    }))<br>  }))</pre> | `[]` | no |
| <a name="input_users"></a> [users](#input\_users) | The list of users | <pre>list(object({<br>    display_name       = string<br>    user_name          = string<br>    locale             = optional(string)<br>    nickname           = optional(string)<br>    preferred_language = optional(string)<br>    profile_url        = optional(string)<br>    timezone           = optional(string)<br>    title              = optional(string)<br>    user_type          = optional(string)<br>    name = object({<br>      family_name = string<br>      given_name  = string<br>    })<br>    emails = optional(list(object({<br>      primary = optional(bool)<br>      type    = optional(string)<br>      value   = optional(string)<br>    })))<br>    phone_numbers = optional(list(object({<br>      primary = optional(bool)<br>      type    = optional(string)<br>      value   = optional(string)<br>    })))<br>    addresses = optional(list(object({<br>      country        = optional(string)<br>      formatted      = optional(string)<br>      locality       = optional(string)<br>      postal_code    = optional(string)<br>      primary        = optional(string)<br>      region         = optional(string)<br>      street_address = optional(string)<br>      type           = optional(string)<br>    })))<br><br>  }))</pre> | `[]` | no |

## Outputs

No outputs.
<!-- END_TF_DOCS -->