<style>
body {
  font: 18px/1.5 sans-serif;
  padding: 1rem;
}

dt {
  font-weight: bold;
}

dl {
  margin-bottom: 50px;
}

#bug:target {
  outline: 4px solid #ccc;
}

/**
 * tab panel widget
 */
.tabPanel-widget {
  position: relative;  /* containing block for headings (top:0) */
  background: #999;
}

/**
 * because labels come first in source order - we use z-index to move them in front of the headings
 */
.tabPanel-widget > label {
  position: absolute;
  z-index: 1;
}

/**
 * labels and headings must share same values so grouping declarations in this rule prevents async edits (risk of breakage)
 * line-height == height -> vertical centering
 * the width dictates the offset for all headings but the first one: left offset = width * number of previous heading(s)
 * note that width and offset of label/heading pair can be customized if necessary
 */

.tabPanel-widget > label,
.tabPanel-widget > h2 {
  font-size: 1.1em;
  width: 9em;
  height: 2em;
  line-height: 2em;
}

/**
 * position:relative is for the markers (the down arrow in tabs)
 */
.tabPanel-widget > h2 {
  position: relative;
  margin: 0;
  text-align: center;
  background: #999;
  color: #fff;
}

.tabPanel-widget > label {
  border-right: 1px solid #fff;  
}

/**
 * all first level labels and headings after the very first ones 
 */
.tabPanel-widget > label ~ label,
.tabPanel-widget > h2 ~ h2 {
  position: absolute;
  top: 0;
}


/**
 * We target all the label/heading pairs
 * we increment the :nth-child() params by 4 as well as the left value (according to "tab" width)
 */

.tabPanel-widget label:nth-child(1),
.tabPanel-widget h2:nth-child(3) {
  left: 0em;
}

.tabPanel-widget label:nth-child(5),
.tabPanel-widget h2:nth-child(7) {
  left: 9em;
}

.tabPanel-widget label:nth-child(9),
.tabPanel-widget h2:nth-child(11) {
  left: 18em;
}

/**
 * we visually hide all the panels
 * https://developer.yahoo.com/blogs/ydn/clip-hidden-content-better-accessibility-53456.html
 */
.tabPanel-widget input + h2 + div {
  position: absolute !important;
  clip: rect(1px, 1px, 1px, 1px);
  padding:0 !important;
  border:0 !important;
  height: 1px !important; 
  width: 1px !important; 
  overflow: hidden;
}
/**
 * we reveal a panel depending on which control is selected 
 */
.tabPanel-widget input:checked + h2 + div {
  position: static !important;
  padding: 1em !important;
  height: auto !important; 
  width: auto !important; 
}

/**
 * shows a hand cursor only to pointing device users
 */
.tabPanel-widget label:hover {
  cursor: pointer;
}

.tabPanel-widget > div {
  background: #f0f0f0;
  padding: 1em;
}

/**
 * we hide radio buttons and also remove them from the flow
 */
.tabPanel-widget input[name="tabs"] {
  opacity: 0;
  position: absolute;
}


/** 
 * this is to style the tabs when they get focus (visual cue)
 */

.tabPanel-widget input[name="tabs"]:focus + h2 {
  outline: 1px dotted #000;
  outline-offset: 10px;
}


/**
 * reset of the above within the tab panel (for pointing-device users)
 */
.tabPanel-widget:hover h2 {
  outline: none !important;
}

/**
 * visual cue of the selection
 */
.tabPanel-widget input[name="tabs"]:checked + h2 {
  background: #333;
}

/**
 * the marker for tabs (down arrow)
 */
.tabPanel-widget input[name="tabs"]:checked + h2:after {
  content: '';
  margin: auto;
  position: absolute;
  bottom: -10px;
  left: 0;
  right: 0;
  width: 0;
  height: 0;
  border-left: 10px solid transparent;
  border-right: 10px solid transparent;
  border-top: 10px solid #333;
}

/**
 * Make it plain/simple below 45em (stack everything)
 */
@media screen and (max-width: 45em) {
  
  /* hide unecessary label/control pairs */
  .tabPanel-widget label,
  .tabPanel-widget input[name="tabs"] {
    display: none;
  }
  
  /* reveal all panels */
  .tabPanel-widget > input + h2 + div {
    display: block !important;
    position: static !important;
    padding: 1em !important;
    height: auto !important; 
    width: auto !important; 
  }
  
  /* "unstyle" the heading */
  .tabPanel-widget h2 {
    width: auto;
    position: static !important;
    background: #999 !important;
  }
  
  /* "kill" the marker */
  .tabPanel-widget h2:after {
    display: none !important;
  }

}
</style>

<p><a href="https://tabpanelwidget.com">
  TabPanelWidget</a> is a Semantic, Accessible, Responsive, and Versatile solution to create Tabpanel and Accordion Widgets for the Web.<br>
<a href="https://tabpanelwidget.com">
  Check it out!</a></p>  
<h1 class="">Pure CSS Tab Panel</h1>
<p>This is mostly a proof of concept. Remember that most "Pure CSS" solutions are rarely Accessible.</p>
  <div class="tabPanel-widget">
    <label for="tab-1" tabindex="0"></label>
      <input id="tab-1" type="radio" name="tabs" checked="true" aria-hidden="true">
    <h2>Strong</h2>
    <div>
      <p>Represents strong importance for its contents. Indicate relative importance by nesting strong elements; each strong element increases the importance of its contents. Changing the importance of a piece of text with the strong element does not change the meaning of the sentence.</p>
      <p>Source: <a href="http://html5doctor.com/element-index/">html5doctor</a> for Strong</p>
    </div>
    <label for="tab-2" tabindex="0"></label>
    <input id="tab-2" type="radio" name="tabs" aria-hidden="true">
    <h2>Section</h2>
    <div>
      <p>Represents a generic document or application section. In this context, a section is a thematic grouping of content, typically with a header, possibly with a footer. Examples include chapters in a book, the various tabbed pages in a tabbed dialog box, or the numbered sections of a thesis. A web site's home page could be split into sections for an introduction, news items, contact information.</p>
      <p>Source: <a href="http://html5doctor.com/element-index/">html5doctor</a> for Section</p>
    </div>
    <label for="tab-3" tabindex="0"></label>
    <input id="tab-3" type="radio" name="tabs" aria-hidden="true">
    <h2>Source</h2>
    <div>
      <p>The source element allows authors to specify multiple alternative media resources for media elements. It does not represent anything on its own. The src attribute gives the address of the media resource. The value must be a valid non-empty URL potentially surrounded by spaces. This attribute must be present.</p>
      <p>Source: <a href="http://html5doctor.com/element-index/">html5doctor</a> for Source</p>
    </div>
  </div>
<p>This <a href="http://cssmojo.com">link</a> is here to better test sequential navigation.</p>
