NEW DJ CARDS.

## Intent:


## Using: Custom HypeSimple Descriptions Function.

The custom version of this allows us to add an image of the Dj.
Initially, the attempt was to include an inline image block in the  css ::before.
This did not work well. So we now include a div wrapper and an image block along with the  construction of the detail.’s block. 

The div wrapper and image are above the detail block. 
The image  path is passed in via the constructor.

We also have are not  using the **::before ** **content in this custom version to place the** **leadingText**.  This is now a `<p>` block.

The leadingText  path is passed in via the constructor, and placed in the `<p>` block directly.

 `  descriptionElement_child.innerHTML = 
<div class=“_wrap”>  <img src=“${image_}” alt=“Girl in a jacket” style=“clip-path: circle(50%); shape-outside:circle(39%);  box-sizing: border-box; margin-right:3rem; float:left;width:100px; height:auto;”> <p class=“def” style=“color: ${leadingTextColor};font-size:${fontSize}; word-wrap: break-word;white-space: pre-line;padding-left:20px;”>${sourceDescription_20}</p>

 </div>

      ```
      <details  id="${summaryClass}" class="details_" data-autoclose="${acceptsAutoClose}">
        <summary class="${summaryClass}" style=";float:right;color: ${leadingTextColor}; font-size:${fontSize};"></summary>
        <p class="def" style="color: ${followingTextColor};font-size:${fontSize};">${sourceDescriptionMore}</p>
      </details>
    ;```

 In the  load() , we  take all the text (objects)  that need to go into this area and calculate the word count simply using split. We then pass that in as the  **splitTextAtWordNumber** so we only have the correct text go into the ::after as the followingText.
There are also additions and deletions in the CSS blocks to adjust all of the above. Along with some inline styling for the image.
 


***
## Using: Clone function.
*Intent: Try to have all the dis show at the same time, hall of fame if you will.*

The new code clones the original DJ card ( not populated in the final result)
The clones are created, then populated.
***

## Using jQuery Animate():
Intent: I want control the cards layout in a row and column order. 
![Screenshot 2023-10-11 at 20.53.36](Screenshot%202023-10-11%20at%2020.53.36.png)
I am using the same JQuery animate  blocks I used in the Filter Tags  project for a Tumult post  ( with some adjustments ). This was a much simpler way of doing the layout for the cards than trying to get the clone functions to do it. The animate  function is called after the population of the cards at the end of the load() function. The added bonus is we get the really nice float left animation of the cards.
**( NOTE: It may be worth merging the Clone and Animation code into one extension. )**
