# Current Trends in FPM
There are multiple optimization algorithms based on Phase Retreival (Ptychography)
1. Maximum likelihood estimation
2. Wirtinger Flow optimization (WFP)
3. EPRY-FPM
4. Sequential Gaussian Newton method
5. mPIE
6. adaptive step-size approach
7. convex relaxation
8. nonlinear method
9. truncated Poisson Wirtinger reconstruction (TPWFP)

These methods are broadly divided into two categories:

**Incremental Algorithms:**
These are sequential algorithms which only update a small patch of the object function in each update. Gradient descent in this case uses an 'approximate gradient' computed from only a part of data.
**Global Algorithms**
They update entire object function in every iteration
