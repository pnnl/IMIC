# IMIC : Iterative Method Fault Injection Collection

This repo houses the experiment results from fault injection study conducted on 6 solvers using 28 datasets. 

## Solvers
*CG

*ICCG

*CGS

*BICG

*BICGSTAB

*QMR


### Datasets

Datasets are gathered from [SuiteSparse](https://sparse.tamu.edu/about) online tool, they are all positive definite sparse matrices.


### Installation

This repo also provide installation tools for reproducing the data collection environment. Here are the steps for installation:

* download IMIC_installer.tar.gz and extract the files

* run `bash IMIC_installer.sh`



If installation finishes without any errors, there should be a IMIC folder ready. Under this folder you will find: 

* SparseLib++/ 	: SparseLib library downloaded from [https://math.nist.gov/sparselib++/](https://math.nist.gov/sparselib++/)

* Datasets/	: Folder for all datasets. There is an example dataset file obtained from [SuiteSparse](http://faculty.cse.tamu.edu/davis/suitesparse.html)

* readRB/	: Rutherford-Boeing format data reader, patched from Harwell-Boeing format reader of SparseLib++

* iters/	: Directory to house solvers' base iteration values. ie. the number of iterations it takes the solver to converge without any errors injected.

  - /cg.csv	: For each solver there should be a csv file, each line corresponding to another dataset, and each line consists of SOLVER,DATASET,ITERATIONS

* src/		: Source files used for the executable, `cg.h` and other solver implementations are obtained from [IML++ v1.2a](https://math.nist.gov/iml++/)  				

  - /cg.h	: This implementation is instrumented with our fault injection mechanism as an example 




### Running the Injector
After the installation is completed you can run your own fault injection experiments for CG solver :

Go to `IMIC/src/` . here you should find `cg_collect`. 

Usage: ./cg_collect RBfile ISINSERT LINE_POSITION VECTOR_NUMBER ITERATION_NUMBER POSITION NUMBITFLIPS BITPOSITIONS 

* RBFile	    : \[string\]Path to dataset file in Rutherford-Boeing format

* ISINSERT	    : \[0|1\]Boolean value to determine if we want an injection to be done or not 0: no injection, 1: injection. If 0 is given, rest of the variables are not read

* LINE_POSITION	    : \[int\]Statement number in the algorithm, for CG it varies between \[0\-7\)

* VECTOR_NUMBER	    : \[int\]The vector id that is going to be injected with a fault, for CG the ids are: p:0, q:1, r:2, x:3, z:4. 

* ITERATION_NUMBER  : \[int\]The iteration in which during an error is injected. max is base iterations (number of iterations it takes for the algorithm to converge without any errors present) 

* POSITION	    : \[int\]Position in the vector that the error is introduced. max is the last index of the vector ( can be determines from the size of the dataset)

* NUMBITFLIPS	    : \[int\]Number of bits to be flipped

* BITPOSITIONS	    :\[space seperated integers \]The bit positions within the 64bit float to be flipped 


Here are some example usages:

`./cg_collect ../Datasets/bcsstk14/bcsstk14.rb 0 0 0 0 0 0`

Run CG solver using bcsstk14 dataset without injecting any erros


`./cg_collect ../Datasets/bcsstk14/bcsstk14.rb 1 4 0 122 164 2 11 58`
Run CG solver using bcsstk14 dataset with an error injected at the 4th statement, into vector id:0, during 122th iteration, 2 bit flips (11th and 58th) in the vector's 164th position.

### Analyzing the output

`Using dataset: bcsstk14

Fault inserted 122

Iterative method: Diagonal Preconditioned CG

iterations performed: 203

Experimental Parameters:

Baseline iterations: 195

Iteration Check: ANOMALY

Place in iterations space (when): 122

Place in vector (where): 164

Place among statements: 4

Place among vectors: 0

Bit flips: 11 58 

Last iteration found: 203`


Above is an example (simplified) output from the second example command. THe output first gives us which dataset, preconditioner, solver is used. 

It gives the number of iterations performed, expected iteration count(baseline iterations) and resulting classification for this result (MASKED | ANOMALY | ADVERSE) 
*MASKED means the execution took the same number of iterations as expected
*ANOMALY means it took more or less than the expected number of iterations
*ADVERSE means it took more than 2 times the expected number of iterations

Some outputs has another line like `Activation enabled at 313`. This means the solver exited the loop at the 313th iteration but it converged to a wrong value, so our system restarted (reactivated) the iteration. 
When classifying these instances, we label them as NOTCONVERGED (as they didn't converge to the right solution)
 
Output also lists other experimental parameters for the injection (vector, statement, position, etc)  

### Files

*Injection_Results: This tarball includes results from the error injections. 
  Data is in json format. Each filename indicates the solver and dataset used for the experiments. 

*Reconstructed_Results: This tarball includes error injection results for all possible statement-vector pairs. 
  Data is in json format. Each filename indicates the solver and dataset used for the experiments. 



## Json Format

Each file in both tar files has the same structure. Each Json line in each file has the information about a separate injection. 

You can find the explanations of each attribute in the Json below:

      "solver"    : The iterative solver used in the experiment
      
      "stmt"      : Statement id in the algorithm that the error was injected
      
      "vec"       : The vector id that the error was injected 
      
      "ds"        : The dataset used in the experiment
      
      "inj_itr"   : The iteration when the error was injected
      
      "vec_pos"   : Position in the vector where error was injected
      
      "err_dist"  : Error distribution used for the injection (uniform, normal, beta)
      
      "num_bits"  : Number of bits flipped for the injection (1,2 or 4)
      
      "bit_pos"   : Position(s) of the bit(s) that were flipped
      
      "base_itr"  : The number of iterations it took the error free run to solve the equation A.x = b
      
      "tot_itr"   : The number of iterations it took the injected run to solve the equation
      
      "activation": After an error is injected, if there is an SDC, solver will converge to a wrong result. In that case, our set-up restarts the loop from the beginning calling it an activation. 
      
      If activation is '-1' it means resulting vector was not wrong, if it is any other value, (>0), it means the solver exited the loop at that iteration but with a wrong value.   
              
      "masked"    : Indicates if the injection was masked or not (0 or 1)
      
      "vec_size"  : The size of the vectors in the algorithm



