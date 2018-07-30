## Problem

You want to test changes you made which are dependent on player level.

## Solution

Either [enable God mode](https://github.com/codecombat/codecombat/wiki/Access-power-user-features), or overwrite the [client User model](https://github.com/codecombat/codecombat/blob/master/app/models/User.coffee)'s `level` function to always return the value you want.

## Details

Level is determined by the number of points you have. God mode increases the player's level, among other things. You can change the `level` function to effectively set all players' level to an arbitrary number (although only on the client side).