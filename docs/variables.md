# Variables

We already saw 'variables' (ways of storing data) in the previous document. There are two kinds of variables in skript. There are local variables, which only exist in the scope of an event or some other kind of block (and get deleted after the block is done running). These variables begin with an underscore ('_'). There are also global variables which are remembered all the time and even if the server restarts!

[More information on variables](https://docs.skunity.com/guides/guide/variables.7)

Let's try to understand variables by making a mod for tag. We start by assigning a random player as the 'tagger'.

```sk
command /start:
    trigger:
        set {tagger} to name of a random element out of players
        send action bar "&4&l %{tagger}% is the Tagger!" to player
```

Now, when we run the start command, a random player is assigned as the tagger. Let's now implement a timer and a counter with a boss bar.

```
command /start:
    trigger:
        set {tagger} to name of a random element out of players # We keep the tagger as before

        set {time} to 60 # We set the time variable to 60
        send action bar "&4&l %{tagger}% is the Tagger!" to player
        set {_bar} to a new yellow boss bar titled "%{time}% seconds remain!":
            set progress of event-bossbar to 1
        add all players to viewers of {_bar}

        # We count down
        while {time} > 0:
            set title of {_bar} to "%{time}% seconds remain!"
            set progress of {_bar} to ({time} / 60)
            wait 1 second
            subtract 1 from {time}

        delete {time}
        remove all players from viewers of {_bar}
        send title "Time's up!" to all players
```

Now let's implement the tag functionality.

```
command /start:
    trigger:
        set {tagger} to name of a random element out of players
        set {time} to 60 # We set the playing time variable to 60
        set {_bar} to a new yellow boss bar titled "%{time}% seconds remain!":
            set progress of event-bossbar to 1
        add all players to viewers of {_bar}

        while {time} > 0:
            send action bar "&4&l %{tagger}% is the Tagger!" to players
            set title of {_bar} to "%{time}% seconds remain!"
            set progress of {_bar} to ({time} / 60)
            wait 1 second
            subtract 1 from {time}

        delete {time}
        remove all players from viewers of {_bar}
        send title "&cTime's up!" to all players

on damage:
    name of attacker is {tagger}
    victim is a player
    {time} > 0

    set {tagger} to name of victim

    cancel event
    play sound "block.note_block.pling" at location of victim
    send action bar "&4&l %{tagger}% is the Tagger!" to players
```

Notice how tagger and time are global variables because if they were local they wouldn't be accessible in the on damage block, however, the bar variable can be local because it's not accessed outside of the start command (in fact a bar can't be set to a global variable!)