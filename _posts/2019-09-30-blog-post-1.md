---
layout: post
title: Digging in
---

# My first week in a Data Science Bootcamp:
## Let's dig in

We just wrapped up our first week of the Metis Data Science Bootcamp. This week was already jam packed and pretty intense. We have explored working in command line, vs code, Git and Github, Python (including packages such as pandas, matplotlib, seaborn, numpy), Big O, and more. All of these principles were taught while we were working on our first project of the bootcamp due the same Friday of that week.

## Street team placement for Women Tech Women Yes

This was our first project assignment at Metis. We were challenged to worked in groups to analyze NYC MTA's Turnstile data help advice Women Tech Women Yes on optimal placement for their street crews.

### Objective

We received a  project request from Women Tech Women Yes in the email below:

> As we mentioned, we are interested in harnessing the power of data and analytics to optimize the effectiveness of our street team work, which is a significant portion of our fundraising efforts.
>
>WomenTechWomenYes (WTWY) has an annual gala at the beginning of the summer each year. As we are new and inclusive organization, we try to do double duty with the gala both to fill our event space with individuals passionate about increasing the participation of women in technology, and to concurrently build awareness and reach.
>
>To this end we place street teams at entrances to subway stations. The street teams collect email addresses and those who sign up are sent free tickets to our gala.
>
>Where we’d like to solicit your engagement is to use MTA subway data, which as I’m sure you know is available freely from the city, to help us optimize the placement of our street teams, such that we can gather the most signatures, ideally from those who will attend the gala and contribute to our cause.
>
>The ball is in your court now—do you think this is something that would be feasible for your group? From there we can explore what kind of an engagement would make sense for all of us.

### Approach

We set out to analyze the most recent four weeks of [MTA data](http://web.mta.info/developers/turnstile.html) for information that will help the client better determine when and where they can place their street teams in order to reach the most people. This will greatly expand their ability to both spread the word about Women Tech Women Yes and receive sign-ups for your upcoming fundraising gala.

For the project we set out to determine:
* The top 5 busiest metro stops in NYC
* The busiest days of the weeks
* The busiest times of day

### Data Cleaning & Data Wranging

Below is a clip of the MTA dataset:
![MTA DataSet](/images/MTA_data_head.png)

As you can see the dataset is not all that useful in the provided format. We cleaned up the data by removing duplicates, cleaning up columns headers, applying datetime, and re-organizing the by turnstile. Each turnstile is determined unique by its 'C/A', 'UNIT', 'SCP', and 'STATION', so we created a separate column that grouped by these values called 'UNIQUE_ID'.

In order to drop the duplicated values (which appeared to be inserted during an audit), we sorted the values by UNIQUE_ID and DATE:

![removing duplicates](/images/removing_duplicates.png)

At this point we felt ready to do some analysis. We chose to take the difference between the total number of entries recorded and use those numbers to determine the stations with the highest amount of traffic. We also decided to cap the total amount of entries per 4 hour time window to 20,000, which limits the amount of entries to just over 1 person per second. this seemed reasonable.

![taking difference in entries](/images/entry_diff.png)
![removing values over 20,000](/images/remove_high_values.png)

### Results
So what did we find...

Top 10 Stations:
![top 20](/images/top10stations3.svg)

We decided to focus on the top five stations and advise on what day of the week and what times to place the street team in order to optimize the amount of people they will interact with at those stations.

Starting with day of week:
![top days](/images/topweekdays.svg)

The weekdays far surpass the weekends, and Tuesday - Friday were all particularly busy days of the week. _This informed our second recommendation for WTWY: send street teams out between Tuesday and Friday._

Now let's check out time of day:
![Penn Station](/images/PennSt_time.svg)
![Grand Central](/images/GrandCentral_time.svg)

We learned that the best times of day across all top five stations was during the morning rush hour and evening rush hour. _This brought us our third recommendation for WTWY: send street teams out between 8am - 12pm and between 4pm - 8pm._

### Conclusions & Recommendations

We would recommend that WTWY place their street team at the following stations:
1. 34th Street - Penn Station
2. Grand Central Station - 42nd Street
3. 34th Street - Herald Square
4. 23rd Street
5. 14th Street - Union Square

These five stations have the highest traffic by total entries. To further optimize the amount of people their street team interact with, WTWY should deploy their teams between Tuesday and Saturday from 8am - 12pm or from 4pm - 8pm (with an emphasis on the evening rush hour).
