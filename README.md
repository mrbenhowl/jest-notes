# jest-notes
things I keep forgetting how to do in Jest

### SPYING ON METHOD IMPORTED FROM MODULE AND NOT CALLING THROUGH, I.E. CALLING MOCK
```javascript
import * as module from 'path/module'

const spy = jest.spyOn(module, 'method')
        .mockImplementation(() => {
          return 'whatever you want to return'
        })

// call method under test here and do assertions
// retore the original implementation of the method spied on.
spy.mockRestore()
```

### SPYING ON METHOD IMPORTED FROM MODULE AND CALLING THROUGH
```javascript
import * as module from 'path/module'

const spy = jest.spyOn(module, 'method')
// call method under test here and do assertions
// retore the original implementation of the method spied on.
spy.mockRestore()
```

