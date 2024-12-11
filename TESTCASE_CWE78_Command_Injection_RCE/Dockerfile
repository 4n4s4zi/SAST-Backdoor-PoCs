FROM ubuntu:20.04
EXPOSE 27015
WORKDIR /testcase
COPY . .
RUN apt update && apt -y install make gcc g++ curl wget python
RUN make build

#Need to run this interactively otherwise it doesn't work
#RUN ./build/CWE78_OS_Command_Injection__char_connect_socket_execl_32

