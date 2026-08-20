# AWScript Rat Royale
AWScript's primary implementation is into Rat Royale.

## _ Variables

```_#PlayerThatJoined``` - Most recent player that joined

```_#PlayerThatLeft``` - Most recent player that left

```_#PlayerThatDied``` - Most recent player that died

## Primary _ Functions

```ConsoleLog``` - Logs to Unity's console, not really useful except for devs

```ConnectToPlayerJoin``` - First argument is function name, second is it's locker name. Connects the function to player join events

```ConnectToPlayerLeave``` - First argument is function name, second is it's locker name. Connects the function to player leave events

```ConnectToPlayerDied``` - First argument is function name, second is it's locker name. Connects the function to player death events

## Generic _ Functions

```Log``` - All arguments are converted into strings, variables are read, spaces are inserted between arguments, and its all appended to log file.

```LogVerbatim``` - Same as log, but doesn't read variable values automatically

```Add``` - First argument is the output variable, all other arguments are numbers to be added

```Subtract``` - First argument is the output variable, all other arguments are numbers to be subtracted

```Divide``` - First argument is the output variable, all other arguments are numbers to be divided

```Multiply``` - First argument is the output variable, all other arguments are numbers to be multiplied
