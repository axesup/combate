To add the sample code, first double-click the Hero Placeholder and navigate to their `programming.Programmable` component. Navigate through the component's tree:
- *programming.Programmable*
  - *programmableMethods*
    - *plan*
      - *languages*
        * ***This is where the alternate language sample code will be filled in. Python is the important one!***
      - *source*
        * ***This is the Javascript sample code.***
      - *i18n*
        * ***Add this field after creating comments so Diplomats can add translations.***
      - *Comments*
        * ***This is where replacement comments will go.***

When filling in the sample code for a level, there are a few neat tips to keep in mind.

* Comments are always given a space between their commenting symbol and the comment itself.
 * `// This is a comment!`
 * `# This is a Python comment.`
 * `-- <%= commentDeclaration %>`

### Hint Arrow
If the level is attempting to teach a concept or guide players through writing code, it is important to direct the player's attention to where the code should be inserted. In each blank area below a comment, an arrow will display.
* **Note:** CodeCombat allows for one block of comments at the start of the sample code before adding an arrow below all comments with an empty space below them.

[<img width="50%" src="http://files.codecombat.com/wiki-images/hint_arrow.png"/>](http://files.codecombat.com/wiki-images/hint_arrow.png)
### Change Arrow
There are some levels where the player is given a hint in the form of pre-existing code. Often times this code is wrong, or, generally should be changed or removed if the user is to progress. Use the `∆` (delta) symbol on the same line as the code and a hint arrow will point to the line until it has been changed.

[<img width="50%" src="http://files.codecombat.com/wiki-images/change_arrow.png"/>](http://files.codecombat.com/wiki-images/change_arrow.png)

### i18n Strings
Simply writing your sample code doesn't provide the Diplomats with access to the strings for translation. You will need to use a special string replacement structure to pull these comments out for translation.

[<img width="50%" src="http://files.codecombat.com/wiki-images/comment_string_example.png"/>](http://files.codecombat.com/wiki-images/comment_string_example.png)