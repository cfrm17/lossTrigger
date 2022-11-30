# Loss Trigger Leveraged Super Senior Tranche Valuation


The loss trigger leveraged super senior tranche (LT-LSS) valuation model is presented. A leveraged super senior tranche trade is a credit linked note, which provides investors with a leveraged exposure to the super senior tranche in a synthetic CDO transaction. The note holder earns the risk premium associated with selling protection on the entire senior exposure when the protection it provides is limited to only the funded principal amount which is just a fraction of the entire exposure. 

There are a series of time varying loss triggers built in the trade. If at any time before the trade maturity the accumulated loss amount of the entire collateral pool reaches a predefined level, the trade terminates and is settled on the mark-to-market (MTM) of the underlying super senior tranche or the funded amount, whichever is less.

The valuation of LT-LSS trades has been a challenging task in both the industry and academia. LSS trades are essentially exotic options on the forward starting super senior tranche conditional on the trigger breach, which depends on the way how the correlated default events, credit spread of each reference obligor, and market implied correlations evolve over time. The exercise of a LSS trade is contingent on the trigger breach, which can happen at any time before the trade maturity. The value of the trade cannot be fully determined unless a dynamic process of the portfolio is modeled. Furthermore, compared with other triggers, the LT-LSS is the most complicated because it directly links the credit spread and the implied correlation movements to the default events of the collateral pool. It is almost impossible to get pertinent market information to calibrate such a conditional loss process, even if we can somehow model one. 

The model does not attempt to dynamically model the forward starting super senior tranche value conditional on trigger breach. Instead, it makes the assumption that, upon the loss trigger breach, the settlement is always the funded amount which is the maximum payoff of the trade. This assumption enables us to model the LT-LSS trade as a digital trigger option, which can be solved via our recently developed weighted Monte Carlo (WMC) method for the forward starting CDO (FSCDO) trade. The WMC methodology and the FSCDO valuation model were approved on May 11, 2006.

For a trade in the sold protection position, the MTM calculated by the LT-LSS model is always conservative. For a trade in the bought protection position, the model is acceptable when an additional model risk reserve is set up. 

The LT-LSS model and the FSCDO model share the same model template and the same WMC model. The model risk reserve methodology to address the uncertainties in the WMC method for the FSCDO model applies to the LT-LSS trade. The limitations and restrictions for the LT-LSS model are directly inferred from that of the FSCDO model, except for the choice of calibrating instruments. Compared with the FSCDO model, more spot tranches are needed in the calibration of the LT-LSS model hence it is more difficult to successfully calibrate the model. Although an extensive testing has been made by GRMMR London and GRMMR QA, the stability of the calibration for the LT-LSS model has to be monitored with caution.

A leveraged super senior tranche (LSS) trade is a credit linked note, which provides investors with a leveraged exposure to the super senior tranche in a synthetic CDO transaction.   The note holder earns the risk premium associated with selling protection on the entire senior exposure when the protection it provides is limited to only the principal amount that is funded, which is just a fraction of the entire exposure. 

One of the key features of a LSS trade is the early unwind trigger. Upon the occurrence of an unwind trigger event, the transaction terminates and is settled on the mark-to-market (MTM) of the super senior tranche or the funded amount, whichever is less.  There are three types of unwind triggers: (i) realized loss trigger; (ii) portfolio weighted average spread trigger; and (iii) threshold market value changes in the super senior tranche itself. Only the loss trigger is discussed in this document. An example of the loss trigger is shown in Table 1.

Table 1. Loss Trigger
Term	Date	Trigger Level (% of total notional amount of the collateral pool)
1y	20-Sep-06	3.75%
2y	20-Sep-07	4.50%
3y	20-Sep-08	5.50%
4y	20-Sep-09	6.50%
5y	20-Sep-10	7.50%
6y	20-Sep-11	8.75%
7y	20-Sep-12	10.00%


If, for example, the reference collateral pool is three years away from maturity and has experienced credit losses to date of 4.5% against a loss trigger level of 7.5%, the transaction would not unwind. 

The valuation of the LSS type of instruments has been a challenging task in both the industry and academia. From the viewpoint of modeling, LSS trades are essentially exotic options on the forward starting super senior tranche conditional on trigger breach, which depends on the way the correlated default events, credit spread of each reference name, and market implied correlations evolve over time. The exercise of a LSS trade is contingent on the trigger breach, which could happen at any time before trade maturity. Currently well established credit derivative models, such as the normal copula model [1], specify a distribution of the credit events directly and imposes no dynamics of the credit spreads and correlation. Therefore these models cannot be used in the pricing of LSS trades. Very recently we have noticed that new approaches, which involve modeling of the dynamic evolution of the loss function, have been proposed by several authors [2-4]. However, as far as we know, it is very difficult to practically implement and calibrate these models.

The submitted loss trigger LSS (LT-LSS) model follows a different way of modeling [5]. Instead of trying to model the forward movement of the value of the super senior tranche value conditional on the breach of the loss trigger, the payoff function is always set to be the funded amount which is the maximum loss amount on the protection leg of the trade.  This assumption enables us to model the LT-LSS trade as a digital time-varying barrier option (see https://finpricing.com/lib/EqBarrier.html), which can be solved via our recently developed weighted Monte Carlo (WMC) method for the forward starting CDO (FSCDO). 

Ignoring the option value in the payoff function is a conservative approach if we are in the position of sold protection while not conservative in the position of bought protection. Therefore, a model risk reserve has been set up for the trade in the bought protection position by GRMMR London. However, it is expected that the payoff at the trigger breach is reasonably close to the funded amount, if the trigger level is fairly high and the leverage ratio is high.  In a scenario in which a large number of obligors default (loss trigger is breached), the credit spread levels of the other surviving obligors will be widen a lot and the implied correlation should be very large. This would lead to the MTM value of the super senior tranche much larger than the funded amount, if the leverage ratio is high. 

Note that, even if the problem is dramatically simplified by this assumption, it is not a trivial task to price a LT-LSS trade for two reasons:

1.	The trigger has a stepping up structure, as shown in Table 1. From the viewpoint of model, any non-flat barrier option pricing is complicated. A LT-LSS trade with a stepping up loss trigger can be viewed as an option on the portfolio of a series of forward thin tranches with different maturities and tranching levels. We need to price a forward tranche expected loss, conditional on survival of all previous tranches.  

2.	As a standard mark-to-market methodology, correlation information of the underlying collateral pool has to be implied by the market information of the CDX and ITraxx quotes via base correlations (see, for example, Ref. [8]). As shown in Table 1, the pricing of LT-LSS trade has to consider a full term structure of the base correlations. This task is actually more difficult than that of a FSCDO trade, in which only the base correlations for two relevant dates are considered.  

The WMC methodology is the appropriate way to model this LT-LSS digital trigger option. The WMC method has the power to price a forward expected loss, with a successful calibration to the spot expected losses with different maturities. In the MC simulation, the stepping up loss trigger can be modeled readily. 

As a non-parametric approach, the model can only be used when it can be successfully calibrated to the appropriate spot market information. Similar to the FSCDO model, there are two sets of calibrating instruments for LT-LSS trades:

•	The unconditional default probabilities (or, equivalently, credit spread curve) of each obligor in the collateral pool. Each obligor has a term structure of the credit spread and so does the unconditional default probability. This is the prerequisite of the WMC method, which applies to both the FSCDO model and the LT-LSS model.

•	The expected losses of spot tranches with different terms and tranching position. Due to the feature of non-parametric approach, the calibration spot tranches have to include a full term structure of the base correlations. The thickness of the tranches has to be reasonably thin so that the trigger probability can be reasonably implied by these spot thin tranche values. 

There are model uncertainties which are fundamentally embedded in the model. Therefore the same model risk reserve procedure as that of the FSCDO model is adopted. The limitations and restrictions are directly inferred from the testing of the FSCDO model, except for the choice of the calibrating instruments.   Similar to that of the FSCDO model, a model risk reserve has been set up to address these uncertainties. GMRMR London and GMRMR QA have agreed that, for each LT-LSS trade, two most conservative scenarios are established by 1) using various calibration instruments with the different levels of calibration tolerance, and 2) using various copulas and correlations to generate prior MC scenario. The model risk reserve is then determined by a combination of the above two.

Assume that an LT-LSS trade has an underlying super senior tranche with an attachment point A, a detachment D, and a b/e spread s. The trade is defined by a maturity T, a time varying loss trigger denoted by K(t), a traded spread  , a leverage ratio Lev,  and the cash flows associated with the fixed fee occur at intervals  (maturity).   The loss function of the super senior tranche is

(1)	 ,

where is the loss function of the reference pool over time.   is defined as the default time of the nth obligor in the collateral pool A and  is the associated loss given default  (LGD) of the   obligor. 

Define the trigger breach time  

(2)	 

The default probability of trigger breach is defined as

(3)	 

The corresponding survival function and probability density function can be written as  and , respectively. 

We also define   as the value of the forward super senior tranche starting from   to   seen at time  ,  conditional on the cumulative loss larger than X at time t.

Provided that   is less than the maturity T, the pay off of the LSS then reads:

(4)	 ,
with

(5)	 .

 and   are defined as the value of protection and risky annuity of the underlying super senior tranche conditional on the trigger breach, respectively.

The value of protection  and the value of fee payment leg  seen at the valuation date  can be written as:

(6)	 

(7)   

As indicated in Eqs. (4) and (5), by definition pricing an LSS trade is challenging because it is a path dependent barrier option with the payoff being a forward starting super senior tranche, which is unknown and hard to model for three reasons:

1.	 is path dependent. For example, for a non-homogeneous pool with 100 names and 10 defaults get to the trigger, there would be   difference paths to have the trigger breached.

2.	 is essentially a CDO tranche starting at  , with the remaining term  , reduced attachment point  , and more importantly, conditional on the default events which bring the loss of the collateral pool to the trigger level, a scenario in which the associated changes in credit spreads and the market implied correlation can not be obtained from today’s market information. 

3.	From the viewpoint of modeling,   directly link the default risk to the credit spread risk.  Because of this the LT-LSS trade is of the most complicated among all types of LSS trades. 

From the viewpoint of mathematical modeling, we need to figure out the dynamic evolution of  from their initial values to price the LSS trade. Several approaches have been proposed to model the loss processes , borrowing the idea from the HJM approach in interest rate modeling [2-4]. However, as far as we know it is difficult to practically implement and calibrate these models and further investigations are needed.

Although directly modeling the pay off at the default time is difficult, we could assume the pay off function be the collateral amount. Eq. (4) can then be rewritten as:

(8)	 .

Eq. (8) means that, instead of trying to find , we always model the payoff to be a digital one which is the upper boundary value. If we are in the position of the selling protection, this payoff is always the maximum value we will pay in the case of trigger breach. Therefore, it is conservative for the sold protection.  For the same reason, it will not be conservative for the bought protection. 

However, we can reasonably speculate that   is close to   for the trades with the following features: 1) the loss trigger level is large, and 2) the leverage ratio is large. 
If the loss trigger level is high, a large number of default events are needed to get to the loss trigger level. If this happens, the credit spread levels of the survival obligors will be widen a lot, leading to a very large expected loss of the super senior tranche. The entire funded amount can be easily depleted, if the leverage ratio is high. Note that these are exactly the case for the all current outstanding trades. 

The LT-LSS trade value can then be written as:

(9)	 

(10)  .

As shown in the Eqs. (9) and (10), the problem is now simplified to calculate  , which is defined as the trigger breach probability.
	
1.4 Pricing of Digital Time Varying Trigger Option via WMC

The MC simulation can be divided into two categories: those are uniformly distributed and non-uniformly distributed. A conventional MC simulation algorithm assigns each simulated MC scenario, or path, an identical probability weight.  On the other hand, we can allow a different probability to be assigned to each simulation path.

To see how the latter method works, consider that a contingent claim has a value    for MC scenario  .  The value computed according to equally-weighted MC simulation will be given by

(11)		  

whereas for non-uniformly weighted Monte Carlo we have

(12)		  

where   is the probability weight for path  .  The details on how to calibrate this weight probability in the WMC model can be found in Refs. [6-7].

In the LT-LSS model, suppose the weight of each scenario has been calibrated successfully and the trigger breach time is found via the standard MC simulation for CDOs. The value of the LT-LSS can be found by:

(13)	 
(14)  .

In a MC simulation, the trigger breach time   for the   path can be calculated accumulating the expected loss over time. The MTM of the trade can then be calculated by subtracting two legs:

(15)	 

In the WMC model, the sensitivities have also been implemented. The credit spread sensitivity has been fully tested and approved for the FSCDO model. Because the LT-LSS model and FSCDO model share the same model template and the same methodologies are employed, the sensitivities approved for the FSCDO model can be extended the LT-LSS model without further testing.

There are two subsets of calibrating instruments. As discussed above, the prerequisite of the WMC is that the optimized path weights should be able to reprice the instruments used to generate prior MC scenarios. For all the structured credit derivatives, they are defined as the unconditional default probabilities (or, equivalently, credit spread curve) of each obligor in the collateral pool. Each obligor has a term structure of the credit spread and so does the unconditional default probability. Normally the terms of a credit spread curve include 1w, 1m, 3m, 6m, 1y, 2y, 3y, 4y, 5y, 7y, 10y, and 20y. It would be ideal if we can calibrate the full term structure of the credit spread curve of each obligor. 

For a LT-LSS trade with loss trigger as shown in Table 1, the terms we need to calibrate are the same as the loss triggers. Specifically, these are 20-Sep-06, 20-Sep-07, 20-Sep-08, 20-Sep-09, 20-Sep-10, 20-Sep-11, and 20-Sep-12. However, if this remaining term for the first term is much less than one year, it may be ignored because the liquidity would be low for very short term credit default swaps.

The second type of calibration instruments are expected losses of spot tranches with different terms. For the same reason discussed above, we need to calibration to spot tranches with maturities being the same as the loss trigger points. However, the minimum term for the on the run CDX and iTraxx indexes are three years. In order to get the market implied correlations less than three years, a extrapolation of the base correlation has to be used hence the uncertainties arise in the calibration process. The base correlation much less than three year term is not accurate. Therefore, we set the minimum term of the calibrating tranches be two years.

As discussed in the next section, the LT-LSS can be viewed as an option related to a series of forward starting thin tranches. Therefore, in the choice of the calibration instruments, it would be best to calibrate to the whole capital structure with a series of thin tranche for each term. However, practically it is hard and/or not necessary to do so due to the market data availability and the target levels of the loss trigger.  We set a minimum requirement for the calibrating tranches for each term as:

1.	The capital structure should at least goes up to the corresponding trigger level 
2.	At least one thin tranche at the trigger level. The default thickness of the thin tranche is set to one percent. From the perspective of the LT-LSS modeling, the thinner the better. However, because the thin tranche value relies on the interpolation on the base correlation curve, the value becomes less reliable if a tranche is too thin. One percent tranche is the market convention for a thin tranche.

Note that a detailed discussion of the calibrating instruments can be found in Ref. [7]. In order to manage the model uncertainty caused by the calibration error and the choice of calibrating tranches, a model risk reserve has to be set up. A procedure to determine the calibrating tranches has been set up so that appropriate capital structure and tranche thickness can be chosen on a trade by trade basis. 


