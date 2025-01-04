# **Lodash**
- For composing and Piping
```javascript
// fp below stands for funcitonal programming
import {compose,pipe} from "lodash/fp"

const trim = str => str.trim()
const toLowerCase = str => str.toLowerCase()

// the following 2 are the same
const transform = compose(toLowerCase,trim)
const transfom = pipe(trim,toLowerCase)
transform(input)
// apply trim(input), then take the result and apply toLowerCase()
```