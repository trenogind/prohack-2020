# prohack-2020
Solution of PROHACK 2020 ML competition at [prohack.org](prohack.org).

This is quite simple solution, that uses only the structure of answers on train time-series, and doesn't use any of the provided features. The main idea is to find similar galaxies in train (I used KNN on differences), and to average differences in their answers to predict difference in answers for galaxies in test. Optimization part played a great role, since some delution of allocation around border allowed me to increase score on public dataset from around 0.045 (when I allocated 100z DSML to every galaxy in top 500 by their potential) to around 0.0215.

All of this allowed me to take 4th place on private leaderboard.

## Competition task

“Beeep…Beeeep….Beeeep… Hooomans*, are you there?...”

This very strange transmission is coming from your narrowband radio signal receiver, pointed towards one of the farthest away galaxies. It’s early morning, you are sitting in your radio observatory high in the mountains.

For the last 10 years you’ve been a Chief Data Scientist in one of the best astrophysics research teams in the world. You are enjoying a quiet time with a cup of coffee and reviewing the data reports from last night, when this strange sound arrived. You almost spill your coffee in surprise. “Am I dreaming?” is your first thought as you move closer towards the speaker and listen…

“Beep…Beeeep….Beeeep… To all Hooomans who can hear us – we need your help”

You lean closer and grab a notebook and a pencil – you don’t really trust computers when it comes to such important tasks as taking notes from a radio transmission. You start recording everything that the strange voice from light years away is saying.

“… We need serious Data Science help and we know you Hooomans are the best at it…. We are an intergalactic species which have almost achieved singularity and the highest possible levels of development. We travel fast through space and explore other galaxies”

“The only essence that we consume is energy, measured in DSML units…Our populace is widespread and we live across many different star clusters and galaxies. What we need now is to optimize our well-being across all those galaxies… We have a lot of data but our сomputers and methods are too weak – we urgently need your data science knowledge to help us”

“Only two steps prevent us from achieving singularity

· To understand what makes us better off.

Our elders used the composite index to measure our well-being performance, but this knowledge has disappeared in the sands of time.

Use our data and train your model to predict this index with the highest possible level of certainty.

· To achieve the highest possible level of well-being through optimized allocation of additional energy

We have discovered the star of an unusually high energy of 50000 zillion DSML.

We have agreed between ourselves that 

· no one galaxy will consume more than 100 zillion DSML 

and 

· at least 10% of the total energy will be consumed by galaxies in need with existence expectancy index below 0,7.

Think of our galaxies as your “countries” (or how you call them??) and our population as citizens. We have similar healthcare and wellbeing characteristic as you, Hooomans”

“We are sending all the data to you right now. Let the data be with you, Hoomans… … …”

Transmission suddenly ends. You put your notebook and pencil away and start thinking. You really want to help this species optimize their well-being. You open up Python and upload the dataset from the narrowband radio signal receiver. It will be another great day at the observatory today.

————

* probably intergalactic species meant to say “humans” here but we will never know for sure

## Description Data Recieved

The solutions are evaluated on two criteria: predicted future Index values and allocated energy from a newly discovered star

1) Index predictions are evaluated using RMSE metric

2) Energy allocation is also evaluated using RMSE metric and has a set of known factors that need to be taken into account.

Every galaxy has a certain limited potential for improvement in the index described by the following function:

Potential for increase in the Index = -np.log(Index+0.01)+3

Likely index increase dependent on potential for improvement and on extra energy availability is described by the following function:

Likely increase in the Index = extra energy * Potential for increase in the Index **2 / 1000

There are also several constraints:

in total there are 50000 zillion DSML available for allocation and no galaxy at a point in time should be allocated more than 100 zillion DSML or less than 0 zillion DSML. Galaxies with low existence expectancy index below 0.7 should be allocated at least 10% of the total energy available in the foreseeable future

3) Leaderboard is based on a combined scaled metric:

80% prediction task RMSE + 20% optimization task RMSE * lambda where lambda is a normalizing factor

4) Leaderboard is 80% public and 20% private

5) The submission should be in the following format:

*Index* - Unique index from the test dataset in the ascending order

*pred* - Prediction for the index on interest

*opt_pred* - Optimal energy allocation
