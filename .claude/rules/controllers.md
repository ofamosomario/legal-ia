---
paths:
  - "app/controllers/**/*.rb"
  - "spec/requests/**/*.rb"
---

# Controller Conventions

- Keep controllers thin: orchestrate, don't implement business logic
- Delegate to service objects for anything beyond simple CRUD
- Always `authorize` with Pundit on every action
- Use `policy_scope(Model)` for index queries (multi-tenant isolation)
- Use strong parameters (`params.require(:x).permit(...)`)
- Use presenters (`app/presenters/`) for view formatting, not controllers
- Follow REST conventions: index, show, new, create, edit, update, destroy
- Prefer `respond_to` with `format.html` and `format.turbo_stream` for Hotwire
- Test with request specs in `spec/requests/`, not controller specs
- Always test: authentication, authorization (404 for unauthorized), valid/invalid params
- For nested resources, extract shared setup into a concern (e.g. `DealScoped`) applied via `before_action`, instead of repeating the same lookup in every controller
- Trigger Turbo Stream broadcasts explicitly from the controller action, not from a model callback -- keeps side effects visible at the call site
