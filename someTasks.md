#Sysbench
##CPU
`bin/boinc2docker_create_work.py mtrnord/docker-benchmark:latest sh -c "sysbench --debug --test=threads run 2>&1 | tee /root/shared/results/benchmark.txt"`

#OpenCV
##GPU
`bin/boinc2docker_create_work.py mtrnord/ProjectStreet_Detection:latest sh -c "python face_detect.py abba.png haarcascade_frontalface_default.xml`
