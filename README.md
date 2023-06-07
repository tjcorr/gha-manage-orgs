# gha-manage-orgs

A series of composite actions to simplifiy the management of GitHub Enterprise Organizations.

## create-org

Creates a new GitHub Enterprise Organization.

### Inputs

#### `admin-pat`

**Required** A personal access token with `[admin:enterprise,user:email,read:user]` scopes.

#### `enterprise`

**Required** The slug of the enterprise to create the organization in.

#### `org`

**Required** The name of the organization to create (this must be globally unique).

#### `admin`

**Required** The login of the admin user for the organization.

## Example usage

```
- name: Create temporary organization
  uses: tjcorr/gha-manage-orgs/create-org@main
  with:
    admin-pat: ${{ secrets.ADMIN_PAT }}
    enterprise: "myenterprise"
    org: "myuniqueorg"
    admin: ${{ github.actor }}
```

## delete-org

Deletes an existing GitHub Enterprise Organization along with all contents.

>**Warning**
>:warning: All resources within the organization will be PERMANENTLY DELETED and are not recoverable. :warning:

### Inputs

#### `admin-pat`

**Required** A personal access token with `admin:org` scope.

#### `org`

**Required** The name of the organization to delete.

## Example usage

```
- name: Delete temporary organization
  uses: tjcorr/gha-manage-orgs/delete-org@main
  with:
    admin-pat: ${{ secrets.ADMIN_PAT }}
    org: "myuniqueorg"
```
