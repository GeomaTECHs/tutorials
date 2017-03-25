![](https://pbs.twimg.com/profile_banners/812364475772837889/1483851647/1500x500)

# Custom Popups Tutorial

**Author:** Brent Thorne <br>
**About:** This will break down how to use hyperlink html code in your leaflet maps in RStudio.<br>
**Youtube video:** [Leaflet Mapping in RStudio - Custom Popups](https://www.youtube.com/watch?v=mTTuUGisxDk)

**[1. Introduction](https://github.com/GeomaTECHs/tutorials/blob/master/custom_popups/add_hyperlinks.md#introduction)**<br>
**[2. Adding Hyperlinks](https://github.com/GeomaTECHs/tutorials/blob/master/custom_popups/add_hyperlinks.md#introduction)**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **_[2.1 Single Static Links](https://github.com/GeomaTECHs/tutorials/blob/master/custom_popups/add_hyperlinks.md#option-1)_**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**_[2.2 Dynamic Variable Links](https://github.com/GeomaTECHs/tutorials/blob/master/custom_popups/add_hyperlinks.md#option-2)_**<br>
**[3 Conclusion](https://github.com/GeomaTECHs/tutorials/blob/master/custom_popups/add_hyperlinks.md#conclusion)**


### Introduction

Here is the final script from the end of the tutuorial video link above. Following this will be a demponstration of including **_hyperlinks_** in your popup windows.

```r
# load leaflet library
library(leaflet)

# Set up your data frame
data <- data.frame(c(43.11940,43.11940),
                   c(-79.24658,-79.244658),
                   c("HQ 1","HQ 2"),
                   c(4736583,3204853),
                   c('<iframe width="300" height="169" src="https://www.youtube.com/embed/vl9D3uTk36k?showinfo=0" frameborder="0" allowfullscreen></iframe>',
                     '<iframe width="300" height="169" src="https://www.youtube.com/embed/dBk8gGX1MNk?showinfo=0" frameborder="0" allowfullscreen></iframe>'))

# give names to your data columns
names(data) <- c("lat","lng","name","score","video")

# create the leaflet map variable
m <- leaflet() %>% 
  addProviderTiles("Esri.WorldTopoMap") %>% 
  addMarkers(data=data,
  lat=~lat,
  lng=~lng,
  popup= ~paste("<h3 style='color: red'>Hello World</h3>","<b>Name:</b>",name,"<br>","<b>Score:</b>",score, video, sep=" ")
            )
  
# print map
m
```
### Adding Hyperlinks
There are plenty of ways to go about doing this in the leaflet package, but I will outline two here.

1.  **A single static link for in all popup windows**
2.  **Creating dynamic variables to use for seperate links in each popup window.**

#### Option 1
- Here we will simply add a new line to the paste function in the origional script above. HTML links can br written using the following notation: ```<a href="url">link text</a>```
- To impliment this into the `paste()` function in `R` we will use a link to the GeomaTECHs YouTube channel: https://www.youtube.com/channel/UCTalI0S14Ek6DcvvvFIFPOg.


```r
# create the leaflet map variable
m <- leaflet() %>% 
  addProviderTiles("Esri.WorldTopoMap") %>% 
  addMarkers(data=data,
  lat=~lat,
  lng=~lng,
  popup= ~paste("<h3 style='color: red'>Hello World</h3>","<b>Name:</b>",name,"<br>","<b>Score:</b>",score, video,
  "<br>","<b>Link:</b>","<a href='https://www.youtube.com/channel/UCTalI0S14Ek6DcvvvFIFPOg'>GeomaTECHs YT Channel</a>",sep=" ")
            )
  
# print map
m
```

#### Option 2

- In this option we will add a different hyperlink to each popup by adding the links into the `data` variable that was created.
    1. First create a list of the links you would like to add to your data frame. This step will only need to be done if you are creating your data from scratch or if you need to combine an existing dataset with a set of hyperlinks. If it is the latter, then be sure the list of hyperlinks is as long as the length of the columns in your origional data or you may have problems.<br>
    
       Okay lets create the list of hyperlinks:
       ```r
       # create list of links in a variable
       links.list <- c("<a href='https://www.youtube.com/channel/UCTalI0S14Ek6DcvvvFIFPOg'>GeomaTECHs YT Channel</a>",
                       "<a href='https://www.youtube.com/watch?v=vl9D3uTk36k'>GeomaTECHs Tutorial</a>")
       ```
    2. Now we can add a `link` colummn to our `data` variable using the `data$link`.
       ```r
       data$link <- links.list    
       ```
    3. The final step is to add the variable `link` to the `paste()` function. In this example I have placed the link under the YouTube videos.
       ```r

       # create the leaflet map variable
       m <- leaflet() %>% 
         addProviderTiles("Esri.WorldTopoMap") %>% 
         addMarkers(
         data=data,
         lat=~lat,
         lng=~lng,
         popup= ~paste("<h3 style='color: red'>Hello World</h3>","<b>Name:</b>",name,"<br>","<b>Score:</b>",score, video,link,sep=" ")
         )

       # print the map
       m    
       ```

### Conclusion
For every tutorial video on YouTube I will try and use this GitHub account to expand on any complicated questions that viewers may have. As more questions come in I will add information to these documents hopefully answering them. So be sure to keep checking back for new information.
