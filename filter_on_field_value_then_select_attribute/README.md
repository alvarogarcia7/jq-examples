2024-08-20 02:00:07 AGB

```sql
SELECT .id
WHERE .parent_id = 10
from data.json
```

```jq
jq '.[] | select(.parent_id == 10) | .id' data.json
```

See `Makefile` for the updated version

