# Overview For Developers
Focuses on the nitty and gritty of the code, IDE, and data used to present the beautiful user interface of My Favorite Albums. 
It is recommended that you are proficient in the coding language R and the IDE RStudio before attempting to develop additional 
features for this software.

___

## R and RStudio
My Favorite Albums is written using the R language. The recommended coding environment for updating and adding code to 
the existing files is RStudio. The reason RStudio is preferred is that you can directly upload your code to a hosted 
server through Shinyapps.io.

#### More on R (for those unfamiliar)
The language R is used for data analysis and statistical computations. To make certain computations or searching easier, 
users can implement packages/libraries to make these processes more efficient. In the case of My Favorite Albums, R will be 
used to analyze the album dataset to interpret user listening patterns.

---

## Shinyapps.io
Shinyapps.io is a web app tool that allows users to upload their own R code from RStudio into a web browser. Shinyapps.io 
manages all the server, security, and scaling for your application, making it easy to set up and share.

You only need a Shinyapps.io account to set this up, so on your end you just need to worry about connecting RStudio to Shinyapps.io.

---

## What is a .csv File?
My Favorite Albums uses the .csv file format to input album data. “csv” stands for Comma-Separated Values, and is a plain text 
file that stores tabular data by separating each point of data with a comma. To input album data into the program, a .csv file 
must be created with information formatted to match expected inputs from the R code.

The .csv file will store the following data:
- **Year:** The year the album was released
- **Ranking:** Where the album ranks in a given year given the user’s personal rating
- **Name:** The name of a given album
- **Artist/Band:** The name of a given artist/band
- **Rating:** The rating the user gave a given album on a 1 to 10 scale
- **Vinyl:** If the user owns the album on vinyl
- **Extended Play (EP):** A music release longer than a single but shorter than an album
- **Live:** If the album is a live recording

> Note: This data is not automatically extracted from music listening platforms and must be extracted manually.

---

## Current Feature List
Please become familiar with the current features on My Favorite Albums. Each one provides unique insight to the user’s music taste. 
It is important to know what each feature does as to not create similar/duplicate ones.


- **Number One Albums:** Displays the users #1 ranked album over each year
- **Top Albums by Year:** Displays the users album rankings for a given year
- **Artists’ Albums:** Displays an artists’ albums in the users collection
- **Favorite Artists:** Displays ranked artists filtered by number of albums
- **Artists Comparison:** Compares two artists’ ratings over the years of their albums
- **Vinyl:** Displays vinyl not owned but are highly rated by the user

Each feature is given its own tab on the webpage, so please follow the tab format below for consistency.

![Tabs.png](/images/Tabs.png)