# Ideal Point Estimation from Legislative Text

Work in progress. 

## Introduction
Since the seminal work by Downs et al. (1957), spatial models have provided a useful framework to understand the behaviour of political actors—including but not limited to legislators, judges and media outlets. In these models, a policy is represented as a point in an n-dimensional euclidean space (typically, n =1,2). Each political actor assumes a single preferred position in this policy space, also known as her ideal point.

The most popular method to empirically estimate ideal points is the NOMINATE (Nominal Three-Step Estimation) algorithm developed by Keith Poole and Howard Rosenthal (see Poole & Rosenthal, 1985; Poole, 1998; Poole, 2005). They applied item response theory used in educational testing (Rasch, 1980) to U.S. Congress roll-call voting data spanning more than 200 years. They located each legislator’s position in a continuous two-dimensional policy space—along the liberal-conservative and the social/racial dimensions. Another alternative approach employs bayesian methods for ideal point estimation (Clinton et al. , 2004). More recently, Argyle (n.d.) demonstrates the use of neural networks to estimate legislator ideal points from roll-call voting data. However, models that rely on roll-call voting do not accurately capture the latent ideology of a legislator for two reasons. First, the bills introduced in congress on which roll-calls are recorded may be systematically different from those that could not pass the congressional committees. Ignoring this leads to a selection bias (Hug, 2010). Secondly, parties exert strong influence on roll-calls of legislators, especially on key issues (Snyder Jr & Groseclose, 2000). This may confound a legislator’s ideological position.

To overcome these shortcomings, recent work uses political text from a variety of sources1 to estimate ideology. Gerrish & Blei (2011) infer legislator ideal points using legislative text by combining roll-call voting data with legislative text. However, they do not take into account the semantic composition of a phrase. Iyyer et al. (2014) use recursive neural network (RNN) to take into account syntax and predict ideology using U.S. congressional floor debate transcripts. Their classification, however, is binary and they do not estimate legislator ideal points in a continuous space.

Most of the existing work that uses legislative text focuses on prediction of bill passage using data on roll-call voting (see for example, Yano et al., 2012; Kornilova et al., 2018). Moreover, most of these studies infer ideologies over a single dimension.

As discussed earlier roll-call voting is subject to party pressures. Therefore, in contrast to the existing literature, we propose to predict a legislator’s ideal points along politically meaningful dimensions based on her bill sponsorship rather than her roll-call voting record. This can help in testing theories of legislator behaviour in political science such as how responsive a legislator’s bill sponsorship is to her constituents vis-à-vis the political party or lobbies. Importantly, inferring ideology from text can predict ideal points in contexts where voting is not recorded or even conducted such as ideology of judges from judgement text. Thus, we can leverage ideal point estimation to understand how ideology has evolved even in legislatures where voting is conducted through voice vote, show of hands or secret ballot.

## Methodology
We propose to use text of each bill to unveil the ideological position it represents. We will do this in following three steps:

1. Vectorizing bill text: We use a pre-trained Universal Sentence Encoder model to obtain bill embeddings from mean of sentence embeddings of bills.

2. Projecting vectors on the ideology space: Next we determine the relative position of bill vectors along the ideology space using information on bill sponsor’s party. The left-right ideology dimension will be recovered using the line connecting the points representing average of vectors of bills introduced by republicans and democrats. Projecting bill vectors on the ideology dimension will give us location of the bill in a given policy space. We will then validate our results by taking pairs of economic bills which oppose each other largely in left-right ideology and taking the (average of) line connecting these as the ideology dimension. An example of such a pair is the Patient Protection and Affordable Care Act (Obamacare) vs. Tax Cuts and Jobs Act that repeals Obamacare.

3. Recovering legislator ideal points: Finally, we will take average of all bill vectors of a particular sponsor and repeat the previous step to model ideology of politicians in terms of the bills they draft. We compute correlation between the ideal points so obtained (i.e. via bill-text) vs ideal points based on legislators voting behaviour (DW-nominate score)

## Data
We use complete texts of all bills introduced in the United States congress available on Congress.gov database— a joint project of Library of Congress, the House, the Senate and the Government Publishing Office—starting from the 101st Congress (1989–1990). The website further contains information on bill type, sponsor, cosponsors, actions taken on the bill, as well as the committee and subcommittees to which the bill was referred. We will further enrich our data using bill text summaries and other bill details available from the 80th (1947–1948) congress onwards using the Congressional Bill Project (Adler & Wilkerson, 2019). Further, the bills are labeled according to major topics in the Comparative Agendas Project. We will also compare our ideology scores to DW-NOMINATE scores (Boche et al. , 2018) for bills as well as legislators available on https://voteview.com/. For our validation exercise, we will compare our ideal points to those obtained by Bonica (2014), who uses data on campaign finance given by donors to political actors.


## Authors
* [Rochana Chaturvedi](https://twitter.com/rochanac?lang=en): rochana [dot] chaturvedi [at] gmail [dot] com
* [Sugat Chaturvedi](https://sites.google.com/view/sugatchaturvedi/home): sugat [dot] chaturvedi [at] gmail [dot] com
