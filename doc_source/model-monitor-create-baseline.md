# Create a Baseline<a name="model-monitor-create-baseline"></a>

The baseline calculations of statistics and constraints are needed as a standard against which data drift and other data quality issues can be detected\. Model Monitor provides a built\-in container that provides the ability to suggest the constraints automatically for CSV and flat JSON input\. This *sagemaker\-model\-monitor\-analyzer* container also provides you with a range of model monitoring capabilities, including constraint validation against a baseline, and emitting Amazon CloudWatch metrics\. This container is based on Spark version 3\.3\.0 and is built with [Deequ](https://github.com/awslabs/deequ) version 2\.0\.2\. All column names in your baseline dataset must be compliant with Spark\. For column names, use only lowercase characters, and `_` as the only special character\.

The training dataset that you used to train the model is usually a good baseline dataset\. The training dataset data schema and the inference dataset schema should exactly match \(the number and order of the features\)\. Note that the prediction/output columns are assumed to be the first columns in the training dataset\. From the training dataset, you can ask SageMaker to suggest a set of baseline constraints and generate descriptive statistics to explore the data\. For this example, upload the training dataset that was used to train the pretrained model included in this example\. If you already stored the training dataset in Amazon S3, you can point to it directly\.

**To Create a baseline from a training dataset** 

When you have your training data ready and stored in Amazon S3, start a baseline processing job with `DefaultModelMonitor.suggest_baseline(..)` using the [Amazon SageMaker Python SDK](https://sagemaker.readthedocs.io)\. This uses an [Amazon SageMaker Model Monitor prebuilt container](model-monitor-pre-built-container.md) that generates baseline statistics and suggests baseline constraints for the dataset and writes them to the `output_s3_uri` location that you specify\.

```
from sagemaker.model_monitor import DefaultModelMonitor
from sagemaker.model_monitor.dataset_format import DatasetFormat

my_default_monitor = DefaultModelMonitor(
    role=role,
    instance_count=1,
    instance_type='ml.m5.xlarge',
    volume_size_in_gb=20,
    max_runtime_in_seconds=3600,
)

my_default_monitor.suggest_baseline(
    baseline_dataset=baseline_data_uri+'/training-dataset-with-header.csv',
    dataset_format=DatasetFormat.csv(header=True),
    output_s3_uri=baseline_results_uri,
    wait=True
)
```

**Note**  
If you provide the feature/column names in the training dataset as the first row and set the `header=True` option as shown in the previous code sample, SageMaker uses the feature name in the constraints and statistics file\.

The baseline statistics for the dataset are contained in the statistics\.json file and the suggested baseline constraints are contained in the constraints\.json file in the location you specify with `output_s3_uri`\.


**Output Files for Tabular Dataset Statistics and Constraints**  

| File Name | Description | 
| --- | --- | 
| statistics\.json |  This file is expected to have columnar statistics for each feature in the dataset that is analyzed\. For more information about the schema for this file, see [Schema for Statistics \(statistics\.json file\)](model-monitor-byoc-statistics.md)\.  | 
| constraints\.json |  This file is expected to have the constraints on the features observed\. For more information about the schema for this file, see [Schema for Constraints \(constraints\.json file\)](model-monitor-byoc-constraints.md)\.  | 

The [Amazon SageMaker Python SDK](https://sagemaker.readthedocs.io) provides convenience functions described to generate the baseline statistics and constraints\. But if you want to call processing job directly for this purpose instead, you need to set the `Environment` map as shown in the following example:

```
"Environment": {
    "dataset_format": "{\"csv\”: { \”header\”: true}",
    "dataset_source": "/opt/ml/processing/sm_input",
    "output_path": "/opt/ml/processing/sm_output",
    "publish_cloudwatch_metrics": "Disabled",
}
```