# Predicting Water Quality using Earthwatch Data

**INTRODUCTION** <br/>
Due to my interest in the field of environment and sustainability and the relevance of using real world data, I chose to do my final project of General Assembly’s Data Science Immersive course, on a dataset provided to me by the environmental charity Earthwatch www.earthwatch.org.uk.

**ABOUT EARTHWATCH** <br/>
Earthwatch uses a ‘blend of science and engagement, to deliver experiences that educate and produce impactful results to halt environmental decline’. The charity manages a number of projects, one of them being FreshWater Watch; a research project investigating the health of global freshwater ecosystems. As I volunteered to gather samples that contributed to this project, assisting in the analysis of their data was of particular interest to me.

**PROBLEM STATEMENT** <br/>
Water is essential to life on Earth, yet only 1% of the world's freshwater is accessible. Declining water quality can have severe impacts on human health and affect the surrounding ecology. Knowing what impacts the quality of water can prevent and/or diminish the detrimental effects. In this analysis I am therefore looking to explore whether certain features are related to water quality and therefore whether these can be predictors in determining the quality of water.

**HYPOTHESIS** <br/>
This investigation will use nitrate and phosphate levels as measures for how ‘clean’ or ‘polluted’ a freshwater source is. Without going too much into the science behind it, nitrates and phosphates appear naturally in freshwater sources, however, high levels can be detrimental to both the immediate ecosystem and human health through consumption.

After speaking to a scientist, I learned that these chemicals are used in abundance in agriculture and I therefore wanted to explore whether the data showed this as well. Of further interest to me was whether rain impacts the chemical levels - through surface run-off.

**DATA COLLECTION** <br/>
The dataset provided contained features describing the immediate water source, yet I was also interested in the impact of weather. I therefore used the API through Darksky www.darksky.net which allowed me to capture weather data by geolocation and date. I also used an API to capture reverse geolocation data www.opencagedata.com.

**DATA CLEANING** <br/>
After adding the weather and location data to the original dataset, my main challenge was dealing with missing values. The original dataset contained 24,000 observations, however, when dropping missing values this would decrease to ~ 6.000 observations. Since I did not want to lose such a large amount of data, I decided to replace ‘NA’ for ‘None’ when that category did not exist, delete rows that contained information on less than 40% of the columns and imputed values for others. I then did some feature engineering by adding features to estimate population (based on proximity to cities/ towns or villages) and grouped waterbody type into standing and flowing. Finally, due to the way the data is collected (multiple choice answers are returned in one cell) - I manually created dummies for each of these categories.

Throughout this process, I noticed some inconsistencies in the data, for example that some water sources had different waterbody types (e.g. lake one day, river another day), or that some ponds had fast flowing water - which may not make intuitive sense. I also noticed that some water sources didn’t exist such as ‘Rio de Janeiro’. I cleaned the data as well as possible, but recognise that these inconsistencies may be cause for concern later down the line.

**EDA** <br/>
After speaking to a scientist at Earthwatch, they explained that they usually split the nitrate and phosphate levels into categories i.e. ‘low’, ‘medium’ and ‘high’. I used the levels found on https://ewgis.org/WaterBlitz-Analysis/ for my classifications.

The first thing I noticed when visualising was that phosphate and nitrate levels have very low correlation - which was slightly surprising but it also intrigued me to see how the site characteristics vary. Some observed differences were:

**Freshwater body types:** <br/>
- phosphate levels higher in rivers and streams
- nitrate levels higher in lakes, wetlands
- ponds have good levels for both nitrates and phosphates
**Land Use:** <br/>
- phosphate higher in residential areas (detergents/additives), agriculture (fertilizer)
- nitrate higher with agriculture/ industrial
- agriculture has stronger effect on phosphate levels than nitrate levels (but bad for both)
- grassland/shrub, forest and indicators for low levels of both (BUT low levels of observations)
**Algae:** <br/>
As nitrate and phosphate can induce algae to grow, I was very interested to see whether algae is an indication of high chemical levels. The results showed that there is a slight tendency to observe higher chemical levels where algae is present, but it is not a large enough difference to conclude this to be statistically significant.

**Time of year** <br/>
I also thought it would be interesting to see whether chemical levels change substantially by time of year (there may be more agriculture and therefore higher levels of chemicals in the soil at certain points of the year). Looking at the observations, however, there doesn’t seem to be a significant trend.

**Precipitation** <br/>
Surface run-off is a common issue in agriculture and I included weather data (1 day ago) to explore whether this is a factor here. The results turned out to be the opposite as expected i.e. with more precipitation there are lower chemical levels present.

**Geolocations** <br/>
Nitrate levels are high in Europe and South America (Note: few observations in South America)
Phosphate levels are high in South America, North America and Asia

**DATA MODELLING** <br/>
Due to the above EDA and lack of clear evidence to distinguish chemical levels based on observed characteristics, I was sceptical as to whether my modelling would be successful.

I ran a number of classifiers including ensemble methods and determined that the best model was a Random Forest for predicting nitrate levels and a Bagging Classifier for predicting phosphate levels. Both made predictions above the baseline, and nitrate had higher accuracy compared to baseline Nitrate accuracy: 65% (baseline: 54%), Phosphate accuracy: 70% (baseline: 0.63%). Both models showed that relevant features were the flow of the water, precipitation and location of the water body. Differences included higher relevance of animals for predicting nitrate and plants for predicting nitrate.

Unfortunately my models didn’t clearly show that agriculture and rain from run-off have a significant impact on elevated chemical levels in water sources. As I noticed some inconsistencies in the data, I believe this could be improved with significantly more data and mechanisms put in place to prevent human error in data collection.

**NEXT STEPS** <br/>
To improve on my results I believe I could also include weather data for several days earlier and get more precise data on the level of precipitation. Furthermore using satellite data on agricultural activities could be more accurate than relying on human inputs.
Furthermore, it would be interesting to define water quality using different metrics (for example including plastics, e-coli ect) in defining the pollution of the water source.
