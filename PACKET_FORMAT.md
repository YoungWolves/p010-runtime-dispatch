# EFFECTOR_EXECUTION_PACKET format

A dispatch packet is an execution instruction produced by the P010 controller. It is not, by itself, proof of authority.

Required fields for mutation-capable work:

```text
PACKET_TYPE=EFFECTOR_EXECUTION_PACKET
PACKET_VERSION=1
PACKET_ID=<unique packet id>
CREATED_AT=<timestamp>
CONTROLLER=P010
DESIGN_AUTHORITY=P001
TARGET_PROJECT=<project>
TARGET_WORKSTREAM=<workstream>
TARGET_SURFACE=<exact browser-visible URL>
OPERATION=<bounded operation>
AUTHORIZATION=<authorization id>
DELEGATION=<delegation id/version>
IDEMPOTENCY_KEY=<idempotency key>
AUTHORIZATION_STATUS_AT_ISSUE=<controller-observed state>
AUTHORIZATION_EXPIRY=<timestamp/condition>
GRANT_STATE_AT_ISSUE=<controller-observed state>
DURABLE_EXECUTION_STATE=<state>
SURFACE_STATE=<state>
NO_CONFLICTING_DURABLE_WRITER=<true/false>
PRECONDITION_EVIDENCE=<bounded revision/state evidence>
PERMITTED_ACTIONS=<explicit list>
FORBIDDEN_SCOPE=<explicit list>
REQUIRED_POSTCONDITIONS=<explicit list>
FAIL_CLOSED=true
```

The Work effector must treat controller observations as bounded execution evidence, not as permission to broaden scope. The target-owned lifecycle path must independently validate the packet before authoritative mutation.

For dispatch-channel tests, use `OPERATION=DISPATCH_TEST_NO_TARGET_MUTATION` and omit target authorization fields that are irrelevant to a no-op test. The effector must perform no target mutation and only report that the trigger and packet were received.
