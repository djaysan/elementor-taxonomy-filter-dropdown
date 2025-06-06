# elementor-taxonomy-filter-dropdown
Use elementor Taxonomy widget as a dropdown instead of horizontal
What you need to adjust:
✅ Give each Elementor taxonomy filter widget a specific class in Elementor (easy via Advanced → CSS Classes).
For example:

.tax-instruments for the Instrument filter widget (remove dot in front)

.tax-programs for the Program filter widget (remove dot in front)

✅ Then the JS can separately process each one into its respective dropdown.

Summary:
You can reuse your original code logic, just wrap it in a function and call it twice — once per taxonomy.


HTML Widget #1 → Instruments dropdown:
```
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

HTML Widget #2 → Programs dropdown:
```
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


OPTIONAL:
Custom order of taxonomies
Example usage in your Programs dropdown script:
Replace this part:
```
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
👉 With this:

```
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
