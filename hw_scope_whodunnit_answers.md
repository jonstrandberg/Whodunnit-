# Scope Homework: Who Dunnit

### Learning Objectives

- Understand function scope
- Know the difference in between the let and const keywords

## Brief

Using your knowledge about scope and variable declarations in JavaScript, look at the following code snippets and predict what the output or error will be and why. Copy the following episodes into a JavaScript file and add comments under each one detailing the reason for your predicted output.

### MVP

#### Episode 1

```js
const scenario = {
  murderer: 'Miss Scarlet',
  room: 'Library',
  weapon: 'Rope'
};

const declareMurderer = function() {
  return `The murderer is ${scenario.murderer}.`;
}

const verdict = declareMurderer();
console.log(verdict);
```

//Yes you will be able to see the murderer as it is accessing the information from outwards in terms of scope, as the const scenario is available in the outer scope and so can be accessed by the function which is one level in in terms of scoping.

#### Episode 2

```js
const murderer = 'Professor Plum';

const changeMurderer = function() {
  murderer = 'Mrs. Peacock';
}

const declareMurderer = function() {
  return `The murderer is ${murderer}.`;
}

changeMurderer();
const verdict = declareMurderer();
console.log(verdict);
```
//This will not work as the functon is trying to reassign a constant value which is not possible. This will therefore return an error and will not show the murderer. 

#### Episode 3

```js
let murderer = 'Professor Plum';

const declareMurderer = function() {
  let murderer = 'Mrs. Peacock';
  return `The murderer is ${murderer}.`;
}

const firstVerdict = declareMurderer();
console.log('First Verdict: ', firstVerdict);

const secondVerdict = `The murderer is ${murderer}.`;
console.log('Second Verdict: ', secondVerdict);
```
//As the murderer has been set as a 'let' this can be changed. The console log in first and second verdicts also call the different let murderers as the first one calls the variable directly and the second one calls the function which contains the let. As a result the firstVerdict will show Professor Plum and the secondVerdict will show Mrs Peacok.  

#### Episode 4

```js
let suspectOne = 'Miss Scarlet';
let suspectTwo = 'Professor Plum';
let suspectThree = 'Mrs. Peacock';

const declareAllSuspects = function() {
  let suspectThree = 'Colonel Mustard';
  return `The suspects are ${suspectOne}, ${suspectTwo}, ${suspectThree}.`;
}

const suspects = declareAllSuspects();
console.log(suspects);
console.log(`Suspect three is ${suspectThree}.`);
```
//So as the suspects are all 'let' functions they can be changed. However this will only be within the function as the function can get the information from the 'let' which is inwards in terms of scope. The let however, wouldn't be able to do it the other way, so couldn't get information from the function. This means that the first console log will return Miss Scalet, Professor Plum and Colonel Mustard, not Mrs Peacock as it has been changed. However console log two will return Mrs Peacock as it will access the letsuspectThree = Mrs Peacock as it isn't accessing information from within the function. This would have to be done by calling the const name declareAllSuspects and then suspect Three. 

#### Episode 5

```js
const scenario = {
  murderer: 'Miss Scarlet',
  room: 'Kitchen',
  weapon: 'Candle Stick'
};

const changeWeapon = function(newWeapon) {
  scenario.weapon = newWeapon;
}

const declareWeapon = function() {
  return `The weapon is the ${scenario.weapon}.`;
}

changeWeapon('Revolver');
const verdict = declareWeapon();
console.log(verdict);
```
//So you can change something within a constant, you just can't reassign it. So the const changeWeapon is creating a function which can access the const information as it is outwards in terms of scope. It can access the scenario.weapon and change it to a new weapon by using the variable name to revolver. The second function returns the string and can access the information from const changeWeapon as they are of the same scope. The const verdict then calls the second function and then prints it in the next line. This means that it will print "The weapon is the Revolver" ONLY. None of the other information has been printed. 

#### Episode 6

```js
let murderer = 'Colonel Mustard';

const changeMurderer = function() {
  murderer = 'Mr. Green';

  const plotTwist = function() {
    murderer = 'Mrs. White';
  }

  plotTwist();
}

const declareMurderer = function () {
  return `The murderer is ${murderer}.`;
}

changeMurderer();
const verdict = declareMurderer();
console.log(verdict);
```
//The let can be changed, so the murderer changes in the changeMurder function however as we can see within the curly brackets the whole function changes the murderer once and then it changes it again. Therefore when the changeMurderer function is called before verdict is printed, the murderer will be the last change within the changeMurderer function, so the murderer is Mrs White. 

#### Episode 7

```js
let murderer = 'Professor Plum';

const changeMurderer = function() {
  murderer = 'Mr. Green';

  const plotTwist = function() {
    let murderer = 'Colonel Mustard';

    const unexpectedOutcome = function() {
      murderer = 'Miss Scarlet';
    }

    unexpectedOutcome();
  }

  plotTwist();
}

const declareMurderer = function() {
  return `The murderer is ${murderer}.`;
}

changeMurderer();
const verdict = declareMurderer();
console.log(verdict);
```
//The murderer will be Mr. Green this is because the function is at the function level, all the others will change within the functin, but as they are nested, this is not what will be returned. You can see this from the indentation. As there is no access identifier this will display in global level. You can see what is on the outside, but you can't see what's inside. This is as the verdict calls changeMurderer and not the other functions within the nested variable. 

#### Episode 8

```js
const scenario = {
  murderer: 'Mrs. Peacock',
  room: 'Conservatory',
  weapon: 'Lead Pipe'
};

const changeScenario = function() {
  scenario.murderer = 'Mrs. Peacock';
  scenario.room = 'Dining Room';

  const plotTwist = function(room) {
    if (scenario.room === room) {
      scenario.murderer = 'Colonel Mustard';
    }

    const unexpectedOutcome = function(murderer) {
      if (scenario.murderer === murderer) {
        scenario.weapon = 'Candle Stick';
      }
    }

    unexpectedOutcome('Colonel Mustard');
  }

  plotTwist('Dining Room');
}

const declareWeapon = function() {
  return `The weapon is ${scenario.weapon}.`
}

changeScenario();
const verdict = declareWeapon();
console.log(verdict);
```
//Unlike number 7 this example is changing elements within the cnstants. The const changeScenario can access the scenario as this is inwards in terms of scope on the const level. The changeScenario is a fucntion so therefore outwards in terms of scope. This function changes as it is nested and can access the scenario elements. The weapon is therefore changes to the last one within the function which is the candle stick which is the answer. 

#### Episode 9

```js
let murderer = 'Professor Plum'; 

if (murderer === 'Professor Plum') {
  let murderer = 'Mrs. Peacock';

}

const declareMurderer = function() {
  return `The murderer is ${murderer}.`;
}

const verdict = declareMurderer();
console.log(verdict);
```
//The murderer is never changed. So it will be Professor Plum. I think this is as it is a nested example within the if, it cannot access the let murderer. I believe it must have something to do with the fact that an if statement won't have access to the information within the let. This could be due to scope, but I am unsure. 


### Extensions

Make up your own episode!
