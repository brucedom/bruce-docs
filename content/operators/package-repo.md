---
title: "PackageRepo Operator"
weight: 7
---
The PackageRepo operator is used to set up a package repository for supported package managers such as `apt`, `dnf`, or `yum`.

## Syntax

```yaml
repoName: <REPO_NAME>
repoLocation: <REPO_LOCATION>
repoType: <REPO_TYPE>
repoKey: <REPO_KEY>
osLimits: <OS_LIMITS>
onlyIf: <sub-command> #(Requires version 1.2.6 or higher)
notIf: <sub-command> #(Requires version 1.2.6 or higher)
```

* `repoName`: The name of the repository.
* `repoLocation`: The URL of the repository.
* `repoType`: The type of package manager used for the repository (apt, dnf, or yum).
* `repoKey`: The URL of the GPG key used to sign the repository packages.
* `osLimits`: A list of operating systems that the operator should run on.
* `onlyIf`: This sub command will run and if an output is received it will return true and thus allow execution
* `notIf`: This sub command will run and if an output is received it will return false and thus prevent execution

## Example:

```yaml
- repoName: docker
  repoLocation: https://download.docker.com/linux/ubuntu
  repoType: apt
  repoKey: https://download.docker.com/linux/ubuntu/gpg
  osLimits: ubuntu|debian
```

In this example, the PackageRepo operator sets up the Docker repository for Ubuntu and Debian systems using the apt package manager. The GPG key used to sign the packages is also specified.

## Example 2:

```yaml
- repoName: docker
  repoLocation: https://download.docker.com/linux/ubuntu
  repoType: apt
  repoKey: https://download.docker.com/linux/ubuntu/gpg
  osLimits: ubuntu
  onlyIf: which docker
```

In this example, the PackageRepo operator sets up the Docker repository for Ubuntu systems using the apt package manager. But does so only if the `docker` command is installed.

## Example 3:

```yaml
- repoName: docker
  repoLocation: https://download.docker.com/linux/ubuntu
  repoType: apt
  repoKey: https://download.docker.com/linux/ubuntu/gpg
  osLimits: ubuntu
  notIf: which docker
```

In this example, the PackageRepo operator sets up the Docker repository for Ubuntu systems using the apt package manager. But does so only if the `docker` command is not installed.

In the next section, we'll discuss the Packages operator and how to use it in your manifest files.