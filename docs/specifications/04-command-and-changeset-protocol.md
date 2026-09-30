# Command and Changeset Protocol

**Status:** Authoritative protocol  
**Audience:** Core, editor, API, AI, audit  
**Owner:** Command protocol area

## Command envelope

~~~ts
type DraftCommand = {
  commandId: string;
  idempotencyKey: string;
  draftId: string;
  expectedRevision: number;
  leaseToken: string;
  type: CommandType;
  payload: JsonValue;
  clientTime?: string;
};
~~~

Command types include section add, remove, move, duplicate, variant change,
content change, control change, binding change, action change, token change,
locale change, template application, policy adoption, and restore.

Generic JSON Patch is not accepted at the public boundary.

## Application

The pure engine verifies command schema, target identity, current structure,
contract semantics, and policy. It returns:

~~~ts
type CommandResult = {
  nextMap: TemplateMap;
  affectedPaths: SemanticPath[];
  inverse: InverseCommandData;
  summary: ChangeSummary;
  findings: ValidationFinding[];
  nextHash: string;
};
~~~

The API additionally authorizes the actor, verifies lease and expected
revision, claims idempotency, persists draft and changeset, increments revision,
and emits an event in one transaction.

## Conflict behavior

A stale revision never silently merges. The response includes authoritative
revision, hash, and safe refresh information. A client may replay only after it
rebuilds the command against synchronized state and obtains a current lease.

## Undo and restore

Undo creates a new command using recorded inverse data and current validation.
It may be rejected if later changes, policy, or contract make the inverse
invalid. Restore validates and migrates a historical map before replacing the
draft through one audited command.

## AI parity

Future AI proposes arrays of ordinary commands. The server applies all or none
against captured hashes and current authority. AI has no private mutation API.
