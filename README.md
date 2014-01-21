## Acceptance tests

This is the scoring system for plugins.

### Dependencies

| Package | Exceptions | Deductions | Reason | Recommended Solution |
|---|---|---|---|---|
| gulp | None | 10 | Creates incompatible plugins. | Don't do this. Use vinyl for your tests. |
| colors | None | 5 | Extends global prototypes | Use chalk |
| through | None | 1 | Old streams | Use through2 |
| event-stream | devDependency | 1 | Old streams | Use through2 |

### Handling file.contents

| Behavior | Deductions | Recommended Solution |
|---|---|---|
| file with null contents not passed through | 1 | Pass them through immediately |
| file with null contents was mutated | 1 | Pass them through immediately - do not modify them |
| file output contents type different than input | 10 | Put out the same type you put in |

### Logging

| Behavior | Deductions | Recommended Solution |
|---|---|---|
| console.log in source code | 5 | Use gulp-util .log |
