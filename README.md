# gcp-ssh

Interactive GCP instance picker for `gcloud compute ssh`.

Lists all your compute instances with name, zone, IP, status, and project, lets you fuzzy-search with `fzf`, then SSHes in. Before connecting it prints the full `gcloud compute ssh` command so you can copy it for direct reuse.

## Requirements

- [`gcloud`](https://cloud.google.com/sdk/docs/install) (authenticated)
- [`fzf`](https://github.com/junegunn/fzf)

## Install

```bash
# clone
git clone https://github.com/jhlubek/gcp-ssh.git ~/tools/gcp-ssh

# symlink to somewhere on $PATH
ln -s ~/tools/gcp-ssh/gcp-ssh ~/.local/bin/gcp-ssh
```

Or just copy `gcp-ssh` to any directory in your `$PATH`.

## Usage

```
gcp-ssh [--project=PROJECT] [--no-iap] [-- <extra gcloud ssh args>]
```

IAP tunneling (`--tunnel-through-iap`) is used by default. Pass `--no-iap` to disable it.

### Basic

```bash
gcp-ssh
```

Opens fzf with all instances from your active `gcloud` project. Select one and press Enter.

### Specific project

```bash
gcp-ssh --project=my-gcp-project
```

### Port forwarding

```bash
gcp-ssh -- -L 8080:localhost:8080
```

Extra args after `--` are passed straight to `gcloud compute ssh`.

## Example output

```
=> gcloud compute ssh my-instance --zone=europe-west1-b --project=my-gcp-project
Warning: Permanently added 'compute.12345' (ECDSA) to the list of known hosts.
me@my-instance:~$
```

Copy the printed command to skip the picker next time.
