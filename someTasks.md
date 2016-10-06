#Sysbench
##CPU
`bin/boinc2docker_create_work.py mtrnord/docker-benchmark:latest sh -c "sysbench --debug --test=threads run 2>&1 | tee /root/shared/results/benchmark.txt"`

#OpenCV
##GPU
`bin/boinc2docker_create_work.py mtrnord/projectstreet_detection:latest sh -c "PYTHONPATH='/usr/lib/python2.7/dist-packages/' ./generateHaarDetector_street.sh 2>&1 | tee /root/shared/results/logs.txt"`
