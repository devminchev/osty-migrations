# OpenSearch Migrations

A collection of our AWS OpenSearch migrations, that are made by the [osty-rs cli](https://gitlab.ballys.tech/excite/native/applications/osty-rs)
Repository containing OpenSearch migrations for creating and managing indexes.

## Validation and Linting

This repository uses pre-commit hooks to ensure all migrations are valid and correctly formatted:

### Installation

1. Install pre-commit:
   ```bash
   pip install pre-commit
   ```

2. Install the hooks:
   ```bash
   pre-commit install
   ```

### Validation Checks

The following checks are performed on all migration files:

1. **Basic JSON validation**: Ensures all JSON is syntactically valid
2. **JSON formatting**: Consistent indentation and formatting
3. **JSON Schema validation**: Validates the structure of migration files
4. **Custom validation**: Additional checks for:
   - Consistent migration IDs
   - Filename matches migration ID
   - Index name conventions
   - Properly configured aliases
   - And more...

### Running Manually

```bash
pre-commit run --all-files
```

## Migration File Format

Each migration file should:
1. Be named with pattern: `<timestamp>-<description>.json`
2. Contain an array of operations with consistent IDs
3. Follow the schema defined in `opensearch-migration-schema.json`

Example migration entry:
```json
{
    "id": 1736523818,
    "command": "apply",
    "method": "put",
    "path": "/my-index",
    "query": {
        "settings": {
            "index": {
                "number_of_shards": 1,
                "number_of_replicas": 2
            }
        },
        "aliases": {
            "my-index-r": {},
            "my-index-w": {
                "is_write_index": true
            }
        }
    }
}
```
