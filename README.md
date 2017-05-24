Mirror Form
===========

Mirror Form adapts redux-form for usage inside Mirror.

Differences between Mirror Form & redux-form:

* Mirror Form requires no setup. `reducer` has been omitted
* The `reduxForm` decorator has been replaced by the `FormContext` component
* Every component exposes a `$state` stream & can be directly `dispatch`ed to
* State selectors & action creators omitted in favour of native Mirror APIs
* `FieldArray` & `Fields` omitted in favour of Mirror Collection
* Fields accept `asyncValidate`!

```js
import FormContext, {Field} from 'react-mirror-form'

const MyForm = Mirror({
  state(mirror) {
    return mirror.child('FORM').$state.map(([state = {}]) => state)
  }
})(({handleSubmit, pristine, reset, submitting}) => (
  <FormContext form="simple">
    <form onSubmit={handleSubmit}>
      <div>
        <label>First Name</label>
        <div>
          <Field
            name="firstName"
            component="input"
            type="text"
            placeholder="First Name"
          />
        </div>
      </div>
      <div>
        <label>Last Name</label>
        <div>
          <Field name="lastName" component="input" type="text" placeholder="Last Name" />
        </div>
      </div>
      <div>
        <label>Email</label>
        <div>
          <Field name="email" component="input" type="email" placeholder="Email" />
        </div>
      </div>
      <div>
        <label>Sex</label>
        <div>
          <label>
            <Field name="sex" component="input" type="radio" value="male" />
            {' '}
            Male
          </label>
          <label>
            <Field name="sex" component="input" type="radio" value="female" />
            {' '}
            Female
          </label>
        </div>
      </div>
      <div>
        <label>Favorite Color</label>
        <div>
          <Field name="favoriteColor" component="select">
            <option />
            <option value="ff0000">Red</option>
            <option value="00ff00">Green</option>
            <option value="0000ff">Blue</option>
          </Field>
        </div>
      </div>
      <div>
        <label htmlFor="employed">Employed</label>
        <div>
          <Field name="employed" id="employed" component="input" type="checkbox" />
        </div>
      </div>
      <div>
        <label>Notes</label>
        <div>
          <Field name="notes" component="textarea" />
        </div>
      </div>
      <div>
        <button type="submit" disabled={pristine || submitting}>Submit</button>
        <button type="button" disabled={pristine || submitting} onClick={reset}>
          Clear Values
        </button>
      </div>
    </form>
  </FormContext>
))
```
