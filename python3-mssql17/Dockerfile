FROM centos:8

# OS deps
RUN yum install -y python3 python3-devel gcc gcc-c++ make unixODBC-devel

# MSSQL 2017 driver
RUN rpm -Uvh https://packages.microsoft.com/config/rhel/8/packages-microsoft-prod.rpm && \
      ACCEPT_EULA=y yum install -y msodbcsql17

# Python deps
RUN pip3 install pyodbc

WORKDIR /app
