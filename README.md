# Datascience Projects

This is not your average run-of-the-mill Kaggle notebook repo that only demonstrates that someone is able to write code for training and testing.
Yes, the above mentioned code is packed inside the individual notebooks, however I tried to cover as much of the ML-lifecycle and applied best-practices to make this code as generic and production-grade-able as possible.
Here are some of the used mechanics / design decisions / technologies used and the motivation behind them

* Using PySpark. This might be an overkill for datasets such as the 1K Titanic-Spaceship samples. However, when transitioning to bigger datasets, the benefits of using PySpark are
  * fault-tolerant: recover from failures easily as DAG is tracked and results of its nodes are cached in case of failure of downstream operations
  * fast: make use of SIMD instructions under the disguise of JVMs vector API
  * horizontal scaling: increase computation speed by adding workers to your spark cluster
* Use of serializable Pipelines
  * reproducible: the entire feature-extraction pipeline can be saved and stored as file and be executed at any time in order to guarantee the same ETL-Pipeline during training and testing
  * customizable: the modular design of the pipeline allows for exchanging specific steps, removing certain steps or adding further steps easily
* mlflow
  * acceleration: logging each experiment accelerates the experimentation process as already tested parameter sets are easily identifiable
  * reproducability: logging metrics, trained models and the training datasets enables reproducability of the experiments
