---
paths:
  - "app/jobs/**/*.rb"
  - "spec/jobs/**/*.rb"
---

# Background Job Conventions

- Use Solid Queue (database-backed, Rails 8 default)
- Jobs must be idempotent -- safe to retry
- Pass IDs, not full objects (serialization safety)
- Use `discard_on ActiveRecord::RecordNotFound` for deleted records
- Use `retry_on` with specific exceptions and limits
- Keep jobs focused: one job, one responsibility
- Pair sync methods with a `_later` variant that enqueues the job, and have the job call back into the sync method (e.g. `Deal#publish` / `Deal#publish_later` -> `PublishDealJob#perform` calls `deal.publish`)
- `Current` (e.g. `Current.user`) is only auto-populated in web requests -- jobs must set it explicitly at the start of `perform` if the business logic depends on it
- Test with `have_enqueued_job` matcher
