#  CloudFormationテンプレートの保管するためのS3バケットを作成
aws cloudformation create-stack --stack-name cfn-template-s3-store --template-body file://cloudformatin-template-s3-store.yml --parameters ParameterKey=CloudFormationTemplateBucketName,ParameterValue=cloudformatin-template-s3-store ParameterKey=ProjectName,ParameterValue=suzukis ParameterKey=Environment,ParameterValue=prod

# 
aws cloudformation create-stack --stack-name cfn-template-s3-store --template-body file://root-network.yml --parameters ParameterKey=CloudFormationTemplateBucketName,ParameterValue=cloudformatin-template-s3-store ParameterKey=ProjectName,ParameterValue=suzukis ParameterKey=Environment,ParameterValue=prod