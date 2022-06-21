# Hull White Volatility Calibration


Hull-White (HW) short interest rate volatilities are calibrated via at the money European swaptions. There are two types of swaptions:

•	Payer swaption: A call option on the swap rate.
•	Receiver swaptions: A put option on the swap rate.

In Black’s framework, a European swaption is at the money if the strike level is equal to the forward swap rate. In this case, the prices of a payer and a receiver swaption on the same underlying swap will be equal. 

Mortgages are mapped to short rate volatilities, in order to value the embedded prepayment option. An open mortgage is a mortgage that allows the mortgagee to refinance at any time after a specified date; we will call this date the first exercise date.

European swaption pricing calculations are carried within Black’s framework. We assume that, under forward swap measure with numeraire equal to the swap’s annuity, the forward swap rate process, S, satisfies an SDE of the form 

The price of a European style payer swaption, with strike level X, is then given by Black Scholes. 

The mortgage short rate volatility mapping is a function of three variables:

•	Valuation date,
•	Mortgage maturity date,
•	First exercise date.

There are two possible cases to consider:

•	Case 1: The valuation date is after the first exercise date (i.e., the mortgage is fully open). In this case, the mortgage is assigned the short rate volatility implied from the European payer swaption with an option tenor of 1 month and an underlying swap maturity equal to the mortgage’s remaining term. 

•	Case 2: The first exercise date is after the valuation date. In this case, the mortgage is assigned the short rate volatility implied from the European payer swaption with an option tenor equal to the time remaining until the exercise date and an underlying swap maturity equal to the mortgage’s remaining term. 

In general, swaptions do not correspond exactly to points on the short rate volatility matrix, in which case, bilinear interpolation is used. For example, the calibrated HW short rate volatility for a 4.5 year option into 4.5 year swap would be computed as the bilinear interpolation of the short rate volatilities corresponding to the following swaptions:

•	4 year option into a 4 year swap, 
•	4 year option into to 5 year swap,
•	5 year option into a 4 year swap,
•	5 year option into a 5 year swap.

We will denote these swaptions by 4-5 and 5-5, respectively. We note that these option terms and underlying swap maturities correspond exactly to grid points on both the Blacks and short rate volatility matrices. Next, assume that the Hull-White short volatility for a 4.5 year option into 5 year swap can be computed by linearly interpolating the 4-5 and 5-5 short rate volatilities. To stress test this interpolation, GA interpolated the 4-5 and 5-5 Blacks volatilities to obtain a reference Blacks volatility for the 4.5-5 swaption. Next, the swaption was priced with respect to this Blacks volatility and, then, a HW short rate volatility was implied from this swaption price. Finally, the two short rates were compared. 


Reference:

https://finpricing.com/lib/EqConvertible.html

https://osf.io/vwpkx/wiki/home/

https://osf.io/q6sv3/download
