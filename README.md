# Scanner Detection Rules - Notion

This repository contains Scanner detection rules for Notion audit log / SIEM
events (https://developers.notion.com/compliance/siem-events).

### Examples

Here are a few examples of the detections that are included in this repository:
- Member Role Escalated
- Page Shared to Web or Public
- Integration or External Account Connected
- SAML/SSO Configuration Changed

### Event Sinks

When these detection rules are triggered, alerts are sent to the [event
sinks](https://docs.scanner.dev/scanner/using-scanner/detection-rules/event-sinks)
you have configured in Scanner. Depending on the alert's severity level, it
will be sent to one of these event sink keys:
- `informational_severity_alerts`
- `low_severity_alerts`
- `medium_severity_alerts`
- `high_severity_alerts`
- `critical_severity_alerts`
- `fatal_severity_alerts`

### Before deploying: two open items

1. **Source type.** Every rule filters on `@scnr.source_type:notion` as a
   placeholder. Confirm the actual source type string assigned to your Notion
   ingestion and update the rules if it differs.

2. **Validated vs. doc-only rules.** Rules fall into two tiers:
   - **Validated** - the matched events and fields were observed in real
     Notion audit-log samples.
   - **Doc-only** - derived from Notion's published SIEM event catalog but not
     observed in available samples (noted in each rule's description). These
     match on event type names, which are reliable, but their event type
     strings and any payload fields should be validated against ingested JSONL.
     Some (SAML/SSO, EKM, HIPAA) are only emitted on Enterprise-tier
     workspaces.

   Notion emits raw activity events only - no risk scores, anomaly verdicts,
   device-trust checks, or failed-login records - so brute-force,
   behavioral-anomaly, and device-based detections are intentionally absent.

### Deployment

To deploy these rules into your Scanner instance, you can follow the
instructions in the [Scanner documentation](https://docs.scanner.dev) under
**Detection Rules as Code**.
