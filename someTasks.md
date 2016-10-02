#Sysbench
##CPU
`bin/boinc2docker_create_work.py mtrnord/docker-benchmark:latest sh -c "sysbench --debug --test=threads run 2>&1 | tee /root/shared/results/benchmark.txt"`
