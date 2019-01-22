# GitHub Action for Zeit

This Action wraps the [Now CLI](https://github.com/zeit/now-cli) to enable common Now commands.

## Usage

```workflow
workflow "Deploy on Now" {
  on = "push"
  resolves = ["alias"]
}

action "deploy" {
  uses = "actions/zeit-now@master"
  args = "--public --no-clipboard deploy ./site > $HOME/deploy.txt"
  secrets = [
    "ZEIT_TOKEN",
  ]
}

action "alias" {
  needs = ["deploy"]
  uses = "actions/zeit-now@master"
  args = "alias `cat /github/home/deploy.txt`"
  secrets = [
    "ZEIT_TOKEN",
  ]
}
```

For more examples, visit: [actions/example-zeit-now](https://github.com/actions/example-zeit-now).

### Secrets

* `ZEIT_TOKEN` - **Required**. The token to use for authentication with the Zeit Now API ([more info](https://zeit.co/blog/introducing-api-tokens-management))

## License

The Dockerfile and associated scripts and documentation in this project are released under the [MIT License](LICENSE).

Container images built with this project include third party materials. See [THIRD_PARTY_NOTICE.md](THIRD_PARTY_NOTICE.md) for details.
