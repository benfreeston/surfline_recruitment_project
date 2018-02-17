# Background
At Surfline we build products to answer the question ‘where and when do I surf 
next?’. One of the key data points considered in answering this is 
‘how big will the waves be?’. The physics of deep water waves are well 
understood and we have excellent numerical weather prediction models for these. 
However the changes that take place as these waves move into shallow water on 
the beach are complex, non-linear and computationally extremely expensive to 
model. For this reason a key project is an attempt to use statistical or 
machine learning to fit offshore predictions to observations of surfing 
wave heights and this project is designed to give a taste of that.

## The Data
Ocean observations came of age around 40 years ago with the advent of the 
modern satellite. These allowed for both direct observation (ocean surface 
wind speed and wave heights can be directly measured with satellite altimetry) 
and a communication channel for ocean sensors. Of these our main interest is 
in Wave Buoys. These use double integration to turn accelerometer data into 
displacement and in doing so can measure wave heights through time at a fixed 
location.

### Offshore Data
For this project the offshore data set is from a wave buoy anchored near the 
famous surfing spots of the North Shore of Oahu in Hawaii:

http://www.ndbc.noaa.gov/station_page.php?station=51201

Historical archive data for this is available for years 2004 - 2017 via the 
link standard meteorological data here:

http://www.ndbc.noaa.gov/station_history.php?station=51201

Descriptions of each field are here:

http://www.ndbc.noaa.gov/measdes.shtml

But the key fields we’d expect you’d find most useful as model features are:
 - WVHT : The average of the largest third of waves over an observation period
 - DPD : The wave period (inverse frequency) at which there's the most energy 
 - MWD : Mean direction of waves

Exactly what this data represents and how it’s derived is interesting and 
relevant to our work but we don’t expect you to need to build that 
understanding to attempt this project - in fact there is some benefit to any 
insights you might have into the relationships between the data here not being 
preempted by the assumptions those more familiar with it might hold. 

This project is NOT intended as a test of your knowledge of the physics of 
ocean waves OR your ability to go learn about that! 

### Surf Height Data
Currently the only robust way to measure the face heights of surfing waves is 
via human observation. This is exactly as costly, time consuming and error 
prone as you might expect. The largest collection of this data anywhere 
is held here at Surfline, but the longest collected record for a single 
location exists from Hawaii and is collected and maintained by oceanographer 
Pat Caldwell. 
A description of this data is here:

https://www.nodc.noaa.gov/archive/arc0012/0001754/1.1/data/1-data/meta/data_file_format_description.txt

Some important notes:
- We’re interested in the fourth column ‘nshor’ as our ground truth surf heights
- Surf heights in the observation data are in feet using a Hawaiian surf 
measurement system that is about half actual face height. 
Eg. nshore x 2 = surf height in feet
- The observations are off the largest observed surf that day. 
We pre-process the buoy data to give daily maximums to align 
with this data.


## The Project
We’re interested in looking at **WVHT**, **DPD** and **MWD** (or any other fields) in the 
offshore data and seeing if we can use this to predict for **nshor**, 
in the surf height data.

The project can be divided into three parts:

- **Preprocess the data** Wave buoy data is twice hourly, observation data the 
maximum daily. These sets need cleaning and aligning, we've done a 
version this for you in the notebook:
```./preprocess_data_example.ipynb```
and the preprocessed data set is in ```./data/prerocessed_all.dat```
- **Exploratory data analysis.** Any insight you can gain directly from the data 
as a non-expert in the field would be interesting. You’re welcome to use other 
parameters in the data sets than the key ones we outlined above. Any 
visualisations that allow us to better understand this data would be a key 
part of this process. There are some very basic plots in the notebook. It'd be 
interesting, for example, to consider whether we could idenity clusters of 
conditions in which human observations might be more or less error prone.
- **Predictive Model.** Explore a solution for predicting nshor from the offshore 
data. This could be treated as a regression problem or, perhaps more 
realistically given the data is human estimated, a classification problem. 
Any technique and framework is fine here.

*There's no time limit for this project, but we'd not expect you to feel 
obliged to spend more than 4-6 hours on it. The expectation and evaluation
WON'T be on the success of the predictive model. The data is dirty and the 
quantity here relatively small. More important is your process and imagination*

### Further Reading
Pat Caldwell wrote a paper in 2007 using regression to build a simple 
predictive model for his observation data. This isn't required reading! 
But if you're interested it's relatively easy to implement his solution with 
the data here and compare your results - the literature here is sparse and 
this is not far from the state of the art!

http://www.16streets.com/MacLaren/Travel%20and%20Surfing/Hawaii/Sunset%20Beach/Empirical%20Method%20fo%20Estimating%20Surf%20Heights%20-%20caldwell2007.pdf
