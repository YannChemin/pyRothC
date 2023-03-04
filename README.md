<p align="center">
<!-- <a href="https://github.com/tiangolo/fastapi/actions?query=workflow%3ATest+event%3Apush+branch%3Amaster" target="_blank">
    <img src="https://github.com/tiangolo/fastapi/workflows/Test/badge.svg?event=push&branch=master" alt="Test">
</a>
<a href="https://coverage-badge.samuelcolvin.workers.dev/redirect/tiangolo/fastapi" target="_blank">
    <img src="https://coverage-badge.samuelcolvin.workers.dev/tiangolo/fastapi.svg" alt="Coverage">
</a> -->
<!-- <a href="https://pypi.org/project/fastapi" target="_blank">
    <img src="https://img.shields.io/pypi/v/fastapi?color=%2334D058&label=pypi%20package" alt="Package version"> -->
<!-- </a>
<a href="https://pypi.org/project/fastapi" target="_blank">
    <img src="https://img.shields.io/pypi/pyversions/fastapi.svg?color=%2334D058" alt="Supported Python versions">
</a> -->

<img alt="GitHub Repo stars" src="https://img.shields.io/github/stars/mishagrol/pyRothC?style=social">

<a href="https://github.com/mishagrol/pyRothC/issues" target="_blank">
    <img src="https://img.shields.io/github/issues/mishagrol/pyRothC" alt="Issues">
</a>



<a href="https://github.com/mishagrol/pyRothC/blob/main/LICENSE" target="_blank">
    <img src="https://img.shields.io/github/license/mishagrol/pyRothC" alt="License">
</a>
</p>

## pyRothC

<p align="left">
    <em>Python version of The Rothamsted carbon model (RothC) 26.3.</em>
</p>

________
**Documentation**: <a href="https://www.rothamsted.ac.uk/sites/default/files/RothC_guide_DOS.pdf" target="_blank">Rothamsted RothC Model</a>

**Source Code**: <a href="https://github.com/mishagrol/pyRothC" target="_blank">https://github.com/mishagrol/pyRothC</a>

---

pyRothc is a Python version of The Rothamsted carbon model (RothC) 26.3.


RothC is a model for the turnover of organic carbon in non-waterlogged topsoil that allows for the effects of soil type, temperature, soil moisture and plant cover on the turnover process.

Inspired by SoilR version <a href="https://www.bgc-jena.mpg.de/TEE/basics/2015/11/19/RothC/" target="_blank">SoilR RothC</a>

## Requirements

Python 3.7+

SciPy

NumPy

Pandas

## Installation

<div class="termy">

```console
$ pip install pyRothC
```

</div>

## Example


```Python

Temp=np.array([-0.4, 0.3, 4.2, 8.3, 13.0, 15.9,18.
                0, 17.5, 13.4, 8.7, 3.9,  0.6])
Precip=np.array([49, 39, 44, 41, 61, 58, 71, 58, 
                51,48, 50, 58])
Evp=np.array([12, 18, 35, 58, 82, 90, 97, 84, 54,
                31,14, 10])

soil_thick=25  #Soil thickness (organic layer 
                #topsoil), in cm
SOC=69.7       #Soil organic carbon in Mg/ha 
clay=48        #Percent clay
Cinputs=2.7   #Annual C inputs to soil in Mg/ha/yr


rothC = RothC(temperature=Temp, 
             precip=Precip, 
             evaporation=Evp,
             clay = 48,
             input_carbon=Cinputs,
             pE=1.0,
             C0=np.array([0, 0, 0, 0, 2.7]))

df = rothC.compute()

fig, ax = plt.subplots(1,1,figsize=(6,4))
df.plot(ax=ax)
ax.set_ylabel('C stocks (Mg/ha)')
plt.show()


```


## Structure of the RothC model

**Credits**: <a href="https://www.bgc-jena.mpg.de/TEE/software/bgc-md/soil/Jenkinson1977SoilScience-S0003/Report.html" target="_blank">Theoretical Ecosystem Ecology group of the Max Planck Institute for Biogeochemistry</a>


<p align="center">
  <a href="RothC"><img src="./plots/Logo.svg" alt="FastAPI"></a>
</p>

### Equations

$$
\begin{aligned}
& \frac{d \boldsymbol{C}}{\mathrm{d} t}=I\left(\begin{array}{c}
\gamma \\
1-\gamma \\
0 \\
0 \\
0
\end{array}\right) 
 +\left(\begin{array}{ccccc}
-k_1 & 0 & 0 & 0 & 0 \\
0 & -k_2 & 0 & 0 & 0 \\
a_{3,1} & a_{3,2} & -k_3+a_{3,3} & a_{3,4} & 0 \\
a_{4,1} & a_{4,2} & a_{4,3} & -k_4+a_{4,4} & 0 \\
0 & 0 & 0 & 0 & 0
\end{array}\right)\left(\begin{array}{l}
C_1 \\
C_2 \\
C_3 \\
C_4 \\
C_5
\end{array}\right) \\
&
\end{aligned}
$$
## Optional Dependencies

Matplotlib

## License

This project is licensed under the terms of the CC0 1.0 Universal license.