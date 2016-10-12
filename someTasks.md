#Sysbench
##CPU
`bin/boinc2docker_create_work.py mtrnord/docker-benchmark:latest sh -c "sysbench --debug --test=threads run 2>&1 | tee /root/shared/results/benchmark.txt"`

#OpenCV
##GPU
`bin/boinc2docker_create_work.py  --rsc_fpops_est 1000000000000 --delay_bound 1.21e+6 mtrnord/projectstreet_detection:latest sh -c "./generateHaarDetector_street.sh 2>&1 | tee /root/shared/results/logs.txt"`
