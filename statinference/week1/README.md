Week 1
======

### [Introduction](introduction.md)

### Probability

- notations
  - the sample space is the collection of possible outcomes of an experiment
  - an event is a subset of the sample space
  - an elementary or simple event is a particular result of an experiment
  - null event is an empty set

- set operations

- probability
  - a probability measure, P, is a function from the collection of possible events

### Random variables, densities and pmfs
  
- **Random variable**: a numerical outcome of an experiment
  - two varieties: discrete or continuous
    - discrete random variables
	- continuous random variables

- **PMF**: probability mass functions
  - a probability mass function evaluated at a value corresponding to the probability that a random variable takes that value
  1. ![$p(x) \geq 0$](http://latex.codecogs.com/gif.latex?p%28x%29%20%5Cgeq%200) for all x
  2. ![$\sum_{x} p(x) = 1$](http://latex.codecogs.com/gif.latex?%5Csum_%7Bx%7D%20p%28x%29%20%3D%201)

- **PDF**: probability density functions
  - a probability density function is a function associated with a continuous random variable
  - areas under pdfs correspond to probability for that random variable
  1. ![$f(x) \geq 0$](http://latex.codecogs.com/gif.latex?f%28x%29%20%5Cgeq%200) for all x
  2. The area under f(x) is one.

### Distribution functions and quantiles
  
- **CDF**: Cumulative Distribution Function
  - ![F(x)=P(X\leq{x})](http://latex.codecogs.com/gif.latex?F%28x%29%3DP%28X%5Cleq%7Bx%7D%29)
  - survival function: ![S(x)=P(X>x)](http://latex.codecogs.com/gif.latex?S%28x%29%3DP%28X%3Ex%29)
  - S(x)=1-F(x)
  - for continuous random variables, the PDF is the derivative of the CDF

- **Quantiles**
  - the ath quantile of a distribution with distribution function F is the point xaso that F(xa)=a
  - a **percentile** is simply a quantile with a expressedas a percent
  - the median (population median) is the 50th percentile

### Expected values, discrete random variables, continuous random variables
  
- **Expected values**
  - the expected value or mean of a random variable is the center of its distribution

- for discrete random variable X with PMF p(x)
  - ![E[X]=\sum_xxp(x)](http://latex.codecogs.com/gif.latex?E%5BX%5D%3D%5Csum_xxp%28x%29) where the sum is taken over the possible values of x
  - E[X] represents the center of mass of a collection of locations and weights

- for continuous random variable, X with density f, the expected value is
  - E[X] = the area under the function tf(t)
  - this definition borrows from the definition of center of mass for a continuous body

### Rules for expected values

- rules
  - E[aX+b] = aE[X]+b
  - E[X+Y] = E[X] + E[Y]
- the expected value of the sample mean is the population mean
- when the expected value of an estimator is what it's trying to estimate, we say that estimator is unbiased
	
*Example*

Let xi for i,...,n be a collection of random variables, each with a distribution with mean mu. Calculate the expected value of the sample average of Xi:

![\begin{align*}E\left[\frac{1}{n}\sum_{i=1}^{n}X_i\right]&=\frac{1}{n}E\left[\sum_{i=1}^nX_i\right]\\&=\frac{1}{n}\sum_{i=1}^{n}E[X_i]\\&=\frac{1}{n}\sum_{i=1}^{n}\mu=\mu\end{align*}](http://latex.codecogs.com/gif.latex?%5Cbegin%7Balign*%7DE%5Cleft%5B%5Cfrac%7B1%7D%7Bn%7D%5Csum_%7Bi%3D1%7D%5E%7Bn%7DX_i%5Cright%5D%26%3D%5Cfrac%7B1%7D%7Bn%7DE%5Cleft%5B%5Csum_%7Bi%3D1%7D%5EnX_i%5Cright%5D%5C%5C%26%3D%5Cfrac%7B1%7D%7Bn%7D%5Csum_%7Bi%3D1%7D%5E%7Bn%7DE%5BX_i%5D%5C%5C%26%3D%5Cfrac%7B1%7D%7Bn%7D%5Csum_%7Bi%3D1%7D%5E%7Bn%7D%5Cmu%3D%5Cmu%5Cend%7Balign*%7D)

### Variance

- **the variance** of a random variable is a measure of spread
  - if X is a random variable with mean mu, the variance of X is defined as the expected (squared) distance from the mean
  ![Var(x)=E[(x-\mu)^2]](http://latex.codecogs.com/gif.latex?Var%28x%29%3DE%5B%28x-%5Cmu%29%5E2%5D)
  - convenient compuational form
  ![Var(X)=E[X^2]-E[X]^2](http://latex.codecogs.com/gif.latex?Var%28X%29%3DE%5BX%5E2%5D-E%5BX%5D%5E2)
  Here ![E[y]=\sum_xyp_y(x)](http://latex.codecogs.com/gif.latex?E%5By%5D%3D%5Csum_xyp_y%28x%29)
  - if a is constance then ![Var(aX)=a^2Var(X)](http://latex.codecogs.com/gif.latex?Var%28aX%29%3Da%5E2Var%28X%29)
  - the square root of the variance is called the **standard deviation**
  - the standard deviation has the same units as X
  
- Interpreting variances
  - Chebyshev's inequality
  ![P(|X-\mu|>=k\sigma)\leq{\frac{1}{k^2}}](http://latex.codecogs.com/gif.latex?P%28%7CX-%5Cmu%7C%3E%3Dk%5Csigma%29%5Cleq%7B%5Cfrac%7B1%7D%7Bk%5E2%7D%7D)
  - IQs are often said to be distributed with a mean of 100 and a sd of 15
  
### Independence

- two events A and B are indepedent if P(A union B) = P(A) P(B)
- two random variables X and Y are independent if for any two sets A and B P([X in A] union [U in B]) = P(X in A) P(X in B)

### Correlation, Variances and IID RVs

- **IID random variables**
  - random variables are said to be *iid* if they a re independent and identically distributed
  - iid RVs are the default model for random samples

- **Covariance** between two random variables X and Y is defined as
  - Cov(X,Y)=E[(X-mu_x)(Y-mu_y)]=E[XY]-E[X]E[Y]
  - Cov(X,Y)=Cov(Y,X)
  - Cov(X,Y) can be either positive or negative
  
- **Correlation** between X and Y is
  - Cor(X,Y)=Cov(X,Y)/sqrt(Var(X)Var(Y))
  - -1 <= Cor(X,Y) <= 1
  - Cor(X,Y) is unitless
  - X and Y are uncorrelated if Cor(X,Y) = 0
  - X and Y are mo positively correlated, the closer Cor(X,Y) is to 1
  - X and Y are mo negatively correlated, the closer Cor(X,Y) is to -1
  
- Sample mean
  - suppose Xi are iid with variance sigma^2

![\begin{align*}Var(\bar{X})&=Var(\frac{1}{n}\sum_{i=1}^{n}X_i)\\&=\frac{1}{n^2}Var\left(\sum_{i=1}^{n}X_i\right)\\&=\frac{1}{n^2}\sum_{i=1}^{n}Var(X_i)\\&=\frac{1}{n^2}n\sigma^2\\&=\frac{\sigma^2}{n}\end{align*}](http://latex.codecogs.com/gif.latex?%5Cbegin%7Balign*%7DVar%28%5Cbar%7BX%7D%29%26%3DVar%28%5Cfrac%7B1%7D%7Bn%7D%5Csum_%7Bi%3D1%7D%5E%7Bn%7DX_i%29%5C%5C%26%3D%5Cfrac%7B1%7D%7Bn%5E2%7DVar%5Cleft%28%5Csum_%7Bi%3D1%7D%5E%7Bn%7DX_i%5Cright%29%5C%5C%26%3D%5Cfrac%7B1%7D%7Bn%5E2%7D%5Csum_%7Bi%3D1%7D%5E%7Bn%7DVar%28X_i%29%5C%5C%26%3D%5Cfrac%7B1%7D%7Bn%5E2%7Dn%5Csigma%5E2%5C%5C%26%3D%5Cfrac%7B%5Csigma%5E2%7D%7Bn%7D%5Cend%7Balign*%7D)

- sigma/sqrt(n) is called the standard error of the sample mean
- the standard error of the sample mean is the standard deviation of the distribution of the sample mean
- sigma is the standard deviation of the distribution of a single observation
- the sample mean has to be less variable than a single observation, therefore its standard deviation is divided by a sqrt(n)

### Sample Variance

![S^2=\frac{\sum_{i=1}^{n}(X_i-\bar{X})^2}{n-1}](http://latex.codecogs.com/gif.latex?S%5E2%3D%5Cfrac%7B%5Csum_%7Bi%3D1%7D%5E%7Bn%7D%28X_i-%5Cbar%7BX%7D%29%5E2%7D%7Bn-1%7D)

- the sample variance is an estimator of sigma^2
- the numerator has a version for quick calculation

![\sum_{i=1}^{n}(X_i-\bar{X})^2=\sum_{i=1}^{n}X_i^2-n\bar{X}^2](http://latex.codecogs.com/gif.latex?%5Csum_%7Bi%3D1%7D%5E%7Bn%7D%28X_i-%5Cbar%7BX%7D%29%5E2%3D%5Csum_%7Bi%3D1%7D%5E%7Bn%7DX_i%5E2-n%5Cbar%7BX%7D%5E2)

- the sample variance is (nearly) the mean of the squared deviations from the mean

![\begin{align*}E\left[\sum_{i=1}^{n}(X_i-\bar{X})^2\right]&=\sum_{i=1}^{n}E[X_i^2]-nE[\bar{X}^2]\\&=\sum_{i=1}^{n}\{Var(X_i)+\mu^2\}-n\{Var(\bar{X})+\mu^2\}\\&=\sum_{i=1}^{n}\{\sigma^2+\mu^2\}-n\{\sigma^2/n+\mu^2\}\\&=n\sigma^2+n\mu^2-\sigma^2\-n\mu^2\\&=(n-1)\sigma^2\end{align*}](http://latex.codecogs.com/gif.latex?%5Cbegin%7Balign*%7DE%5Cleft%5B%5Csum_%7Bi%3D1%7D%5E%7Bn%7D%28X_i-%5Cbar%7BX%7D%29%5E2%5Cright%5D%26%3D%5Csum_%7Bi%3D1%7D%5E%7Bn%7DE%5BX_i%5E2%5D-nE%5B%5Cbar%7BX%7D%5E2%5D%5C%5C%26%3D%5Csum_%7Bi%3D1%7D%5E%7Bn%7D%5C%7BVar%28X_i%29&plus;%5Cmu%5E2%5C%7D-n%5C%7BVar%28%5Cbar%7BX%7D%29&plus;%5Cmu%5E2%5C%7D%5C%5C%26%3D%5Csum_%7Bi%3D1%7D%5E%7Bn%7D%5C%7B%5Csigma%5E2&plus;%5Cmu%5E2%5C%7D-n%5C%7B%5Csigma%5E2/n&plus;%5Cmu%5E2%5C%7D%5C%5C%26%3Dn%5Csigma%5E2&plus;n%5Cmu%5E2-%5Csigma%5E2%5C-n%5Cmu%5E2%5C%5C%26%3D%28n-1%29%5Csigma%5E2%5Cend%7Balign*%7D)

- suppose Xi are iid with mean mu and variance sigma^2
  - S^2 estimates sigma^2
  - the calculation of S^2 involves dividing by n-1
  - S/sqrt(n) estimates sigma/sqrt(n) the standard error of the mean
  - S/sqrt(n) is called the sample standard error (of the mean)
  
