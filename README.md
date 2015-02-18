Using: https://github.com/gf3/Levenshtein

```
var search1 = "I like to eat Brians"; // Search String (Example)
var search2 = "brians"; // Search String 2 (Example)
var title1 = "I like to eat brains"; // Blog Title (Example)
```

VERSION 1
Full string search:
```
	var ver1 = new Levenshtein(search1.toLowerCase(), title1.toLowerCase()); // Convert strings to lower case to reduce the distance, allowing cleaner searches.
	var calc1 = ver1.distance / string1.length * 100; // Gives a percentage based difference between the strings, as opposed to a number
	if(calc1.toFixed(2) < 35) { // I chose 35 as it's a leniency I thought worked, obviously you could be more exact or less exact for comparison.
		// Insert code to do if it's true.
	}
	// Insert code to do if it's false.
```
	
	
VERSION 2
Word by word search: (Good for searching via multiple words)
```
	var compare1 = search2.toLowerCase().split(" "); // Split string into an array
	var compare2 = title1.toLowerCase().split(" "); // Split string into an array
	var results = [];
		
	for(var i = 0; i < compare1.length; i++) {
			
		for(var j = 0; j < compare2.length; j++) {
			var lev = new Levenshtein(compare1[i], compare2[j]);
			var calc = ((lev.distance / len) * 100).toFixed(2);
			if(calc < 35) {
				results.push({'search':compare1[i], 'compare':compare2[j]}); // Add to result
			}
		}
			
	}
```
	
EXAMPLE
Simple search on a blog for article titles
```
	$("#search-btn").click(function() {
		var news_items = [{'title':'Apple'}, {'title':'Banana'}, {'title':'Chocolate'}]; // Example Object
		var search_items = []; // Array for searching against
		var val = $("#search").val().split(" "); // Get value from input and split it
			
		for(var i = 0; i < news_items.length; i++) {
			var title = news_items[i].title.split(" "); // For a real example, a blog title will tend to have spaces.
				
			for(var j = 0; j < title.length; j++) { // For each word in the title, lets see if there is a match
				
				for(var k = 0; k < val.length; k++) { // Compare against the search value array
					
					var len = val[k].length; // For the distance percentage calculation.
					var lev = new Levenshtein(val[k].toLowerCase(), title[j].toLowerCase()); // Lets compare the two values, once again lowercase to reduce unneeded distance
					var calc = lev.distance / len * 100; // Convert to a nice percentage
						
					if(calc.toFixed(2) < 35) { // As said before, 35% is personal preference.
						search_items.push(news_items[i]); // It was close enough, lets add it to the search
						break;
					}
					
				}
			}
		}
		// Clean up search_items and ensure no duplicates (unless you want it)
		searchFunc(); // Do your search, using your new 'search_items'
	});
```
