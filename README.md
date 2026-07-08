# Elementor taxonomy filter dropdown

Turns Elementor's Taxonomy Filter widget into a dropdown (select) instead of the default horizontal button list. Works with multiple filter widgets on the same page, one dropdown per taxonomy.

## Setup

1. Give each Elementor taxonomy filter widget its own CSS class (Advanced tab, CSS Classes, without the leading dot). For example:
   - `tax-instruments` for the Instrument filter widget
   - `tax-programs` for the Program filter widget
2. Add one HTML widget per taxonomy with the matching code below. The script reads the widget's filter buttons, builds the dropdown options, and clicks the matching button when a selection is made.

You can reuse the same logic for any number of taxonomies: wrap it in its own HTML widget and change the class name and dropdown ID.

### HTML widget 1: Instruments dropdown

```html
<!-- Instruments Dropdown -->
<label for="instrument-dropdown">Instrument</label>
<select id="instrument-dropdown">
    <option value="">Select Instrument</option>
</select>

<style>
    label {
        font-size: 12px;
        text-transform: uppercase;
        color: #222222;
        letter-spacing: 0.5px;
        padding-bottom: 6px;
        display: block;
    }

    select {
        padding: 0px;
        border-radius: 0px;
        margin-bottom: 10px;
        min-width: 200px;
        border-width: 0px;
        border-bottom-width: 1px;
    }
</style>

<script>
document.addEventListener("DOMContentLoaded", function() {
    var taxonomyButtons = document.querySelectorAll('.tax-instruments .e-filter-item');
    var dropdown = document.getElementById('instrument-dropdown');

    var allOption = document.createElement('option');
    allOption.value = "__all";
    allOption.text = "All";
    dropdown.appendChild(allOption);

    taxonomyButtons.forEach(function(button) {
        var filterValue = button.getAttribute('data-filter');
        if (filterValue !== "__all") {
            var option = document.createElement('option');
            option.value = filterValue;
            option.text = button.textContent;
            dropdown.appendChild(option);
        }
    });

    dropdown.addEventListener('change', function() {
        var selectedFilter = this.value;
        if (selectedFilter) {
            taxonomyButtons.forEach(function(button) {
                if (button.getAttribute('data-filter') === selectedFilter) {
                    button.click();
                }
            });
        }
    });
});
</script>
```

### HTML widget 2: Programs dropdown

```html
<!-- Programs Dropdown -->
<label for="program-dropdown">Program</label>
<select id="program-dropdown">
    <option value="">Select Program</option>
</select>

<style>
    label {
        font-size: 12px;
        text-transform: uppercase;
        color: #222222;
        letter-spacing: 0.5px;
        padding-bottom: 6px;
        display: block;
    }

    select {
        padding: 0px;
        border-radius: 0px;
        margin-bottom: 10px;
        min-width: 200px;
        border-width: 0px;
        border-bottom-width: 1px;
    }
</style>

<script>
document.addEventListener("DOMContentLoaded", function() {
    var taxonomyButtons = document.querySelectorAll('.tax-programs .e-filter-item');
    var dropdown = document.getElementById('program-dropdown');

    var allOption = document.createElement('option');
    allOption.value = "__all";
    allOption.text = "All";
    dropdown.appendChild(allOption);

    taxonomyButtons.forEach(function(button) {
        var filterValue = button.getAttribute('data-filter');
        if (filterValue !== "__all") {
            var option = document.createElement('option');
            option.value = filterValue;
            option.text = button.textContent;
            dropdown.appendChild(option);
        }
    });

    dropdown.addEventListener('change', function() {
        var selectedFilter = this.value;
        if (selectedFilter) {
            taxonomyButtons.forEach(function(button) {
                if (button.getAttribute('data-filter') === selectedFilter) {
                    button.click();
                }
            });
        }
    });
});
</script>
```

## Optional: custom order of options

To control the order of the dropdown options, replace this part of the script:

```js
taxonomyButtons.forEach(function(button) {
    var filterValue = button.getAttribute('data-filter');
    if (filterValue !== "__all") {
        var option = document.createElement('option');
        option.value = filterValue;
        option.text = button.textContent;
        dropdown.appendChild(option);
    }
});
```

with this:

```js
var desiredOrder = [
    "performance",
    "chamber-music",
    "staff-accompanist",
    "conducting",
    "artist-in-residence"
];

desiredOrder.forEach(function(filterValue) {
    taxonomyButtons.forEach(function(button) {
        if (button.getAttribute('data-filter') === filterValue) {
            var option = document.createElement('option');
            option.value = filterValue;
            option.text = button.textContent;
            dropdown.appendChild(option);
        }
    });
});
```

## Support

If this saved you time, you can support my work:

[<img src="https://storage.ko-fi.com/cdn/kofi2.png?v=6" alt="Buy Me a Coffee at ko-fi.com" height="36">](https://ko-fi.com/H2H81I6YY1)
