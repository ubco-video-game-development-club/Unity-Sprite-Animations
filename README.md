# Unity-Sprite-Animations
 Base project for the Unity Sprite Animations event
 
## Follow along instructions
Base Project includes:
Player game object with basic movement script
Sprite sheets for idle, up, down, left, right animations.

### Sprite sheet splicing
* Sprite mode: multiple
* For pixel art:
  * Filter mode: point (no anti-aliasing when the sprite is rendered)
  * Compression: none (no compression on colours)
* Go to sprite editor:
  * slice->grid by cell size: input size of sprite -> slice ->apply
* Now when you expand your sprite sheet, you will see multiple sprites

### Creating animation files
* Shortcut: Select sliced sprites and drag them into the scene, this will create an animation file + animation controller with the default animation set to the corresponding animation file(you will only need one of these since our default animation will be the idle animation, keep this and delete the rest).
* If you open the animation file, you can see the keyframes (diamonds), drag them around if you need to, say if you want one of the frames to last longer
* If you don’t want your animation to loop, say if you need a death animation that only plays once, select the anim file and make sure loop time is not selected
* Notes:
  * Loop pose is useful for 3d animations: loops the animation for you, The last frame of the animation is merged with the first to something in-between
  * Cycle offset: changes when the animation start in the loop, we don’t need this 

### Animation transitions in the controller and Script parameters
* Attach an animator component to the player game object
* Drag controller to the animator component
* Open controller, we see that at entry, the gameobject has defaulted to the idle animation because that’s the one that we have created. Press play and admire
* Create transitions between the animations
  * Create state, then right-click this new state and select make the transition, then select the transition arrow
  * Untick 'has exit time' if you don’t want the animation to fully play out before switching to the next one ie you want the animation to play immediately
  * In settings: also have transition duration at 0 if you want the animation to switch immediately (this is usually used in 3d animations to smooth the transition, but we don’t need that here)
  * Note: Any state: special events that will happen no matter what animation state you’re in
* Set conditions for these transitions, this will depend on your script (i.e if speed>0.1/ismoving=true then transition). Since our movement script depends on incrementing and decrementing the x and y axis, we will set our parameters Vertical and Horizontal to check if the player is moving vertically or horizontally, and make animation transitions accordingly.
  * Example: create the parameter Vertical to check when our player is moving up. Let’s say when Vertical>0.1 then transition to the up animation, and so on
  * After we’ve added all the parameters and transitions. Adjust script: add this:

`animator.SetFloat("Vertical", dy);`

`animator.SetFloat("Horizontal", dx);`
  * This makes it so that when your script is changing the y/x transform of your player, it will set the animator’s Vertical and Horizontal parameters and change the transitions of your animations accordingly

