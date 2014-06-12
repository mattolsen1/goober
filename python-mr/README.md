
$ wget http://www.gutenberg.org/cache/epub/2701/pg2701.txt
$ head -n1000 pg2701.txt | ./mapper.py | sort | ./reducer.py
$ hadoop dfs -mkdir wordcount
$ hadoop dfs -copyFromLocal ./pg2701.txt wordcount/mobydick.txt
$ hadoop dfs -ls wordcount/mobydick.txt


$ hadoop \
   jar /opt/hadoop/contrib/streaming/hadoop-streaming-1.0.3.jar \
   -mapper "python $PWD/mapper.py" \
   -reducer "python $PWD/reducer.py" \
   -input "wordcount/mobydick.txt"   \
   -output "wordcount/output"
