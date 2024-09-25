## Cheat code to avoid getting banned

Run the check_gpu_util.py file in your terminal on any login node. I recommend to start a screen and run it in the background. It picks up jobs on it's own and maintain underutilisations of each of the jobs and kills an underutilised job.
To actually kill a job, you need to uncomment the kill_job(job_id) lines
