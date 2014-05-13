## Acceptance tests

This is the scoring system for plugins. There may be exceptions in certain edge cases, but this should provide enough feedback to keep people on the right track.

### Dependencies

| Package | Reason | Recommended Solution |
|---|---|---|
| gulp | Creates incompatible plugins | Don't do this. Use vinyl for your tests. |
| colors | Extends global prototypes | Use chalk |
| through | Old streams | Use through2 |
| event-stream | Old streams + bloated kitchen sink | Use through2 or other streams2 pattern libraries |

### Handling file.contents

| Behavior | Recommended Solution |
|---|---|
| file with null contents not passed through | Pass them through immediately |
| file with null contents was mutated | Pass them through immediately - do not modify them |
| file output contents type different than input | Put out the same type you put in |
| file with streaming contents not handled correctly | Emit an error or support it |

### Static analysis

| Behavior | Recommended Solution |
|---|---|
| console.log | Use gulp-util .log |
| require('fs') | Plugins should not read/write - gulp handles that |
| index.js > 100 lines | Break it up into multiple modules/files |
| High code complexity | Break it up into multiple modules/files |

### Other

| Behavior | Recommended Solution |
|---|---|
| Tests failing | Fix your tests |
| No tests | Write tests |
| No source link | [package.json link](https://www.npmjs.org/doc/json.html#repository) to github |

### Manual

Plugins will be manually checked and deductions will result from the following items.

* Can be done with existing node modules (doesn't need to be a plugin)
* Doing multiple things in a plugin
* Excess configuration
* Duplication of functionality already existing in another plugin
* Aggregating multiple `gulpplugins`
* Poorly documented
