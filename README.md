# ci-templates

Shared pipeline snippets for the projects of the `examples` group.

- `rocky.yml`
  - `.rocky-dnf` pins Rocky's repositories to `dl.rockylinux.org` and sets dnf timeouts (the mirrorlist can pick a mirror that serves a few kB/s)
  - `.ssh-setup` prepares `~/.ssh` for the deploy server (`ssh deploy`, `rsync -e ssh deploy:...`)

## CI configuration

`.rocky-dnf` needs no variables. `.ssh-setup` reads the CI/CD variables below, which the group `examples` defines and every project in it inherits (*Settings > CI/CD > Variables* of the group):

| Variable | Type | Used for |
|----------|------|----------|
| `SSH_PRIVATE_KEY` | File, **protected** | Copied to `~/.ssh/id_deploy`; protected means only pipelines on protected branches and tags get it |
| `SSH_KNOWN_HOSTS` | Variable | Written to `~/.ssh/known_hosts` (`StrictHostKeyChecking yes`) |
| `DEPLOY_HOST`, `DEPLOY_SSH_PORT` | Variable | `HostName` and `Port` of the `deploy` host alias |
| `DEPLOY_USER` | Variable | `User` of the alias (`deploy`) |
| `SSH_USER` | optional, in the `variables:` of a job | Logs in as this account instead of `DEPLOY_USER`. It is a separate name because a `variables:` entry of `.gitlab-ci.yml` cannot override a group variable of the same name |

The job image needs `openssh-clients` (and `rsync` for uploads). Projects document the variables of their own in the section CI configuration of their README.
