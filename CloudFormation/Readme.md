# CloudFormationテンプレートの保管するためのS3バケットを作成
aws cloudformation create-stack --stack-name cfn-template-s3-store --template-body file://cloudformatin-template-s3-store.yml --parameters ParameterKey=CloudFormationTemplateBucketName,ParameterValue=cloudformatin-template-s3-store ParameterKey=ProjectName,ParameterValue=suzukis ParameterKey=Environment,ParameterValue=prod

## ネットワーク環境の構築
aws cloudformation create-stack --stack-name network --template-body file://root-network.yml --parameters ParameterKey=ProjectName,ParameterValue=suzukis ParameterKey=Environment,ParameterValue=prod

## S3 アップロード
aws s3 cp ~/Desktop/IaC/CloudFormation s3://suzukis-cloudformatin-template-s3-store-prod --recursive

## aws cli cloudformation package
aws cloudformation package --template-file ./NW/root-network.yml \
	--s3-bucket suzukis-cloudformatin-template-s3-store-prod \
	--output-template-file ./NW/package/packaged.yml

## aws cli cloudformation deploy
aws cloudformation deploy --template-file /Users/shota/Desktop/IaC/CloudFormation/NW/package/packaged.yml \
  --stack-name suzukis-network --parameter-overrides ProjectName=suzukis Environment=prod

## ROLLBACK_COMPLETE 削除
aws cloudformation 
