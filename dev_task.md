# Walkthroughs For Developers
This section focuses on the structural foundation that runs My Favorite Albums, allowing developers to create their own features and
deploy their own version of My Favorite Albums.

---

## Packages To Install

Listed below are the packages that need to be installed on RStudio and what they do:
```R Console
install.packages('shiny')     // Used to install the Shiny R package
install.packages('rsconnect') // Used to publish webpages from Shinyapps.io
install.packages('dplyr')     // Used to collect/filter grammar data with its provided functions
install.packages('ggplot2')   // Used to create visual graphics such as data plots and graphs
```
These can be directly copied into the RStudio console.

---

## Creating a .csv File
There are many ways to make .csv files, this tutorial covers two of them.

* Manually Making a .csv File 
* Exporting a .csv File From Excel

#### Manually Making a .csv File

1) Open any text editor application (such as Microsoft’s notepad).
2) List the categories for the data in the first line with separated commas.
3) For the proceeding lines enter data in the correct columns to align with the categories in the first line.
4) Save the file as a .csv.

The final file should be formatted like this:
```csv
Year,Ranking,Album,Artist,Rating,Vinyl,EP,Live
1993,1,August and Everything After,Counting Crows,10,v,,
1993,2,Siamese Dream,The Smashing Pumpkins,9,v,,
1993,3,Cure for Pain,Morphine,9,v,,
1993,4,"Everybody Else Is Doing It, So Why Can't We?",The Cranberries,8,v,,
1993,5,Debut,Bjork,8,v,,
```
When formating for My Favorite Albums the **Vinyl**, **EP**, and **Live** columns are optional and do not need to be filled. This can be denoted by `,,` indicating that the column in empty.
If commas are a part of the album title, the name can be encased in quotes `"Everybody Else Is Doing It, So Why Can't We"`.

> Note: Copy the exact format for the data columns. Improper formatting results in incorrect data collection and processing. 

#### Exporting a .csv File From Excel
The below steps assume that you have previously created and formated an Excel spreadsheet with album data.

1) Click **File**.

![excel_file.png](/images/excel_file.png)

2) Click **Export**.

![excel_export.png](/images/excel_export.png)

3) Click **Change File Type**.

![excel_type.png](/images/excel_type.png)

4) Select **CSV**.

![excel_csv.png](/images/excel_csv.png)

Excel then prompts to choose a location to save the file to.

---

## Setting Up Shinyapps.io

1) Make an account at https://www.shinyapps.io/.

2) Once logged in, it takes you to your account dashboard. The dashboard has two tabs, one for setting up Shinyapps.io with R and another for Python. We are using the R tutorial called **Start with R**.

3) Install the rsconnect package from the RStudio console using `install.packages(‘rsconnect’)`.

4) Copy the token and secret from the website to your clipboard. On the Shinyapps.io webpage, it looks like this:

```R Console
rsconnect::setAccountInfo(name='YOUR ACCOUNT NAME',
token='YOUR TOLKEN',
secret='<SECRET>')
```

> Note: When copying to your clipboard, you have the option to **Show Secret** which decrypts your token.

5) Paste the whole line into the RStudio console. This links your Shinyapps.io account to RStudio.

6) Open the app.R file in RStudio, and press **Run App** to open the webpage on your local browser.

![rstudio_run.png](/images/rstudio_run.png)

7) To publish the webpage and make a shareable url, press the **Publish/Republish** button next to run app.

![rstudio_publish.png](/images/rstudio_publish.png)

>Note: If My Favorite Albums is copied directly from Github, please delete the folder named rsconnect. If it is not deleted, 
Shinyapps refuses to publish the webpage because it tries to launch the page from another user's account and not your own.

#### Managing Shinyapp Applications
Applications can be managed from the Shinyapp.io website.
* Clicking on **Dashboard** shows all of your online applications, their online statuses, and quick links to their Shinyapps.io information.
   * Quick links are located underneath **Recent Applications** and under **Name**. **These bring you to the applications homepage on where the webpage url can be grabbed**. It also shows application metrics.
* By clicking on **Applications**, it drops down a menu where you can see your **Running**, **Sleeping**, and **Archived** applications.

![shiny_dash.png](/images/shiny_dash.png)

___

## Making New Functions
This section focuses on how to make new functions to extract data from the .csv file.

Many functions take a similar form to `albums_by_bands` where the primary goal of the function is to acquire data from the .csv file and return it.

```R
# Example Function albums_by_bands

albums_by_bands <- function(band.var){
band_albums <- select(filter(album_data[order(album_data$Year),], Artist==band.var), Album, Year, Rating)
}
```

1) In this example the data is gathered by first specifying how to sort the data. By using the **order** keyword, it defaults to ordering with the years ascending.

```R
album_data[order(album_data$Year),]
```

2) We can then filter the sorted data to only include rows of information with the given condition. The **filter** keyword should only keep rows with the given band name in this case.

```R
filter(album_data[order(album_data$Year),], Artist==band.var)
```

3) For the last step, we can use the **select** keyword to choose the columns of data to keep by listing the column names.

```R
select(filter(album_data[order(album_data$Year),], Artist==band.var), Album, Year, Rating)
```

Using this framework, developers can build new functions to grab information from the data stored in the .csv file.

Some functions have additional calculations such as `band_mean_rating`.

```R
band_mean_rating <- function(band.var){
band_albums <- select(filter(album_data[order(album_data$Year),], Artist==band.var), Album, Year, Rating)
avg_rating <- mean(band_albums$Rating)
print(paste0("Average Rating: ", format(round(avg_rating, 2), nsmall =2)))
}
```
In this case, the average rating is calculated and rounded to two decimal places before being printed. The **$** used in `mean(band_albums$Rating)`
is used to grab the entire rating column for the given artist/band and produce the mean.

___

## Making New Features
A given feature can be comprised of multiple different functions, for example albums_by_band.R

```R
all_bands <- sort(unique(album_data$Artist))

albums_by_bands <- function(band.var){
band_albums <- select(filter(album_data[order(album_data$Year),], Artist==band.var), Album, Year, Rating)
}

band_mean_rating <- function(band.var){
band_albums <- select(filter(album_data[order(album_data$Year),], Artist==band.var), Album, Year, Rating)
avg_rating <- mean(band_albums$Rating)
print(paste0("Average Rating: ", format(round(avg_rating, 2), nsmall =2)))
}

band_album_count <- function(band.var){
band_albums <- select(filter(album_data[order(album_data$Year),], Artist==band.var), Album, Year, Rating)
band_count <-count(band_albums)
print(paste0("Number of Albums Ranked: ", band_count))
}
```

This file comprises multiple different functions, all of which are used to display information on a given feature tab. However, a feature does not necessarily
need more than one function.

**Example output from albums_by_band.R:**

![example_feature.png](/images/example_feature.png)

This example displays how multiple functions for a single feature could be used, displaying the list of albums from the artist/band, 
the number of ranked albums, and the average rating of the band.

#### Populating New Features
To have new features show up on the webpage you must populate the following files:
 
1) **app.R**

Add the feature's file name to app.R

```R
source("file_name.R")
```

2) **app_ui.R**

In this file specify the tab name, the inputs and outputs to be used in the feature, and the labels for each input.

```R
tabPanel("Top Albums by Year",
                 htmlOutput("text4"),
                 selectInput("year", "Choose a year:", all_years),
                 actionButton("action_button2", label = "Submit"),
                 htmlOutput("text5"),
                 tableOutput("year_table")),
```

* `tabPanel` Creates a tab in the tabset layout.
* `htmlOutput` Labels the tab on the application interface.
* `selectInput` Creates a dropdown menu from the list `all_years` with an input variable of `year` and label "Choose a year".
* `actionButton` Creates a button with an input variable of `action_button2` and label "Submit".
* `tableOutput` Creates a table placeholder for output `year_table`.

3) **app_server.R**

Please specify the additional information needed to run the server inputs and outputs through Shinyapps.io.
> Note: Notice how `text4`, `text5`, and `action_button2` are used in the previous code for app_ui.R. Please ensure that these names match between the two files and 
that are not used by other features.

```R
# Second tab - Top Albums By Year
  output$text4 <- renderUI({
    HTML("<h2>Top Albums by Year</h2><br>")
  })

  output$text5 <- renderUI({
    HTML("<br><br>")
  })

  observeEvent(input$action_button2,{

    output$year_table <- renderTable({
      return(year_albums(input$year))
    })

  })
```

The `observeEvent` tells Shinyapps.io to only run the block of code when `action_button2` is clicked. In this case 
it will return a filtered list from the function call `year_albums` with the `input$year` as the input.


___

## How to Write Good Code Comments
Code comments should be kept as concise as possible while providing all the necessary information to tell other 
developers what a function or part of code does.

Good code comments have the following:

* **Behavior** (what the function accomplishes)
* **Exceptions** (what invalid inputs cause errors)
* **Returns** (what the function returns)
* **Parameters** (the function inputs)

Each bullet point should be around one sentence in length and provide enough info for other developers to use the functions.

#### In Line Code Comments

Typically use these to quickly explain confusing or “strange” portions of code. These should be kept to a sentence at max.
