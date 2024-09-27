## Cheat code to avoid getting banned

Run the gpu_util_checker.py file in your terminal on any login node. I recommend to start a screen and run it in the background. It picks up jobs on it's own and maintain underutilisations of each of the jobs and kills an underutilised job.
To actually kill a job, you need to uncomment the kill_job(job_id) lines


## Checking Balance

The following commands on the terminal will help you in checking the budget for a certain project. Please note that these commands are to be run on the login node only example: (base) [mt1210236@login02 ~]
```console
amgr login
```
You will be prompted to enter the password. To list your projects:
```console
amgr ls project
```
Now, I work with Prof. Tanmoy Chakraborty, so I have a project named tanchak.onetim. To check how much budget I have in this project, I run the following:
```console
amgr checkbalance project -n tanchak.onetime
```
