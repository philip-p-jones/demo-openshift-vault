# demo-openshift-vault

Vault on OpenShift: auto-initialised, auto-unsealed, and ready for use as a simple declarative example. Probably not for production.

## Description

This repository includes a kustomization to deploy a demo of [Hashicorp Vault](https://www.vaultproject.io/), auto-initialised, auto-unsealed, and ready for use as a simple declarative example. While this example is tuned for deployment on [OpenShift 4](https://www.redhat.com/en/technologies/cloud-computing/openshift), modification to apply on other types of kubernetes should hopefully be a fairly trivial task.

Inspired by an end-to-end example presented by the Red Hat Communities of Practice team for [vault-config-operator](https://github.com/redhat-cop/vault-config-operator), this demo simplifies the end-to-end example somewhat for demo purposes, and modifies the deployment to suit security context constraints provided in OpenShift 4.

The demo deployment adds [vault-plugin-secrets-github plugin](https://github.com/martinbaillie/vault-plugin-secrets-github) to Vault, allowing the creation of ephemeral, finely-scoped GitHub access tokens (as demoed at HashiCorp’s [HashiTalks Australia/New Zealand 2021](https://youtu.be/JuzBolDyGdg?t=17320)).

Values for the Vault Helm Chart are delivered inline in kustomization.yaml, requiring `--enable-helm` to be passed when building with Kustomize.

Note that auto-unsealing in this manner might be fine for a simple demo. However, in production, this may be less than ideal. External key services such as [AWS KMS](https://developer.hashicorp.com/vault/tutorials/auto-unseal/autounseal-aws-kms) or equivalent services from other hyperscalers may provide operationalisable alternatives.

## Usage

To inspect the kubernetes resources built by the kustomization (assuming `kustomize` and `helm` are installed):

```shell
$ kustomize build --enable-helm .
```

To dry-run the deployment of these resources to a kubernetes cluster (assuming `kubectl` is configured):

```shell
$ kustomize build --enable-helm . | kubectl apply -f- --dry-run=client
```

(Remove `--dry-run=client` if you wish to apply to the kubernetes cluster for real.)

## Roadmap

At this stage, it's just a simple example (see #support).

## Contributing

If you wish to make a change, we'd certainly be grateful for any suggestions and contributions. Feel free to do so in the usual way with [fork-pull](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request-from-a-fork).

## Support

This demo may still need some work, but no long tail of support was invisaged here. Done for love, not money.
![Han Solo saying "It's not my fault" in a gif](https://media.tenor.com/Fi_oI34mE8MAAAAC/hansolo-notmyfault.gif).

## Further Reading

  - https://catalog.redhat.com/software/container-stacks/detail/61954b7020da7eae27db0e2a
  - https://github.com/hashicorp/vault
  - https://github.com/redhat-cop/vault-config-operator
  - https://github.com/martinbaillie/vault-plugin-secrets-github

## Attribution

This example vault deployment adapts exerpts from [vault-config-operator](https://github.com/redhat-cop/vault-config-operator)'s end-to-end example, included under the provisions of [The Apache 2.0 license](https://github.com/redhat-cop/vault-config-operator/blob/main/LICENSE).

## License

This work is licensed under The MIT License.

`SPDX-License-Identifier: MIT`
