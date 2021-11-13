# CloudFormationテンプレートの保管するためのS3バケットを作成
aws cloudformation create-stack --stack-name cfn-template-s3-store --template-body file://cloudformatin-template-s3-store.yml --parameters ParameterKey=CloudFormationTemplateBucketName,ParameterValue=cloudformatin-template-s3-store ParameterKey=ProjectName,ParameterValue=suzukis ParameterKey=Environment,ParameterValue=prod

# ネットワーク環境の構築
aws cloudformation create-stack --stack-name network --template-body file://root-network.yml --parameters ParameterKey=ProjectName,ParameterValue=suzukis ParameterKey=Environment,ParameterValue=prod

