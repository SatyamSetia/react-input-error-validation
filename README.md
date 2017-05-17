# react-input-error-validation


[![Greenkeeper badge](https://badges.greenkeeper.io/harshmaur/react-input-error-validation.svg)](https://greenkeeper.io/)


A basic input validation HOC to provide error validations around the input. No need for the complete form validation. You can pass in number of validators and do error handling every input wise. 


## Usage

```jsx
import React, { Component } from 'react'
import withValidations from 'react-input-error-validation'

// Create any input field. All props are required
const TextField = props => (
  <div>
    <input {...props} />
    {error && <div>{error}</div>}
  </div>
)

// Applying HOC
const ValidatedTextField = withValidations(TextField)





/*
Validations - 
It will take in the value prop from the input field as well and and `config` prop if passed. 
The config prop can be used to do extra checking like in the case of fixDigits. 
*/
const notEmpty = val => {
  if (!val) {
    return 'Field Cannot Be Empty'
  }
  return
}

const onlyNumber = val => {
  const pattern = /^\d+$/
  if (!pattern.test(val)) {
    return 'Please Enter a Valid Number'
  }
  return
}


// You can use config object to check for any custom configurations. 
const fixDigits = (val, config = {}) => {
  if (val.length !== config.digits) {
    return `Content should be ${config.digits} only`
  }
  return
}


// Finally we render it out. 

class App extends Component {
  state = {
    first: '',
    second: '',
    third: ''
  }

  render() {
    return (
      <div>
        Must be filled :
        <ValidatedTextField
          value={this.state.first}
          onChange={first => this.setState({ first })}
          validations={[notEmpty]} // Pass array of functions in the validations prop
        />
        <br />
        Should be a number and filled:
        <ValidatedTextField
          value={this.state.second}
          onChange={second => this.setState({ second })}
          validations={[notEmpty, onlyNumber]}
        />
        <br />
        Number, 7 digits and filled:
        <ValidatedTextField
          value={this.state.third}
          onChange={third => this.setState({ third })}
          config={{ digits: 7 }} // this is how we pass in config. 
          validations={[notEmpty, onlyNumber, fixDigits]} // you can pass as many validators in squence
        />
        <br />
      </div>
    )
  }
}

export default App


```
