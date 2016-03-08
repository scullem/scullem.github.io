---
layout: post
title: Casting Quantified
description: Identify impact of casting decisions on Box Office Revenue
img: /img/film.jpg
---

My first independent project at Metis is to use movie data scraped from the web to build a linear regression model that answers a question of my choosing about the movie industry. All of our projects run the full lifecycle from defining the problem to communicating results. This project lasts two weeks, so it is no small feat to cover all of the bases while also taking in lectures and working on challenges for practice.

# The Target
</br>
Even if I'm not working with real-world, proprietary business data, I always like to tie what I'm investigating back to something that feels like it has a business application. So I knew from the start that I wanted my target variable to be the Domestic Total Gross (i.e. Revenue) of a film. One of the nice things about linear regression is that, in spite of its various limitations, it is really intuitive to interpret (assuming you don't get too craaaazy with nonlinear transformations).

# The Objective
</br>
I settled on using my model to isolate the impact of a film's cast on revenue. If we assume creative and budgetary factors to be constant, can we tie a casting decision back to the potential for that cast to impact domestic total gross for a film? Imagine you are a studio casting a new comedy and have the choice between two casts: Jason Schwartzman/Rachel McAdams/Justin Long vs. Zach Galifianakis/Scarlett Johansson/Jonah Hill. Based on their histories of domestic total gross for past films, can we select the best cast based on projected contribution to domestic total gross for this new film?

# The Process
</br>
* Scrape and clean movie data from Box Office Mojo & OMDb API websites
* Select additional features for modeling
* Use linear regression to create multiple models of Domestic Total Gross
* Select best performing model based on test & train error and adjusted R squared
* Apply findings to selecting casting for films

# Feature and Model Selection

The final model uses 5 features: total budget, the number of days the film is in market, the number of theaters it is shown in, the runtime of the film, and the film's casting score.

The casting score is calculated as the log of the product of a film's top actors' average film revenue prior to the release of the film. That's a bit of a mouthful, so you can see this more clearly in the slides below.

<div class="img_row">
	<img class="col one" src="{{ site.baseurl }}/img/actor_score.png" alt="" title="calculating actor average revenue"/>
	<img class="col one" src="{{ site.baseurl }}/img/film_score.png" alt="" title="calculating film casting score"/>
	<img class="col one" src="{{ site.baseurl }}/img/log_score.png" alt="" title="plots of score and log score"/>
</div>

<div class="col three caption">
	On the left, Rachel McAdams' score prior to the release of The Family Stone is calculated. Middle, the full score is calculated for The Family Stone. Right, The plot of the log of the film score against revenue is visualized.
</div>

The final model is selected by looking at the change in mean squared error of the test and train datasets across models with the 5 key features successively added. Ultimately, runtime is dropped from the model because it doesn't add any additional improvement in the model.

<div class="img_row">
	<img class="col three" src="{{ site.baseurl }}/img/mse.png" alt="" title="comparison of model error for model selection"/>
</div>
<div class="col three caption">
	The error of the model is reduced considerably as more features are added, with the exception of the film's runtime. 
</div>

The final model is able to isolate the impact of the film's casting score by controlling for other factors that we would expect to have an impact on the film's revenue. The model's features and coefficients are shown below. Because the score is a log value, the interpretation of the coefficient is the impact on dollars in terms of a percentage increase in score as opposed to a unit increase.

<div class="img_row">
	<img class="col two" src="{{ site.baseurl }}/img/model.jpg" alt="" title="example image"/>
	<img class="col one" src="{{ site.baseurl }}/img/scorecard.jpg" alt="" title="example image"/>
</div>
<div class="col three caption">
	Left, a 1% increase in casting score is related to a $1.89M increase in revenue. Right, by keeping a scorecard for each actor based on film performance to date, casting decisions can be made by creating the film score using different casting combinations.
</div>


<br/><br/><br/>
