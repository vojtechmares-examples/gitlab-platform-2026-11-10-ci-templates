# ci-templates

Shared pipeline snippets for the projects of the `examples` group.

- `rocky.yml`
  - `.rocky-dnf` pins Rocky's repositories to `dl.rockylinux.org` and sets dnf timeouts (the mirrorlist can pick a mirror that serves a few kB/s)
  - `.ssh-setup` prepares `~/.ssh` for the deploy server (`ssh deploy`, `rsync -e ssh deploy:...`)
