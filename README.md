# react-number-format
React component to format number in an input or as a text

### Features
1. Allow prefix, suffix and thousand seperator. 
2. Allow format pattern.
3. Allow masking.
4. Allow custom formatting handler.
5. Allow formatting a input or a simple text

### Install
Through npm 
`npm install react-number-format --save`

Or get compiled development and production version from ./dist

### Props
| Props        | Options           | Default  | Description |
| ------------- |-------------| -----| -------- |
| thousandSeperator | Boolean: true/false | false | Add thousand seperators on number |
| prefix      | String (ex : $)     |   none | Add a prefix before the number |
| suffix | String (ex : /-)      |    none | Add a prefix after the number |
| value | Number | null | Give initial value to number format |
| displayType | String: text / input | input | If input it renders a input element where formatting happens as you input characters. If text it renders it as a normal text in a span formatting the given value |
| format | String : Hash based ex (#### #### #### ####) <br/> Or Function| none | If format given as hash string allow number input inplace of hash. If format given as function, component calls the function with unformatted number and expects formatted number.
| mask | String (ex : _) | none | If mask defined, component will show non entered placed with masked value.  

### Examples
#### Prefix and thousand seperator : Format currency as text
```jsx
var NumberFormat = require('react-number-format');

<NumberFormat value={2456981} displayType={'text'} thousandSeperator={true} prefix={'$'} />
```
Output : $2,456,981

#### Format with pattern : Format credit card as text
```jsx
<NumberFormat value={4111111111111111} displayType={'text'} format="#### #### #### ####" />
```
Output : 4111 1111 1111 1111

#### Prefix and thousand seperator : Format currency in input
```jsx
<NumberFormat thousandSeperator={true} prefix={'$'} />
```
![Screencast example](https://i.imgur.com/d0P2Db1.gifv)

#### Format with pattern : Format credit card in an input
```jsx
<NumberFormat format="#### #### #### ####" />
```
![Screencast example](https://i.imgur.com/KEiYp4o.gifv)

#### Format with mask : Format credit card in an input
```jsx
<NumberFormat format="#### #### #### ####" mask="_"/>
```
![Screencast example](https://i.imgur.com/qvmydpH.gifv)

#### Custom format method  : Format credit card expiry time
```jsx
  function formatExpiryChange(val){
    if(val && Number(val[0]) > 1){
      val = '0'+val;
    }
    if(val && val.length >1 && Number(val[0]+val[1]) > 12){
      val = '12'+val.substring(2,val.length);
    }
    val = val.substring(0,2)+ (val.length > 2 ? '/'+val.substring(2,4) : '');
    return val;
  }

<NumberFormat format={formatExpiryChange}/>
```
![Screencast example](https://i.imgur.com/9wwdyFF.gifv)

### Development
- Download the zip
- `npm install`
- `npm start` to run example server
- `npm run test` to test changes
- `npm run bundle` to bundle files

#### Testing
Test cases are written in jasmine and run by karma
Test file : /test/test_input.js
To run test : `npm run test`