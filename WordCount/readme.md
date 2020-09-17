#### compile source code
$ bin/hadoop com.sun.tools.javac.Main WordCount.java      
$ jar cf wc.jar WordCount*.class      

${JAVA_HOME}/lib/tools.jar 的目录结构有com/sun/tools/javac/Main.class,
hadoop指令会在classpath中找com.sun.tools.javac.Main类，而其搜索路径就包含了tools.jar   

平时很多时候用的是javac命令，而现在用hadoop com.sun.tools.javac.Main    
两者都是可以正常编译java文件的   
javac程序应该是com.sun.tools.javac下的class文件打包而成的可执行程序，作用是一样的，只是一个是由javac指令来执行    
另一个是由hadoop调用com.sun.tools.javac.Main.class文件来执行    

如果用javac命令的话，还需要针对其另外配置   
在/etc/profie中加入以下路径     
export CLASSPATH="${HADOOP_HOME}/share/hadoop/common/hadoop-common- 2.7.7.jar:${HADOOP_HOME}/share/hadoop/mapreduce/hadoop-mapreduce-client-core-2.7.7.jar:${HADOOP_HOME}/share/hadoop/common/lib/commons-cli-1.2.jar
      
#### about job
     // Create a new Job
     Job job = Job.getInstance();
     job.setJarByClass(MyJob.class);
     
     // Specify various job-specific parameters     
     job.setJobName("myjob");
     
     job.setInputPath(new Path("in"));
     job.setOutputPath(new Path("out"));
     
     job.setMapperClass(MyJob.MyMapper.class);
     job.setReducerClass(MyJob.MyReducer.class);

     // Submit the job, then poll for progress until the job is complete
     job.waitForCompletion(true);

       
 
#### ref url
https://blog.csdn.net/helloworld0906/article/details/89455806      
https://blog.csdn.net/beijihukk/article/details/53810939    

https://hadoop.apache.org/docs/stable/api/org/apache/hadoop/mapreduce/Job.html
