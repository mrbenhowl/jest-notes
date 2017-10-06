# jest notes
things I keep forgetting how to do in Jest (with React, Redux-Saga etc)

### Spying on method imported from module and not calling through, i.e. calling mock
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

### Spying on method imported from module and calling through
```javascript
import * as module from 'path/module'

const spy = jest.spyOn(module, 'method')
// call method under test here and do assertions
// retore the original implementation of the method spied on.
spy.mockRestore()
```

### Testing the catch block in Redux-Saga
```javascript
export function * generatorName () {
  try {
    yield call(doSomethingPositive)
    yield call(whatIsYourFavColour)       
  } catch (error) {
    yield put(errorActionCreator)
    throw error
  }
}

test('catch block for generator/saga', () => {
  const mockError = {
    message: 'boom!'
  }

  const generatorName = sagaFileContainingGeneratorAbove.generatorName()
  try {
    expect(generatorName.next().value).toEqual(call(doSomethingPositive))
    expect(generatorName.throw(mockError).value).toEqual(put(errorActionCreator))
  } catch (error) {
    expect(error).toEqual(mockError)
  }
  
  // expect(generatorName.next().done).toEqual(true) - only needed if we didn't throw error in the generator
})
```
