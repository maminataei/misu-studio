# Marketplace Package Authoring

**Status:** Authoritative future contract  
**Audience:** Ecosystem publishers and registry implementers  
**Owner:** Marketplace area

## Package boundary

A marketplace renderer package contains host-installed implementation code,
declarative contract/module and renderer manifests, conformance adapters,
fixtures, documentation, license, SBOM, provenance, and signatures. Studio
imports only the declarative artifacts.

Templates may be distributed without renderer code when they target existing
contracts. Packages may use an approved open-source license or commercial
terms recorded by the registry.

## Publisher requirements

Publishers verify identity, control namespaces, protect release workflows, use
immutable versions, sign digests, declare permissions and external services,
publish vulnerability contact, and maintain compatible versions through the
declared support period.

## Registry validation

The registry verifies schema, namespace, dependency closure, conformance,
malware and vulnerability policy, SBOM, provenance, license, publisher
signature, and exact digest before countersigning. Rejected packages receive
stable reasons and are not discoverable.

## Installation

A host developer downloads and verifies the package, reviews permissions and
license, installs it in the renderer application, deploys it, runs target
certification, and registers the deployment with Studio. A Studio user cannot
install executable code with one click.

## Updates and advisories

Updates are explicit immutable releases. Registry metadata may recommend an
upgrade but cannot change a site's map or target. Security advisories identify
affected digests, mitigation, replacement, and revocation status.
