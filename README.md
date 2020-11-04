# amazon_mapreduce
Java code for map reduce on dsba-hadoop.uncc.edu.  There are 14,741,571 amazon products and 153,871,242 amazon product reviews.

# Executing AmazonProductAnalyzeFields
**Be sure to replace "rfox12" with your own user name below!**
1. Log into dsba-hadoop.uncc.edu using ssh
2. `git clone https://github.com/rfox12-edu/amazon_mapreduce.git` to clone this repo
3. Go into the repo directory.  In this case: `cd amazon_mapreduce`
4. Make a "build" directory (if it does not already exist): `mkdir build`
5. Compile the java code (all one line).  You may see some warnings--that' ok. 
`javac -cp /opt/cloudera/parcels/CDH/lib/hadoop/client/*:/opt/cloudera/parcels/CDH/lib/hbase/* AmazonProductAnalyzeFields.java -d build -Xlint`
6. Now we wrap up our code into a Java "jar" file: `jar -cvf process_products.jar -C build/ .`
7. This is the final step  
 - Note that you will need to delete the output folder if it already exists: `hadoop fs -rm -r /user/rfox12/product_fields` otherwise you will get an "Exception in thread "main" org.apache.hadoop.mapred.FileAlreadyExistsException: Output directory hdfs://dsba-nameservice/user/... type of error.
 - Now we execute the map-reduce job: `HADOOP_CLASSPATH=$(hbase mapredcp):/etc/hbase/conf hadoop jar process_products.jar AmazonProductAnalyzeFields '/user/rfox12/product_fields'`
 - Once that job completes, you can concatenate the output across all output files with: `hadoop fs -cat /user/rfox12/product_fields/*` or if you have output that is too big for displaying on the terminal screen you can do `hadoop fs -cat /user/rfox12/product_fields/* > output.txt` to redirect all output to `output.txt`
 
 The output is:
 |field            |count       |
|-----------------|-----------:|
|also_buy|14741571|
|also_buy-array|3858772|
|also_buy-empty-array|10882799|
|also_view|14741571|
|also_view-array|4526771|
|also_view-empty-array|10214800|
|asin|14741571|
|asin-string|14741571|
|brand|14741571|
|brand-blank-string|1412807|
|brand-string|13328764|
|category|14741571|
|category-array|13492510|
|category-empty-array|1249061|
|date|14741571|
|date-blank-string|8746493|
|date-string|5995078|
|description|14741571|
|description-array|11466750|
|description-empty-array|3274821|
|details|12186060|
|details-empty-object|8808749|
|details-object|3377311|
|feature|14741571|
|feature-array|8770227|
|feature-empty-array|5971344|
|fit|14741571|
|fit-blank-string|14300379|
|fit-string|441192|
|image|14741571|
|image-array|6568214|
|image-empty-array|8173357|
|main_cat|14741571|
|main_cat-blank-string|71696|
|main_cat-string|14669875|
|price|14741571|
|price-blank-string|7654647|
|price-string|7086924|
|rank|14741571|
|rank-array|5854170|
|rank-empty-array|343097|
|rank-string|8544304|
|similar_item|14741571|
|similar_item-blank-string|12739411|
|similar_item-string|2002160|
|tech1|14741571|
|tech1-blank-string|12808681|
|tech1-string|1932890|
|tech2|14741571|
|tech2-blank-string|14690866|
|tech2-string|50705|
|title|14741571|
|title-blank-string|4366|
|title-string|14737205|
