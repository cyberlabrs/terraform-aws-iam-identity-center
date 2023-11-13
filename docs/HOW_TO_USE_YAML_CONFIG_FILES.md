# Guide: How to use yaml config files to set variables

## Warning

`.yaml` files take precedence over `.yml` files, and both take precedence over Terraform variables

## Create yaml config files

1. Create a folder named `conf` inside your module directory and relevant config files inside that folder. If you don't define some of the config files, Terraform variables will be used instead.

2. Create `permission_sets.yaml` or `permission_sets.yml`:

```yaml
# permission sets
permission_sets:
  # managed policy and customer_managed_policy
  - name: "AdministratorAccess"
    description: "Description for administrator access"
    managed_policies: ["arn:aws:iam::aws:policy/AdministratorAccess"]
    customer_managed_policies:
      - name: "customized_billing_policy" # imagine we have a policy in IAM
        path: "/"
    session_duration: "PT4H"
  # example for inline with json path
  - name: "CustomizedS3ReadAccessJsonPath"
    description: "S3 read only"
    inline_policy_json_path: "./policies/S3ReadCustomizedBucket.json"
    session_duration: "PT4H"
    boundary_policy:
      type: "CUSTOMER_MANAGED"
      customer_policy_name: "s3_boundary_customer_managed_policy" # imagine we have a policy in IAM
      customer_policy_path: "/"
  # example for inline with json path
  - name: "CustomizedS3ReadAccessInline"
    description: "S3 read only"
    inline_policy:
      {
        "Version": "2012-10-17",
        "Statement":
          [
            {
              "Effect": "Allow",
              "Action": ["s3:GetObject", "s3:GetObjectVersion"],
              "Resource": "arn:aws:s3:::example/*",
            },
          ],
      }
    session_duration: "PT4H"
    boundary_policy:
      type: "MANAGED"
      managed_policy_arn: "arn:aws:iam::aws:policy/S3ReadOnly"
```

3. Create `groups.yaml` or `groups.yml`:

```yaml
# groups
groups:
  - name: "Admin"
    description: "Description for admin group"
    users: ["test.admin"]
  - name: "TeamA"
    description: "Description for team A"
    users:
      - "teamA.user1"
      - "teamA.user2"
  - name: "TeamA"
    description: "Description for team B"
    users:
      - "teamB.user1"
      - "teamB.user2"
```

4. Create `attachments.yaml` or `attachments.yml`:

```yaml
# attachments
attachments:
  - permission_set_name: "AdministratorAccess"
    principal_type: "GROUP"
    principal_group_name: "Admin"
    target_account_id: "ACCOUNT_ID" # account id
  - permission_set_name: "CustomizedS3ReadAccessJsonPath"
    principal_type: "GROUP"
    principal_group_name: "TeamB"
    target_account_id: "ACCOUNT_ID" # account id
  - permission_set_name: "CustomizedS3ReadAccessInline"
    principal_type: "GROUP"
    principal_group_name: "TeamA"
    target_account_id: "ACCOUNT_ID" # account id
```

5. Create `users.yaml` or `users.yml`:

```yaml
# users
users:
  - display_name: "Display Name"
    user_name: "test.admin"
    name:
      family_name: "Display"
      given_name: "Name"
    emails:
      - primary: true
        type: "AnyType"
        value: "example1@example.com"
  - display_name: "Display Name"
    user_name: "test.admin"
    name:
      family_name: "Display"
      given_name: "Name"
    emails:
      - primary: true
        type: "AnyType"
        value: "example1@example.com"
  - display_name: "Display Name"
    user_name: "teamA.user1"
    name:
      family_name: "Display"
      given_name: "Name"
    emails:
      - primary: true
        type: "AnyType"
        value: "example2@example.com"
  - display_name: "Display Name"
    user_name: "teamA.user2"
    name:
      family_name: "Display"
      given_name: "Name"
    emails:
      - primary: true
        type: "AnyType"
        value: "example3@example.com"
  - display_name: "Display Name"
    user_name: "teamB.user1"
    name:
      family_name: "Display"
      given_name: "Name"
    emails:
      - primary: true
        type: "AnyType"
        value: "example4@example.com"
```
