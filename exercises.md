
## Exercise 3.1: Submitting a simple job

Open the file called *hello_hpc.pbs*. This is a PBS script template, which will run the following bash command
echo hello hpc > result_hello_hpc.txt
Change some of the lines to match your details. In particular, for the following lines add your email address and your project name

- '#PBS -M your.email@sydney.edu.au'

- '#PBS -P RDS-FSC-VirusRates-RW'


Before you run the script, try running the command interactively. It will create a file called 'result_hello_hpc.txt' which will consist of a line: 'hello hpc'. After you run the script, inspect the contents of the file using *cat*, or with one of the text editors ('emacs' or 'nano').

Now submit the script to the HPC. To do this, use the command *qsub*:
qsub hello_hpc.pbs
Use *ls* to inspect the contents of your current directory:
HPC_training_test]$ ls
hello_hpc.pbs  hello_hpc.stderr  hello_hpc.stdout  result_hello_hpc.txt
Inspect the contents of the output files (hello_hpc.stderr, hello_hpc.stdout, and result_hello_hpc.txt)






## Exercise 3.2: Checking the status of a job

Open the file called *sleep.pbs*. It is an other PBS script with the following commands:
sleep 300
echo sleep complete > result_hello_hpc.txt
The first line will wait for 300 seconds (5 minutes). The second line will print a line to result_hello_hpc.txt when the process is complete. Again set your email address and project name, as in 3.1.
Run the job using qsub:
qsub sleep.pbs
We will now use the command bellow to check the job (substitute the content in <> with your corresponding details):
qstat -u <hpc_username>
This command will show you a list of the jobs that you are runnig or have in the queue. For example, my current jobs in the hpc are:
                                                            Req'd  Req'd   Elap
Job ID          Username Queue    Jobname    SessID NDS TSK Memory Time  S Time
--------------- -------- -------- ---------- ------ --- --- ------ ----- - -----
225548.mgmt1    sduc7183 gpu      p_229       36707   1   1    --  120:0 R 01:52
225549.mgmt1    sduc7183 gpu      pest_230    36750   1   1    --  120:0 R 01:52
225575.mgmt1    sduc7183 gpu      para_263    36897   1   1    --  120:0 R 01:52
225576.mgmt1    sduc7183 gpu      p_265       36908   1   1    --  120:0 R 01:52
225577.mgmt1    sduc7183 gpu      typh_266    36950   1   1    --  120:0 R 01:52
225746.mgmt1    sduc7183 compute  sleep      116888   1   1    --  01:00 R 00:00
Some important columns are the Job ID, and S. The job ID is useful if we need to kill the job, while *S* tells us whether the jobs is running (R) or queued (Q). Use the *qstat* command again after 5 minutes. You will find that your job is is no longer in the list of jobs in the queue or running.

## Excercise 3.3: Killing a job

Use qsub to sumbit the jobs called sleep_long.pbs. This is the same as sleep.pbs, but it will sleep for 10 minutes.
qsub sleep_long.pbs
Check that the job is running by using qstat:
qstat -u <hpc_username>
                                                            Req'd  Req'd   Elap
Job ID          Username Queue    Jobname    SessID NDS TSK Memory Time  S Time
--------------- -------- -------- ---------- ------ --- --- ------ ----- - -----
225576.mgmt1    sduc7183 gpu      p_265       36908   1   1    --  120:0 R 02:06
225577.mgmt1    sduc7183 gpu      typh_266    36950   1   1    --  120:0 R 02:06
225759.mgmt1    sduc7183 compute  sleep       32700   1   1    --  01:00 R 00:00
We will now kill the jobs before it is finished. This is useful if we need to correct a mistake, or if we need to free the queue. To do this, we use the command qdel and the process name. Note the job id from the qstat output and pass this argument to qdel. Note that you dont need to use the .mgmt1:
qdel 225759
Use qstat again to verify that the job is no longer running or in the queue.

# Exercise 4.1: Running a Python script on the HPC

Open the files *hello_python.pbs* and *my_python_script.py*. *my_python_script.py* is some simple python code. Note that the pbs file has the following line:
module load python
This is important when we need special modules from within python, such as numpy or scipy. The command *module load* is also what you should use to call any of the programs listed using *module avail*

Also note the following line in the script:
python my_python_script.py
This will execute the python code in *my_python_script.py*.

submit this job using *qsub* and check the output

## Exercise 4.2: Running an Rscript with a pdf plot

Open the files *my_r_script.R* and *hello_r.pbs*. *my_r_script.R* is some R code to generate a histogram of a standard normal variable into a pdf. Note the following line in the *hello_r.pbs* script.
module load R
In the pbs script, the following line executes the R code:
Rscript my_r_script.R
Run *hello_r.pbs* in the HPC using *qsub* and check the output. Note that there will be a pdf called *my_r_plot.pdf*. For some analyses it might be convenient to process the output and plot the results all in the HPC. Transfer this file to your system to see the output.


    
