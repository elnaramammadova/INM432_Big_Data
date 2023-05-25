# INM432 Big Data Coursework

</br></br>
<i>https://colab.research.google.com/drive/1_FAdoDNE2SnyjFUuL9-4RH1IFtozXERU?usp=sharing</i>
<b>Task 1</b> – <i>Write TFRecord files to the cloud with Spark 1d. Optimization, experimentation, and discussion</i>
</br></br>
After compiling all our functions in a script file, we parallelize the data pre-processing in Spark using Google Cloud (GC) Dataproc. Three different cluster configurations (with 8vCPUs, SSD capacity = 500GB, and Standard disk capacity = 4096 GB) were tested to run PySpark jobs on the cloud:
</br>
</br>
- Single Cluster – Single machine with eightfold recourses (n1-standard-8) and max SSD of 500GB.
- Maximal Cluster – 1 master and 7 workers nodes each with 1 virtual CPU (n1-standard- 1). Master with full SSD capacity (500GB) and 7 worker nodes with equal shares of the standard disk capacity to maximize throughput (4096 GB / 7 ~= 585 GB).
- Four Cluster – 4 machines (1 master, 3 workers) with 2vCPUs each (n1-standard-2). Master full SSD capacity (500GB) and 3 worker nodes with equal shares to the standard disk capacity to maximize throughput (4096GB / 3 ~= 1365GB).

</br>
</br>
<b>Task 2</b> – <i>Speed Test</i>
</br>
</br>
In this task we implement code for time measurement to determine the throughput in images per second. We used multiple parameters in parallel with Spark:
batch_sizes = [8, 16, 32, 64] batch_numbers = [10, 30, 60] num_repetitions = [3]

<b>Task 3</b> – <i>Machine Learning in the cloud</i>
</br>
</br>
In this section we experimented with different distributed learning strategies (Mirrored- Strategy, Multi-Worker-Mirrored-Strategy, Experimental-Multi-Worker-Mirrored-Strategy) and batch sizes (16, 32, 64) on our ML model. While analyzing the batch sizes, the worst accuracies corresponded with the batch sizes of 16 and 64, making 32 the most suitable batch size for our model. When comparing between the strategies however, even though MirroredStrategy showed highest accuracies for both training and the validation, the validation accuracies are higher than training, which indicates that there is a high chance our model is overfitting. Hence, the best performing strategy is MultiWorkerMirroredStrategy with 32 batch sizes, up until epoch 15, after which our validation accuracies exceed of the training.
