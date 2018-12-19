# IMIC : Iterative Method Fault Injection Collection

In this study, we present a comprehensive characterization of the impact of soft errors on the convergence characteristics of six iterative methods using application-level fault injection. In particular, we consider the use of iterative methods to incrementally solve a linear systems of equations, which constitutes the core kernel in many scientific applications. We analyze the impact of soft errors in terms of the type of error (single- vs multi-bit), the distribution and location of bits affected, the data structure and the statement impacted, and variation with time. In addition to understanding the vulnerability of iterative solvers to soft errors, this characterization can aid the design of fault injection campaigns that ensure systematic coverage.

This repo houses the experiment results from fault injection study conducted on 6 solvers using 28 datasets. 

## Solvers
* CG

* ICCG

* CGS

* BICG

* BICGSTAB

* QMR


### Datasets

Datasets are gathered from [SuiteSparse](https://sparse.tamu.edu/about) online tool, they are all positive definite sparse matrices.


### Data	 

All the data is provided in json format (see [Details](DETAILS.md) for explanation). 

You can find json files for each solver under the /data directory in this repository. 

### Reproducing the data

We also provide tools for reproducing the data collection environment. Head over to [Installation](INSTALL.md) for details. 

### NOTICE

This material was prepared as an account of work sponsored by an agency of the United States Government.  Neither the United States Government nor the United States Department of Energy, nor Battelle, nor any of their employees, nor any jurisdiction or organization that has cooperated in the development of these materials, makes any warranty, express or implied, or assumes any legal liability or responsibility for the accuracy, completeness, or usefulness or any information, apparatus, product, software, or process disclosed, or represents that its use would not infringe privately owned rights.
Reference herein to any specific commercial product, process, or service by trade name, trademark, manufacturer, or otherwise does not necessarily constitute or imply its endorsement, recommendation, or favoring by the United States Government or any agency thereof, or Battelle Memorial Institute. The views and opinions of authors expressed herein do not necessarily state or reflect those of the United States Government or any agency thereof.


<p align="center">PACIFIC NORTHWEST NATIONAL LABORATORY<br>
<i>operated by</i><br>
BATTELLE<br>
<i>for the</i><br>
UNITED STATES DEPARTMENT OF ENERGY<br>
<i>under Contract DE-AC05-76RL01830</i></p>


### COPYRIGHT

Copyright © 2018, Battelle Memorial Institute

1.	  Battelle Memorial Institute (hereinafter Battelle) hereby grants permission to any person or entity lawfully obtaining a copy of this software and associated documentation files (hereinafter “the Software”) to redistribute and use the Software in source and binary forms, with or without modification.  Such person or entity may use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and may permit others to do so, subject to the following conditions:
•	  Redistributions of source code must retain the above copyright notice, this list of conditions and the following disclaimers. 
•	  Redistributions in binary form must reproduce the above copyright notice, this list of conditions and the following disclaimer in the documentation and/or other materials provided with the distribution. 
•	  Other than as used herein, neither the name Battelle Memorial Institute or Battelle may be used in any form whatsoever without the express written consent of Battelle.  
2.	  THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL BATTELLE OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.

 
