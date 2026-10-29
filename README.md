# SpaceApp issue #61: local Jaeger integration fixture evidence (2026-10-29)

This screenshot was captured from **Jaeger v2.22.0 running locally on macOS arm64**. The Jaeger binary was downloaded from the official release and verified against its published SHA-256 checksum.

The view contains **one connected W3C trace with 5 spans across two services**:
- a real Fastify HTTP SERVER span (`space-api`) from a disposable local `GET /__jaeger_local_demo` route;
- the Temporal test workflow `traceFixtureRoot` (`space-worker`);
- a child Temporal test workflow `traceFixtureChild`;
- one activity span within each workflow.

A local Vitest integration demonstration using `@temporalio/testing`, real project interceptors, and the shared OTLP exporter **PASSED (1/1)**. The Jaeger UI shows an 879 ms trace and the actual parent/child relationships. No Docker, paid services or external credentials were needed.

**Important limitation:** This is a *local integration fixture*, not a recording of a production SpaceApp chat turn or normal application route. It demonstrates that exported API/worker spans can be assembled in Jaeger, but it does **not** replace issue #61's requested manual screenshot of a real app turn. The production-route manual screenshot remains unverified.

The fixture test is intentionally uncommitted and outside the upstream PR. This evidence-only branch does not modify the tested PR code.

Related upstream PR: https://github.com/oll4com/spaceapp/pull/265
