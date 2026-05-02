# monday.com GraphQL API Reference

The monday.com API is a GraphQL API. This document captures the high-level surface, endpoint, and authentication. The full schema is introspectable directly from the GraphQL endpoint and the canonical, version-aware documentation lives at the official developer reference.

## Endpoint

`https://api.monday.com/v2`

## Authentication

monday.com supports three authentication mechanisms:

- **API Token** - Personal API token from Admin or Member account, sent in the `Authorization` header.
- **OAuth 2.0** - For third-party apps that act on behalf of monday.com users.
- **Short-Lived Token** - For embedded app contexts and guest scenarios.

See: https://developer.monday.com/api-reference/docs/authentication

## Versioning

The monday.com API uses release-based versioning. Specify a version with the `API-Version` header. Without it, the request defaults to the current stable version.

## Core Object Types

The API exposes the following primary object types - each can be queried, and most can be mutated:

- `Board` - The core container; holds groups, items, columns, views.
- `Item` - A row within a board, holds column values, updates, subitems.
- `Group` - A logical grouping of items within a board.
- `Column` / `ColumnValue` - Schema and data for board columns.
- `Update` - Comments and activity on items.
- `User` / `Team` / `Account` - Identity and tenancy.
- `Workspace` - Top-level container of boards and folders.
- `Doc` / `DocBlock` - monday.com docs and their content blocks.
- `Webhook` - Push notifications for board events.
- `Tag` - Item tagging.
- `Notification` - User notifications.
- `App` / `AppSubscription` - Marketplace app management.

## Query Roots

Common top-level queries:

- `boards`, `items`, `items_page`, `items_by_column_values`
- `users`, `teams`, `me`, `account`
- `workspaces`, `folders`
- `docs`, `tags`, `webhooks`
- `app_subscription`, `app_subscription_operations`
- `complexity`, `version`, `versions`

## Mutation Roots

Common top-level mutations:

- `create_board`, `duplicate_board`, `archive_board`, `delete_board`
- `create_item`, `change_column_value`, `change_multiple_column_values`, `move_item_to_group`, `archive_item`, `delete_item`
- `create_group`, `delete_group`, `duplicate_group`
- `create_update`, `delete_update`, `like_update`
- `create_webhook`, `delete_webhook`
- `create_doc`, `create_doc_block`, `update_doc_block`

## Rate Limits and Complexity

monday.com applies a complexity budget to each query. Each query can return a `complexity` block reporting cost, remaining budget, and reset time. Heavy nested queries should use `items_page` cursor-based pagination.

## References

- API Reference: https://developer.monday.com/api-reference/
- Authentication: https://developer.monday.com/api-reference/docs/authentication
- API Playground: https://monday.com/developers/v2/try-it-yourself
- Developer Center: https://developer.monday.com/api-reference/docs/the-developer-center
