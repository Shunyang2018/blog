## How to Speed up QCEIMS
### QC method

1. Multiple time step integrator

  **Plan:** break down GFN-xTB Hamiltonian into fast and slow part

 This is a challenging but doable part for me. To solve this problem, I need better understand on
 quantum chemistry and molecular dynamics. Also, since Lee-Ping is the expert in this field,
 I need to talk to him more frequently and regularly. If I can solve this problem before my QE,
 I will have 100% confidence to pass it.

 2. Combine different methods

  **Plan:** OM2 as ground state MD and GFN-xTB as production

  **Ground state MD Energy**  
  ![GFN_energy](/image/new143energy.png)

  GFN *GFN has more energy levels*
  ![OM2_energy](/image/143energy.png)

  OM2 methods

  This is an easy trial. Just modify the codes and keep the nodes running. Can be done at free time.


### Statistical method
1. Get a stable spectrum with less MD times

**Production MD #fragments**
  ![GFN_fragment](/image/newversion143.png)

  GFN *GFN has longer simulation time*

  ![OM2_fragment](/image/143fragments.png)

  OM2 methods

2. Change parameters

This could be the main part for my QE project. We already had some results and it's easy
to draw some conclusions. But we need to collect more chemistry knowledge into explanation.


### CS method
1. openMP
  how to parallel
2. running time analyses
  Find out witch step takes more time:
  [Performance Profiling](https://docs.oracle.com/cd/E19957-01/805-4940/6j4m1u7q2/index.html)


I am very interested in this subproject, this will help us understand how it runs on CPUs better.
And we can find a way to optimize the codes, even transfer the code to GPUs. But this project is
a littel far away from chemistry. I am more willing to dig into this after QE.

## Need to do
* At this time, finishing the QCEIMS paper has the highest priority. **Before Friday Dec 6**
* Get the statistical method test code running. **This weekend**
* Finish a review paper on QCEIMS and it's application in metabolomics.**Before the end of this quarter**
* Finish the draft and talk with Dean about the gold project paper. **Winter break**


## Task external

1) Code parser for qceims.out to calculate the reason of exit and time steps.
````
step   time [fs]    Epot       Ekin       Etot    error  #F   eTemp   frag. T | 	Reason
--------------------------------------------------------------------------------------------------
    900   1380.    -25.06868   0.1446   -24.92406  0.0006 1   21000.    4104.        	E X I T   M D  because of tmax has been reached
    900   1380.    -25.06868   0.1446   -24.92406  0.0006 1   21000.    4104.        	E X I T   M D  because of tmax has been reached
    900   1380.    -25.06868   0.1446   -24.92406  0.0006 1   21000.    4104.        	E X I T   M D  because of tmax has been reached
    900   1380.    -25.06868   0.1446   -24.92406  0.0006 1   21000.    4104.        	E X I T   M D  because of tmax has been reached
    900   1380.    -25.06868   0.1446   -24.92406  0.0006 1   21000.    4104.        	E X I T   M D  because of tmax has been reached
    900   1380.    -25.06868   0.1446   -24.92406  0.0006 1   21000.    4104.        	E X I T   M D  because of tmax has been reached
    900   1380.    -25.06868   0.1446   -24.92406  0.0006 1   21000.    4104.        	E X I T   M D  because of tmax has been reached
    900   1380.    -25.06868   0.1446   -24.92406  0.0006 1   21000.    4104.        	E X I T   M D  because of tmax has been reached

````


2) Analyze time [fs] for exit and


```

    							Count	Percent
    E X I T   M D  because nothing happens here anymore	194	25.12953
    E X I T   M D  because of nfrag=nfragexit		186	24.09326
    E X I T   M D  because of tmax has been reached	339	43.91192
    E X I T   M D  because of multiple fragments	53	6.86528




```
3) Analyze quality of spectra with 5,10,15,20,25 * number of atoms, based on qceims.res analysis for subsequent temp directories

## Program got stuck

### SCC not converged
#### Reason1: Actual 2 fragments, but we thought it's one. (qceims.out)
```
   inter fragment distances (Angst.)

           1         2         3         4

    1   0.00000
    2   4.93472   0.00000
    3  15.69160  18.64043   0.00000
    4  16.03335  13.62240  28.79924   0.00000

 computing IPs with XTB at (K)   4916.
SCC not converged
```
**solution: hard to find a better way to define a fragment; need a lot of tests.**
coord:
```
8

S	4.21054	8.02837	-0.31989
C	5.1151	8.0825	-3.048
C	13.0601	7.79535	-1.04052
H	6.92649	8.61662	-3.82286
H	3.65999	7.29727	-4.28192
H	11.0054	7.33935	-0.98352
H	14.30881	7.11221	0.40712
H	13.01674	9.77721	-1.83008
```

#### Reason2: Just not converged(qceims.out)
```
avcycle =   50    more =  250

step   time [fs]    Epot       Ekin       Etot    error  #F   eTemp   frag. T
      0      0.    -20.18971   0.0594   -20.13029  0.0000 1    5000.     695.
    100     50.    -20.17594   0.0966   -20.07935  0.0000 1    5000.     942.
    200    100.    -20.14071   0.1454   -19.99528  0.0000 1    5000.    1151.
    300    150.    -20.07645   0.1649   -19.91152  0.0000 1    5000.    1381.
    400    200.    -20.08032   0.2432   -19.83716  0.0000 1    5000.    1659.
    500    250.    -20.03967   0.2505   -19.78916  0.0000 1    5000.    1905.
    600    300.    -20.02677   0.2772   -19.74956  0.0000 1    5000.    2129.
    700    350.    -19.98898   0.3543   -19.63470  0.0000 1    5000.    2345.
    800    400.    -19.98386   0.4064   -19.57748  0.0000 1    5000.    2606.
    900    450.    -19.92756   0.3623   -19.56528  0.0000 1    5000.    2842.
   1000    500.    -19.92721   0.4715   -19.45567  0.0000 1    5000.    3064.
   1100    550.    -19.95021   0.5111   -19.43912  0.0000 2    5000.    3645.  8466.
   1200    600.    -20.00059   0.5600   -19.44060  0.0000 2    5000.    3916.  9360.
   1300    650.    -19.92554   0.4969   -19.42863  0.0000 2    5000.    3781.  7905.
   1400    700.    -19.84840   0.4265   -19.42191  0.0000 2    5000.    3796.  6122.
   1500    750.    -19.81527   0.3804   -19.43484  0.0000 3    5000.    3270.  4055.  7832.
SCC not converged
```
**solution: catch the error information and stop the process**
coord:
```
18			

S	1.78274	7.82976	8.34857
C	6.40366	17.0264	-11.22789
C	4.90113	18.73804	-10.46774
C	-10.72444	17.38046	-14.34567
C	1.40078	4.1999	13.71945
C	1.08827	1.57931	12.5908
H	5.1336	19.74066	-8.86432
H	6.48994	15.31812	-10.83998
H	7.30355	18.84539	-11.56004
H	3.15313	10.02538	7.96832
H	-10.06331	16.13587	-13.007
H	-10.03317	16.27188	-16.18967
H	-10.04083	18.98395	-13.82771
H	-0.45977	5.08437	13.87991
H	3.23205	4.78335	14.31882
H	2.93856	0.97881	11.74942
H	0.36766	2.51487	10.51831
H	0.00497	-0.07728	13.04497
```
When we repeat those two mnolecules, it will be converged.
Something could be wrong with the system!
### Can't find parameter file
**solution: complie the GFN parameter file in the program**
