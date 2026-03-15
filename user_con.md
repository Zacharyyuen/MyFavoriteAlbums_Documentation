# Getting Started with My Favorite Albums
A brief introduction to the webpage where users can become familiar with the feature list and the data used by My Favorite Albums.

---

## What is My Favorite Albums?
This web browser application strives to visualize and organize your favorite albums so that you can easily view how your music tastes have changed over the years. There are many different features to try in this software such as:
- **Number One Albums:** Displays your #1 ranked album over each year
- **Top Albums by Year:** Displays your album rankings for a given year
- **Artists’ Albums:** Displays an artists’ albums in your collection
- **Favorite Artists:** Displays ranked artists filtered by number of albums
- **Artists Comparison:** Compares two artists’ ratings over the years of their albums
- **Vinyl:** Displays vinyl not owned but are highly rated by you

Each feature has its own tab on the webpage, and will give insight into how you listen to music.

![Tabs.png](/images/Tabs.png)

#### .csv Files
This application cannot automatically pull from your default music listening app, and instead retrieves data from a manually inputted .csv file. 
A .csv file is a plain text file that can store tabular data by separating each point of the data with a comma. Hence, the abbreviated name csv
which stands for Comma-Separated Values. You can update and change the album dataset being analyzed by importing a new .csv file. 

Here is a tutorial on how you can make your own .csv file: [Creating a .csv File](/dev_task#creating-a-csv-file).

---

## Understanding Album Data
To interpret the information shown to you on a given feature, it is important that you understand the data presented, and what the definitions of each are. Here are the common points of data used to classify albums:
- **Year:** The year the album was released
- **Ranking:** Where the album ranks in a given year given your personal rating
- **Name:** The name of a given album
- **Artist/Band:** The name of a given artist/band
- **Rating:** The rating you gave a given album on a 1 to 10 scale
- **Vinyl:** If you own the album on vinyl
- **Extended Play (EP):** A music release longer than a single but shorter than an album
- **Live:** If the album is a live recording
