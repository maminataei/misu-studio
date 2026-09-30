# Commerce Studio

Commerce Studio is a self-hosted control plane for authoring, validating, versioning, previewing, and publishing semantic commerce template maps. Host platforms provide renderer implementations that interpret those maps and combine them with authoritative commerce data and actions.

This repository is the authoritative home of the product, architecture, protocol, security, operations, integration, and delivery specifications for Commerce Studio.

## Status

The project is in specification and foundation development. The documents in
[docs](./docs/README.md) are the source of truth for implementation. No
production API or package is stable until the beta exit gate is satisfied.

## Principles

- Studio authors semantic maps; it does not generate or execute storefront code.
- Commerce platforms own operational truth and renderer implementations.
- Published maps are immutable, signed, portable, and independently renderable.
- Manual editing is complete without AI.
- Security, accessibility, and required commerce tasks are publication invariants.

## Documentation

- [Product specification](./docs/product/README.md)
- [Architecture](./docs/architecture/README.md)
- [Protocols and schemas](./docs/specifications/README.md)
- [Security](./docs/security/README.md)
- [Operations](./docs/operations/README.md)
- [Integrations](./docs/integrations/README.md)
- [Delivery plan](./docs/delivery/README.md)
- [Architecture decisions](./docs/adr/README.md)

Read [CONTRIBUTING.md](./CONTRIBUTING.md) before proposing a change.

## License

Commerce Studio is licensed under the [Apache License 2.0](./LICENSE).
