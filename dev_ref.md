# Reference for Developers
Reference for the R files and their functions, .csv file formatting, and Shinyapps.io documentation.

___

## R Files and Their Functions
This section will briefly go over the R files used and the functions within their code.

### Structural Files
Files that are important and necessary to running the webpage. The glue to all the features.

#### app.R

Used to compile the Shinyapps application on RStudio. This is the file that is used to run and publish the actual webpage.
Tells the webpage what libraries to use and the files to be executed.

#### app_server.R

Manages inputs and outputs for each tab and what to display, connecting user interface outputs to the functions that can compute the results needed.

#### app_ui.R

Creates the UI for the webpage.

Acts as the top level or “highest” hierarchical file for the webpage and creates the many tabs, text boxes, and tables seen on the webpage.

### Feature Files
Files that host the main features that make up the webpage.

#### albums_by_band.R

This file is used find albums by a certain band, calculate their mean rating, and the total number of albums in their discography.

Functions Present:

* `albums_by_bands`
    * Grabs the album information from a given artist/band (album name, year, and rating).
    * Function input is artist/band name.
* `band_mean_rating`
    * Calculates the mean rating for an artist/band’s albums and prints the result.
	* Function input is artist/band name.
* `band_album_count`
    * Calculates the total number of albums an artist/band has and prints the result.
	* Function input is artist/band name.

#### albums_by_year.R

This file is used to list the top ranked albums for a given year from highest to lowest.

Functions Present:

* `year_albums`
    * Lists the top ranked albums from highest to lowest for a given year.
	* Function input is a given year.

#### compare_bands.R

This file visually compares two artists’/bands’ ratings over the span of their albums in the database.

Functions Present:

* `band_album_comparison_chart`
    * Grabs the album data from two artists/bands and displays their ratings on a line graph using ggplot.
    * Function input is the first artist/band name, and then the second artist/band name.

![compare_example.png](/images/compare_example.png)

**Example of band_album_comparison_chart(Elliot Smith, Acid House Kings)**

#### fav_bands.R

This file display up to 15 bands with the highest average rating with a given number of albums, with the option to include EPs and Live albums in the count.

Functions Present:

* `favorite_bands`
    * Determines if the count should include EPs and Live Albums and then counts the number of albums that the artist/band has, calculates the average rating, and then filters out all the artists/bands in the database that do not meet the album count specified by the user.
	* Function input is the minimum albums an artist/band should have for consideration, and a Boolean `live_ep.var` for if EPs and Live albums should be counted.

![excluded.png](/images/excluded.png) ![included.png](/images/included.png)

**Example of excluded vs not excluded**

#### home.R

This file is used to grab basic counting information about the user’s music database.

Functions Present:

* `total_album_count`
	* Counts the total number of albums in the database and prints the result.
	* No function input.
* `total_band_count`
	* Counts the total number of artists/bands in the database and prints the result.
	* No function input.
* `most_pop_artist`
	* Finds the artist/band with the most albums in the database and prints the result.
	* No function input.

#### number_one_albums.R

This file is used to find the number one ranked album per year in a given range specified by the user.

Functions Present:

* `number_one_album`
	* Finds the number one albums for each year in a specified range by the user.
	* Function input takes in the range of years to consider from a starting year to an ending year as two inputs.

![num1.png](/images/num1.png)

**Example of number_one_album(2003, 2006)**

#### vinyl.R

This file is used to find the user’s unowned vinyl that they have highly ranked.

Functions Present:

* `missing_vinyl`
	* Finds the vinyl that the user does not own given a rating cutoff.
	* Function input takes in the minimum rating to be considered.

---

## Format for .csv Files

The format is: Year, Ranking, Album, Artist, Rating, Vinyl, EP, Live. Respectively each column takes the following data inputs:

* Year: int
* Ranking: int
* Album: String
* Artist: String
* Rating: int
* Vinyl: String `v` if applicable
* EP: String `EP` if applicable
* Live: String `Live` if applicable

> Note: When formating for My Favorite Albums the **Vinyl**, **EP**, and **Live** columns are optional and do not need to be filled. This can be denoted by `,,` indicating that the column in empty.
If commas are a part of the album title, the name can be encased in quotes `"Everybody Else Is Doing It, So Why Can't We"`.

```csv
Year,Ranking,Album,Artist,Rating,Vinyl,EP,Live
1993,1,August and Everything After,Counting Crows,10,v,,
1993,2,Siamese Dream,The Smashing Pumpkins,9,v,,
1993,3,Cure for Pain,Morphine,9,v,,
1993,4,"Everybody Else Is Doing It, So Why Can't We?",The Cranberries,8,v,,
1993,5,Debut,Bjork,8,v,,
```

---

## Shinyapps.io Documentation

Here is a link to the Shinyapps.io official documentation: [Shinyapps.io](https://docs.posit.co/shinyapps.io/guide/)
