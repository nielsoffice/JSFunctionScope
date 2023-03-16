# JS Object Function Scope
JavaScript function scope arrow vs regular function or function expression in object.
 
 
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
        otherExpertise : 2, // within the scope || local scope
        // function expression
        getExp : function() {
          let yE = this.yearsExperience; 
          if( yE > 1 ) {
            return ("Congratulation You are qualify : " + yE );
          }
        },
        // arrow function
        getOtherExpertise: () => {
          let op = this.otherExpertise; // from GLOBAL SCOPE !
          return ("Plus your Other expertise : " + op );
        } 
    }

    console.log("Hey! " + Developer.getExp() ); // Read from local scope

    // If we base on "within scope" the < otherExpertise : 2 > value is 2
    // but the GLOBAL SCOPE it is 7
    // It rendered the GLOBAL SCOPE NOT the local scope base on object itself! 
    // That is how arrow function works in objectData in JS !
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

 Parent SCOPE 

 ```JS
     
    // ARROW FUNCTION IN METHOD ALSO KNOW AS PARENT SCOPE 
    
    var otherExpertise = 7; // GLOBAL SCOPE

    const Developer = {
      
      yearsExperience : 6,
      otherExpertise : 2, // within the scope || local scope
      // function expression OR METHOD !
      getExp : function() {
         
        /* PARENT SCOPE : arrow function can also use to grab the local property it's parent or Developer Object,
           as it is use inside of METHOD, this way it have an access to it's parent PROPERTIES which is Developer Object.
           In addition arrow function can access the local scope properties of Object once it is INSIDE of Object METHOD instead of accessing the 
           GLOBAL PROPERTIES OR GLOBAL VARIABLE once arrow function is a METHOD. 
           
           PROPERTIES :
            yearsExperience : 6,
            otherExpertise : 2, */
            
          // arrow function inside of getExp method now can access local properties of Object Developer NOT GLOBAL SCOPE!
          const parentScope = () => {
            let oE = this.otherExpertise;
            return('This is Parent scope arrow function works' + oE ); // result 2
          }
          
          // Then finally invoke arrow function inside of METHOD getExp
          return parentScope();
        /*
        ----------------------------------------------------------------------------------------------------------
          THIS APPROACH NOT WORK!
          const parentScope => function() {
              let oE = this.otherExpertise;
              return('This is Paretn scope arrow function works' + oE ); // result ERROR !
          }
        ----------------------------------------------------------------------------------------------------------
          THIS APPROACH IS WORK < Preserved the "this" keyword > OLD WAY BUT NOW AS ARROW FUNCTION!
          Preserved the "this" keyword, now can access local properties.
          This is alternative of arrow function (() => { ... });
          const self = this;
          const parentScope => function() {
             let oE = self.otherExpertise; // instead of "this" use "self"
             return('This is Paretn scope arrow function works' + oE ); // result  2
          }
        */
        
      }
  }

  console.log("Hey! " + Developer.getExp() ); // Read from local scope or Object Developer using arrow function inside the method.
```

```JS
  // Result 
  Hey! This is Parent scope arrow function works2
```

```JS
 // Factory Function that creates an object and returns it
 // Similar to Class and constructor
 // This approach is NOT recommend if the method or properties having a thousand. \
 // can't handle by mermory heap.
 function createDev(name, skills, experience) {
  return {
    name,       // name: name,  | If the property and argument is the same. 
    skills,     // skills: skills, | If the property and argument is the same.
    experience, // experience: experience, | If the property and argument is the same.
    report() {
      return 'Hi!, My name is ' + name + ' My skills are ' + skills +' Yrs of experience '+ experience;
    }
   } 
 }
```

```JS
 // Concole.log() | Result 
 const niel = createDev('Niel', 'PHP, JS, C++', 6);
 console.log(niel); // Result: {name: 'Niel', skills: 'PHP, JS, C++', experience: 6, report: ƒ}
 console.log(niel.report()); // Result: Hi!, My name is Niel My skills are PHP, JS, C++ Yrs of experience 6
```
