# Mini-project development process

## Phase one - Multiple rocks

For this phase, you will keep a set of rocks and spawn new rocks into this set. This requires the following steps:

1. Remove 𝚊_𝚛𝚘𝚌𝚔 and replace it with 𝚛𝚘𝚌𝚔_𝚐𝚛𝚘𝚞𝚙. Initialize the rock group to an empty set. Modify your rock spawner to create a new rock (an instance of a Sprite object) and add it to 𝚛𝚘𝚌𝚔_𝚐𝚛𝚘𝚞𝚙.

2. Modify your rock spawner to limit the total number of rocks in the game at any one time. We suggest you limit it to 12. With too many rocks the game becomes less fun and the animation slows down significantly.

3. Create a helper function 𝚙𝚛𝚘𝚌𝚎𝚜𝚜_𝚜𝚙𝚛𝚒𝚝𝚎_𝚐𝚛𝚘𝚞𝚙. This function should take a set and a canvas and call the update and draw methods for each sprite in the group.

4. Call the 𝚙𝚛𝚘𝚌𝚎𝚜𝚜_𝚜𝚙𝚛𝚒𝚝𝚎_𝚐𝚛𝚘𝚞𝚙 function on 𝚛𝚘𝚌𝚔_𝚐𝚛𝚘𝚞𝚙 in the draw handler.

## Phase two - Collisions

For this phase, you will detect collisions between the ship and a rock. Upon a collision, the rock should be destroyed and the player should lose a life. To implement ship-rock collisions, you need to do the following:

1. Add a 𝚌𝚘𝚕𝚕𝚒𝚍𝚎 method to the Sprite class. This should take an 𝚘𝚝𝚑𝚎𝚛_𝚘𝚋𝚓𝚎𝚌𝚝 as an argument and return 𝚃𝚛𝚞𝚎 if there is a collision or 𝙵𝚊𝚕𝚜𝚎 otherwise. For now, this other object will always be your ship, but we want to be able to use this collide method to detect collisions with missiles later, as well. Collisions can be detected using the radius of the two objects. This requires you to implement methods 𝚐𝚎𝚝_𝚙𝚘𝚜𝚒𝚝𝚒𝚘𝚗 and 𝚐𝚎𝚝_𝚛𝚊𝚍𝚒𝚞𝚜 on both the Sprite and Ship classes.

2. Implement a 𝚐𝚛𝚘𝚞𝚙_𝚌𝚘𝚕𝚕𝚒𝚍𝚎 helper function. This function should take a set 𝚐𝚛𝚘𝚞𝚙 and a sprite 𝚘𝚝𝚑𝚎𝚛_𝚘𝚋𝚓𝚎𝚌𝚝 and check for collisions between 𝚘𝚝𝚑𝚎𝚛_𝚘𝚋𝚓𝚎𝚌𝚝 and elements of the group. If there is a collision, the colliding object should be removed from the group. To avoid removing an object from a set that you are iterating over (which can cause you a serious debugging headache), iterate over a copy of the set created via 𝚜𝚎𝚝(𝚐𝚛𝚘𝚞𝚙). This function should return 𝚃𝚛𝚞𝚎 or 𝙵𝚊𝚕𝚜𝚎 depending on whether there was a collision. Be sure to use the 𝚌𝚘𝚕𝚕𝚒𝚍𝚎 method from part 1 on the sprites in the group to accomplish this task.

3. In the draw handler, use the 𝚐𝚛𝚘𝚞𝚙_𝚌𝚘𝚕𝚕𝚒𝚍𝚎 helper to determine if the ship hit any of the rocks. If so, decrease the number of lives by one. Note that you could have negative lives at this point. Don't worry about that yet.

## Phase three - Missiles

For this phase, you will keep a set of missiles and spawn new missiles into this set when firing using the space bar. This requires the following steps:

1. Remove 𝚊_𝚖𝚒𝚜𝚜𝚒𝚕𝚎 and replace it with 𝚖𝚒𝚜𝚜𝚒𝚕𝚎_𝚐𝚛𝚘𝚞𝚙. Initialize the missile group to an empty set. Modify your shoot method of 𝚖𝚢_𝚜𝚑𝚒𝚙 to create a new missile (an instance of the Sprite class) and add it to the 𝚖𝚒𝚜𝚜𝚒𝚕𝚎_𝚐𝚛𝚘𝚞𝚙. If you use our code, the firing sound should play automatically each time a missile is spawned.

2. In the draw handler, use your helper function 𝚙𝚛𝚘𝚌𝚎𝚜𝚜_𝚜𝚙𝚛𝚒𝚝𝚎_𝚐𝚛𝚘𝚞𝚙 to process 𝚖𝚒𝚜𝚜𝚒𝚕𝚎_𝚐𝚛𝚘𝚞𝚙. While you can now shoot multiple missiles, you will notice that they stick around forever. To fix this, we need to modify the Sprite class and the 𝚙𝚛𝚘𝚌𝚎𝚜𝚜_𝚜𝚙𝚛𝚒𝚝𝚎_𝚐𝚛𝚘𝚞𝚙 function.

3. In the 𝚞𝚙𝚍𝚊𝚝𝚎 method of the Sprite class, increment the age of the sprite every time 𝚞𝚙𝚍𝚊𝚝𝚎 is called. If the age is greater than or equal to the lifespan of the sprite, then we want to remove it. So, return 𝙵𝚊𝚕𝚜𝚎 (meaning we want to keep it) if the age is less than the lifespan and 𝚃𝚛𝚞𝚎 (meaning we want to remove it) otherwise.

4. Modify 𝚙𝚛𝚘𝚌𝚎𝚜𝚜_𝚜𝚙𝚛𝚒𝚝𝚎_𝚐𝚛𝚘𝚞𝚙 to check the return value of 𝚞𝚙𝚍𝚊𝚝𝚎 for sprites. If it returns 𝚃𝚛𝚞𝚎, remove the sprite from the group. Again, you will want to iterate over a copy of the sprite group in 𝚙𝚛𝚘𝚌𝚎𝚜𝚜_𝚜𝚙𝚛𝚒𝚝𝚎_𝚐𝚛𝚘𝚞𝚙 to avoid deleting from the same set over which you are iterating.

## Phase four - Collisions revisited

Now, we want to destroy rocks when they are hit by a missile. We can't quite use 𝚐𝚛𝚘𝚞𝚙_𝚌𝚘𝚕𝚕𝚒𝚍𝚎, because we want to check for collisions between two groups. All we need to do is add one more helper function:

1. Implement a final helper function 𝚐𝚛𝚘𝚞𝚙_𝚐𝚛𝚘𝚞𝚙_𝚌𝚘𝚕𝚕𝚒𝚍𝚎 that takes two groups of objects as input. 𝚐𝚛𝚘𝚞𝚙_𝚐𝚛𝚘𝚞𝚙_𝚌𝚘𝚕𝚕𝚒𝚍𝚎 should iterate through the elements of a copy of the first group using a 𝚏𝚘𝚛-loop and then call 𝚐𝚛𝚘𝚞𝚙_𝚌𝚘𝚕𝚕𝚒𝚍𝚎 with each of these elements on the second group. 𝚐𝚛𝚘𝚞𝚙_𝚐𝚛𝚘𝚞𝚙_𝚌𝚘𝚕𝚕𝚒𝚍𝚎 should return the number of elements in the first group that collide with the second group as well as delete these elements in the first group. You may find the 𝚍𝚒𝚜𝚌𝚊𝚛𝚍 method for sets to be helpful here.

2. Call 𝚐𝚛𝚘𝚞𝚙_𝚐𝚛𝚘𝚞𝚙_𝚌𝚘𝚕𝚕𝚒𝚍𝚎 in the draw handler to detect missile/rock collisions. Increment the score by the number of missile collisions.

## Phase five - Finish it off

1. Add code to the draw handler such that, if the number of lives becomes 0, the game is reset and the splash screen appears. In particular, set the flag 𝚜𝚝𝚊𝚛𝚝𝚎𝚍 to 𝙵𝚊𝚕𝚜𝚎, destroy all rocks and prevent any more rocks for spawning until the game is restarted.

2. When the game starts/restarts, make sure the lives and the score are properly initialized. Start spawning rocks. Play/restart the background music loaded in the variable 𝚜𝚘𝚞𝚗𝚍𝚝𝚛𝚊𝚌𝚔 in the program template.

3. When you spawn rocks, you want to make sure they are some distance away from the ship. Otherwise, you can die when a rock spawns on top of you, which isn't much fun. One simple way to achieve this effect to ignore a rock spawn event if the spawned rock is too close to the ship.

4. Experiment with varying the velocity of rocks based on the score to make game play more difficult as the game progresses.

5. Tweak any constants that you have to make the game play the way you want.
