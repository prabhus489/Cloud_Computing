##### Tagging Strategy
https://docs.aws.amazon.com/general/latest/gr/aws_tagging.html
https://d0.awsstatic.com/aws-answers/AWS_Tagging_Strategies.pdf
https://d1.awsstatic.com/whitepapers/aws-tagging-best-practices.pdf
https://docs.aws.amazon.com/general/latest/gr/aws_tagging.html
https://aws.amazon.com/about-aws/whats-new/2020/11/aws-managed-services-ams-now-offers-infrastructure-auto-tagging-functionality/
https://aws.amazon.com/premiumsupport/knowledge-center/tags-billing-cost-center-project/


https://aws.amazon.com/getting-started/hands-on/handle-serverless-application-errors-step-functions-lambda/

https://docs.aws.amazon.com/codepipeline/latest/userguide/reference-variables.html#w2aac47c29b9b7

https://boto3.amazonaws.com/v1/documentation/api/1.9.42/reference/services/sagemaker-runtime.html#SageMakerRuntime.Client.invoke_endpoint

https://docs.aws.amazon.com/lambda/index.html

#### Commands:
aws sagemaker-runtime invoke-endpoint \
  --endpoint-name https://runtime.sagemaker.Prod-endpoint/invocations \
  --body file://payload.csv \
  --content-type "text/csv" \
  predictions.txt
  
cat predictions.txt 
