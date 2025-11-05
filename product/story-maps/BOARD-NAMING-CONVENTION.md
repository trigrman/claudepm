# Miro Board Naming Convention

## Format

```
Story Map - YYYY-MM-DD - [Name]
```

**Examples**:
- `Story Map - 2025-11-04 - Iteration-1`
- `Story Map - 2025-11-04 - Dark-Mode`
- `Story Map - 2025-11-15 - Payment-Flow`

**Components**:
- `Story Map` - Prefix for all story map boards
- `YYYY-MM-DD` - Date created (enables chronological sorting)
- `Name` - Initiative or epic name (matches cycle/epic naming)

---

## Board Creation

**⚠️ Important**: Miro does not support board creation via API/MCP. You must create boards manually.

### When Creating a Story Map

1. Go to https://miro.com
2. Click "Create new board"
3. Name it: `Story Map - YYYY-MM-DD - [Name]`
4. Copy the board ID from the URL

**Board ID location**:
```
https://miro.com/app/board/uXjVJwAPJ3U=/
                              ^^^^^^^^^^^^
                              Board ID
```

---

## Lifecycle Management

### Active Boards
- Keep boards for current/recent initiatives
- Update as stories evolve
- Use for planning and grooming

### Archiving
**When to archive**:
- Initiative is complete and deployed
- Stories are no longer changing
- 3+ months since last update

**How to archive**:
1. Prefix board name with `[ARCHIVED]`
2. Move to archived folder in Miro
3. Keep markdown files as source of truth

**Example**: `[ARCHIVED] Story Map - 2025-11-04 - Iteration-1`

---

## Notes

- **Board IDs are permanent** - Don't change when you rename the board
- **Miro API limitations** - Cannot create, delete, or rename boards via API
- **Source of truth** - Markdown files are authoritative, Miro is visualization
