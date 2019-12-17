# Roles

The role of the NAO defines how it decides to operate on the field. A striker is
meant to play offensively and score goals while the purpose of a keeper is to
keep enemy Strikers from scoring goals. This document provides a look at how a
NAOs role is chosen and why.

In the PlayingRoleProvider.json file lies the configuration for some variable
parameters that are used to determine certain roles. The common setting for the
file looks like this:

```json
{
  "useTeamRole": true,
  "assignBishop": false,
  "assignBishopWithLessThanFourFieldPlayers": false,
  "playerOneCanBecomeStriker": true,
  "allowReplacementKeeper": true,
  "playerOneDistanceThreshold": 1.5,
  "KeeperTimeToReachBallPenalty": 0,
  "forceRole": "none"
}
```

Usually the first NAO to enter the cycle-Method of the PlayingRoleProvider will
set the roles not only for himself but for his teammates too. When the next NAO
reaches the PRP (PlayingRoleProvider) it will skip through most of the method
because he already has a role assigned. This increases efficiency and speed.

## How are roles chosen?

### Striker

A player becomes a striker if the current game states allows for one (i.e.
when there is a free strike going or if we are the striking team) and if the
player is the one closest to the ball, that does not have a role yet.
The player must also not be penalized in order to be eligible for the role of
striker.

### Keeper

The keeper role is *always* assigned to the player with player number 1.

### Replacement Keeper

If player one is far away or if there is not player one then another NAO will
be set as keeper. This mechanism ensures a more defensive playstyle as every
team usually has a player with number one and thus will always prioritise
setting it up as the keeper instead of a striker for example.

### Other Roles

If there are still players left after setting one striker and one keeper they
will have roles assigned to them depending on the team size.

The decision on what player to assign support striker or bishop to is made by
setting a variable that is higher if the player has been a support striker or
bishop before. This ensures that players will not switch roles all the time and
tend to stay in their current role. A bishop can only be assigned if the
requirements set in the JSON file above are met.

#### 3 Players

The remaining player will become a defender.

#### 4 Players

One player will become a defender whilst the other is assigned either bishop or
support striker.

#### 5 Players

In this case there will be two defenders and one bishop or support striker.

#### 6 Players

Here there will be two defenders one support striker and one bishop guaranteed.
