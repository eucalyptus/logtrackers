========================
 EUCALYPTUS LOG TRACKER
========================

* WHAT IS THIS?  

Since Eucalyptus is a distributed Cloud platform, it is often challenging to 
track and troubleshoot distributed computations that is the result of an 
end-user's request. For example, <RunInstances> result in database transaction 
at CLC, VM scheduling at CC, and VM allocation at NC. If any of the sub-operations 
fail, debugging the distributed systems can be a challenging task to cloud administrators.

To ease the pain, Eucalyptus 4.1 introduces a core support and tools for tracking 
distributed computations that is the result of a Cloud user's request. 


* EXAMPLE USAGE

[root@]# ./euca-req-history eucalyptus
DATE                      SERVICE        REQUEST                        ID
------------------------  -------------  -----------------------------  --------
Thu Aug 28 22:56:31 2014  compute        DescribeInstances              49fe265b
Thu Aug 28 22:29:09 2014  compute        TerminateInstances             95e9933e
Thu Aug 28 16:09:19 2014  compute    	 RunInstances                   c9fcf72f

[root@]# ./euca-req-track --ssh 95e9933e
=======  ==============  ============  ==================  =======  ========================  ================================================================================
  ORDER  DATE            HOST          SERVICE             LEVEL    LOCATION                  LOG
=======  ==============  ============  ==================  =======  ========================  ================================================================================
      0  08-28 22:54:13  10.111.1.127  EC2/AS/ELB/OSG/IAM  DEBUG    ComputeService            TerminateInstancesType:59409956-5029-4cdd-99c8-4241365003a0:return=true:epoch=nu
      0                                                                                       ll:status=null
      0  08-28 22:54:13  10.111.1.127  EC2/AS/ELB/OSG/IAM  DEBUG    ComputeService            TerminateInstancesResponseType:59409956-5029-4cdd-99c8-4241365003a0:return=true:
      0                                                                                       epoch=null:status=null
      1  08-28 22:54:13  10.111.1.127  EC2/AS/ELB/OSG/IAM  INFO     VmRuntimeState            i-b4c4daae state change: RUNNING -> SHUTTING_DOWN (previously PENDING)
      1  08-28 22:54:13  10.111.1.127  EC2/AS/ELB/OSG/IAM  DEBUG    VmInstances               Cleaning up instance: i-b4c4daae RUNNING -> SHUTTING_DOWN
      1  08-28 22:54:13  10.111.1.127  EC2/AS/ELB/OSG/IAM  DEBUG    VmInstances               :1409291653892:VmInstances:VM_TERMINATING:SYSTEM_ADDRESS:Address 10.111.101.180
...
      2  08-28 22:54:14  10.111.1.135  CC                  DEBUG    init_thread               init=1 0x7fbb29b1f000 0x7fbaa41da000 0x7fbadae3b000 0x7fbadac35000
      2  08-28 22:54:14  10.111.1.135  CC                  INFO     print_abbreviated_instan  terminating 1 instance(s): i-b4c4daae
...
      3  08-28 22:54:14  10.111.1.176  NC                  INFO     doTerminateInstance       [i-b4c4daae] termination requested
      3  08-28 22:54:14  10.111.1.176  NC                  DEBUG    sensor_refresh_resources  polled statistics for 4 instance(s)
      3  08-28 22:54:14  10.111.1.176  NC                  DEBUG    terminating_thread        [i-b4c4daae] spawning terminating thread
      3  08-28 22:54:14  10.111.1.176  NC                  DEBUG    shutdown_then_destroy_do  shutting down instance

      
* DEPENDENCIES

  tabulate
  dnspython
  For Centos, run <yum install python-pip>, followed by <pip install tabulate dnspython>
