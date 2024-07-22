The index.html files consists simple text editor which changes dynamically according to the changes done by the user.
This application is made using front end technologies like HTML,CSS,JavaScript
This application is done with default fonts since it is not loading the fonts with API

Unit Test of each section of the code

<head> Section:
Contains metadata and styling (<style> block) for the HTML document, defining how elements in the text editor will be displayed.

Font Controls (<div class="font-controls">):

Provides UI elements for selecting font family (<select id="fontFamily">), font weight (<select id="fontWeight">), and an italic checkbox (<input type="checkbox" id="italicCheckbox">).

Text Editor (<textarea id="editor">):

A textarea element where users can input and edit text. It has an id of editor for easy identification in JavaScript.
Button Container (<div class="button-container">):

Contains buttons (<button>) for saving (id="saveBtn") and resetting (id="resetBtn") the text editor content.
JavaScript (<script> block):

JavaScript Code (Inside <script> Block):



  // Function to set font styles on the editor
  function setEditorFontStyle(fontFamily, fontWeight, isItalic) {
    editor.style.fontFamily = fontFamily;
    editor.style.fontWeight = fontWeight;
    editor.style.fontStyle = isItalic ? 'italic' : 'normal';
  }

  // Event listener for font family selection change
  fontFamilySelector.addEventListener('change', function() {
    const selectedFamily = fontFamilySelector.value;
    const selectedWeight = fontWeightSelector.value;
    const selectedItalic = italicCheckbox.checked;

    // Get font variants based on selected family
    const fontVariants = getFontVariants(selectedFamily);

    // Find closest variant based on selected options
    let selectedVariant = { weight: selectedWeight, italic: selectedItalic };
    selectedVariant = findClosestVariant(fontVariants, selectedVariant);

    // Update font weight selector based on available variants
    updateFontWeightSelector(fontVariants);

    // Apply selected font style to the editor
    setEditorFontStyle(selectedFamily, selectedVariant.weight, selectedVariant.italic);
  });

  // Event listener for font weight selection change
  fontWeightSelector.addEventListener('change', function() {
    const selectedFamily = fontFamilySelector.value;
    const selectedWeight = fontWeightSelector.value;
    const selectedItalic = italicCheckbox.checked;

    const fontVariants = getFontVariants(selectedFamily);
    let selectedVariant = { weight: selectedWeight, italic: selectedItalic };
    selectedVariant = findClosestVariant(fontVariants, selectedVariant);

    setEditorFontStyle(selectedFamily, selectedVariant.weight, selectedVariant.italic);
  });

  // Event listener for italic checkbox change
  italicCheckbox.addEventListener('change', function() {
    const selectedFamily = fontFamilySelector.value;
    const selectedWeight = fontWeightSelector.value;
    const isItalic = italicCheckbox.checked;

    const fontVariants = getFontVariants(selectedFamily);
    let selectedVariant = { weight: selectedWeight, italic: isItalic };
    selectedVariant = findClosestVariant(fontVariants, selectedVariant);

    setEditorFontStyle(selectedFamily, selectedVariant.weight, selectedVariant.italic);
  });

  // Event listener for save button click
  saveBtn.addEventListener('click', function() {
    const textContent = editor.value;
    localStorage.setItem('textEditorContent', textContent);
    alert('Text saved!');
  });

  // Event listener for reset button click
  resetBtn.addEventListener('click', function() {
    editor.value = '';
    editor.style.fontFamily = '';
    editor.style.fontWeight = '';
    editor.style.fontStyle = 'normal';
    localStorage.removeItem('textEditorContent');
    alert('Text cleared!');
  });

  // Initialize editor content from local storage if available
  const savedContent = localStorage.getItem('textEditorContent');
  if (savedContent) {
    editor.value = savedContent;
  }
 

  // Function to find closest font variant based on selected options
  function findClosestVariant(variants, selectedVariant) {
    const selectedWeight = selectedVariant.weight;
    const selectedItalic = selectedVariant.italic || false;

    // Check if exact selected variant exists
    const selectedExists = variants.some(variant =>
      variant.weight === selectedWeight && variant.italic ===





