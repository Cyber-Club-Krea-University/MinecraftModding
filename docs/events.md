# Events

Skript has 'events' like many other mod making tools. This basically means that you can run code whenever something happens. You can find a list of events on the [documentation](https://docs.skriptlang.org/events.html). You can, for example do something like
```
on join:
    broadcast "Welcome to the cyber club server!"    
```
Note how you have to put all strings (text) in quotes.

Every event also has data (or 'variables') attached to it. For example, you can do

```
on join:
    broadcast "Hello %player%! Welcome to the cyber club server!"
```

Note how you have to put "%" around variables in Skript if they are part of a message. The documentation has far more examples, but you can do some pretty fun stuff.

Apart from events, you can also create commands. For example, something like
```sk
command /ping:
    trigger:
        send "Pong!" to player
```

## If Statements

With if statements you can do things when certain conditions are met. For example, the following script sends a player who breaks a dirt block the message "You got dirty!".
```
on break:
    if block is dirt:
        send "You got dirty!" to player
```

You can even add else if and else statements
```
on break:
    if block is dirt:
        send "You got dirty!" to player
    else if block is stone:
        send "You got stony" to player
    else:
        send "You didn't get dirty" to player
```

A cool example of if statements (inspired by [this video](https://youtu.be/KEeY7bJYzR4)) is
```
on step on a gold block:
    if player is holding a gold ingot:
        push the player upwards
        send "Whoosh!" to player
    else:
        send "You need to be holding a gold ingot to use this!" to player
```

## Loops

Skript also has loops. Here you can simply do something a number of times, for example

```
command /do-something:
    trigger:
        loop 5 times:
            wait 1 second
            send "It's been %loop-number% s since you asked me to do something!" to player
            # Do something
```

But you can also loop over every thing in a list. For example, you can create a command to make everything around you gold!

```
command /midas:
    trigger:
        loop all blocks in radius 5 of player:
            if loop-block is not air:
                set loop-block to gold block
```