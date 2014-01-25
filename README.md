## Acceptance tests

This is the scoring system for plugins. There may be exceptions in certain edge cases, but this should provide enough feedback to keep people on the right track.

### Dependencies

| Package | Deductions | Reason | Recommended Solution |
|---|---|---|---|
| gulp | 10 | Creates incompatible plugins | Don't do this. Use vinyl for your tests. |
| colors | 5 | Extends global prototypes | Use chalk |
| through | 1 | Old streams | Use through2 |
| event-stream |  1 | Old streams + bloated kitchen sink | Use through2 or other streams2 pattern libraries |

### Handling file.contents

| Behavior | Deductions | Recommended Solution |
|---|---|---|
| file with null contents not passed through | 1 | Pass them through immediately |
| file with null contents was mutated | 1 | Pass them through immediately - do not modify them |
| file output contents type different than input | 10 | Put out the same type you put in |
| file with streaming contents not handled correctly | 10 | Throw an errror or support it |

### Static analysis

| Behavior | Deductions | Recommended Solution |
|---|---|---|
| console.log | 5 | Use gulp-util .log |
| require('fs') | 5 | Plugins should not read/write - gulp handles that |
| index.js > 100 lines | 5 | Break it up into multiple modules/files |
| High code complexity | 0 | Break it up into multiple modules/files |

### Other

| Behavior | Deductions | Recommended Solution |
|---|---|---|
| Tests failing | 1 | Fix your tests |
| No tests | 5 | Write tests |

### Manual

Plugins will be manually checked and deductions will result from the following items.

* Can be done with existing node modules (doesn't need to be a plugin)
* Doing multiple things in a plugin
* Excess configuration
* Duplication of functionality already existing in another plugin
* Aggregating multiple `gulpplugins`
