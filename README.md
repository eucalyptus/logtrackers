========================
 EUCALYPTUS LOG TRACKER
========================

## WIKI
See why LogTracker is useful: https://github.com/eucalyptus/logtrackers/wiki

## WHAT IS THIS?  

Since Eucalyptus is a distributed Cloud platform, it is often challenging to 
track and troubleshoot distributed computations that is the result of an 
end-user's request. For example, "RunInstances" result in database transaction 
at CLC, VM scheduling at CC, and VM allocation at NC. If any of the sub-operations 
fail, debugging the distributed systems can be a challenging task to cloud administrators.

To ease the pain, Eucalyptus 4.1 introduces a core support and tools for tracking 
distributed computations that is the result of a Cloud user's request. 


## EXAMPLE USAGE

`euca-req-history eucalyptus`

 *Print out the history of requests by account "eucalyptus". From the history, request-id is used below.*

`euca-req-track --ssh 95e9933e`
 
 *Ssh into the distributed Eucalyptus services and gather all the logs related to the request-id.*

`euca-req-track -d /var/log/eucalyptus -t rsyslog 95e9933e`

 *If the log files are being aggregated with rsyslog, the tool gathers the logs from the directory.*
     
 
## DEPENDENCIES

  tabulate
  dnspython
  
  For Centos, run `yum install python-pip`, followed by `pip install tabulate dnspython`
