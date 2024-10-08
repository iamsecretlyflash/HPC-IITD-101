## Internet connectivity

Use proxy.sh script to activate a proxy connection on a node. Recommended steps are to start a screen on a specific node and run ./proxy.sh.

```console
screen -S proxy
chmod +x proxy.sh
./proxy.sh
```
Use Ctrl + A, D to detach from screen

## PIP SSL ERROR

In case of an SSL error, this usually works for me

```console
pip install <PACKAGE/REQUIREMENTS_LIST/BUILD>  --trusted-host=pypi.org --trusted-host=files.pythonhosted.org --user
```

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
## Requesting Jobs

For requesting a job, you will be using a command like below

```console
qsub -P <PROJECT_NAME> -q high -lselect=1:ncpus=4:ngpus=1:centos=<haswell/skylake/icelake> -lwalltime=23:59:59 -I
```

Let's understand the command a little but. 
- I am confident you are smart enough to understand what PROJECT_NAME is. 
- Let's look at the -q flag. It's my favourite. There are three values this flag can take:
  - standard : denoting standard queue where the priority is very basic. Also, the prices are also normal: Rs 1/GPU/HOUR and Rs 0.1/GPU/HOUR
  - high : high queue. Priority is higher than standard. Prices are 5 times: Rs 5/GPU/HOUR and Rs 0.5/GPU/HOUR
  - scai_q : The big mommy/daddy of all queues. Dedicated queue for projects under Yardi School of AI. Used to get access to 80 GB A100s available in ScAI. I am not sure of prices but hey you get fricking awesome GPUs for cheap

- -lselect is again basic. The only argument that's interesting here is centos:
    - haswell : Poop GPUs
    - skylake : 32 GB V100s
    - icelake : 40GB A100 (standard) / 80GB A100 (scai_q)
 
- you can also request for memory in lselect
- lwalltime - you can request for a maximum of 168 hours on standard and high queue GPUs. 24 hours for scai_q A100s
-  -I : Interactive job

### HOW TO NOT LOSE A NODE AFTER JOB GETTING ALLOCATED

Very very important. I wish somebody told this to me when I was starting to use HPC.

HPC is so kind to offer the facility to use the screen command. (search screen on linux)

Make sure you send a job request on a screen session.

```Console
screen -S anti_job_blowout
```
screen window will open

```
qsub -P agi_is_here -q high -lselect=1:ncpus=4:ngpus=1:centos=icelake -lwalltime=23:59:59 -I
```

The job will start in this screen. Say you get allocated aice009. You should exit this screen by using Ctrl + A, D. From a login node do:

```
ssh aice009
```

This will take you to the GPU node where you can play.
