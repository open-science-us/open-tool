# [H2O](http://www.h2o.ai)

### Installation
~~~
# Goto http://www.h2o.ai/download/h2o/desktop

curl -o h2o.zip http://download.h2o.ai/versions/h2o-3.8.1.4.zip

unzip h2o-3.8.1.4.zip

cd h2o-3.8.1.4

java -jar h2o.jar

Goto http://192.168.1.8:54321/
~~~

### Installation with R
~~~
# The following two commands remove any previously installed H2O packages for R.

if ("package:h2o" %in% search()) { detach("package:h2o", unload=TRUE) }
if ("h2o" %in% rownames(installed.packages())) { remove.packages("h2o") }

Removing package from ‘/Library/Frameworks/R.framework/Versions/3.2/Resources/library’

# Next, we download packages that H2O depends on.

pkgs <- c("methods","statmod","stats","graphics","RCurl","jsonlite","tools","utils")
for (pkg in pkgs) {
    if (! (pkg %in% rownames(installed.packages()))) { install.packages(pkg) }
}

# Now we download, install and initialize the H2O package for R.

> install.packages("h2o")

> library(h2o)

> localH2O <- h2o.init(nthreads = -1)

H2O is not running yet, starting it now...

Note:  In case of errors look at the following log files:
    /var/folders/6k/26gz272d5t503whnjyd5ssj80000gn/T//RtmpeD62jp/h2o_scheng_started_from_r.out
    /var/folders/6k/26gz272d5t503whnjyd5ssj80000gn/T//RtmpeD62jp/h2o_scheng_started_from_r.err

java version "1.8.0_66"
Java(TM) SE Runtime Environment (build 1.8.0_66-b17)
Java HotSpot(TM) 64-Bit Server VM (build 25.66-b17, mixed mode)

Starting H2O JVM and connecting: ... Connection successful!

R is connected to the H2O cluster: 
    H2O cluster uptime:         2 seconds 722 milliseconds 
    H2O cluster version:        3.8.1.3 
    H2O cluster name:           H2O_started_from_R_scheng_txh686 
    H2O cluster total nodes:    1 
    H2O cluster total memory:   0.89 GB 
    H2O cluster total cores:    4 
    H2O cluster allowed cores:  4 
    H2O cluster healthy:        TRUE 
    H2O Connection ip:          localhost 
    H2O Connection port:        54321 
    H2O Connection proxy:       NA 
    R Version:                  R version 3.2.3 (2015-12-10) 

Goto http://192.168.1.8:54321/
~~~
