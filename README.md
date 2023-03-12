# JSFunctionScope
JavaScript function scope arrow vs regular function in object.
 
 
 ```JS
 
    /*
      Function scope:
      REGULAR FUNCTION:
        Can only accept properties using "this" keyword [ within inside ] the object itself!
        for instance like object and propery named < yearsExperience: 6 > below.
      ARROW FUNCTION: 
        Only arrow function CAN inject data from GLOBAL VARIABLE using "this" keyword 
        "this" keywork in arrow function is only recognize 
        the GLOBAL VARIABLE OR GLOBAL SCOPE using 
        "var followed by varName equal variable "value" 
        ex. var otherExpertise = 7;

    */

    var otherExpertise = 7; // GLOBAL SCOPE

    const Developer = {
      
        yearsExperience : 6,
        otherExpertise : 2, // within the scope
        getExp : function() {
          let yE = this.yearsExperience; 
          if( yE > 1 ) {
            return ("Congratulation You are qualify : " + yE );
          }
        },
        getOtherExpertise: () => {
          let op = this.otherExpertise; // from GLOBAL SCOPE !
          return ("Plus your Other expertise : " + op );
        } 
    }

    console.log("Hey! " + Developer.getExp() ); // Read from local scope

    // If we base on "within scope" the < otherExpertise : 2 > value is 2
    // but the GLOBAL SCOPE it is 7
    // It rendered the GLOBAL SCOPE NOT the local scope base on object itself! 
    // That is how arrow function works in objectData or OOP approach!
    console.log("Hey! " + Developer.getOtherExpertise() ); // Read from GLOBAL VARIABLE
```

```JS
  // Result 
  Hey! Congratulation You are qualify : 6
  JS1.html:49 Hey! Plus your Other expertise : 7
```

  <br />Checking GLobal SCOPE
  <br />console.log(window);
    
```JS
  // result 
  otherExpertise : 7
```
     
  <br />Checking Object SCOPE
  <br />console.log(Developer);
    
```JS
  // result 
  otherExpertise : 2
```
