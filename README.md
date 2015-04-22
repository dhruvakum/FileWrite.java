# FileWrite.java
//This java code explains how to create a file in HDFS or Append a line if file already exists


import java.io.IOException;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.fs.FileSystem;
import org.apache.hadoop.fs.FSDataOutputStream;

public class FileWrite {
 public static void main(String[] args)throws Exception {
 FSDataOutputStream fout =null;
 Configuration config = new Configuration();
 FileSystem fs= FileSystem.get(config);
 Path filenamepath = new Path(args[0]);
 try{
 if(fs.exists(filenamepath)){
 fout = fs.append(filenamepath);
 fout.writeUTF("Appending a new Line\n"); //this line will be printed if file already exits
 }
 else {
 fout = fs.create(filenamepath);
 //write a line to the file
 fout.writeUTF("This is is the first line in the file that you just created\n");
 //This line will create a new file if it is not available and adds the above line
 }
 }catch(Exception e){
 }
 finally{
 fout.close();
 }
 }
 }
