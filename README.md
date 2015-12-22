#Accessibility Guidelines


##ARIA Landmark Roles

>ARIA Landmark Roles help assistive devices navigate your site. Important roles to be aware of include:

> **banner** – Typically the “header” of your page that includes the name of the site

> **search** – For the search form

> **form** - Group of elements that as a whole, assemble a form (please note that there isn’t a great deal of legacy support for this role)

> **main** – This would designate the main content area on your site

> **navigation** – Use on any navigation list, typically on the nav element

> **contentinfo** – Typically the “footer” of your page that contains information about the parent document such as copyrights and links to privacy statements
To add a role to an element, simply add the “role” as an attribute:

>`<header role="banner" class="site-header">`

>It’s recommended to label the areas with a descriptive name using aria-label, aria-labelledby or title. This get’s more important in case you use a role more than once. Please note that ‘banner’, ‘main’ and ‘contentinfo’ should only be used once.


<cite>Source: [http://a11yproject.com/posts/aria-landmark-roles/](http://a11yproject.com/posts/aria-landmark-roles/)
</cite>

###Other resources: 

[https://www.w3.org/WAI/GL/wiki/Using_ARIA_landmarks_to_identify_regions_of_a_page](https://www.w3.org/WAI/GL/wiki/Using_ARIA_landmarks_to_identify_regions_of_a_page)

[https://accessibility.oit.ncsu.edu/training/accessibility-handbook/aria-landmarks.html](https://accessibility.oit.ncsu.edu/training/accessibility-handbook/aria-landmarks.html)


- - - 

##`aria-hidden` (state)

Tells the screen reader not to read that part.

> Indicates that the element and all of its descendants are not visible or perceivable to any user as implemented by the author. See related aria-disabled.

> If an element is only visible after some user action, authors MUST set the aria-hidden attribute to true. When the element is presented, authors MUST set the aria-hidden attribute to false or remove the attribute, indicating that the element is visible. Some assistive technologies access WAI-ARIA information directly through the DOM and not through platform accessibility supported by the browser. Authors MUST set aria-hidden="true" on content that is not displayed, regardless of the mechanism used to hide it. This allows assistive technologies or user agents to properly skip hidden elements in the document.

> It is recommended that authors key visibility of elements off this attribute, rather than change visibility and separately have to remember to update this property. CSS 2 provides a way to select on attribute values ([CSS]). The following CSS declaration makes content visible unless the aria-hidden attribute is true; scripts need only update the value of this attribute to change visibility:

> `[aria-hidden="true"] { visibility: hidden; }`

Source: <cite>[http://www.w3.org/TR/wai-aria/states_and_properties#aria-hidden](http://www.w3.org/TR/wai-aria/states_and_properties#aria-hidden)</cite>

- - - 

##`aria-haspopup` (property)

Used to let the screen reader know that there is a submenu to expand.

> Indicates that the `element` has a popup context menu or sub-level menu.

> This means that activation renders conditional content. Note that ordinary tooltips are not considered popups in this context.

> A popup is generally presented visually as a group of items that appears to be on top of the main page content.

While, I originally thought this would be a good idea for the modals, it appears that this is really only used for submenus.



- - - 



##`aria-describedby` (property)

Used to link to a description. In our case, to describe the content of the box before it reads the content of the `div`, because it starts with close button. We'll probably want to just move the close button to the bottom of the `div`.

> Identifies the element (or elements) that describes the object. See related [aria-labelledby](http://www.w3.org/TR/wai-aria/states_and_properties#aria-labelledby).

> The `aria-labelledby` attribute is similar to aria-describedby in that both reference other elements to calculate a text alternative, but a label should be concise, where a description is intended to provide more verbose information.

> The element or elements referenced by the `aria-describedby` comprise the entire description. Include ID references to multiple elements if necessary, or enclose a set of elements (e.g., paragraphs) with the element referenced by the ID.


Example: 

```
<div role="dialog" aria-labelledby="dialog1Title" aria-describedby="dialog1Desc">
  <h2 id="dialog1Title">Your personal details were successfully updated</h2>
  <p id="dialog1Desc">You can change your details at any time in the user account section.</p>
  <button>Close</button>
</div>
```

- - - 

##`aria-live` (property)

Update the reader if content in this `div` has changed.

> The `aria-live` property indicates a section within the content that is live and the verbosity in which changes shall be announced. The following values may be used to determine the verbosity.

> - **`aria-live="off"`**:
The default value that indicates that a region is not live, and changes will not be announced.

> - **`aria-live="polite"`**:
The update should be announced at the next graceful interval, such as when the user stops typing.

> - **`aria-live="assertive"`**: 
The update is announced to the user immediately. As this is obtrusive, a value of assertive should only be used when the update is important and the user should be informed immediately.

Source: [http://juicystudio.com/article/wai-aria_live-regions_updated.php](http://juicystudio.com/article/wai-aria_live-regions_updated.php)


--


> To create a live region, the developer adds the aria-live property to the element with a value of `off`, `polite`, `assertive`, or `rude`. The value, or politeness level (or alternatively the intrusiveness level), specifies what a screen reader should do when the element is updated.

>A value of off (`aria-live="off"`) tells the screen reader to not announce the update. If/when the screen reader user encounters the updated content, it will be read at that time. This would be used for non-important or irrelevant content updates.
A value of **`polite`** will notify the user of the content change as soon as he/she is done with the current task. This might take the form of a beep or an audio indication of the update. The user can then choose to directly jump to the updated content. This value would be the most common for content updates, especially for things like status notification, weather or stock updates, chat messages, etc.

>An aria-live value of **`assertive`** will result in the user being alerted to the content change immediately or as soon as possible. Assertive would be used for important updates, such as error messages

>You can also define which content should be read when an update occurs. Additionally, there are special ARIA roles that define certain types of highly dynamic content, such as alerts, logs, and timers. The high level of fidelity with ARIA live regions allows great flexibility both for developers and for end users.

Source: [http://webaim.org/techniques/aria/](http://webaim.org/techniques/aria/)


- - -

##`aria-atomic` (property)

Re-read everything in this div if the content is updated. Related back to `aria-live`.

>The `aria-atomic` property is an optional property that can have the values true or false (default). When the region is updated, the atomic property is used to indicate if assistive technologies should present all or part of the changed region to the user, and is influenced by the aria-relevant property. If the aria-atomic property is set to true, assistive technologies should present the entire region as a whole depending on the aria-relevant property; otherwise, the part of the region that changed might be announced on its own.

>Sometimes, updates make sense on their own, such as a new line arriving in a chat application. Other times, changes in the content may not make sense without the context of other parts of the region. In these cases, aria-atomic="true" should be set on the relevant container so the region is presented as a whole. In the following example, if a change is made anywhere in the div element, the whole content is announced to the user.

Source: [http://juicystudio.com/article/wai-aria_live-regions_updated.php](http://juicystudio.com/article/wai-aria_live-regions_updated.php)


- - -

##`aria-relevant` (Property)


> The `aria-relevant` property is an optional property used to indicate the type of update that should be announced within a region: see changes to document content or node visibility for technical details. The aria-relevant property accepts a space separated list of the following property values:

> **`aria-relevant="additions"`**:
Announcements are made when elements are added to the DOM within the region or the CSS display state reveals hidden text in the region.

> **`aria-relevant="removals"`**:
Announcements are made when elements are removed from the DOM within the region or the CSS display state hides text in the region.

> **`aria-relevant="text"`**
Announcements are made when text is added or removed from the DOM or the CSS display state changes.
`aria-relevant="all"`

>All of the above (additions, removals, text) apply to this region.
In the absence of an explicit aria-relevant property, the default is to assume there are text changes and additions (aria-relevant="text additions"). In the following example, only additions to the unordered list will be announced to the user.

Source: [http://juicystudio.com/article/wai-aria_live-regions_updated.php](http://juicystudio.com/article/wai-aria_live-regions_updated.php)

- - -

##`tabindex` (property)

Sets the order of the object when tabbing through the page.

The couple exceptions:

>**`tabindex="0"`**: A value of 0 indicates that the element should be placed in the default navigation order. This allows elements that are not natively focusable (such as `<div>`, `<span>`, and `<p>`) to receive keyboard focus. Of course one should generally use links and form controls for all interactive elements, but this does allow other elements to be focusable and trigger interaction.

>**`tabindex="-1"`**: removes the element from the default navigation flow (i.e., a user cannot tab to it), but it allows it to receive programmatic focus, meaning focus can be set to it from a link or with scripting. This can be very useful for elements that should not be tabbed to, but that may need to have focus set to them. A good example is a modal dialog window - when opened, focus should be set to the dialog so a screen reader will begin reading and the keyboard will begin navigating within the dialog. Because the dialog (probably just a `<div>` element) is not focusable by default, assigning it tabindex="-1" allows focus to be set to it with scripting when it is presented.

Source: [http://webaim.org/techniques/keyboard/tabindex](http://webaim.org/techniques/keyboard/tabindex)

- - -

##`aria-expanded` (state)

Is this `element` expanded? True or false.

Used on collapsable objects, such as a “Read more” link that exposed the rest of an article on that page…or a navigation item expanding to show the sub-menu.

Additional Resources: [http://heydonworks.com/practical_aria_examples/](http://heydonworks.com/practical_aria_examples/#progressive-collapsibles)

- - -

##`aria-controls` (property)

Works in tandem with `aria-expanded`. It identifies that “this button or link controls that object — based on the ID”.

Also used for tabs, checkboxes, etc.

>Identifies the element (or elements) whose contents or presence are controlled by the current element. See related aria-owns.

>For example:

>A table of contents tree view may control the content of a neighboring document pane.
A group of checkboxes may control what commodity prices are tracked live in a table or graph.
A tab controls the display of its associated tab panel.

Source: [http://www.w3.org/TR/wai-aria/states_and_properties#aria-controls](http://www.w3.org/TR/wai-aria/states_and_properties#aria-controls)

###An Example of Mobile Navigation Button

```
<button class="secondary-toggle toggled-on" aria-expanded="true" aria-controls="secondary">Menu and widgets</button>
<div id="secondary" class="secondary toggled-on" aria-expanded="true">

<nav id="site-navigation" class="main-navigation" role="navigation">
	<div class="menu-demo-menu-container">
		<ul id="menu-demo-menu" class="nav-menu">
			<li><a href="/about-twenty-fifteen/">About Twenty Fifteen</a></li>
			<li><a href="/readability/">Readability</a></li>
			<li><a href="/a-parent-page/">A Parent Page</a>
				<button class="dropdown-toggle" aria-expanded="false">
					<span class="screen-reader-text">expand child menu</span>
				</button>
				<ul class="sub-menu">
					<li>
						<a href="/a-parent-page/first-child/">First Page</a>
						<button class="dropdown-toggle" aria-expanded="false">
							<span class="screen-reader-text">expand child menu</span>
						</button>
						<ul class="sub-menu">
							<li><a href="/a-parent-page/second-child/a-grandchild-page/">A Grandchild Page</a></li>		
						</ul>
					</li>
				</ul>
			</li>
		</ul>
	</div>			
</nav>
```

- - -

#Code Examples

- [Accessible Modal Popup](http://codepen.io/scottohara/pen/lIdfv)
- [aria-label for Read More](http://codepen.io/joe-watkins/pen/xaDbJ)
- [Hidden Skip to Content Link](http://codepen.io/joe-watkins/pen/rjhiK)

- - -

##Accessibility Checklist




[http://a11yproject.com/checklist.html](http://a11yproject.com/checklist.html)

- - -


##Section 508 Requirements Checklist

There are 16 criteria in this subsection which cover the range of impairments listed in the Functional Performance Criteria.

- A text equivalent for every non-text element shall be provided (e.g., via "alt", "longdesc", or in element content).
- Equivalent alternatives for any multimedia presentation shall be synchronized with the presentation.
- Web pages shall be designed so that all information conveyed with color is also available without color, for example from context or markup.
- Documents shall be organized so they are readable without requiring an associated style sheet.
- Redundant text links shall be provided for each active region of a server-side image map.
- Client-side image maps shall be provided instead of server-side image maps except where the regions cannot be defined with an available geometric shape.
- Row and column headers shall be identified for data tables.
- Markup shall be used to associate data cells and header cells for data tables that have two or more logical levels of row or column headers.
- Frames shall be titled with text that facilitates frame identification and navigation.
- Pages shall be designed to avoid causing the screen to flicker with a frequency greater than 2 Hz and lower than 55 Hz.
- A text-only page, with equivalent information or functionality, shall be provided to make a web site comply with the provisions of this part, when compliance cannot be accomplished in any other way. The content of the text-only page shall be updated whenever the primary page changes.
- When pages utilize scripting languages to display content, or to create interface elements, the information provided by the script shall be identified with functional text that can be read by assistive technology.
- When a web page requires that an applet, plug-in or other application be present on the client system to interpret page content, the page must provide a link to a plug-in or applet that complies with §1194.21(a)
- When electronic forms are designed to be completed on-line, the form shall allow people using assistive technology to access the information, field elements, and functionality required for completion and submission of the form, including all directions and cues.
- A method shall be provided that permits users to skip repetitive navigation links.
- When a timed response is required, the user shall be alerted and given sufficient time to indicate more time is required.

To get a better handle on these requirements they can be summarized with the following list of 11 topics.

- Provide alternative text for all images, or in the case of image maps, provide plain text links
- Do not depend on color alone for communicating information
- The logical flow of the page should follow the source code, or DOM.
- Data tables should have headings
- Frames should have titles
- Avoid flickering on the screen between 2-55 Hz
- Content displayed with scripts must be accessible
- Content delivered via plugins must be accessible
- Online forms must be coded correctly
- Provide a way for users to skip repetitive navigation links
- Allow users to adjust the time permitted for timed responses

Source: [https://accessibility.oit.ncsu.edu/training/accessibility-handbook/508.html](https://accessibility.oit.ncsu.edu/training/accessibility-handbook/508.html)
