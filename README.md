# flat-transform

### A small library tranforming your flat objects into rich ones using declarative rules.

## Installation

```javascript
npm install flat-transform
```

## Use cases
Relational databases usually return flat row objects. The goal of an arbitrary API is to present data in a structured form.

This library's goal is to transform this flat relation into a structured object simply by declaring the output structure with matching property names of the original relation.

## API
### transform(rules, original, preserve_original = false)
Transforms original object into the new one, which is defined by rules. Optionaly it can ommit original fields in the new object by setting `preserve_original` parameter.


## Example

```javascript
var flat = require("flat-transform")

var obj = {
  message: "Hello",
  username: "John Doe",
  user_id: 1,
  phone_country_code: "+420",
  phone_number: "123 456 789"
}

var rules = {
  user: {
    id: "user_id",
    username: "username",
    phone: {
      country_code: "phone_country_code",
      number: { stringified: "phone_number" }
    }
  },
  phone1: "phone_number",
  phone2: "phone_number",
  phone3: "phone_number",
  phone4: "phone_number"
}

var transformed = flat.transform(rules, obj)

/*
{
  user: { 
    id: 1,
    username: "John Doe",
    phone: { 
      country_code: "+420" 
      number: { stringified: "123 456 789" }
    }
  },
  phone1: "123 456 789",
  phone2: "123 456 789",
  phone3: "123 456 789",
  phone4: "123 456 789",
  message: "Hello"
}
*/
```

## License

MIT