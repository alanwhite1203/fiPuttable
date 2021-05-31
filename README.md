# Valuing Puttable Bond 

A puttable bond is a bond in which the investor has the right to sell the bond back to the issuer at specified times for a specified price. At each puttable date prior to the bond maturity, the investor may get the investment money back by selling the bond back to the issuer. The underlying bonds can be fixed rate bonds or floating rate bonds. A puttable bond can therefore be considered a vanilla underlying bond with an embedded Bermudan style option. Puttable bonds protect investors. Therefore, a puttable bond normally pays investors a lower coupon than a non-callable bond. 

Although a puttable bond is a higher cost to the investor and an uncertainty to the issuer comparing to a regular bond, it is actually quite attractive to both issuers and investors. For investors, puttable bonds allow them to reduce interest costs at a future date should rate increase. For issuers, puttable bonds allow them to pay a lower interest rate of return until the bonds are sold back. If interest rates have increased since the issuer first issues the bond, the investor is like to call its current bond and reinvest it at a higher coupon. This presentation gives an overview of puttable bond and valuation model. 


	Puttable Bond Definition
	A puttable bond is a bond in which the investor has the right to sell the bond back to the issuer at specified times (puttable dates) for a specified price (put price).
	At each puttable date prior to the bond maturity, the investor may sell the bond back to its issuer and get the investment money back.
	The underlying bonds can be fixed rate bonds or floating rate bonds.
	A puttable bond can therefore be considered a vanilla underlying bond with an embedded Bermudan style option.
	Puttable bonds protect investors. Therefore, a puttable bond normally pays investors a lower coupon than a non-callable bond. 

	The Advantage of Puttable Bonds
	Although a puttable bond is a higher cost to the investor and an uncertainty to the issuer comparing to a regular bond, it is actually quite attractive to both issuers and investors.
	For investors, puttable bonds allow them to reduce interest costs at a future date should rate increase.
	For issuers, puttable bonds allow them to pay a lower interest rate of return until the bonds are sold back.
	If interest rates have increased since the issuer first issues the bond, the investor is like to call its current bond and reinvest it at a higher coupon.

	Puttable Bond Payoffs
	At the bond maturity T, the payoff of a puttable bond is given by


V_p (T)={■(F+C                    if not ptted@〖max⁡(P〗_p,F+C)        if putted)┤
where 
F – the principal or face value; 
C – the coupon; 
	P_p – the put price; 
max (x, y) – the maximum of x and y
T -  the maturity date;


	The payoff of the puttable bond at any call date T_i can be expressed as

V_p (T_i )={■(¯V_(T_i )                                  if not putted@max⁡(P_p,¯V_(T_i ) )                        if putted)┤
where 	
¯V_(T_i ) – continuation value at T_i
P_p – the put price; 
max (x, y) – the maximum of x and y
T_i -  the i-th call date;




	Model Selection Criteria
	Given the valuation complexity of a callable bond (e.g., embedded Bermudan option), there is no closed form solution. Therefore, we need to select an interest rate term structure model and a numeric solution to price the callable bond.
	The selection of interest rate term structure models
	Popular IR term structure models: 
Hull-White, Linear Gaussian Model (LGM), Quadratic Gaussian Model (QGM), Heath Jarrow Morton (HJM), Libor Market Model (LMM).
	HJM and LMM are too complex.
	Hull-White is inaccurate for computing sensitivities.
	Therefore, we choose either LGM or QGM.
	 The selection of numeric approaches
	After selecting a term structure model, we need to choose a numeric approach to approximate the underlying stochastic process of the model.
	Commonly used numeric approaches are tree, partial differential equation (PDE), lattice, and Monte Carlo simulation.
	Tree and Monte Carlo are notorious for inaccuracy in sensitivity calculation.
	Therefore, we choose either PDE or lattice.
	We decide to use LGM plus lattice. 

	LGM Model
	The dynamics
dX(t)=α(t)dW
	Where X is the single state variable; W is the Wiener process.
	The numeraire is given by
N(t,X)=(H(t)X+0.5H^2 (t)ζ(t))/D(t)
	The zero coupon bond price is
B(t,X;T)=D(T)exp(-H(t)X-0.5H^2 (t)ζ(t))

	LGM Assumption
	The LGM model is mathematically equivalent to the Hull-White model but offers
	Significant improvements in calibration stability and accuracy.
	More accurate and stable in sensitivity calculation.
	The state variable is normally distributed under the appropriate measure.
	The LGM model has only one stochastic driver (one-factor), thus changes in rates are perfected correlated.

	LGM calibration
	Match today’s curve
At time t, X(0)=0 and H(0)=0. Thus Z(0,0;T)=D(T). In other words, the LGM automatically fits today’s discount curve.
	Select a group of market swaptions.
	Solve parameters by minimizing the relative error between the market swaption prices and the LGM model swaption prices.

	Valuation Implementation
	Calibrate the LGM model.
	Create the lattice based on the LGM: the grid range should cover at least 3 standard deviations.
	Find the underlying swap value at each final note.
	Conduct backward induction process iteratively rolling back from final dates until reaching the valuation date.
	Compare exercise values with intrinsic values at each exercise date.
	The value at the valuation date is the price of the callable bond.

	A real world example

Bond specification	Callable schedule
Buy Sell	Buy	Call Price	Notification Date
Calendar	NYC	100	1/26/2015
Coupon Type	Fixed	100	7/25/2018
Currency	USD		
First Coupon Date	7/30/2013		
Interest Accrual Date	1/30/2013		
Issue Date	1/30/2013		
Last Coupon Date	1/30/2018		
Maturity Date	7/30/2018		
Settlement Lag	1		
Face Value	100		
Pay Receive	Receive		
Day Count	dc30360		
Payment Frequency	6		
Coupon	0.012		



References:

https://finpricing.com/lib/EqRangeAccrual.html

https://bitbucket.org/cmrm11/fiputtable/downloads/FiPuttableBond-16.pdf



