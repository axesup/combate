## Problem

You want to test changes you made which are dependent on player level.

## Solution

Either [enable God mode](https://github.com/codecombat/codecombat/wiki/Access-power-user-features), overwrite the [client User model](https://github.com/codecombat/codecombat/blob/master/app/models/User.coffee)'s `level` function to always return the value you want, or set your user's points [through MongoDB](https://github.com/codecombat/codecombat/wiki/Access-dev-database).

## Details

Level is determined by the number of points you have. God mode increases the player's level, among other things. You can change the `level` function to effectively set all players' level to an arbitrary number (although only on the client side). Finally, you can set the player's points in the db, thereby changing their level throughout the system. Use whichever method best suits your needs.