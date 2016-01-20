# lockContention

Utility to diagnose lock contention on a Caché DB System

This tool analyzes the lock table, and reports the lock and process information for any process that is either waiting on a lock, or the owner of a lock being waited on. 

# Example:

usage: 

    do ^lockContention()

example output:

     Owner       Mode      Flags FullReference
      2188          X            ^["^^/intersystems/latest/mgr/tools/"]x
        2189       X:E
        2190       X:E
        2191       X:E


       PID        Src    GblRefs       Cmds      State       Line
      2188        h 1        269        948       HANG +8^testlocks
      2189      l +^x         23        183      LOCKW +5^testlocks
      2190      l +^x         23        183      LOCKW +5^testlocks
      2191      l +^x         23        183      LOCKW +5^testlocks

In this case, process 2188 is waiting owns an exclusive lock on ^x, and processes 2189, 2189 and 2191 are waiting on the lock. The first table only shows locks for which at least one process is waiting, and the second table only shows information for the processes found in the first table. 

This is equivalent to using ^LOCKTAB or the Management Portal to find contended locks, and manually looking up the process in ^JOBEXAM or the Portal, only this is done automatically, and (nearly) instantaneously, so transient issues are easier to identify accurately. 
