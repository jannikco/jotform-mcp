# Jotform MCP server

Find an authorized form and read a bounded page of its submitted responses.

A direct-provider MCP server with useful local execution. No PipMCP account is required for local use. Provider API access and any provider charges are your responsibility.

## Quick start

Requires Node.js22+. Clone this repository, then run:

```sh
npm ci --ignore-scripts
npm test
npm start
```

The default command inspects the tools offline. Configure your own credentials in your environment:

- `JOTFORM_API_KEY`



Credential help: https://api.jotform.com/docs/

## Provider setup

Use your own read-only Jotform API key. This manifest targets standard api.jotform.com, not EU/HIPAA endpoints. Submission data may contain sensitive personal information; no writes or exports are exposed.

## Supported scope

- Read-only form discovery and submission retrieval. Regional/HIPAA endpoints require a separately reviewed matching manifest.

## Execute a real read

Replace example record IDs with records you are authorized to access.

```sh
npm start -- --call jotform_list_forms '{"limit":10}'
```

## Use with an MCP client

Launch `node /absolute/path/jotform-mcp/server.mjs` using stdio transport; pass credentials through the client environment. Stdout is reserved for JSON-RPC.

## Tools

| Tool | Effect | Purpose |
| --- | --- | --- |
| jotform_list_forms | Read | List account forms using the APIKEY header. |
| jotform_list_submissions | Read | Read one page of submissions for a chosen form; results may contain personal information. |

## Concrete workflow

Find an authorized form and read a bounded page of its submitted responses.

1. jotform_list_forms
2. jotform_list_submissions

## Optional writes

Writes are disabled by default. Set CONNECTOR_ALLOW_WRITES=true and supply `_approval: {approved:true,idempotencyKey:"unique-request-id"}` on the specific call. Do not reuse a key for a different request. Uncertain outcomes are never automatically replayed; inspect the provider before another attempt.

## Capability evidence

Local: **Tested — HTTP fixtures and real stdio tools/call**. Managed: **Documented**. Provider authentication and live operations have not been established by these fixture tests. Evidence applies per operation and execution mode; setup discovery does not imply provider execution.

## Managed production

[Import with PipMCP](https://pipmcp.com/github/start?integration=openapi-to-mcp&utm_source=github&utm_campaign=github-jotform-mcp&utm_content=readme) when you want the hosted service. This provider is not currently listed as a managed template. Import selected-openapi.json (REST) or the official GraphQL schema linked in provenance, configure authentication, and review the tools before execution. Local credentials are not uploaded by this code. Review provider permissions in the managed onboarding. [Directory and related projects](https://jannikco.github.io/pipmcp-connectors/integrations/jotform/).

## Provenance and maintenance

- https://api.jotform.com/docs/

Maintainer:jannikco. MIT license for this code. See connector.json for selected operations and integration.json for evidence. Runtime dependencies retain their own licenses. Report sensitive issues through https://pipmcp.com/contact; do not post credentials or customer data in public issues.
