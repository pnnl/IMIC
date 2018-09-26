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


### Files

*Injection_Results: This tarball includes results from the error injections. 
  Data is in json format. Each filename indicates the solver and dataset used for the experiments. 

*Reconstructed_Results: This tarball includes error injection results for all possible statement-vector pairs. 
  Data is in json format. Each filename indicates the solver     and dataset used for the experiments. 



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



