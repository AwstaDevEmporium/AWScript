# AWScript
AWScript, in-house scripting proprietary language for Awsta's Dev Emporium. This is only introductory and lacks most AWScript nonessential instructions.

## Basics/philosophy
AWScript lacks significant nesting. You could nest functions however. This is intentional. AWScript code also executes one instruction per line. You cannot feed the input of a function into another function without first taking it into another variable. Most instructions will provide you the ability to feed an input function. AWScript's perchance statements are the implementation of ifs, however they are global. It is recommended for you to cache the perchance state (in the functions or outside it just in case) before you execute any function and then return it. AWScript also lacks scoping. Rather, the closest thing to scope are @Lockers/Lockers which store functions and variables. Functions must be in a Locker but variables may also be put into '_Global'. AWScript is incredibly small. It has no built in adder or subtractor or mathematical operators, other than for comparing via the perchance statement. Moreover the language is incredibly permissive in naming stuff. You can emulate scope by naming stuff with periods and etc. Only characters off limit in names are whitespace and a shashtag at the start (IF it isn't a variable).

## Lockers
Lockers are the base of all thats AWScript. Lockers cannot be put in Lockers and are all globally accessible. To create one simply use this instruction:

```new @Locker MyLockerName;```

## Functions and _ functions
Functions in the 'Locker' _ are the only functions that can take arguments directly without requiring you to manually set variables before hand so that it can do something based off a shared state. This is because _ functions lack Lockers because they are directly implemented in C#. This is where the plugin capability exists, and where AWScript can be treated as a DSL. For example the Low Level/ Console flavor of AWScript comes with Print. You invoke arguments in a _ function with 'with'. This is required. 

```run Print in _ with hello wrold i am here;```

This prints "hello wrold i am here". Please note there are no numbers in AWScript, in the sense as in other languages. Everything is assumed to be a string. You can create a function under a Locker as such (note the Locker specification is optional if mounted):

```new @Function MyFunctionName in MyLockerName;```

To add code to a function, enter construction (a global flag!) with ```construct FunctionName in Locker;```. After doing that you can then prefix any line of code with ```> ```, this will then append it to the actively constructed function. 

## Variables
AWScript requires variables to do most things. First announce a variable via the announce command, this creates it as null. Variables require hashtags as their first character in their name or else they will not be parsed as variables, but rather as strings.

```announce #VariableName in LockerName;```

Note all 'in LockerName's are mandatory if your not mounted to a locker. Using the mount instruction and specifying a name of a Locker, it will assume all ommitted Locker specifications refer to the mounted Locker. You can then set variables as such:

```set #VariableName in LockerName to 10;```

Note you cannot set a variable to multiple words immediately. Why? Well because whitespace is the grand seperator. Instead you can use the concat instruction to append ```_#Space```, which is simply a global variable that refers to a single space. Example:

```concat #VariableName@Location with _#Space to #VariableName@Location;```

This appends a space to #VariableName@Location and returns it TO #VariableName@Location. Note the @ sign is used to specify the Locker the variable is 'at/@'. This is only used when the variable name is being used as an argument. You use long-precise form if your unmounted in announce or set instructions, as seen above. You do not need to use the @Location, as if your unmounted it will look for global variables by the variable name and then search through every locker. However it is more performative to use it. Plus, if you omit it while mounted, it only looks in your mounted Locker for the variable.

## Perchance
Perchance is the 'if' of AWScript. It is confusing at first. You cannot nest perchances inside of eachother in the way you can with ifs. Perchances have no ands or ors, only comparators are ```is```, ```isn't```, ```less``` (than), and ```greater``` (than). You can simulate ands and ors by making a perchance alter whether a second perchance executes, acting like a second requirement.

```perchance #VarName@LocationLocker is 10;```

Now here is the weird part. Perchances are global. They change the entire interpretation of code globally. Here is how it works: you can simply place a perchance-modifier before a line and it will modify whether it is interpretted or not. These are ```/ ``` for "if true" and ```\ ``` for "if false". You can also stack these with the construction indicators. For instance ```/ > ``` for "add to function if true" or ```\ > ``` for "add to function if false".

## Looping/ anchoring/ 'jerking the chain'
Instead of loops you have anchors and pulleys. The anchor command instantiates an anchor by the name following it, as such:

```anchor AnchorName;```

Anchors are globally defined HOWEVER they are not globally compatible. If you try to run an anchor in another function, it will cause issues to say the least. Pulleys work as such:

```pulley AnchorName;```

## Garbage
AWScript doesn't have garbage collectors. You are trusted. Creating a second variable of the same name in the same Locker will error. Same with creating an anchor with a preexisting name. Solution? Disavow. The disavow command has four modes you can use. First the simple variable annihalator:

```disavow #VarName@Location;```

Then the function destroyer (note the Locker specification can still be ommitted if mounted):

```disavow @Function FunctionName in Locker;```

Then the locker destroyer:

```disavow @Locker LockerName```

And finally one of the most important, the anchor destroyer:

```disavow @Anchor anchorName;```

# The Future
AWScript+ is a possible planned superset over AWScript, including the ability to pass arguments into functions and the ability to embed other instructions within instructions, say to directly set a variable tot he output of a function. And also may possibly include the ability to set a function to a certain shortcut, like so you can execute (funcName 10 20;)
