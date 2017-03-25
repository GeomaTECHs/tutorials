# GeomaTECHs Tutorials ![Logo]()

**Author:** Brent Thorne <br>
**About:** This will break down how to use hyperlink html code in your leaflet maps in RStudio.<br>
**Youtube video:** https://www.youtube.com/watch?v=mTTuUGisxDk

### Origional final script from video
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
### Adding hyperlinks in the popup window
There are plenty of ways to go about doing this in the leaflet package, but I will outline two here.

1.  **A single static link for in all popup windows**
2.  **Creating dynamic variables to use for seperate links in each popup window.**

#### **Option 1**
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
