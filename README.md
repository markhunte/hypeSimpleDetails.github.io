# Hype-SimpleDetails-Extension-Plugin--API
A Tumult Hype Extenion Project


---

# Hype SimpleDetails Extension Plugin  API Documentation

## Introduction

This documentation explains the usage and functionality of **Hype SimpleDetails** Extension plugin API.

The Extension allows you to easily create HTML detail/summary elements in a Tumult Hype projects just using  text boxes in scenes, either inside a symbol or not. This plugin enables users to interactively display additional information  on their pages.

### Installation

To use this script, follow these steps:

1. Open your Tumult Hype project.
2. Go to the "Head HTML" section of your project.
3. Paste the provided script into the "Head HTML" section.

## Setting up Your Elements for Usage on a scene.

We use text boxes as the element for the HTML details/summary. To set up your elements:

1. Place text boxes (as many as you need) in your scenes where you want to add detail/summary elements.
2. Add the attribute `data-disclosure` to each text box. This designates it as a details element for the API.
3. Add a second attribute `data-id` to each text box. This attribute will be used as an individual ID for each text box.

Example Data-Id Key and Values

To clarify, here are some examples of data-id keys and values:

**Text box1 has**:

`data-disclosure` Additionl HTML attribute and no value
It also has the

``data-id`   Additionl HTML attribute with the value  of `foo1`  This unique data-id value identifies a text box

**Text box1 has:**

`data-disclosure` Additionl HTML attribute and no value
It also has the

``data-id`   with the value  of  `foo2`  This unique data-id value identifies another text box with the ID "foo2" 

## 



### **Symbol Instances**

Using  Detail/Summary Text box Elements Inside Symbol Instances.

You may want to use a text box inside a symbol and use multiple instances of the symbol within your project. Each with its own setup. 

 However, in this scenario, you MUST give each symbol instance the attribute `data-id` instead of giving the individual text boxes  used inside this attribute.

Note: It's essential to give each symbol instance a unique `data-id` value to distinguish it from other instances of the same symbol. This ensures that the API can identify and manipulate the text box within each instance of a symbol correctly.



To clarify, here are some examples of data-id keys and values:

One Instance of a symbol named **symbolFoo** has the 

``data-id`   Additionl HTML attribute with the value  of  `symFoo1`  This unique data-id value identifies this symbol with the ID "symFoo1" 

Because its a symbol instance with the `data-id` , the extension will look inside it for a text box with an Additionl HTML attribute  of `data-disclosure`

The text box does not need the `data-id` 

A second Instance of symbol named **symbolFoo** has the attribute:

``data-id`   with the value  of  `symFoo2`  This unique data-id value identifies this symbol with the ID "symFoo2" 

Because its a symbol instance with the `data-id` , the extension will look inside it for a text box with an Additionl HTML attribute  of `data-disclosure`

The text box does not need the `data-id` 



The two text boxes in symbol instances will be treated as individuals.  ( Even though they are techniclly the same text box since we are using a Symbol instance )

## 

## Constructing API Calls



**API Call Structure**

We can setup and call all the API calls to all the details in one  Hype function.

They are best called On Scene Load. You can either  add a On Scene Load action to run the Javascript function to each scene. Or use a Convenience HypeSceneLoad API call in the head.

i.e



```javascript
	<script>
	
//== The name of your hype function that loads the descriptions.
var My_Description_Function_Name = 'loadDisclosures'
	
/*== Convenience function to call your description loader function on all scene loads. */
function loadDesc(hypeDocument, element, event) {hypeDocument.functions()[My_Description_Function_Name](hypeDocument, element, event);return true;} if ("HYPE_eventListeners" in window === false) {window.HYPE_eventListeners = Array();}window.HYPE_eventListeners.push({ "type": "HypeSceneLoad", "callback": loadDesc });
</script>
```



Note if you have any details on scenes not yet displayed. The Browser will warn you that it cannot find said element. In most cases you should be able to ignore the warning. I have left it in just in case...



### API Call Construction 



To create detail/summary elements, construct API calls by defining the following variables:

- `targetElement`: The value  of either the containing symbol or the standalone text box's `data-id` attribute.
- `descriptionText`: The literal formatted text for the detail/summary. ( or string text if you so choose )
- `options`: Optional settings to style the resulting detail/summary.



API Options

**splitTextAtWordNumber**

This option specifies the number of leading words to display before the "Show more" button appears in the detail/summary element.
Usage Example: If you set splitTextAtWordNumber: 10, the detail/summary element will initially display the first 10 words of the text content. Users will then see the "Show more" button to reveal the remaining content.

**leadingTextColor** option

 This option allows you to set the color for the leading summary text in the detail/summary element.
Usage Example: Suppose you specify leadingTextColor: 'purple'. The text color of the initial summary will be purple. If you do not include this option, the text color will inherit from the Typography Inspector settings in Hype.

**followingTextColor** option

This option lets you set the color for the following summary text in the detail/summary element.



**Text Color Explained further**

Usage Example (With some Options Included): 

If you use 

```javascript
followingTextColor: 'blue'
```

While  omitting the **leadingTextColor**.

The color of the following summary text (after the "Show more" button) will be blue,

while the leading text  (before the "Show more" button ) color will follow the Hype Typography Inspector settings.

**fontSize** option

This option allows you to set the font size for the text within the detail/summary element.

If you set fontSize: '20px', the text within the element will have a font size of 20 pixels. 

However, please note that the font size will inherit from the Typography Inspector settings in Hype if you don't specify this option.

**Inheritance of Typography Inspector Settings**

When any of the text styling options **leadingTextColor**, **followingTextColor**, **fontSize** are  not explicitly defined in the API call, it will inherit the corresponding settings from the Typography Inspector in Hype.

For example, if you have set the text color to blue in the Typography Inspector and only include All text color for that detail/summery will inherited from Typography settings.

The use of these options allows you to customize text styling while still benefiting from the global typography settings within your Hype project by default,.



details/summaries will remain open when others are opened. You can override this behavior for individual details by setting the `acceptsAutoClose` option to `true`.



**acceptsAutoClose** option.

By default all details will open and close independently of each other. The **acceptsAutoClose** option allows for this to be overridden for each individual detail element. 



 **Scenario 1:**

- Detail A (acceptsAutoClose: true)
- Detail B (acceptsAutoClose option not included)
- Detail C (acceptsAutoClose: true)

Explanation:
When you open "Detail A" which has acceptsAutoClose set to true, it will close any other details that are also set to acceptsAutoClose:true. In this case, it will close "Detail C" because it also has acceptsAutoClose: true, but "Detail B" will remain open since it follows the default behavior of not auto closing. 

Additionally, opening or closing "Detail B" will also not affect the states of "Details A" and "C."

**Scenario 2:**

Detail A (acceptsAutoClose option not included)
Detail B (acceptsAutoClose option not included)
Detail C (acceptsAutoClose option not included)

Explanation:
In this scenario, when you open any of the details (A, B, or C), none will not affect the behavior of the others because the acceptsAutoCloseo ption is not included in any of them. Each detail operates independently, and opening one detail will not close any others. Any detail without the acceptsAutoClose option will act independently and not affect or be affected by any that do include the option.


## API construction Examples

**Example 1**

```javascript
// Define the attribute value for the target element
const targetAttributeValue_1 = "description1";

// Define the text containing the content for the detail/summary, including optional HTML formatting
var text1 = `This Detail is using the <b>acceptsAutoClose</b>  option. 
It will close when the other  acceptsAutoClose   details are clicked open.

<strong>This text is important!</strong>

<small>This is some smaller text.</small>

My favorite color is <del style='color:blue;'>blue</del> <ins style='color:orange;'>orange</ins>

This is <sup>superscripted</sup> text.

<p >This is inside a  &#60;p&#62; &#60;&#47;p&#62;  block </p>
<h1>This is H1 text</h1>

<span style='color:#FF2F92'>And will close any others that are using <b>acceptsAutoClose</b>  option when it is opened. It will not affect any that are not using the option</span>
`

// Call the setDescription function to set up a description for the target element
hypeDocument.setDescription(targetAttributeValue_1, text1, {
  splitTextAtWordNumber: 7, 
  acceptsAutoClose: true,
  leadingTextColor: 'purple',    // Set the color of the leading summary 
  followingTextColor: 'black',  // Set the color of the following summary 
  fontSize: '20px'              // Set the font size for the text
});
```

**Explanation:**

1. **Targeting the Element:** The `targetAttributeValue_1`  variable identifies the element with the attribute `data-id`  and the value  "description1"  in the HTML document. This element will be the target for adding the detail/summary to,  if it's a stand-alone text box which also has a `data-disclosure` attribute or if it's a symbol instance with the `data-id` attribute,   then the text box inside it, which should have the `data-disclosure` attribute  final will be the target.
2. **Text Content:** The `text1` variable contains the content for the detail/summary. It includes optional HTML-formatted text with various elements like headings, text formatting, and inline styles.
3. **Text Splitting**: The `splitTextAtWordNumber` option is set to 7, which means that after the 7th word in the content, a "Show more" button will appear to expand the remaing words when clicked.
4. **Setting Up the Detail/Summary:** The `hypeDocument.setDescription` function is called to set up the detail/summary for the specified target element.
5. **acceptsAutoClose** Option: The `acceptsAutoClose` option is set to `true`, indicating that this detail/summary will automatically close when other details with the same option are opened and will close others that also have this option when it is opened.
6. **Text Colors**: The `leadingTextColor` option is set to 'purple', which changes the color of the leading summary text. 
7. **Font Size**: The `fontSize` option is set to '20px', which specifies the font size for the text.

**Behavior Outcome**:

When the user interacts with the detail/summary element identified by `data-id="description1"`:
- The detail/summary text will be divided into two parts: leading and following text. The first 7 words will be displayed initially, and the rest will be hidden behind a "Show more" button. The Show More will change to Show less with a dimmed opacity.
- The summary text will appear in purple with a font size of 20px, and the following text will appear in black also with a font of 20px.
- If there are other detail elements  **with** the `acceptsAutoClose` option set to `true`, opening this detail will automatically close those other details with the same option.
- If there are details **without** the `acceptsAutoClose` option, they will not be affected by the opening or closing of this detail.

The result is an interactive detail/summary element with optional HTML formatting and specified behavior for different types of target elements.



**Example 2**

```javascript
// Define the attribute value for the target element
const targetAttributeIDValue_2 = "description2";

// Define the text containing the content for the detail/summary (plain text with new lines)
const text2 = `This Detail is not using the  acceptsAutoClose option.
It will remain open when the other details are clicked open.

It will not affect any that are  using the option`
;

 /*== Call the setDescription function to set up a description for the target element
   Specify optional customisation options */
setDescription(targetAttributeIDValue_2, text2, {
  splitTextAtWordNumber: 10,
  leadingTextColor: 'blue',     // Set the color of the leading summary
  fontSize: '16px'              // Set the font size for the text
});
```

**Expected Behavior:**

1. **Targeting the Element:** The `targetAttributeIDValue_2`  variable identifies the element with the attribute `data-id`  and the value  "description2"  in the HTML document. This element will be the target for adding the detail/summary to,  if it's a stand-alone text box which also has a `data-disclosure` attribute or if it's a symbol instance with the `data-id` attribute,   then the text box inside it, which should have the `data-disclosure` attribute  final will be the target.
2. **Content and Styling**: The content for the detail/summary is defined in the `text2` variable. It contains plain text with new lines and does not include any HTML markup or inline styling.
3. **Text Splitting**: The `splitTextAtWordNumber` option is set to 10, which means that after the 10th word in the content, a "Show more" button will appear to expand the remaing words when clicked.
4. **Text Colors**: The `leadingTextColor` option is set to 'blue', which changes the color of the leading summary text. The `followingTextColor` option is set to 'green', which changes the color of the following summary text.
6. **Font Size**: The `fontSize` option is set to '16px', which specifies the font size for the text.

**Behavior Outcome**:

- The detail/summary text will be divided into two parts: leading and following text. The first 10 words will be displayed initially, and the rest will be hidden behind a "Show more" button. The Show More will change to Show less with a dimmed opacity.

- The leading text will be in blue, while the following text will inherite  whatever text color is set in the Typoraphy Inspector settings.

- This detail/summary will not close automatically when other details are opened and will not close any others when it is opened.

  

  This example demonstrates how to set up a detail/summary for a plain text content with custom styling and behavior using the `setDescription` function.



In most cases you should use **splitTextAtWordNumber** option but it is optional so you can just have a Show More button initially.



## Global Auto Close Control

To globally control auto-closing, you can use the  the API call hypeDocument.descriptionAutoClose(true/false)  to turn it globally of or on.



Example JavaScript: where we are using a button with an id of turn off one one scene and another with a different id. They bot call this function.

```javascript
if (element.id == 'turnoff') {
  hypeDocument.descriptionAutoClose(false);
} else {
  hypeDocument.descriptionAutoClose(true);
}
```

This script allows you to toggle auto-closing behavior on or off  for any details that have been set to **acceptsAutoClose**

Turning on will not affect any details that where never set to **acceptsAutoClose**

---

