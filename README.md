# gha-manage-orgs

A series of composite actions to simplifiy the management of GitHub Enterprise Organizations.

## add-users

Adds users to an existing GitHub organization.

### Inputs

#### `admin-pat`

**Required** A personal access token with `[admin:org]` scope.

#### `org`

**Required** The name of the organization to invite users to.

#### `users`

**Required** A comma separated list of github handles who should be made admins of the organization (e.g. `tjcorr` or `tjcorr,otherhandle`).

#### `team-names`

A comma separated list of team slugs to invite the user to (e.g. `myteam` or `myteam,otheteam`).

## Example usage

```
- name: Invite users
  uses: tjcorr/gha-manage-orgs/add-users@main
  with:
    admin-pat: ${{ secrets.ADMIN_PAT }}
    org: "myuniqueorg"
    users: "tjcorr,otherhandle"
```


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

**Required** A comma separated list of github handles who should be made admins of the organization (e.g. `tjcorr` or `tjcorr,otherhandle`).

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

## create-team

Create a team in a GitHub organization.

### Inputs

#### `admin-pat`

**Required** A personal access token with `[admin:org]` scope.

#### `org`

**Required** The name of the organization to invite users to.

#### `team-name`

**Required** The name of the team to create.

## Example usage

```
- name: Create team
  uses: tjcorr/gha-manage-orgs/create-team@main
  with:
    admin-pat: ${{ secrets.ADMIN_PAT }}
    org: "myuniqueorg"
    team-name: "MyTeam"
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
